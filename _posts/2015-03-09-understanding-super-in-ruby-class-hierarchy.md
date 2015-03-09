---
title: "Understanding super keyword in ruby class hierarchy"
keywords: "super keyword, class hierarchy, ruby programming"
description: "explain how keyword super is used in Ruby and hierarchy chain for method look up"
layout: "post"
permalink: "/2015/03/understanding-super-keyword-in-ruby-class-hierarchy.html"

---

# Introduction

Developers with OOP background are familiar with one key word **_super_** .

> super is used to refer parent method from child object, it is a important concept to implement [polymorphism][1]

Ruby is a OOP language, it has super keyword as well, but since ruby is a single inheritance language with [Mixin][2] as extension, super has some different behaviour in Ruby.

# The code

I write a short snippet of Ruby code to demostrate how super is used in Ruby.

```ruby
module M1
  def method1
    puts "Module1\#method1"
    super
  end
end

module M2
  def method1
    puts "Module2\#method1"
    super
  end
end

class Parent
  def method1
    puts "Parent\#method1"
  end  
end

class Child < Parent

  def method1
    puts "Child\#method1"
    super
  end

  include M1
  include M2   # M2 is included after M1

end


Child.new.method1
puts '----------------------'
puts Child.ancestors
puts '----------------------'
puts Child.superclass
```

- From line 1 to line 13, we define 2 modules M1 and M2 , they both define the same method 'method1'
- From line 15 to 19 the Parent class is defined with the same method 'method1'
- Line 21 to 31 define Child class which inherit Parent class, include M1 and M2

We notice that every method1 use super to invoke parent's same method

If we run this code, we can the output is as follows:

```text
Child#method1
Module2#method1
Module1#method1
Parent#method1
----------------------
Child
M2
M1
Parent
Object
PP::ObjectMixin
Kernel
BasicObject
----------------------
Parent
```

Since each method1 calls its super method, all methods from inheritance hierarchy get invoked. One question might pop up in your mind is: **why method1 in M2 is called before M1?**

To answer this quesiton, we need to understand how super search for method in ruby inheritance hierarchy.

If only 2 classes are defined, without any module mixin, the diagram is like this:

![Child and Parant class relation][child_parent]

When we define one Module M1

![Child Parant class with Module relation][cpm]

Then, we mixin second module M2, method1 defined in M2 does _NOT_ override method1 in M1, instead, M2 is added to method search path beneath M1:

![Child Parant class with 2 Modules relation][cpmm]

As shown in the code output, we can also get this method search chain from **Class.ancestors**

The interesting point is, by comparing output of Class.ancestors and Class.superclass, we can see superclass only show class, modules are excluded; but the actually method search chain is represented by Class.ancestors, which includes both super classes and modules mixed in.

# Take away

- Mixined modules are included in method search chain.
- use Class.ancestors instead of Class.superclass to investigate Ruby's method search chain.

---

<!-- images -->
[child_parent]: https://dl.dropboxusercontent.com/u/2390116/blog/images/ruby_super/child_parant.png "child parent class relation"
[cpm]: https://dl.dropboxusercontent.com/u/2390116/blog/images/ruby_super/cpm.png "child parent class with one module"
[cpmm]: https://dl.dropboxusercontent.com/u/2390116/blog/images/ruby_super/cpmm.png "child parent class with 2 modules"

<!-- links -->
[1]: http://en.wikipedia.org/wiki/Polymorphism_%28computer_science%29
[2]: http://www.tutorialspoint.com/ruby/ruby_modules.htm