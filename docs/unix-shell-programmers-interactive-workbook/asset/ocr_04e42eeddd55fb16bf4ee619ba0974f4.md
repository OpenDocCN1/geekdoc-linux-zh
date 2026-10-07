# FOR EXAMPLE

The following interaction illustrates using getopts from the command line:

```
[5051]: set --vu -do hello
[5052]: getopts douv optletter
[5053]: print $optletter
v
[5054]: getopts douv optletter
[5055]: print $optletter
u
[5056]: getopts douv optletter
[5057]: print $optletter
d
[5058]: getopts douv optletter
[5059]: print $optletter
o
```

You usually use getopts inside a script or function, but we will use the example as a model for experimenting with the getopts command by running it interactively.

+   a) What is the purpose of the double dash ( -- ) on line 5051?

+   b) What would be output if you printed a reference to the special variables # and @ between lines 5051 and 5052?

+   c) Write a set command that would be equivalent to line 5051 but would use just two parameters instead of three.