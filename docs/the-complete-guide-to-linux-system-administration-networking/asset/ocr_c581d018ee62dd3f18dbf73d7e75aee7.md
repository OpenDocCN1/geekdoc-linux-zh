# CHAPTER SUMMARY

+   - Shell scripts let you execute a complex set of commands by entering a single script name. Scripts can include control statements and tests to determine which commands in the script file are executed. Every Linux system includes dozens of examples of shell scripts.
+   - Each script uses keywords from a programming language. An interpreter converts the source code of the script to an executable format as you run it. Compilers perform a similar conversion before a program is executed. The bash shell interpreter is often used for shell scripts.
+   - Each script file must start with a line identifying the interpreter to use for that script; it must have the execute permission set; and it must use only correctly formed statements for the interpreter you are using.
+   - Environment and positional variables are often referenced in scripts. You can also create shell variables to hold information the script needs to process.
+   - When a program closes unexpectedly, the operating system creates a record of the state of the system at the time the program ended and stores this information in a file named core. These core dump files can be used by developers to diagnose what caused the program to end.
+   - Well-written scripts include many comments to help developers understand how a script was designed and what each part of it does.
+   - The read command waits for users to enter information at the keyboard and assigns that information to a variable.
+   - The if-then-else statement tests a condition and executes statements if the condition is present.
+   - The case statement is a cleaner way to provide multiple tests of a variable, with a statement block to be executed for each matching value.
+   - Loops using for and while repeatedly execute a statement block based on either a fixed number of iterations or a condition being tested.
+   - The normal flow of a loop statement can be altered using a break statement (to exit the loop immediately) or a continue statement (to begin the next iteration of the loop immediately).
+   - Functions let a programmer create a set of commands to complete a chosen task, assign those commands a name, and then complete the task by referring to the name at a later time in the script or program. Complex scripts make extensive use of functions.
+   - Shell scripts can be debugged using shell options to check syntax, or to print out each line of the script, either as it is read from the script file or as it is executed by the shell (after all substitutions have been made by the shell). The latter method is called shell tracing.