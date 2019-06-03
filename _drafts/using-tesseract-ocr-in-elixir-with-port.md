---
layout: post
title: Using Tesseract OCR in Elixir with Port
categories: elixir
---

Lately, I am exploring the use of OCR in [Expendere][1] (my expense tracking
application) and came across [Tesseract OCR][2].

At the time of writing this blog post, there is no native binding of Tesseract OCR in Elixir.
However, there are two Elixir wrapper available on GitHub:

- [tesseract-ocr-elixir][3]
- [tesseract-elixir][4]

Both wrapper use `System.cmd/3` to invoke the `tesseract` command line
interface and return the results of the executed command.

Seeing there are wrappers available out there, I quickly grab one and scaffold
a Phoenix application to test it out.

## Code
In `mix.exs`, add `tesseract-ocr-elixir` as dependency:
```elixir
def deps do
  [
    ...,
    {:tesseract_ocr, "~> 0.1.0"}
  ]
end
```

In `page_controller.ex`:
```elixir
defmodule OcrWeb.PageController do
  use OcrWeb, :controller

  def index(conn, _params) do
    render(conn, "index.html")
  end

  def create(conn, %{"upload" => %Plug.Upload{} = upload}) do
    result = TesseractOcr.read(upload.path)
    render(conn, "show.html", result: result)
  end
end

```

In `router.ex`, add this under `scope "/"`:
```elixir
get "/", PageController, :index
post "/upload", PageController, :create
```

In `templates/page/index.html.eex`:
```eex
<%= form_for @conn, Routes.page_path(@conn, :create),
                    [multipart: true], fn f-> %>
    <%= file_input f, :upload, class: "form-control" %>
    <%= submit "Upload", class: "btn btn-primary" %>
<% end %>
```

In `templates/page/show.html.eex`:
```eex
<h1>Result:</h1>

<%= @result %>
```

While it works perfectly fine, it is a bit slow. **The request takes around 900ms
in my Macbook Pro 2015**. I am not quite satisfied with the performance. Hence, I
tried to look around to see if any Elixir/Erlang `tesseract` native port is
available.

## Port

Somehow, I came across Native Implemented Functions (NIFs) and Port in
Elixir/Erlang. NIFs can be complicated, so I decided to look into `Port` instead.
It turns out that `Port` is fairly easy to understand.

Basically, `Port` can be used to communicate with the external world (code)
through ports. It provide a mechanism to start an operating system process and
allow Erlang VM to communicate with them through message passing.

Here is the code snippet of my own `tesseract` wrapper implemented using
`Port`.

In, `lib/app_name/tesseract.ex`:
```elixir
defmodule Ocr.Tesseract do
  def read(upload = %Plug.Upload{}) do
    File.cp!(upload.path, upload.filename)
    spawn_tesseract(upload.filename)
  end

  defp spawn_tesseract(file_path) do
   port = Port.open({:spawn, "tesseract"}, [:binary])
    send(port, {self(), {:command, "'#{file_path}' result"}})

    receive do
      _ -> File.read!("result.txt")
    end
  end
end
```

In `page_controller.ex`, change the `create` function to:
```elixir
def create(conn, %{"upload" => %Plug.Upload{} = upload}) do
  result = Ocr.Tesseract.read(upload)
  render(conn, "show.html", result: result)
end

```

By using `Port`, we are also fundamentally using `tesseract` through the CLI.
However, it is way faster. With this implementation, **the request now only takes around 25ms**.
What a huge performance improvement compared to the previous approach.


## Benchmark

To measure the performance difference more accurately, I decided to run a
benchmark using [`benchee`][5].


```elixir
# benchmark.exs
# Assuming you have a "test-image.jpg" in the same directory.

Benchee.run(%{
  "System.cmd" => fn ->
    # TesseractOcr modules from `tesseract-cor-elixir`
    TesseractOcr.read("test-image.jpg")
  end,
  "Port.open" => fn ->
    port = Port.open({:spawn, "tesseract"}, [:binary])
    send(port, {self, {:command, "test-image.jpg result"}})

    receive do
      _ -> File.read!("result.txt")
    end
  end
})

```

**Results:**
```
Operating System: macOS
CPU Information: Intel(R) Core(TM) i5-5257U CPU @ 2.70GHz
Number of Available Cores: 4
Available memory: 8 GB
Elixir 1.8.1
Erlang 20.2.2

Benchmark suite executing with the following configuration:
warmup: 2 s
time: 5 s
memory time: 0 ns
parallel: 1
inputs: none specified
Estimated total run time: 14 s

Benchmarking Port.open...
Benchmarking System.cmd...

...

Name                 ips        average  deviation         median         99th %
Port.open          56.65       17.65 ms     ±4.50%       17.37 ms       20.69 ms
System.cmd          1.41      709.55 ms     ±0.14%      709.43 ms      710.80 ms

Comparison:
Port.open          56.65
System.cmd          1.41 - 40.19x slower +691.90 ms
```

Now, it become clear that using `Port` is really more performant compared to
`System.cmd`. This is probably due to some additional checking/validation
in `System.cmd`.

## Closing
As for now, I am not very clear on what are the trade offs of using `Port` instead
of `System.cmd/3` to invoke CLI commands in Elixir. Maybe it can be a
topic for another day.


[1]: https://expendere.herokuapp.com
[2]: https://github.com/tesseract-ocr/tesseract
[3]: https://github.com/dannnylo/tesseract-ocr-elixir
[4]: https://github.com/bchase/tesseract-elixir
[5]: https://github.com/bencheeorg/benchee
