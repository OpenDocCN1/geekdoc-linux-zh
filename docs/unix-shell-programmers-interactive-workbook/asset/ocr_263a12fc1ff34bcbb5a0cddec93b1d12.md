# Chapter 10: Patterns, Expansions, and Substitutions 473

value. In the present case, BROWSER is undefined, so the value printed is lynx.

```
BROWSER=netscape
print Your browser is ${BROWSER:-lynx}
```

+   c) What prints this?
Answer:Your interaction should look like the following:
[1037]: BROWSER=netscape
[1038]: print Your browser is ${BROWSER:-lynx}
Your browser is netscape.
[1039]:

This time, BROWSER does have a value, and that's what gets substituted for the ${ ... }.

```
unset BROWSER
if ! (whence ${BROWSER:-lynx} >/dev/null)
then print -u2 no browser
fi
```

+   d) What was printed when you ran these commands?
Answer:"no browser" prints.

If you recall, the shell's whence command tells you whether a command is a function or an external command, and if it is external, where it is located in the file system. In this code, we are using the fact that whence sets its exit code to false if the shell cannot find the command anywhere. The exclamation mark changes the logical value being tested to true if the value of the ${ ... } is not the name of an executable file, and if this is the case, the print command gets executed.

+   e) What does the > on the second line accomplish?
Answer:It redirects the output of the whence command.

If the parameter passed to whence is the name of something executable, whence prints a message telling you about it, but we don't want to see that message, so we redirect it to /dev/null. We're interested only in the value of whence's exit code in this statement, so we get rid of the-sage.