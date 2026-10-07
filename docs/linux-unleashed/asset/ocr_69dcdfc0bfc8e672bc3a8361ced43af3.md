# Debugging and Profiling Options

GCC supports several debugging and profiling options. Of these options, the two that you are most likely to use for C++ programs are the -gstats+ option and the -pg option.

The -gstats+ option tells GCC to produce stabs format debugging information that the GNU debugger (gdb) can use to help you debug your program. For more information on debugging your C++ programs, see the “Debugging C++ Applications” section later in this chapter.

The -pg option tells GCC to add extra code to your program that will, when executed, generate profile information that can be used by the gprof program to display timing information about your program. For more information on gprof, refer to the “gprof” section in Chapter 26, “Programming in C.”

# GCC C++ Specific Options

The GCC options that control how a C++ program is compiled are listed in Table 27.1.

**TABLE 27.1. GCC OPTIONS.**

| Option | Meaning |
| :--- | :--- |
| -fall-virtual | Treats all possible member functions as virtual. This applies to all functions except for constructor functions and new or delete member functions. |
| -fdollars-in-identifiers | Accepts $ in identifiers. You can also prohibit the use of $ in identifiers by using the -fno-dollars-in-identifiers option. |
| -felide-constructors | Tells the compiler to leave out constructors whenever possible. |
| -fenum-int-equiv | Permits implicit conversion of int to enumeration types. |
| -fexternal-templates | Produces smaller code for template declarations. This is done by having the compiler generate only a single copy of each template function where it is defined. |
| -fmemoize-lookups | Uses heuristics to compile faster. These heuristics are not enabled by default because they are effective only for certain input files. |
| -fno-strict-prototype | Treats a function declaration with no arguments the same way that C would treat it. This means that the compiler treats a function prototype that has no arguments as a function that will accept an unknown number of arguments. |