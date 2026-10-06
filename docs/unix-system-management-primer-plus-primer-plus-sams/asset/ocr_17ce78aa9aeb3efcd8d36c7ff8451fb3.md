# 20 UNIX SYSTEM MANAGEMENT PRIMER PLUS

+   - Upgrading processors
- Utilizing multiple processors
- Tracing processes

# Choosing the Right Compiler Options

Many administrators build a significant number of third-party applications from source code such as Perl and Apache. One of the easiest ways to boost performance is to use the compiler's optimization features when building these packages. Though you can choose from many compilers for Unix systems, this section focuses on the GNU C compiler, because it is universal to all Unix systems. Most techniques for the GNU C compiler apply to every compiler.

# Using Generic GNU C Compiler Optimization

The GNU C Compiler, or GCC as it is commonly known, is a generic compiler that is available on all platforms. Because GCC is a generic compiler, its default optimizations are common to all platforms. These optimizations include the following:

+   - Using register variables: This stores variables directly on the processor instead of memory.
- Loop unrolling: This repeats lines of code inside a loop where possible to reduce the number of iterations.
- Function inlining: This integrates a simple function directly into the calling code, eliminating the overhead of calling the function.

You can activate these individual optimizations by using special flags to the gcc program, including -funroll-loops and -inline. But those flags can be difficult to remember and certain combinations can produce strange side effects that cause a program to fail when run. For this reason, GCC offers the 0 flag, which can specify different levels of optimization with a single flag. The format of this flag is -On, where n is an optional number between 0 and 3 (it is the same as -01). Compiling a program with the highest level of optimization is as simple as following:

```
bash$ gcc -03 -o foo foo.c
```

An in-depth discussion of compiler optimizations is beyond the scope of this book. Consult a text on compilers or the GCC manual page for more information.

# Using GNU Configure

A large percentage of application source code is configured using GNU Configure. To specify the optimization for these applications, put the appropriate flags in the CFLAGS environment variable before running the configure script.

![](bbox=[0.138, 0.793, 0.203, 0.833])