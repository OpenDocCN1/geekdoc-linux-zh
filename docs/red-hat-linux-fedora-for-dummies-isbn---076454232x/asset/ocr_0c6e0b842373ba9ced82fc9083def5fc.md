If you chose (during installation) not to have X start automatically whenever you boot your system, you see the `login:` prompt.

If you make a mistake while typing the password or your login, the system asks you to retype it.

We strongly recommend that you do most of your experimentation with Red Hat Linux as a nonprivileged user and log in as the root user only when necessary. By operating as root, you run the risk of corrupting your system, having to reinstall again, or losing data because you can delete or change anything and everything. When you are logged in as a regular user, you can accidentally erase your own files and data, but you can’t erase someone else’s files or system files.

Fortunately, Red Hat Linux provides many graphical administration utilities you can start as a nonprivileged user. Each Red Hat administrative utility prompts you to enter the root password as it starts and then performs its specific function, but only that function, with root privileges. You’re prevented, therefore, from doing unintended damage to other systems. (See Appendix C for information about how file permissions work and how you can modify them.)

# The Command-Line Interface (CLI) versus the Graphical User Interface (GUI)

Red Hat Linux installs the X Window System by default. You can perform most administrative tasks with the GUI-based tools (GUI stands for graphical user interface) that Red Hat provides. Most of the how-to instructions in this book use the X-based applications and utilities. We do that because they’re generally easier to use and because this book wasn’t written for systems administrators.

Occasionally, a utility or program doesn’t run graphically; at other times, using nongraphical methods and systems is just more interesting or convenient. Believe it or not, some geekier Linux users *prefer* to use a text-based, command-line interface (CLI). If you’re not familiar with doing some basic administrative tasks with a CLI, we don’t recommend using one just to prove that you can. Being less of a geek is okay. We still like and respect you. On the other hand, it makes good sense to know some basics, just in case a need arises for you to have to wing it with the text-based interface.