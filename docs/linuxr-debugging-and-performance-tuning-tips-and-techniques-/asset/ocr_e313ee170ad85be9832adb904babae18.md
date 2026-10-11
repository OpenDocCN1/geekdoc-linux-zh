then those same calls expand to nothing. (This is essentially how `assert()` works; we described `assert()` in Section 12.1, "Assertion Statements: `assert()`," page 428.)

This technique works; we have used it ourselves and seen it recommended in textbooks. However, it can be refined a bit further, reducing the number of macros down to one:

```
/* TECHNIQUE 2 --- most portable; recommended */
/* In application header file: */
#ifdef MYAPPDEBUG
#define DPRINT(stuff)    printf stuff
#else
#define DPRINT(stuff)
#endif

/* In application source file: */
DPRINT(stderr, "myvar = %d\n", myvar);     Note the double parentheses
```

Note how the macro is invoked, with two sets of parentheses! By making the entire argument list for `printf()` into a single argument, you no longer need to have an arbitrary number of debugging macros.

If you are using a compiler that conforms to the 1999 C standard, you have an additional choice, which produces the cleanest-looking debugging code:

```
/* TECHNIQUE 3 --- cleanest, but C99 only */
/* In application header file: */
#ifdef MYAPPDEBUG
#define DPRINT(msg, ...)    printf(stderr, msg, __VA_ARGS__)
#else
#define DPRINT(msg, ...)
#endif

/* In application source file: */
DPRINT("myvar = %d\n", myvar);
...
DPRINT("v1 = %d, v2 = %f\n", v1, v2);
```

The 1999 C standard provides *variadic macros*; that is, macros that can accept a variable number of arguments. (This is similar to variadic functions, like `printf()`.) In the macro definition, the three periods, `, . . .`, indicate that there will be zero or more arguments. In the macro body, the special identifier `__VA_ARGS__` is replaced with the provided arguments, however many there are.

The advantage to this mechanism is that only one set of parentheses is necessary when the debugging macro is invoked, making the code read much more naturally.