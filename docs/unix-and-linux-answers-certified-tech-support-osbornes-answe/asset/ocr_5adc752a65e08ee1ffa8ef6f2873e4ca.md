# Can I use grep -v to find files that don’t belong to me?

Yes. Here is a quick way to find out if anyone has written files in your home directory that don’t belong to you:

```
ls -lA | grep -v "$LOGNAME"
```

This will return a list of only the files in the current directory that are not owned by you. There’s one exception: it would miss a file that included your login name in the filename even if the file belonged to someone else.

# Is it possible to use grep -i for case-insensitive searching?

Certainly. In fact, this can be quite handy for making sure that you use something consistently. For example, in this book we use "system administrator" as the form for that ultimate of UNIX gods, the superuser. But we found that sometimes we had the capitalization wrong and we weren’t consistent between "system" and "systems". So, we used the following to find all of these instances, complete with their line numbers in the file:

```
grep -in "system.*" administrator chp[1-8].txt
```

This translates into "search chp1.txt through chp8.txt for the string "system administrator" where the string may be upper or lowercase, or any mixture thereof, and where there may or may not be a single character after the "m" in system.

> Warning: The "." wildcard by itself will fool you! If we had neglected to put an asterisk after the "t" in the above grep expression, it would have missed the times we spelled system administrator without the "s" at the end. But the asterisk said to match zero or more instances of the previous metacharacter.