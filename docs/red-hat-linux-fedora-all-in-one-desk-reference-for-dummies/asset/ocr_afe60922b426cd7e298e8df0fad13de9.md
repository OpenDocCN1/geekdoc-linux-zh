In addition to learning the basic programming steps, you also need to be familiar with the following terms and concepts:

+   - *Variables* are used to store different types of data. You can think of each variable as being a placeholder for data — kind of like a mailbox, with a name and room to store data. The content of the variable is its value.
+   - *Expressions* combine variables by using operators. An expression may add several variables; another may extract a part of a string.
+   - *Statements* perform some action, such as assigning a value to a variable or printing a string.
+   - *Flow-control statements* allow statements to be executed in various orders, depending on the value of some expression. Typically, flow-control statements include `for`, `do while`, `while`, and `if then else` statements.
+   - *Functions* (also called *subroutines* or *routines*) allow you to group several statements and give them a name. This feature allows you to execute the same set of statements by invoking the function that represents those statements. Typically, a programming language provides many predefined functions to perform tasks such as opening (and reading from) a file.

# Exploring the Software Development Tools in Red Hat Linux

Red Hat Linux includes these traditional UNIX software development tools:

+   - Text editors such as `vi` and `emacs` for editing the source code. (To learn more about `vi`, see Book II, Chapter 6.)
+   - A C compiler for compiling and linking programs written in C — the programming language of choice for writing UNIX applications (though nowadays many programmers are turning to C++ and Java). Red Hat Linux includes the GNU C and C++ compilers. Originally, the GNU C Compiler was known as GCC — which now stands for *GNU Compiler Collection* (see description in gcc.gnu.org).
+   - The GNU `make` utility for automating the software *build process* — the process of combining object modules into an executable or a library.
+   - A debugger for debugging programs. Red Hat Linux includes the GNU debugger `gdb`.
+   - A version-control system to keep track of various revisions of a source file. Linux comes with RCS (Revision Control System) and CVS (Concurrent Versions System). Nowadays most open-source projects use CVS as their version-control system.