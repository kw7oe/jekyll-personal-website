---
layout: default
title: Home
---

## Hello

Welcome to my blog. Here I write mostly about technical stuff.
Most of the time, I work on Ruby and Rails, Elixir and JavaScript
framework such as React and Vue. I use vim as my main text editor,
and sometimes Sublime Text and Visual Studio Code.


So,  most of posts will be related to the mentioned
technology. Sometimes, I write about random thoughts and experience
on productivity and learning.

I just started this blog. Hopefully I can be more consistent on
my writing.

Thanks for reading the blog. Much appreciated.

<em><small>Want to know more about me? Read it [here][1]</small></em>


## Posts
<table class="table">
{% for post in site.posts %}
{% include component/post_title.html post=post %}
{% endfor %}
</table>

<p class="rss-subscribe">subscribe <a href="{{ "/feed.xml" | relative_url }}">via RSS</a></p>

[1]: about
