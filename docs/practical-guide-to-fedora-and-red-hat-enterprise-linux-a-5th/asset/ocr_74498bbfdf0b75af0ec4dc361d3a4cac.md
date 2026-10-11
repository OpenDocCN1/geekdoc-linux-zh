# CHAPTER SUMMARY  669

The **break** and **continue** control structures alter control within loops: **break** transfers control out of a loop, and **continue** transfers control immediately to the top of a loop.

The Here document allows input to a command in a shell script to come from within the script itself.

+   - **File descriptors**  The Bourne Again Shell provides the ability to manipulate file descriptors. Coupled with the **read** and **echo** builtins, file descriptors allow shell scripts to have as much control over input and output as programs written in lower-level languages.

+   - **Variables**  You assign attributes, such as *readonly*, to *bash* variables using the *type set* builtin. The Bourne Again Shell provides operators to perform pattern matching on variables, provide default values for variables, and evaluate the length of variables. This shell also supports array variables and local variables for functions and provides built-in integer arithmetic capability, using the *let* builtin and an expression syntax similar to the C programming language.

+   - **Builtins**  Bourne Again Shell builtins include *type*, *read*, *exec*, *trap*, *kill*, and *getopts*. The *type* builtin displays information about a command, including its location; *read* allows a script to accept user input.
+   
+      The *exec* builtin executes a command without creating a new process. The new command overlays the current process, assuming the same environment and PID number of that process. This builtin executes user programs and other Linux commands when it is *not* necessary to return control to the calling process.
+   
+      The *trap* builtin catches a signal sent by Linux to the process running the script and allows you to specify actions to be taken upon receipt of one or more signals. You can use this builtin to cause a script to ignore the signal that is sent when the user presses the interrupt key.
+   
+      The *kill* builtin allows you to terminate a running program. The *getopts* builtin parses command-line arguments, making it easier to write programs that follow standard Linux conventions for command-line arguments and options.

+   - **Utilities in scripts**  In addition to using control structures, builtins, and functions, shell scripts generally call Linux utilities. The *find* utility, for instance, is commonplace in shell scripts that search for files in the system hierarchy and can perform a vast range of tasks, from simple to complex.
+   
+      A well-written shell script adheres to standard programming practices, such as specifying the shell to execute the script on the first line of the script, verifying the number and type of arguments that the script is called with, displaying a standard usage message to report command-line errors, and redirecting all informational messages to standard error.

+   - **Expressions**  There are two basic types of expressions: arithmetic and logical. Arithmetic expressions allow you to do arithmetic on constants and variables, yielding a numeric result. Logical (Boolean) expressions compare expressions or strings, or test conditions to yield a *true* or *false* result. As with all decisions within Linux shell scripts, a *true* status is represented by the value zero; *false*, by any nonzero value.