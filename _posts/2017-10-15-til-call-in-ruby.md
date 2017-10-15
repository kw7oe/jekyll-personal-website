---
layout: post
title: 'TIL: call in Ruby'
date:   2017-10-15 18:12:19 +0800
categories: ruby til
---

Surprisingly, you can actually do this in `ruby`:

```ruby
class Person
  def call
    "Hello World"
  end
end

Person.new.()
#=> Hello World
```

or even this: 

```ruby
class Person
  def initialize(name, age)
    @name = name
    @age = age
  end

  def self.call(name:, age:)
    self.new(name, age)
  end
end

Person.(name: "Peter", age: 12)
#=> #<Person:0x00007f991b80b8d8 @name="Peter", @age=12>
```
