---
layout: default
title: Home
---

## Hello
Welcome to my blog. Here I write about technology and life.

Some of the technologies I used in my work and side projects are:

- vim
- Elixir
- JavaScript
- React
- React Native
- Ruby

So, you can expect posts about these technologies from my blog. Most of the
time, I wrote what I learn on my [TIL application][1] and update it here on a
later time.

Lately, due to work schedule, I have not been able to write a lot. Hopefully, I
can write consistently in the coming month.

## Projects

I work on some side projects to learn and solve my personal problems in my
spare time. Here are some of them:

- [TIL][1]: A Today I learned web application developed
with Phoenix. It includes basic features like adding post with Markdown and tagging.
The idea of the application is inspired by [Hashrocket TIL](https://til.hashrocket.com).
- [Expendere](https://expendere.herokuapp.com): A personal finance management web
application which includes features like expense tracking, budget and recurring
transaction (bills). It is developed with Ruby on Rails and a little bit of
Preact. Due to limited time available, _it is sort of abandoned now_.


## Posts
<div class="post-lists">
  {% for post in site.posts %}
    {% include component/post_title.html post=post %}
  {% endfor %}
</div>

<p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

[1]:https://til.kaiwern.com

