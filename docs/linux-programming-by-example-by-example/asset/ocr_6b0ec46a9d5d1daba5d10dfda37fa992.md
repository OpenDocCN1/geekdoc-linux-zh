case, `clean` removes the editor executable and its constituent object files. You might create such a target if you wanted to create a source-code *tarball*, an archive file created using the `tar` command, or wanted to start a build with a clean build tree.

+   - For a detailed discussion of the `tar` command, see "*tar Usage*," page 444.

If, however, a file named `clean` happened to exist, `make` would see it. Again, because it lacks dependencies, `make` would assume that it is up to date and would not execute the commands associated with the `clean` target. To deal with this situation, use the special `make` target, `.PHONY`. Any dependencies of the `.PHONY` target will be evaluated as usual, but `make` will disregard the presence of a file whose name matches one of `.PHONY`'s dependencies and execute the corresponding commands anyway.

# ### Examples

![](bbox=[0.05, 0.35, 0.13, 0.4])

# #### Example

+   1. Refer to the previous makefile for this example. Without the `.PHONY` target, if a file named `clean` exists in the current directory, the `clean` target will not work correctly.

![](bbox=[0.05, 0.49, 0.15, 0.54])

# #### Output

```
```
$ touch clean
$ make clean
make: 'clean' is up to date.
```
```

As you can see, without the `.PHONY` target, `make` evaluated the `clean` target's dependencies, saw that it did not have any and that a file named `clean` already existed in the current directory, concluded that the target was up to date, and did not execute the rule's commands.

![](bbox=[0.05, 0.72, 0.13, 0.77])

# #### Example

+   2. However, with the `.PHONY` special target, the `clean` target works perfectly, as illustrated:

![](bbox=[0.05, 0.85, 0.15, 0.9])

# #### Output

```
```
$ make clean
rm -f hello pedant newhello newhello noret inline packme *.o *.a *~
```
```