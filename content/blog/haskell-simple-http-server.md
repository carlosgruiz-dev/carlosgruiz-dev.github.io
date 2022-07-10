---
title: "Haskell Simple HTTP Server"
date: 2017-08-20T19:00:24-05:00
lastmod: 2017-08-20T20:00:00-05:00
tags: [lab, haskell, open source, english]
---

I'm pushing myself to learn Haskell, but I realized that the best way to learn is
to make things, broke them and build them again. So I decided to start a toy
project to create a substitute for commands like `$ python3 -m http.server` or
`$ php -S 0.0.0.0:8000` that fires a simple HTTP server to look your HTML files.
For this, I have a [twitter thread](https://twitter.com/octonemo/status/897987573024399361)
to log me and avoid procrastination.

<!--more-->

![Plane Blueprint](/images/plane-blueprint.png)

To meet my goal, I must find a way to work with a web server like in other
programming languages or better. Let's find out what we can do for this.

## Reference Implementation

So, let's start with a reference implementation, and since JavaScript is widely in
use this could be a good idea. On [NodeJS](https://nodejs.org/) we can walk through
this with this snippet:

{{< rawhtml >}}
<script src="https://gist.github.com/carlosgruiz-dev/effb9afcf5c82399a609ad622fc99a61.js"></script>
{{< /rawhtml >}}

It's self-explaining, we call for a module _(line 1)_, define a server _(lines 2-7)_
and start the server _(line 8)_. For the project this is the kind of things I will
like to do rather than going too low-level programming.

## Using Sockets

For any project, we need a bit of research looking for options of how to do what we
want, the [Haskell Wiki](https://wiki.haskell.org/) has a page with a reference for
creating [Simple Servers](https://wiki.haskell.org/Simple_Servers), plus it is in a
concurrent fashion.

{{< rawhtml >}}
<script src="https://gist.github.com/carlosgruiz-dev/214d3da2f2814dfe3edaa8ae42b51bd0.js"></script>
{{< /rawhtml >}}

Since we are using sockets
_(line 5 [withSocketsDo](http://hackage.haskell.org/package/network-2.6.3.2/docs/Network-Socket-Internal.html#v:withSocketsDo))_
it's clear that its lower level programming in comparison with our JavaScript reference.
If you still have doubts just see the _line 15_, and this string
`"HTTP/1.0 200\r\nContent-Length: 13\r\n\r\nHello, World!\r\n"` rings the low-level
programming bell again.

Nothing bad with this kind of fine grain control, but is not the abstraction level
I'm looking for. Anyway, it is worth to take a look at this example because even using
sockets and other low-level abstraction resources Haskell still is a very expressive
and concise.

## Using Wai

Some more googling and I found [Wai](https://github.com/yesodweb/wai), a package of
the [Yesod](http://www.yesodweb.com/) framework. This is pretty much is what I
expect to use for my project. To be honest this code and the reference one maybe
are oversimplifications, but still, give us valuable information about how our
application is going to deal with the web server.

{{< rawhtml >}}
<script src="https://gist.github.com/carlosgruiz-dev/ba6ba743b5f1e35e089b9227cf41009f.js"></script>
{{< /rawhtml >}}

To build this example you need to install two packages, since I use
[Haskell Stack](https://haskellstack.org) you can do it writing:

```bash
$ stack install wai warp
```

or:

```bash
$ cabal install wai warp
```

if you use the [cabal](https://www.haskell.org/cabal/) build tool.

A quick and dirty explanation of this code is, a language pragma to make strings
polymorphic _(line 1)_, imports for modules and specific functions _(lines 2-4)_,
a function definition for the application _(lines 6-7)_ and finally a call for that
function at the `main` entry point.

And this is all for now, hope you find this post useful.

---

{{< rawhtml >}}
<small>Credits for the plane blueprints image to the
<a href="https://commons.wikimedia.org/wiki/File:General_Motors_TBM-3S_Avenger_3-side-view_Blueprint.png">
Bureau of Aeronautics, U.S. Navy
</a>
</small>
{{< /rawhtml >}}
