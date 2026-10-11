```
```
22  for (; ix < argc; ix++) {
24      DEBUG_PRINT ("args", ("argv[%d] = %s", ix, argv[ix]));
24      result = factorial (atoi (argv[ix]));
25      printf ("%d\n", result);
26      fflush (stdout);
27  }
28  DEBUG_RETURN (0);
29 }
```
```

This program illustrates most of the salient points. The `DEBUG_ENTER()` macro (line 12) must be called after any variable declarations and before any other code. (This is because it declares some private variables of its own.¹⁵)

The `DEBUG_PROCESS()` macro (line 13) sets the name of the program, primarily for use in output messages from the library. This macro should be called only once, from `main()`.

The `DEBUG_PUSH_ENV()` macro (line 14) causes the library to look at the named environment variable (`DEBUG` in this case) for control strings. (The `dbg` control strings are discussed shortly.) The library is capable of saving its current state and using a new one, creating a stack of saved states. Thus, this macro pushes the state obtained from the given environment variable onto the stack of saved states. As used in this example, the macro creates the initial state. If there is no such environment variable, nothing happens. (As an aside, `DEBUG` is rather generic; perhaps something like `GAWK_DEBUG` [for `gawk`] would be better.)

The `DEBUG_PUSH()` macro (line 18) passes in the control string value obtained from the `-#` command-line option. (New code should use `getopt()` or `getopt_long()` instead of manual argument parsing.) This is normally how debugging is enabled, but using an environment variable as well provides additional flexibility.

The `DEBUG_PRINT()` macro (line 23) is what produces output. The second argument uses the technique we described earlier (see Section 15.4.1.1, “Use Debugging Macros,” page 577) of enclosing the entire `printf()` argument list in parentheses, making it a single argument as far as the C preprocessor is concerned. Note that a terminating newline character is *not* provided in the format string; the `dbg` library provides the newline for you.

> ¹⁵ C99, which allows variable declarations mixed with executable code, makes this less of a problem, but remember that this package was designed for K&R C.