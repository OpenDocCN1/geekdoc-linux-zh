Lint is another useful tool. The **lint** command examines the source code for possible problems. The code may compile completely and cleanly, but it may execute incorrectly. Lint is stricter than the compiler. It detects and reports on a wide variety of problems and potential problems, including variables that are used before a value has been assigned to it, arguments to functions that are never used, and functions using return values that were never returned.

You are free to ignore Lint's warnings and complete the compile, but a warning typically means that the program has a bug or a non-portable construct, or that you have violated a standard of good programming. Paying attention to Lint's warnings is a good way not only to debug your programs but also to hone your programming skill.

# # 13 - C Language

There are many programming basics that span both C and C++. These basics will be introduced using C language. The upcoming programming sections are only an introduction. They don't provide enough of information to be used as a reference for the C language. You want to supplement this section with a book dedicated to the C language.

C programs are written in terms of functions. A program will go into functions, execute the logic and leave. Frequently, functions are made up of other functions and statements. Statements are lines of code that carry out a task.

A C program must have a function called main(). Within the main() function is the body of the program as shown in Figure 14-15. The body consists of statements and functions. Preprocessor directives are listed outside and above the main() function.