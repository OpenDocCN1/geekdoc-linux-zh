+   • **env** This command displays the environment variables for the currently logged-in user.

+   • **echo** This command is used to echo a line of text on the screen. It’s frequently used to display environment variables. For example, if you wanted to see the current value of the PATH variable, you could enter echo $PATH.

![](bbox=[0.05, 0.2, 0.14, 0.28])

> **EXAM TIP** The $ character tells echo that the text that comes after it is a variable, not a literal string, and that it should use the current value of that variable. If you were to leave off the $, the echo command would simply display “PATH” on the screen.

+   • **top** This command is a very useful command that displays a list of all applications and processes currently running on the system. You can sort them by CPU usage, memory usage, process ID number, and which user owns them.

+   • **which** This command is used to display the full path to a shell command or utility. For example, if you wanted to know the full path to the ls command, you would enter which ls.

+   • **whoami** This command displays the username of the currently logged-in user.

+   • **netstat** This command displays the status of the network, including current connections, routing tables, etc.

+   • **route** This command is used to view or manipulate the system’s routing table.

+   • **ifconfig** This command is used to manage network boards installed in the system. It can be used to display or modify your network board configuration parameters. This command can be run only by the root user.

+   • **uname** This command returns information about your Linux system using several different options, including:

+   • -s Displays the Linux kernel’s name

+   • -n Displays the system’s hostname

+   • -r Displays the Linux kernel’s release number

+   • -v Displays the Linux kernel’s version number

+   • -m Displays the system’s hardware architecture (such as x86_64)

+   • -p Displays the processor type

+   • -i Displays the hardware platform

+   • -o Displays the operating system

+   • -a Displays all of this information

The list of commands presented here is only intended to acquaint you with com- mon Linux commands and utilities. You will need to be very familiar with these and many other commands for your LPIC-1 and Linux+ exams. Additional commands and utilities will be covered in later chapters in this book.