+   * Adding dummy functions to make breakpoints easier to set.
+   * A number of tools and libraries besides just general-purpose debuggers exist to help with debugging. The `gdb` library provides a nice internal debugger that uses many of the techniques we described, in a consistent, coherent way.
+   * Multiple dynamic memory debugging libraries exist, with many similar features. We looked at three of them (`etrace`, Electric Fence, and `dmalloc`), and provided pointers to several others. The Valgrind program goes further, finding problems related to uninitialized memory, not just dynamic memory.
+   * `splint` is a modern alternative to the venerable V7 `lint` program. It is available on at least one vendor's GNU/Linux system and can be easily downloaded and built from source.
+   * Besides debugging tools, software testing is also an integral part of the software development process. It should be understood, planned for, and managed from the beginning of any software development project, even personal ones.
+   * Debugging is a skill that can be learned. We recommend reading the book *Debugging* by David J. Agans and learning to apply his rules.

# Exercises

+   1. Compile one of your programs with GCC, using both `-g` and `-O`. Run it under GDB, setting a breakpoint in `main()`. Single-step through the program, and see how closely execution relates (or doesn't relate) to the original source code. This is particularly good to do with code using a `while` or `for` loop.
+   2. Read up on GDB's `conditional breakpoint` feature. How does that simplify dealing with problems that occur only after a certain number of operations have been done?
+   3. Rewrite the `parse_debug()` function from Section 15.4.2.1, "Add Debugging Options and Variables," page 595, to use a table of debugging option strings, flag values, and string lengths.
+   4. (Hard.) Study the `gawk` source code; in particular the NODE structure in `awk.h`. Write a debugging helper function that prints the contents of a NODE based on the value in the `type` field.