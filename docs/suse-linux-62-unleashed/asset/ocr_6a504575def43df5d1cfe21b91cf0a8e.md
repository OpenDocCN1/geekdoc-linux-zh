# SuSE System Administration
PART III

learn, of course, is to experiment on your own. For example, if you have any question about
what man tr means by "translation," it's an easy matter to experiment, like so:

```
# tr pf PF <<HERE
abcopqOPQ
FfpPab
HERE
```

You can conclude that you're on the right track when you see the following:

```
abcopqOPQ
FFpPab
```

This is one of the charms of relying on shells for automation; it's easy to test commands
interactively, providing an easy way to understand how a particular command works.

The sample product catalog script in Listing 22.1 is written for sh recognize. I strongly
recommend this to be your target for scripts, rather than ksh, csv, or bash. I prefer any of the
latter for interactive command-line use. When automating, however, or I'm often
connecting to hosts that don't use SuSE Linux, have therefore found that it is a good idea to code
using constructs that sh and therefore all the shells recognize. Default SuSE Linux
ations use a linked named /bin/sh that points to /bin/bash. All the work in this
chapter is written so that the scripts will function no matter what the details of
y host's configuration are. Chapter 25 gives more details on the differences among
shells.

Did I really include the inline comments, the lines that begin with #, when I first wrote the
script in Listing 22.1? Yes, I've made this level of source-code documentation a habit, co-workers
chat, and power supplies fail; If your life is like all mine, telephone ring, I find it easier to type this much detail as I'm thinking about
it, rather than risk having to re-create my thoughts in case of an interruption. It's also much
easier to pick up the work again days or weeks later. Writing for human readability eases
t transition when you pass your work to others. Listing 22.1 begins by assigning
ash variable DIR in line 3. It's good practice to make such an assignment, even for a
variable (apparently) used only once. It contributes to self-documentation and generally
enhances maintainability; it's easy to look at the top of the script and see immediately what
magic words or configuration in the outside environment depends upon
(/particular/directory/for/my/client in this case; see the third line down).

Many of the folks you want to accomplish involve a quantifier: "change all,..." "correct
every...," and so on. The shell's looping constructs, and for while, are your friends. You'll
make almost daily use of them.