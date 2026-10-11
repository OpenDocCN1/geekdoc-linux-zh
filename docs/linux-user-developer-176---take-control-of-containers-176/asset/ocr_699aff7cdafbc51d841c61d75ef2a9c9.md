# BYTECODE TO JAVASCRIPT COMPILER

# Js_of_ocaml 2.8.4

OCaml in the browser: powerful, expressive, typesafe code

Perhaps you've come to OCaml through its relative SML, and the wonderful University of Washington MOOC on programming languages; perhaps through curiosity about F#'s parent, or maybe a search for statically typed languages that compile to JavaScript. Perhaps this is the first time you looked at it. However you've got here, welcome to strong, static typing and a great reduction in runtime errors.

Install OCaml from your operating system's packaging manager and you'll get the OPAM package manager, from which

```
```bash
opam install js_of_ocaml
```
```

will grab you all of the dependencies. However, Js_of_ocaml is a component of the Ocsigen web application framework and

```
```bash
opam install ocsigen-start
```
```

will give you Js_of_ocaml within a wider group of packages. The website features Api documentation and a tutorial on working with Ocsigen. Using the Ocsigen component Eliom, you can write client and server-side code in OCaml, in a single program, with automatic bidirectional communication. The session mechanism allows functional reactive web pages, and quite complex sites take very few lines of code. Because Js_of_ocaml takes OCaml bytecode as its input, you can even use it with OCamll libraries for which you don't have access to the source code. If you've never written OCaml before, don't be afraid of diving in and pushing on through the confusion.

# Pros

Expressive language with good record on runtime safety, without the overhead of runtime checks.

# Cons

Hindley-Milner type system is a discipline too far for some (try ClojureScript instead!).

# Great for…

Writable web code from single-pass or functional proc. ocamldoc or guides:
ocsigen.org/js_of_ocaml/

# STATIC WEBSITE GENERATOR

# Hugo 0.18

Bring website generation back to the text editor!

Hugo is a static blogging solution that has enough flexibility to build many types of website, and features the usual extra like RSS feed generation, and customizable URLs and aliases. It won't be long before you are up and running – you don't even need a Go language compiler, as Hugo is available as a binary which means – as the website boasts – “simply download and run!” The first task is to set up the site with:

```
```bash
hugo new site name-of-site
```
```

which generates the scaffold for the site. Next:

```
```bash
hugo new post/hello-world.md
```
```

generates a Markdown page for you to edit, creating the first post. Templates use the Go html/template library, enabling you to make quite complex sites. Hugo ships with its own web server for testing, but it's actually good enough for production use if you don't already have an Apache or Nginx setup to hook into. You'll need to install a theme before you can see your site this way. Alternatively let Hugo compile your posts (typically taking around 1ms per page), and upload the HTML produced to your server anywhere. Documentation is good for getting you up and running quickly and covers areas like the many migration tools available to get your existing site into Hugo.

![](bbox=[0.38, 0.56, 0.95, 0.82])

# Pros

Very fast, flexible and quick to set up. Great to have sites without database back-end to administer.

# Cons

The command line interface means you must persuade WordPress using friends to try it. Comments are not static.

# Great for…

Blogs, sites without the overhead of a blogging engine:

gohugo.io/