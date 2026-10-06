# Part I ✦ Linux First Steps

+   Special shell features enable you to gather data input and direct data output between commands and the Linux file system. To save on typing, you can find, edit, and repeat commands from your shell history. Many power users hardly touch a graphical interface, doing most of their from a shell.

+   You can gather commands into a file using programming constructs such as loops and case statements to quickly do complex operations that would be difficult to retry over and over. Programs consisting of commands that are stored and run from a file are referred to as shell scripts. Most Linux system administrators use shell scripts to automate tasks such as backing up data, monitoring log files, or checking system health. (See Chapter 28 for information on shell scripts).

The shell is a command interpreter. If you use Microsoft operating systems, you'll find using a shell in Linux is similar to—but generally more powerful than—the interpreter used to run commands in DOS. You can use Linux from a graphical desktop interface, but as you grow into Linux you will surely need to use the shell at some point to track down a problem or administer features.

How use the shell isn't obvious at first, but with the right help you can quickly learn many of the most important shell features. This chapter is your guide to working with the Linux system commands, processes, and file system from the shell. It describes the shell environment and helps you tailor it to your needs. It explains how to use and move around the file system.

# Starting a Shell

There are several ways to get to a shell interface in Linux. Three of the most common are the shell prompt, Terminal window, and virtual terminal. They're described in the following sections.

# Using the Shell Prompt

If your Linux system has no graphical user interface (or one that isn't working at the moment), you will most likely see a shell prompt after you log in.. Typing commands from the shell will probably be your primary means of using the Linux system.

The default prompt for a regular user is simply a dollar sign:

```
$
```

The default prompt for the root user is a pound sign (also called a hash mark):

```
#
```