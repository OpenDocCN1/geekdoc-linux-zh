This *make*file relies on GNU make’s implicit rules. The conversion of `.c` files to `.o` files uses the built-in rule. Defining the variable `CFLAGS` passes the flags to the C compiler.

![](bbox=[0.11, 0.2, 0.2, 0.3])

The target named all is defined as the first target for a reason — if you run GNU make without specifying any targets in the command line (see the *make* syntax described in the following section), the command builds the first target it finds in the *make*file. By defining the first target all as *xdraw*, you can ensure that *make* builds this executable file, even if you do not explicitly specify it as a target. UNIX programmers traditionally use all as the name of the first target, but the target’s name is immaterial; what matters is that it is the first target in the *make*file.

# How to run make

Typically, you run *make* by simply typing the following command at the shell prompt:

```
make
```

When run this way, GNU make looks for a file named `GNUmakefile`, `makefile`, or `Makefile` — in that order. If *make* finds one of these *make*files, it builds the first target specified in that *make*file. However, if *make* does not find an appropriate *make*file, it displays the following error message and exits:

```
make: *** No targets specified and no makefile found.  Stop.
```

If your *make*file happens to have a different name from the default names, you have to use the `-f` option to specify the *make*file. The syntax of the *make* command with this option is

```
make -f *filename*
```

where *filename* is the name of the *make*file.

Even when you have a *make*file with a default name such as `Makefile`, you may want to build a specific target out of several targets defined in the *make*file. In that case, you have to use the following syntax when you run *make*:

```
make target
```

For example, if the *make*file contains the target named *clean*, you can build that target with this command:

```
make clean
```