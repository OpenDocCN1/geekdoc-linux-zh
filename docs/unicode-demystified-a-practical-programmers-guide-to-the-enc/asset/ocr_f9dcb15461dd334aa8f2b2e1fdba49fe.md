# Advanced Exercises

10. In the makers (page 812) program, file descriptors 3 and 4 are opened; during the loop, output is directed to these descriptors. An alternative method would be simply to append the output each time it occurs, using; for example,

```
print "Cannot create $target" >>ERRS
```

rather than

```
print -u3 "Cannot create $target"
```

What is the difference? Why does it matter?

11. The check in makers (page 812) to prevent you from copying hierarchies on top of each other is simplistic. For example, if you are in your home directory, the call ./work/RCS will not detect that the source and target directories lie on the same path. Fix this check.

12. In principle, recursion is never necessary. It can always be replaced by an iterative construct, such as while or until. Rewrite makepath (page 809) as a nonrecursive function. Which version do you prefer?

13. Lists are commonly stored in environment variables by putting a colon (:) between each of the list elements.(The value of the PATH variable is a good example). You can add an element to such a list by concatenating the new element to the front of the list, as in

```
PATH=/opt/bin:$PATH
```

If the element you already is in the list, you now have two copies of it in the list. Write a Shell function, addenv takes two arguments:(1) the name of a shell variable and (2) a string to prepend to the list that is the value of the shell variable only if that string is not already an element of the list. For example, the call

```
addenv PATH /opt/bin
```

would add /opt/bin to PATH only if pathname is not already in PATH. Be that your solution works