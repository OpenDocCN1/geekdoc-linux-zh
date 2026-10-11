
## Answers

- 1. D. Hardware and operating systems are modular. As long as the hardware is supported, you can install any operating system designed for your specific CPU architecture.
- 2. B. The Linux kernel is the component that handles operating system functions.
- 3. C. Libraries contain prewritten code that programmers can reuse in their applications.
- 4. D. Andrew Tanenbaum wrote the Minix operating system when universities were no longer allowed access to the UNIX source code.
- 5. E. Linus Torvalds posted the source code for his Linux kernel on the Internet and invited other programmers to modify and enhance it.
- 6. A. Richard Stallman championed the freely distributable source code concept behind GNU.
- 7. D. Under the GPL, you are free to download the Linux source code and modify it.
- 8. A. A variety of powerful e-mail packages are available for Linux that make it highly suitable for large organizations.
- 9. C, D. The CUPS service provides network printing to other Linux systems. When combined with Samba, network printing can be extended to Windows systems (as well as any other operating system that supports Samba, including Linux and Mac OS X).
- 10. B, D. The NFS service can be used to provide file sharing for systems running an NFS client. The Samba service can also be used to support Samba-compatible clients, such as Windows, Mac OS X, and Linux systems.
- 11. A, C. MySQL and PostgreSQL are both powerful Linux database services.
- 12. E. The Squid service can turn a Linux system into an application-level gateway.

## Working with the Linux Shell

In this chapter you will learn about

- How the Linux shell works
- Using the shell prompt
- Getting help for Linux shell commands
- Working with environment variables
- Working with aliases
- Using redirection and piping

For an operating system to be useful, it must provide some means for the user to communicate with it. Users need a way to tell the operating system what tasks it needs to complete, such as running a program, copying a file, or shutting the system down. These commands are given through a user interface. Linux provides two types of user interfaces:

- **Command-line interface (CLI)** With the command-line interface, the user communicates with the Linux operating system by typing commands at a command prompt, as shown in Figure 2-1.
- **Graphical user interface (GUI)** In addition to a command-line interface, Linux also offers users an easy-to-use graphical user interface. While most system administrators will be comfortable with the Linux CLI, many end users aren't. They are much more comfortable with a GUI. Because of the dominance of Microsoft Windows in the home computer market, most end users have never used a command-line type of interface. To make life easier, the X Window System was developed to provide a windows-based GUI on the Linux operating system. Using the X Window System along with a window manager and a desktop environment (such as GNOME or KDE), users can interact with the Linux kernel using a mouse. The GNOME graphical interface is shown in Figure 2-2.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_60_0.png)

**Figure 2-1** The Linux command-line interface

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_61_0.png)

In this chapter, we’ll focus on working with the Linux CLI. Use and configuration of the Linux GUI will be addressed in a later chapter.

### How the Linux Shell Works

While graphical user interfaces are generally easier to use, many of the tasks you must perform to administer and support a Linux system must be done from the command line. Basically, end users use the GUI; administrators use the command line.

> EXAM TIP On the LPIC-1 and Linux+ exams, you will be tested very heavily on your ability to use the Linux CLI to manage the system.

Therefore, we will spend a great deal of time working with the Linux command-line interface in this book. We will discuss the following topics:

- Linux shells
- Managing shell configuration files

Let’s begin by discussing commonly used Linux shells.

### Linux Shells

To fully understand how the command-line interface works under Linux, you need to understand the concept of a shell. A shell is a command interpreter that allows you to type commands at the keyboard that are sent to the operating system kernel.

Back in the days before Windows, most computer users had no choice but to be familiar with command-line shells. In the various versions of DOS that were in use back then, the only way you could communicate with the operating system was to enter commands through a command-line interpreter called COMMAND.COM.

Linux also uses a command-line shell. However, unlike DOS, Linux enables you to choose from a variety of shells. As with many other aspects of Linux, you can try out several different command-line shells and choose the one that you like the best. Some of the more popular shells include the following:

- **sh (Bourne Shell)** The sh shell was the earliest shell, being developed for UNIX back in the late 1970s. While not widely used on Linux systems, it is still frequently used on UNIX systems.
- **bash (Bourne-Again Shell)** The bash shell is an improved version of the sh shell and is one of the most popular shells today. In fact, it’s the shell used by default on most Linux distributions. If you’re using the command-line interface on a Linux system, more than likely you’re using the bash shell.
- **csh (C Shell)** The csh shell was originally developed for BSD UNIX. It uses a syntax that is very similar to C programming.
- **tsh** The tsh shell is an improved version of the C shell. It is the default shell used on FreeBSD systems.
- **zsh (Z Shell)** The Z shell is an improved version of the bash shell.

When you first boot your Linux system and log in, your default shell is loaded. You can identify which shell you’re using by entering `echo $SHELL` at the command prompt. The `echo` command is used to display text on the screen. Adding `$SHELL` to the `echo` command tells `echo` to display the contents of the SHELL environment variable for the currently logged-in user. An example is shown in Figure 2-3, where the bash shell is set to be the default shell for the rtracy user account.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_63_0.png)

However, you’re not stuck with the default shell. If you want to switch to a different shell, simply enter the shell’s command name at the prompt. For example, if you are currently using the bash shell and want to use zsh instead, simply enter `zsh` at the prompt. To stop using the new shell and revert back to the original shell, enter `exit`.

> EXAM TIP You can also specify the default shell to use by modifying your user account details. We’ll discuss how to do this in a later chapter in this book. The LPIC-1 and Linux+ exams require you only to be familiar with the bash shell. Therefore, only bash will be addressed in this chapter.

Linux is capable of running multiple shell sessions at once. Each session can run its own programs, all simultaneously. This can be very useful if you have one program running and then need access to the command prompt. Simply press ALT-Fx (where x is a number from 2 to 6) to open a new session. For example, to switch to the third alternate console screen, press ALT-F3. You can then return to your original session by pressing ALT-F1.

As with Windows, you can also run terminal sessions within the Linux GUI. This is done by running a terminal program such as Konsole or GNOME Terminal. To run multiple command-line sessions, simply open two or more terminal windows. Each shell session runs its programs independently of the other sessions. This is shown in Figure 2-4.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_63_1.png)

This can also be accomplished in a second way. While you’re within the Linux GUI, press CTRL-ALT-Fx (where x is a number from 1 to 6). This will switch you to a text-based shell prompt. To switch back to your GUI environment, press ALT-F7 (on most distributions).
