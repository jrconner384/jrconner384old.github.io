---
layout: page
title: Open Integer
permalink: /open_integer/
---
[OpenInteger](https://github.com/jrconner384/open_integer) is a set of extensions I've been writing for Ruby's Integer class. The whole thing started as a very ad-hoc mess of random methods I'd been writing to solve [Project Euler](projecteuler.net) problems. Once I got over being lazy, I pulled all of that work into one place and learned how to make and publish RubyGems.

##What about the standard library?##
That's a great question, imaginary reader! Ruby's a mature language with a lot of great functionality built in and a bunch of extra stuff available in the [standard library](http://ruby-doc.org/stdlib-2.2.2/). I use that whenever possible (and whenever I can find it) but, sometimes, it's just not there.

Of course, the functionality is sometimes there but I just didn't find it at first. That's how my [sieve of Eratosthenes](https://github.com/jrconner384/erats_sieve) came to be. I'd been using that as my prime number sieve before I found the Prime library. The sieve repo is still out there because why would I delete it? I stopped using it in OpenInteger, though, in favor of the built-in Prime library.

##Is this thing usable?##
For the most part, yes. Every single method is one I wrote to solve a problem on Project Euler and each one led to the correct solution but that's not really enough, as I soon discovered.

I use [Minitest](https://github.com/seattlerb/minitest) as my test runner and [Coveralls](https://coveralls.io) for the test components of my CI framework. As I write this, Coveralls tells me the code is 100% covered but that's still not enough.

The excellent spec framework describes what I think should happen and lets me write code to demonstrate it. You can find my specs [here](https://github.com/jrconner384/open_integer/tree/open_CI/test/specs) to see what I think the library should be doing.

I'll write more tests, even for methods that are already "covered", and I hope to have the functionality covered in concept rather than just by the metrics. A green badge that says "100%" is nice but it's not a guarantee.

##It's Alive!##
Like I wrote above, I started this to help me solve Project Euler problems but the project has taken on a life entirely its own. I plan to add more functionality and improve the existing code whether it leads to new Euler solutions or not.

##Credits##
I've learned the ins and outs of the following excellent tools while working on this and I encourage anyone using Ruby or any language to have a look.

[Minitest](https://github.com/seattlerb/minitest) - A lightweight test framework written in Ruby.

[Travis-CI](https://travis-ci.org) - An awesome continuous integration tool which is free for publicly hosted GitHub projects. It also does the awesome work of conditionally publishing builds to [rubygems](rubygems.org)

[Coveralls](https://coveralls.io) - Works with SimpleCov and Travis to analyze test coverage. Generates awesome reports and badges.
