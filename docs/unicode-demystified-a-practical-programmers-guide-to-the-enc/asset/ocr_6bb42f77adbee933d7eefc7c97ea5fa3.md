try to create the path /a/b, which requires that you create directory a in the root directory. Unless you have privileges, you are not permitted to do that:

```
zsh % makepath /a/b
+zsh:463> makepath /a/b
+makepath:2 [[ [ 4 -eq 0 -d /a/b ]]
+makepath:6 [[ [ /a == /a/b ] ]
+makepath:11: makepath /a
+makepath:2 [[ [ 2 -eq 0 || -d /a ]]
+makepath:6 [[ /a == /a ] ]
+makepath:11: makepath
+makepath:2 [[ [ 0 -eq 0 ]]
makepath: return: too many arguments [4]
+makepath:6 [[ == ]]
+makepath:8: mkdir
mkdir: too few arguments
` Try mkdir --help for more information.
+makepath:9> return 1
+makepath:11: return 1
+makepath:11: return 1
```

The recursion stops only when makepath is passed a null argument and the error return is passed all the way back, so the original makepath exits with nonzero status.

# Use Local Variables with Recursive Functions

The example has glossed over a potential problem that you may encounter when you use a recursive function. During the execution of a recursive function, many separate instances of that function may be simultaneously active. But all one of them are waiting for their child invocation to complete.

By default, Shell variables are global. When a recursive Z Shell function uses global variables, all instances of the function share a single copy of each variable. Sharing variables can rise to side effects that are rarely what you want. As a rule, use typeset (page 743) to make local all the variables of a recursive function.

# A Programming Problem: makercs

This section combines some of the Z Shell programming constructs into a complete program. The example uses ci, one of the Revision Control System (RCS) commands. If you are not familiar with RCS, refer to page 871 for a description. The example also makes use of find (page 1165). The specification for the program follows.