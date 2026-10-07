# Lab 1.2: Setting Up Your Interactive Environment

```
function l1 {
  ls -l "$@" | $PAGER
}
function la {
  ls -la "$@" | $PAGER
}
```

It's common practice in UNIX systems for programs to read commands from a file when they start up to set up user's preferences for the program. Such files typically have names that begin with ~. (to make them hidden files in the user's home directory), followed by the name of the program (ksh, in this case), followed by rc (short for “read commands”). Knowing this can remove some of the mystery from looking at a list of the hidden files in your home directory.

# LAB 1.2 SELF-REVIEW QUESTIONS

To test your progress, you should be able to answer the following questions:

+   1) What is the environment of a process?
   a) The computer that executes it.
   b) The user who runs it.
   c) The other programs in memory at the same time.
   d) A list of variables with associated values.
   e) Its network neighborhood.

+   2) What is an environment variable?
   a) A name and its associated value that is part of a process's environment.
   b) A peripheral device that works in different ways at different times.
   c) A peripheral device that always works the same way.
   d) A symbol that is exported to a process's external environment.
   e) Anything that affects the weather.