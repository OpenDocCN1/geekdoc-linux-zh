# 15.5.1  The `dbug` Library — A Sophisticated `printf()`

The first package we examine is the `dbug` library. It is based on the idea of conditionally compiled debugging code we presented earlier in this chapter, but carries things much further, providing relatively sophisticated runtime tracing and conditional debug output. It implements many of the tips we described, saving you the trouble of implementing them yourself.

The `dbug` library, written by Fred Fish in the early 1980s, has seen modest enhancements since then. It is now explicitly in the public domain, so it can be used in both free and proprietary software, without problems. It is available from Fred Fish’s FTP archive, $^{14}$ as both a compressed tar file, and as a ZIP archive. The documentation summarizes `dbug` well:

```
"dbug is an example of an internal debugger. Because it requires internal instrumentation of a program, and its usage does not depend on any special capabilities of the execution environment, it is always available and will execute in any environment that the program itself will execute in. In addition, since it is a complete package with a specific user interface, all programs which use it will be provided with similar debugging capabilities. This is in sharp contrast to other forms of internal instrumentation where each developer has their own, usually less capable, form of internal debugger...
```

The `dbug` package imposes only a slight speed penalty on executing programs, typically much less than 10 percent, and a modest size penalty, typically 10 to 20 percent. By defining a specific C preprocessor symbol both of these can be reduced to zero with no changes required to the source code.

The following list is a quick summary of the capabilities of the `dbug` package. Each capability can be individually enabled or disabled at the time a program is invoked by specifying the appropriate command line arguments.

+   - Execution trace showing function level control flow in a semi-graphical manner using indentation to indicate nesting depth.
+   
+   - Output the values of all, or any subset of, key internal variables.