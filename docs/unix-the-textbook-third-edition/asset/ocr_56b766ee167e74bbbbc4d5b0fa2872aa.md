```
Name: redhat.com

Address: 209.132.183.105

$
```

16. Modify the script in the case_demo file in Section 12.6.6 so that it allows you to try any number of options and quits only when you use the q option.

17. Write a Bourne Shell script that displays the following menu and prompts you for one-character input to invoke a menu option, as follows:

+   a. List all files in the present working directory
+   b. Display today's date and time
+   c. Invoke the shell script for Problem 14
+   d. Display whether a file is a simple file or a directory
+   e. Create a backup for a file
+   f. Start a secure shell (ssh) session
+   g. Start an ftp session
+   h. Exit

Option (c) requires that you ask for a list of login names; and for options (d) and (e), insert a prompt for file names before invoking a shell command/program. For options (f) and (g), insert a prompt for a domain name (or IP address) before initiating an ssh or ftp session. The program should allow you to try any option any number of times and should quit only when you give option x as input. A good programming practice for you to adopt is to build code incrementally—that is, write code for one option, test it, and then go to the next option.

18. Modify the Bourne Shell script for Problem 17 so that it executes code for each option under a child shell. Display the PID for the child shell whenever it is initiated to run the code for an option, before the code is executed.

19. What is the purpose of the echo * command? Run the command on your system and explain the output of the command.