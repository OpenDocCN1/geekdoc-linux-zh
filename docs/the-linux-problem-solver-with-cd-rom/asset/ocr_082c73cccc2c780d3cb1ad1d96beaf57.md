# Command substitution.

The shell executes any command inside two backticks, and passes the output of that command as an argument (for example, FOO=`ls` places the output of the ls command into the variable FOO).

To pass any of the three quotes as literal arguments, put a forward slash (/) in front of the quote outside any single or double quotes. There are other ways to do it in bash, though; for example, `'`' passes a single quote, and `""` passes a double quote. Because there are so many ways to get literal characters as arguments, users often try to use all of them at once and end up with unexpected results. The best way to debug a problem with quoting is to use echo to see what arguments follow the substitution—for example:

```
$ echo '$this should put a dollar sign before the text'
```

NOTE
Annoyingly, ISO 8859-1 defines an acute accent that looks a lot like a single quote; you might have come across it in email messages, or you may have seen it on keyboards from outside the United States.

That's it for the basics. In the following chapters, you'll not only encounter solutions to over a hundred Linux problems, but you'll also see in-depth detail on why the solutions work. With this information in hand, you'll have everything you need to fix your Linux headaches.