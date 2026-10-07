# Chapter 7: Basic Tests 345

# LAB 7.2

# LAB 7.2

# THE [[ COMMAND...
]] OPERATOR

LAB OBJECTIVES
After this lab, you will be able to:
* Use [[ ... ]] in an if Statement
* Use [[ ... ]] Instead of if
* Write Logical Expressions

The purpose of the double-bracket operator ([[ ... ]]) is to generate an exit value that can be tested, and for this reason it is sometimes called the test command. In fact, it replaces an older built-in command, test, and an equivalent, single-bracket ( ) command. You may find those other two commands in older scripts, and they continue to be supported by the KornShell but are no longer needed except backward compatibility. The double-bracket command operator does everything they did, and more.

Because the purpose of [[ ... ]]) is to generate an exit value, it is always used with an if statement or other shell construct that depends on exit values, such as the && and || operators.

The [[ ... ]]) operator allows you to perform a large number of tests that allow your scripts and functions to react intelligently to their environment. You can use the double-bracket to find out files, directories, I/O devices, FDs, and shell options. Many of these tests wouldn't make sense at