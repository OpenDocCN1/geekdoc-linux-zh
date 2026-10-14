
Linux"), is called KDevelop. This tool is shown in Figure 14-5; you can start it by selecting Programming, then KDevelop on the GNOME main menu.

![](img/43f64015de86d989e30eff5bb284fb96_689_0.png)

Figure 14-5 The KDevelop programming IDE

Another type of programming tool is called a Rapid Application Development (RAD) tool. RAD packages try to simplify the development of complex software projects by providing prewritten modules, by helping you track multiple parts of a project and reusing parts of the software you have written, and by using many other advanced techniques. One powerful example of a RAD package for Linux is OmniStudio, currently marketed by Raining Data Corporation (see www.rainingdata.com).

You can learn about programming for Linux using C, C++, or other interpreted or compiled languages by reviewing the documentation that comes with your Linux distribution. But a beginning guide to computer programming or classroom training usually provides a much better learning experience. Red Hat Software offers 5-day programming courses for beginning Linux software developers, or for more advanced developers to learn about converting applications from other systems to Linux, programming for devices, programming for the Linux kernel, and other related topics. Information about these courses is available at www.redhat.com/training.

Many independent training companies also offer programming courses for working professionals. At least a basic understanding of computer programming in Linux with commonly used languages is an important skill for system administrators who hope to advance in their careers.

## CHAPTER SUMMARY

- Shell scripts let you execute a complex set of commands by entering a single script name. Scripts can include control statements and tests to determine which commands in the script file are executed. Every Linux system includes dozens of examples of shell scripts.
- Each script uses keywords from a programming language. An interpreter converts the source code of the script to an executable format as you run it. Compilers perform a similar conversion before a program is executed. The bash shell interpreter is often used for shell scripts.
- Each script file must start with a line identifying the interpreter to use for that script; it must have the execute permission set; and it must use only correctly formed statements for the interpreter you are using.
- Environment and positional variables are often referenced in scripts. You can also create shell variables to hold information the script needs to process.
- When a program closes unexpectedly, the operating system creates a record of the state of the system at the time the program ended and stores this information in a file named core. These core dump files can be used by developers to diagnose what caused the program to end.
- Well-written scripts include many comments to help developers understand how a script was designed and what each part of it does.
- The read command waits for users to enter information at the keyboard and assigns that information to a variable.
- The if-then-else statement tests a condition and executes statements if the condition is present.
- The case statement is a cleaner way to provide multiple tests of a variable, with a statement block to be executed for each matching value.
- Loops using for and while repeatedly execute a statement block based on either a fixed number of iterations or a condition being tested.
- The normal flow of a loop statement can be altered using a break statement (to exit the loop immediately) or a continue statement (to begin the next iteration of the loop immediately).
- Functions let a programmer create a set of commands to complete a chosen task, assign those commands a name, and then complete the task by referring to the name at a later time in the script or program. Complex scripts make extensive use of functions.
- Shell scripts can be debugged using shell options to check syntax, or to print out each line of the script, either as it is read from the script file or as it is executed by the shell (after all substitutions have been made by the shell). The latter method is called shell tracing.
- Many scripting languages are used on Linux systems, including perl, PHP, Python, and Tcl/Tk. Some are appropriate for use with Web servers via CGI; some are appropriate for creating graphical programs.
- Linux includes support for many computer languages. The C and C++ languages are the most widely used. Each relies on a compiler to convert source code to an executable file. IDEs and RAD programs are commonly used to ease the complexity of developing large programs.
- A knowledge of programming languages and tools is very useful for advanced system administrators.

## COMMAND SUMMARY

| Command | Description | Example |
|---|---|---|
| break | Used within a for or while loop to exit from the loop immediately | {qQ} break ; |
| case | Introduces a test that is compared against a set of values, each followed by a statement block to be executed if the value matches the variable being tested | case $# in |
| configure | Creates a configuration file for the make command based on various parameters | configure |
| continue | Used within a for or while loop to immediately begin with the next iteration of the loop (return to the top of the loop) | continue |
| do | Used with the done command to enclose a statement block as part of a for loop or a while loop | do |
| done | Used with the do command to enclose a statement block as part of a for loop or a while loop | done |
| elif | Introduces an if-then-else statement that is the first statement in the else block of another if-then-else statement. Used in place of else if | elif [ $# = 3 ]; then |
| else | Extends the capability of an if-then statement by adding a statement block that is only executed if the test after it returns a value of false (that is, if the test fails) | else |
| esac | Ends a case statement block | esac |
| exit | Stops the execution of a script immediately; can optionally include an exit code | exit 1 |
| fi | Marks the end of an if-then or if-then-else statement block | fi |
| for | Repeats a statement block one time for each item in a list | for NEXTFILE in $@ |
| if | Introduces a test within a shell script. An if command is always followed by a then command. | if [ ! -f "$NEXTFILE" ]; |
| in | Used as part of a for loop, before the list of items to be used as variable values for each iteration of the loop | for NEXTFILE in $@ |
| perl | Starts the perl language interpreter | perl ./myscript.pl |
| read | Pauses for a user to input data at the keyboard and assigns that input to a variable | read FILENAME |
| set | Views or sets environment variables or shell options | set -x |
| test | Evaluates the arguments provided after the command name and returns either true (a value of 1) or false (a value of 0) | if test $1 -eq report |
| then | Begins a statement block of commands to be executed if the test introduced by an if command succeeds (returns a value of true) | then |
| while | Creates a loop based on a test. The loop executes a statement block as long as the test returns true. | while [ ! -f $DB_FILE ] ; |
| wish | Starts the Tcl/Tk language interpreter | wish ./myscript.tcl |

## Key Terms

$@ — A special shell variable that includes all of the parameters on the command line.

binary file — See executable file.

comment — A line in a script or source code that is not processed by the interpreter or compiler, but is only included to help someone reading the file understand the purpose or operation of the script or source code. Comments in shell scripts and many other languages are created by beginning a line with the # character.

Common Gateway Interface (CGI) — A method of communication between two programs using the standard input and standard output channels.

compiled language — A computer language for which the source code is converted to a binary file before the program is executed.

compiler — A program that converts the source code of a compiled language into a binary file.

computer language — A set of words and syntax rules that can be arranged in predefined ways to cause a computer to perform tasks defined by the person using the language.
