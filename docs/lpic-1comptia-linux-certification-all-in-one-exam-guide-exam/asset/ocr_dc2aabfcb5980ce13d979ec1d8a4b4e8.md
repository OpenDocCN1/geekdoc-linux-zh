| Metacharacter | Function | Example |
| :--- | :--- | :--- |
| * | Matches any number of any characters. | Myfile* would match Myfile1, Myfile2, Myfiles, Myfiles23, etc. |
| . | Matches a single character | Myfile. would match Myfile1, Myfile2, and Myfiles, but would not match Myfiles23. |
| ^ | Matches an expression if it appears at the beginning of a line. | ^server would match any instance of "server" as long as it appears at the beginning of a line. |
| $ | Matches an expression if it appears at the end of a line. | server$ would match any instance of "server" as long as it appears at the end of a line. |
| \| | Matches the expressions on either side of the pipe character. | Server\|server would match either "Server" or "server". |
| [nnn] | Matches any one character between the braces. | [xyz] would match any one of "x", "y", or "z". |
| [^nnn] | Matches an expression that does not contain any one of the characters specified. | [^aei] would not match the characters "a", "e", or "i". |
| [n-n] | Matches any single character in the range. | [1-5] would match any number between 1 and 5. |

# Table 4-6 Regular Expressions

The grep utility searches files for lines that match a fixed string. Unlike egrep, it does not perform searches for regular expressions. Instead, fgrep uses direct string comparisons to find matching lines of text in the input. The syntax is fgrep pattern filename. For example, running the fgrep *.c command searches for the string "server" in all files in the current directory whose filename has a ".c" extension.

Let's practice using Linux search tools in the following exercise.

# Exercise 4-4: Using grep

In this exercise, you will practice using Linux search tools. Complete the following:

+   1. With your Linux system running and authenticated as a regular user, switch to root by entering su - followed by your root user's password at the shell prompt.
+   2. Locate references to the initab file in your system log file by entering grep initab /var/log/messages. What can you learn about this file from the output of grep?
+   3. Use egrep to find information about the init process in your system log file by entering egrep init* /var/log/messages at the shell prompt.
+   4. Use egrep again to find information about all the Ethernet interfaces installed in your system by entering egrep eth[0-3] /var/log/messages at the shell prompt.
+   5. Find all lines in your system log file that end with "Enabled" by entering grep Enabled$ /var/log/messages at the shell prompt.

You are now a file system pro! You have to be humble when you know this much!