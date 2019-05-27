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

While it works perfectly fine, it is a bit slow. The request takes around 800ms
in my Macbook Pro 2015. I am not quite satisfied with the performance. Hence, I
tried to look around to see if any Elixir/Erlang `tesseract` native port is
available.

Then, I came across Native Implemented Functions (NIFs) and Port in
Elixir/Erlang. NIFs can be complicated, so I decided to look into `Port` instead.
It turns out that `Port` is fairly easy to understand.

Basically, `Port` can be used to communicate with the external world (code)
through ports. It provide a mechanism to start an operating system process and
allow Erlang VM to communicate with them through message passing.

By using `Port`, we are also fundamentally using `tesseract` through the CLI.
However, it is way faster. With the implementation of using `tesseract`
CLI through `Port`, the request now only takes around 5ms. It has a huge
performance improvement compared to the use of `System.cmd/3`

As for now, I am not very clear on what are the caveats of using `Port` instead
of `System.cmd/3` to invoke CLI commands in Elixir. Maybe it will be an
interesting topic for another day.


[1]: https://expendere.herokuapp.com
[2]: https://github.com/tesseract-ocr/tesseract
[3]: https://github.com/dannnylo/tesseract-ocr-elixir
[4]: https://github.com/bchase/tesseract-elixir
