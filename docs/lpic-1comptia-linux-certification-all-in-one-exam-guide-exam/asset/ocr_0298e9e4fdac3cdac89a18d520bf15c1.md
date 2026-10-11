Therefore, we will spend a great deal of time working with the Linux command-line interface in this book. We will discuss the following topics:

+   • Linux shells
+   • Managing shell configuration files

Let’s begin by discussing commonly used Linux shells.

# ## Linux Shells

To fully understand how the command-line interface works under Linux, you need to understand the concept of a shell. A shell is a command interpreter that allows you to type commands at the keyboard that are sent to the operating system kernel.

Back in the days before Windows, most computer users had no choice but to be familiar with command-line shells. In the various versions of DOS that were in use back then, the only way you could communicate with the operating system was to enter commands through a command-line interpreter called COMMAND.COM.

Linux also uses a command-line shell. However, unlike DOS, Linux enables you to choose from a variety of shells. As with many other aspects of Linux, you can try out several different command-line shells and choose the one that you like the best. Some of the more popular shells include the following:

+   • **sh (Bourne Shell)** The sh shell was the earliest shell, being developed for UNIX back in the late 1970s. While not widely used on Linux systems, it is still frequently used on UNIX systems.
+   • **bash (Bourne-Again Shell)** The bash shell is an improved version of the sh shell and is one of the most popular shells today. In fact, it’s the shell used by default on most Linux distributions. If you’re using the command-line interface on a Linux system, more than likely you’re using the bash shell.
+   • **csh (C Shell)** The csh shell was originally developed for BSD UNIX. It uses a syntax that is very similar to C programming.
+   • **tsh** The tsh shell is an improved version of the C shell. It is the default shell used on FreeBSD systems.
+   • **zsh (Z Shell)** The Z shell is an improved version of the bash shell.

When you first boot your Linux system and log in, your default shell is loaded. You can identify which shell you’re using by entering `echo $SHELL` at the command prompt. The `echo` command is used to display text on the screen. Adding `$SHELL` to the `echo` command tells `echo` to display the contents of the SHELL environment variable for the currently logged-in user. An example is shown in Figure 2-3, where the bash shell is set to be the default shell for the rtracy user account.

However, you’re not stuck with the default shell. If you want to switch to a different shell, simply enter the shell’s command name at the prompt. For example, if you are currently using the bash shell and want to use zsh instead, simply enter `zsh` at the prompt. To stop using the new shell and revert back to the original shell, enter `exit`.