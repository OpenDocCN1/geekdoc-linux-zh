This is one of the charms of relying on shells for automation; it’s easy to bounce between interaction and automation, which shapes a powerful didactic perspective and a check on understanding.

The sample product catalog script in Listing 26.1 is written for **sh** processing. I strongly recommend this be your target for scripts, rather than **ksh**, **csh**, or **bash**. I prefer any of the latter for interactive command-line use. In automating, however, when I’m often connecting to hosts that don’t use Red Hat Linux, availability and esoteric security issues have convinced me to code using constructs that **sh**—and therefore all the shells—recognize. Default Red Hat Linux installations use a link named **/bin/sh** to point to **/bin/bash**. All the work in this chapter is written so that the scripts will function properly no matter what the details are of your host’s configuration. Chapter 25 gives more details on the differences among shells.

Did I really include the inline comments, the lines that begin with `#`, when I first wrote the script in Listing 26.1? Yes. I’ve made this level of source-code documentation a habit, and it’s one I recommend to you. If your life is at all like mine, telephones ring, co-workers chat, and power supplies fail; I find it easier to type this much detail as I’m thinking about it, rather than risk having to re-create my thoughts in case of an interruption. It’s also much easier to pick up the work again days or weeks later. Writing for human readability also eases the transition when you pass your work on to others.

Listing 26.1 begins by assigning a shell variable `DIR` in the third line. It’s good practice to make such an assignment, even for a variable (apparently) used only once. It contributes to self-documentation and generally enhances maintainability; it’s easy to look at the top of the script and see immediately on what magic words or configuration in the outside environment (`/particular/directory/for/my/client` in this case; see the third line down) the script depends.

Many of the jobs you’ll want to accomplish involve a quantifier: “change all…,” “correct every…,” and so on. The shell’s looping constructs, `for` and `while`, are your friends. You’ll make almost daily use of them.

**basename** and **tr** are universally available and widely used. **tr**, like many UNIX utilities, expects to read standard input. If you have information in shell variables, you can feed **tr** the information you want, either through a pipe from **echo**, as in the example, or an equivalent:

```
echo $VARIABLE | tr [a-z] [A-Z]
```

You can also do it with a so-called HERE document, such as this one:

```
tr [a-z] [A-Z] <<HERE
VARIABLE
HERE
```