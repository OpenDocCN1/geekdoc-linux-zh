# LE WORKING FROM THE COMMAND LINE

+   Advantages of the textual interface

Before the introduction of the GUI, UNIX and then Linux provided only a textual (command-line) interface (CLI). Today, a textual interface is available when you log in from a terminal, a terminal emulator, or a textual virtual console, or when you use ssh to log in on a system.

Although the concept might seem antiquated, the textual interface has a place in modern computing. In some cases an administrator might use a command-line tool either because a graphical equivalent does not exist or because the graphical tool is not as powerful, flexible, or refined as the textual one. For example, chmod (page 193) provides finer granularity than its GUI counterpart (File Browser Object Properties window, Permissions tab; page 105). On a server system, a graphical interface might not even be installed. The first reason for this omission is that a GUI consumes a lot of system resources; on a server, those resources are better dedicated to the main task of the server. Additionally, security considerations mandate that a server system run as few tasks as possible because each additional task provides an additional attack vector.

You can also write scripts using the textual interface. Using scripts, you can easily reproduce tasks on multiple systems, enabling you to scale the tasks to larger environments. When you are the administrator of only a single system, using a GUI is often the easiest way to configure the system. When you act as administrator for many systems, all of which need the same configuration installed or updated, a script can make the task go more quickly. Writing a script using command-line tools is frequently easy, whereas the same task can be difficult to impossible using graphical tools.

+   Pseudographical interface

Before the introduction of GUIs, resourceful programmers created textual interfaces that included graphical elements such as boxes, borders outlining rudimentary windows, highlights, and, more recently, color. These textual interfaces, called pseudographical interfaces, bridge the gap between textual and graphical interfaces. The Midnight Commander file management utility (mc; midnight-commander.org) is a good example of a utility with a well-designed pseudographical interface.

+   Command-line (bash) coverage

This section introduces the Linux CLI. Chapter 5 is the first of three chapters dedicated to the Bourne Again Shell (bash). Chapter 7 describes some of the more important utilities you can use from the command line. Chapter 9 covers advanced bash concepts. Chapter 27 describes shell programming using bash. Most of the examples in Parts III and IV of this book use the CLI, adding examples of graphical tools where available.

# RUNNING COMMANDS FROM THE COMMAND LINE

This section describes three ways to work from the command line: using a terminal emulator, using a virtual console, and logging in remotely. If the local system does not