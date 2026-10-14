+   - Execute a `return` statement in `main()`, optionally passing a return value in the range 0 to 255 back to `main()`’s caller—for example, a shell script.
+   - Call `exit()` to end the program at any time or place. To make `exit()` available to your program, include the `stdlib.h` header file. Pass to `exit()` a literal value in the range 0 to 255, or use one of the two `stdlib.h` constants `EXIT_SUCCESS` or `EXIT_FAILURE`.
+   - Call the `abort()` function, also declared in `stdlib.h`, from anywhere in the program. Calling `abort()` ends the program immediately and creates a core dump file. This is a drastic measure that is rarely necessary and is not considered good programming.
+   - Throw an exception, but don’t try this yet.

# SUMMARY

This chapter introduced GNU C++ programming with a simple program, welcome.cpp, that shows elements common to all C++ programs large and small. The chapter also explained how to compile and run C++ programs, display text on the console using a variety of methods, call C library functions, create and use C- and C++-style comments, write `main()` functions, and properly begin and end programs.

For more information on subjects introduced in this chapter, turn to the following chapters:

+   - Chapter 6, “Creating Data Objects”
+   - Chapter 8, “Controlling Input and Output”
+   - Chapter 10, “Creating and Calling Functions”
+   - Chapter 11, “Managing Memory with Pointers”
+   - Chapter 16, “Handling Exceptions”
+   - Chapter 20, “Customizing I/O Streams”