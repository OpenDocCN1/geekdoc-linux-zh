# 12.1 Compiler flags 209

The last of the major toolchains is the Intel® compiler, designed specifically for producing heavily optimized code for Intel® processors. The Intel compiler is available free for noncommercial use on Linux. More information is available at https://software.intel.com/en-us/c-compilers.

This chapter focuses on the GNU toolchain, due to its ubiquitous nature and the fact that many of its extensions are supported by other toolchains for compatibility. The author will do his best to point out areas where the different idiosyncrasies of the toolchains can be problematic.

# 12.1 COMPILER FLAGS

The first step in leveraging the compiler to produce better code is to learn how to control the compiler's optimization stages and instruction generation. These are selected through the use of command arguments to the compiler, often called compiler flags or CFLAG.

Looking at the list of individual optimizations available in GCC is daunting, partially due to the large number of options available. To remedy this problem, GCC exposes predefined optimization levels that automatically toggle the appropriate optimizations. These levels are selected by the -0 compiler flag, a capital letter O.

The levels, and this is fairly standard between compilers, are described in Table 12.1. The exact optimizations enabled at each level can be manually queried with

| Level | CFLAG | Description |
| --- | --- | --- |
| 0 | -0 | No optimizations enabled. |
| 1 | -01 | Optimizations are enabled that reduce code and execution time, but don't significantly increase compilation time. |
| 2 | -02 | All optimizations are enabled that reduce code and execution, excluding those that involve a tradeoff between code size and speed. |
| 3 | -03 | Enables all optimizations at Level 2, plus those that drastically increase code size and those that may not improve performance. |
| s | -Os | Optimizes for Level 2, except without optimizations that could increase code size, plus additional optimizations to reduce code size. |
| fast | -Oast | Optimization Level 3, plus additional optimizations that may violate the language standards. |
| g | -Og | Enables any optimizations that do not interfere with the debugger or significantly increase the compilation time. |