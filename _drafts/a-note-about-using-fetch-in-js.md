---
layout: post
title: A note about using 'fetch' in JS
categories: JavaScript
---

Another story about bug. This time, related to native `fetch` API for
making request in JS.

### Backstory

After serveral days of having my first production application online,
my client contact me and inform me that, the application has a bug,
again.

"The button doesn't work for one of the customer again", my client said.

Well, if I can reproduce it, I can fix it. I went on and try to
reproduce it on my machine.

"Hmm, I can't seem to reproduce the bug locally."

It turns out that the bug only occur in iOS 10.2.1

I go ahead and download the Simulator for iOS 10.2, so I could
debug.

It turns out to be `fetch` not being supported in iOS 10.2. In this
case, it is easy to resolve the bug. I can:
 - replace `fetch` with `axios`
 - use `fetch` polyfill


### Lesson Learned
1. `fetch` is not supported for iOS 10.2 and below.
2. Having more information about the environment when the bug occured
   is always helpful.

