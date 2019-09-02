---
layout: post
title: Connection timeout in HTTPoison
categories: elixir
---

One day, while working in Naluri, our team receive bug reports where user
cannot upload their food journal from our mobile application.

As usual, our QA team tried to replicate the issues in staging. They can't
replicate it. But, the team know that restarting the server, always magically
solve the issue.

At first, I was suspecting there are some failures with the 3rd party API.
However, I turned out to be wrong because if the 3rd party API failed, it would
also failed in the staging environment, since both production and staging use
the same endpoint for that API.

Not knowing what is the root cause, our CTO decided to add the additonal log
statements in our Phoenix application to find out the root cause of the issue.

It turns out to be, `{:error, %HTTPoison.Error{id: nil, reason:
:connect_timeout}}`.

Connection timeout? How could that be?

After some investigation _(google search)_, we found that this issue is common
for `HTTPoison` user, especially if they are sending high volume of request at
a time.

These is due to `HTTPoison` uses `hackney` default pool which only have a
maxiumum of 50 connections.

So, to resolve the issue, we started our default pool for `hackney` with a
higher `max_connection` count.

