---
layout: post
title: How I keep track of tasks for multiple side projects
date: 2019-02-18 21:51 +0800
categories: productivity
---

Most developers have countless of side projects. Some are burried somewhere
else after some times. It's the same for me. I used to jump from one side
projects to another. In the end, I always lost track of the todos of each
of the side projects.

Keeping track of tasks in all of your side projects isn't easy without using
any project management software. However, it might feel overkill to do so.

### Where I left off last time?

Every now and then, when I am working on my side projects, I always forget
what are the last changes I made. Luckily with version control and the
practice of writing good commit message, I can always use `git log` to
view the past commits to get an overview what I should do next and
what have been done.

However, this approach is limited. Sometime, the past commits can't really
tell me what should I do next.

Hence, I use a simple way to keep track of what I need to do in my side
projects, which is a todo list.

### Introducing `.todo` file

The idea is straighforward. I write down my tasks in the `.todo` file located
at the root directory of the project.

To edit it, I just use `vim .todo`. Adding tasks or deleting tasks are the
same as manipulating text.


  - Not using `vim`? use any text editor you prefer, it's just
    a text file.
- List the style quickly with `cat -n .todo`
- What's the benefits?
  - No extra dependencies. We use everything available natively.
    Cross compatible to every machine (Unix based).
  - Highly customizable of output.
  - Can use pipe to show most important tasks. E.g. use `cat -n .todo | head -n 5'
    to show top 5 tasks to do.
- It's too long to type the command...
- Write a function using bash/zsh script.
```bash
function whattodo() {
    cat -n .todo
}
```
