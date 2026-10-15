11. Enhance the diff2 script in Section 13.5 so that it displays the line numbers where the two files differ.

12. Enhance the diff2 script of Problem 11 so that, if only one file is passed to it as a parameter, it uses standard input as the second file.

13. Write a Bourne shell script for Problem 16 in Chapter 12, but use functions to implement the service code for various options.

14. Suppose a function, f, is defined first, followed by defining f as a variable. Would f refer to the function or the variable after you have provided the second definition? Why? Show a shell session to support your answer.

15. Write a Bourne shell script that implements the following menu options:

+   a. Display the CPU used by your system
+   b. Display the name of the operating system used by your computer
+   c. Display a and b on the screen separated by a vertical tab
+   d. Display the full pathnames for the commands that have been executed on your system
+   e. Display the maximum number of files a process may open
+   f. Display the maximum number of simultaneous processes a user may have on the system

Your program should not terminate on signals 1, 2, 3, 15, and 18. Make use of a function to display the program menu.

Hint: Review the man pages for the following commands: hash, ulimit, uname.