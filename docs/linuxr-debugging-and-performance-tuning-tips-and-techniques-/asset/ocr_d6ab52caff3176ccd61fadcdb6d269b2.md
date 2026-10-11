To change an environment variable or to add a new one to the environment, use `setenv()`:

```
```
if (setenv("PATH", "/bin:/usr/bin:/usr/ucb", 1) != 0) {
    /* handle failure */
}
```
```

It’s possible that a variable already exists in the environment. If the third argument is true (nonzero), then the supplied value overwrites the previous one. Otherwise, it doesn’t. The return value is \-1 if there was no memory for the new variable, and 0 otherwise. `setenv()` makes private copies of both the variable name and the new value for storing in the environment.

A simpler alternative to `setenv()` is `putenv()`, which takes a single `*name=value*` string and places it in the environment:

```
```
if (putenv("PATH=/bin:/usr/bin:/usr/ucb") != 0) {
    /* handle failure */
}
```
```

`putenv()` blindly replaces any previous value for the same variable. Also, and perhaps more importantly, the string passed to `putenv()` is placed *directly* into the environment. This means that if your code later modifies this string (for example, if it was an array, not a string constant), the environment is modified also. This in turn means that you should *not* use a local variable as the parameter for `putenv()`. For all these reasons `setenv()` is preferred.

> NOTE The GNU `putenv()` has an additional (documented) quirk to its behavior. If the argument string is a name, then without an = character, the named variable is *removed*. The GNU env program, which we look at later in this chapter, relies on this behavior.

The `unsetenv()` function removes a variable from the environment:

```
```
unsetenv("PATH");
```
```

Finally, the `clearenv()` function clears the environment entirely:

```
```
if (clearenv() != 0) {
    /* handle failure */
}
```
```

This function is not standardized by POSIX, although it’s available in GNU/Linux and several commercial Unix variants. You should use it if your application must be very security conscious and you want it to build its own environment entirely from