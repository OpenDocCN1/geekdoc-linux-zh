+   i
+   Identify the process emitting each line of debug or trace output with the process ID for that process.

+   L
+   Mark each debugger output line with the source-file line number of the macro causing the output.

+   o[\, file]
+   Redirect the debugger output stream to the specified file. The default output stream is stderr. A null argument list causes output to be redirected to stdout.

+   t[\, N]
+   Enable function control flow tracing. The maximum nesting depth is specified by *N*, and defaults to 200.

To round out the discussion, here are the rest of the macros defined by the dbug library.

```
DEBUG\_EXECUTE(string, code)

This macro is similar to DEBUG\_PRINT(): The first argument is a string selected with the d option, and the second is code to execute:

```c
DEBUG\_EXECUTE("abort", abort());
```
```

```
DEBUG\_FILE

This is a value of type FILE \*, for use with the `<stdio.h>` routines. It allows you to do your own output to the debugging file stream.
```

```
DEBUG\_LONGJMP(jmp\_buf env, int val)

This macro wraps a call to longjmp(), taking the same arguments, so that the dbug library will know when you've made a nonlocal jump.
```

```
DEBUG\_POP()

This macro pops one level of saved debugging state, as created by DEBUG\_PUSH(). It is rather esoteric; you probably won't use it.
```

```
DEBUG\_SETJMP(jmp\_buf env)

This macro wraps a call to setjmp(), taking the same argument. It allows the dbug library to handle nonlocal jumps.
```