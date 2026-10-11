# In Depth

One of the most popular programming languages used today is C. Although many computer buffs never need to understand the language or how to work with it, Linux administrators need to have a basic knowledge of how Linux deals with packages written in C. The RPM format has reduced the number of programs people have to compile for their system, but sometimes you won't be able to avoid compiling in C. Knowing a bit about how Linux works with C code can help immensely when you need to fix a package that will not compile properly on your system.

# Linux C Components

Several useful tools are available for C programmers under Linux. This chapter cannot possibly cover all of them, so only the most commonly available tools—mostly GNU tools—and most common tasks are presented here. Do not consider this chapter in any way to be a tutorial on C programming. If you are interested in learning more on this subject, try a book, such as A Book On C, Second Edition, by Al Kelley and Ira Pohl (The Benjamin/Cummings Publishing Company, Inc., 1990).

# The Compiler And Helpers

C is a compiled language, which means that you do not just run C code by itself. Instead, you run it through a processing program that converts your C program into machine language—raw bits and bytes. Compiled software typically runs faster than interpreted software, because the computer does not have to spend time converting the code into its own language.

The C—and C++—compiler used in Linux is often gcc (GNU C Compiler). When you utilize this program to build your code into a machine-executable format, it follows a particular progression of tasks, unless you tell it to do otherwise. This progression breaks down as follows:

+   1.  *Preprocess the code.* This task involves locating the macros contained within the code and expanding them. These macros are typically declared with the **\#define** command.
+   2.  *Compile the code.* The actual job of converting the code to machine language.
+   3.  *Assemble the code.* C code tends to be spread among a collection of files. This task merges the combined compiled code into one file.