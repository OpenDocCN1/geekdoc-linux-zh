
# SUMMARY

In this chapter, you learned:

- Open source software is software with source code that anyone can freely use, study, modify, and share.
- A Linux distribution is an installable operating system constructed from a Linux kernel and supporting user programs and libraries.
- Red Hat participates in supporting and contributing code to open source projects, sponsors and integrates project software into community-driven distributions, and stabilizes the software to offer it as supported enterprise-ready products.
- Red Hat Enterprise Linux is Red Hat's open source, enterprise-ready, commercially-supported Linux distribution.

## CHAPTER 2

## ACCESSING THE COMMAND LINE

## GOAL

Log in to a Linux system and run simple commands using the shell.

## OBJECTIVES

- Log in to a Linux system on a local text console and run simple commands using the shell.
- Log in to a Linux system using the GNOME 3 desktop environment and run commands from a shell prompt in a terminal program.
- Save time using tab completion, command history, and command editing shortcuts to run commands in the Bash shell.

## SECTIONS

- Accessing the Command Line (and Quiz)
- Accessing the Command Line Using the Desktop (and Guided Exercise)
- Executing Commands Using the Bash Shell (and Quiz)

## LAB

Accessing the Command Line

![](img/59afb92e10b67a9cecc358a2c65e93b5_32_0.png)

## ACCESSING THE COMMAND LINE

## OBJECTIVES

After completing this section, you should be able to log in to a Linux system and run simple commands using the shell.

## INTRODUCTION TO THE BASH SHELL

A command line is a text-based interface which can be used to input instructions to a computer system. The Linux command line is provided by a program called the shell. Various options for the shell program have been developed over the years, and different users can be configured to use different shells. Most users, however, stick with the current default.

The default shell in Red Hat Enterprise Linux is the GNU Bourne-Again Shell (bash). Bash is an improved version of one of the most successful shells used on UNIX-like systems, the Bourne Shell (sh).

When a shell is used interactively, it displays a string when it is waiting for a command from the user. This is called the shell prompt. When a regular user starts a shell, the default prompt ends with a $ character, as shown below.

```
[user@host ~]$
```

$ is replaced by a # character if the shell is running as the superuser, root. This makes it more obvious that it is a superuser shell, which helps to avoid accidents and mistakes which can affect the whole system. The superuser shell is shown below.

```
[root@host ~]#
```

Using bash to execute commands can be powerful. The bash shell provides a scripting language that can support automation of tasks. The bash shell can simplify or make possible operations that are hard to accomplish efficiently with graphical tools.

> similar in concept to the command-line interpreter found in recent versions of Microsoft Windows, cmd.exe, although bash has a more sophisticated scripting language. It is also similar to Windows PowerShell in Windows 7 and Windows Server 2008 R2 and later. Administrators using the Apple Mac who use the Terminal utility may be pleased to note that bash is the default shell in macOS.

## SHELL BASICS

Commands entered at the shell prompt have three basic parts:

- Command to run
- Options to adjust the behavior of the command
- Arguments, which are typically targets of the command

The **command** is the name of the program to run. It may be followed by one or more options, which adjust the behavior of the command and what it will do. Options may start with one or two dashes (-a or --all), to distinguish them from arguments. Arguments may be followed by one or more arguments, which often identify a target that the command should operate upon.

For example, the command `usermod -l user01` has a command **(usermod)**, an option (-l), and an argument **(user01)**. The effect of this command is to lock the password of the **user01** account.

## LOGGING IN TO A LOCAL COMPUTER

To run shell, you need to log in the computer on a **terminal**. A terminal is a text-based interface used to enter commands and print output from a computer system. There are several ways to do this.

The computer might have a keyboard and display for input and output directly connected to it. This is the Linux machine's **physical console**. The physical console supports multiple virtual **consoles**. Each virtual console supports an independent login session. You can switch between these consoles by pressing **Ctrl+1+Alt** and a function key (**F1** through **F6**) at the same time. Most of these virtual consoles provide a terminal providing a login prompt, and if you enter your username and password, you get a shell.

The computer might provide a graphical login prompt on one of the virtual consoles. You can use this to log in a graphical environment. The graphical environment also runs on a virtual console. To get a shell you must start a terminal program in the graphical environment. The shell prompt is provided in an application window of your graphical terminal program.

> NOTE Many system administrators choose not to run in a graphical environment on their servers. This allows resources which would be used by the graphical environment to be used by the server's services instead.

In Red Hat Linux 8, if the graphical environment is available, the login screen will run on the first virtual console, **tty1**. Five additional virtual login prompts are available on virtual consoles two through six.

If you log in using the graphical login, your graphical environment will start on the first virtual console that is not currently being used by a login session. Normally, your graphical session will replace the login prompt on the second virtual console (**tty2**). However, if console is used by an active text session (not just a login), the next free virtual console is used instead.

The graphical login continues to run on the first virtual console (**tty1**). If you are already logged in to a graphical session, log in another on the graphical login screen or use the **Switch User** menu item to switch users in the graphical environment without logging out, another graphical environment will be started for that user on the next free virtual console.

When you log out of a graphical environment, it will exit and the physical console will automatically switch back to the graphical login screen on the first virtual console.

## CHAPTER 2 | Accessing the Command Line

## NOTE

In Red Hat Enterprise Linux 6 and 7, the graphical login screen runs on the first virtual console, but when you log in your initial graphical environment replaces the login screen on the first virtual console instead of starting on a new virtual console.

In Red Hat Enterprise Linux 5 and earlier, the first virtual consoles always provide text login prompts. If the graphical environment is running, it is on virtual console (accessed through Ctrl+Alt+F7).

A headless server does not have a keyboard and display connected to it. A data center may be filled with racks of headless servers, and not providing each with a keyboard and display saves space and expense. To allow administrators in, a headless server might have a login prompt provided by its serial console, on a serial port which is connected to a networked server for remote access to the serial.

The serial console would normally be used to fix the server if its own network card becomes misconfigured and logging over its own network connection becomes impossible. Most of the time, headless servers are accessed by other means over the network.

## LOGGING OVER THE NETWORK

Linux users and administrators often need to get shell access to a remote system by connecting to it over the network. In modern computing environment, many headless servers are actually virtual machines or running as public or private cloud instances. These systems are physical and do not have hardware consoles. They might not even provide access to their (simulated) physical console or serial console.

In Linux, the most common way to get a shell prompt on a remote system is to Use Shell (SSH). Most Linux systems (including Red Hat Enterprise Linux) and macOS provide the OpenSSH command-line program for this.

In this example, a user with a shell prompt on the machine host uses ssh to log in to the remote Linux system remotehost as the remoteuser:

```
[user@host ~] ssh remoteuser@remotehost
remoteuser@remotehost: password
[remoteuser@remotehost ~$]
```

The ssh command encrypts the connection to secure the communication against eavesdropping or hijacking of the passwords and content.

Some systems (such as cloud instances) do not allow users to use a password to log in with ssh for tighter security. An alternative way to authenticate a remote machine without entering a password is through public key authentication.

With this authentication method, users have a special file containing a private key, which is equivalent to a password, and they keep it secret. Their account on the server is configured with a matching public key, which does not have to be secret. When logging in, users can configure ssh to provide the private key and if their matching public key is installed in that account on remote server, it will log them in without asking for a password.
