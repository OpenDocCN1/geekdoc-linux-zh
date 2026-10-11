Some of the environment variables that you will see on the exam that have been covered include PATH, PROMPT, HOME, SHELL, and USER. In addition, commands used to manipulate your command history, such as HISTFILE and HISTFILESIZE, were discussed. Aliases are user variables that enable you to use a short name to enter a complex command.

We also covered how the shell handles command substitution and command completion. The Esc and Tab keys are used to invoke command completion.

You now understand what processes and jobs are, how they work, and how to manipulate them (including background and foreground execution). Setting the priority of a command can be accomplished with the nice command.

The top utility can be used to change the priority of a running process. It also provides information on all running processes. Unlike the ps command, which displays a static view of running processes, top provides a dynamic view.

You also know how to discover the ID of processes (using ps or top) and jobs (using the job command). Use this information in conjunction with the kill or killall command to stop them.

# QUESTIONS AND ANSWERS

+   1.  What command is used to change your shell to another one?
+       A. You would use the chsh command.

+   2.  How do you prevent error messages from appearing on your screen when running a command?
+       A. Redirect the error messages to a location other than the display. There are two ways to do this. If you never want to see them, use command 2> /dev/null. However, if you want to review them at a later time, save them to a file instead by using command 2> filename.

+   3.  You have a file containing the names of your child's teachers. How could you display them in alphabetical order?
+       A. Of course, there are lots of what-ifs here pertaining to how the file is organized. Let's assume that the file contains one name per line. Therefore, you could use
+   
+       `cat file | sort | lpr`

...continues