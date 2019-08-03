---
layout: default
title: Home
---

## Hello
Welcome to my blog. Here I write mostly about technical stuff.
Most of the time, I work on Ruby and Rails, Elixir, JavaScript and React.
I use vim as my main text editor.


Most of posts will be related to the mentioned
technology. Sometimes, I write about random thoughts and experience
on productivity and learning.

Thanks for reading the blog. Much appreciated.

<em><small>Want to know more about me? Read it [here][1]</small></em>

## Projects

I work on some side projects to learn and solve my personal problems in my
spare time. Here are some of them:

- [TIL](https://til.kaiwern.com): A Today I learned web application developed
with Phoenix. It includes basic features like adding post with Markdown and tagging.
The idea of the application is inspired by [Hashrocket TIL](https://til.hashrocket.com).
- [Expendere](https://expendere.herokuapp.com): A personal finance management web
application which includes features like expense tracking, budget and recurring
transaction (bills). It is developed with Ruby on Rails and a little bit of
Preact. Due to limited time available, _it is sort of abandoned now_.


## Posts
<table class="table">
{% for post in site.posts %}
{% include component/post_title.html post=post %}
{% endfor %}
</table>

<p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

[1]: about
