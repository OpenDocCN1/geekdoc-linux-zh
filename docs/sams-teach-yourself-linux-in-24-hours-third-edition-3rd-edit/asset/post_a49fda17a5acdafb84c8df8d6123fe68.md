
## PART II
### Learn the Ropes
### Hour
- 5 Getting Acquainted with the Shell
- 6 Looking at the Command Line
- 7 Moving Around the Filesystem
- 8 Text Editing with vi

![](img/782ecfdc0b083a767896cc983e10427f_94_0.png)

## Hour 5
### Getting Acquainted with the Shell
As you follow along in the hours to come, you'll learn how to type a few words on the infamous Linux command line and have the Linux operating system do what you want done. This magical rapport is accomplished with the help of a small Linux program called a shell. The shell program is the interpreter through which you communicate with the operating system. As you type in a command at the shell prompt, it is interpreted and passed to the Linux kernel. The kernel, in turn, tells the computer what to do.

In this hour, you will
- Learn how shells interact between you, the user, and the Linux kernel
- Use environment variables to customize the look and behavior of the shell
- Edit text on the command line, and recall previously used commands
- Create shortcuts for long commands, or frequently used commands, with command aliases

![](img/782ecfdc0b083a767896cc983e10427f_96_0.png)

### Task: Creating a Temporary User Account
When you installed Linux, you created a superuser (or root user) account and possibly one unprivileged user account. For each account, you might have selected a shell program or you might have used the default settings. Whichever shell you chose, the shell loads automatically when you log in to your account. The shell found in most Linux distributions and installed by default is the bash shell.

If you didn't create an account for an unprivileged user during the installation of the Linux operating system, you will want to do so now. You will remember from previous chapters that the superuser account should be used only for system administration and configuration jobs. Before you begin working with the shell, experimenting with commands and applications, and exploring the Linux operating system, you need to create a login for a user account. Here's how to use the adduser and passwd commands to create a login:

1. Select a username. Each user on the system needs a unique login name to access the system and his or her user account. Usernames should be no more than eight characters. To make the job of the system administrator simpler, use lowercase letters for usernames.

In this task, we'll create a user account for Rusty Spoon. The username that we have selected is rusty. You can substitute your own username, or you use this username to play with the Linux commands and explore the system.

2. Choose a password. A good password should be a combination of uppercase letters, lowercase letters, and numbers. A password should be at least eight characters. Do not use any word that can be found in the dictionary and use a character only once in a password.

3. Log in as superuser. At the login prompt, type root and press Enter. You are then prompted for a password. Type the password and press Enter. The shell prompt for the superuser account on a Linux-Mandrake system might look something like:

```
[root@localhost /root]#
```

4. Create the user account. At the shell prompt, type adduser rusty and press Enter (you may substitute your own username). Your display should look like the following:

```
[root@localhost /root]# adduser rusty
[root@localhost /root]#
```

5. Assign the password to the account. Type passwd rusty and press Enter. You'll see the following:

```
[root@localhost /root]# passwd rusty
Changing password for user rusty
New UNIX password:
```

Type the password and press Enter. If the system uses shadow passwords, you'll notice that the password does not appear while you are typing. This ensures that your system stays secure. You will need to verify the password by entering it a second time and pressing Enter. The system shows the following:

```
Retype new UNIX password:
passwd: all authentication tokens updated successfully
[root@localhost root]#
```

6. Switch to a new terminal. Instead of logging out of the superuser account to get to your user account, press Alt+F2 to display a new terminal window and a login prompt as follows:

```
Linux Mandrake release 7.1b (hydrogen)
Kernel 2.2.15-0.25mdk on an i586 / tty2
localhost login:
```

In the second line, tty2 is the virtual terminal that you are currently using. If you need to return to the superuser account, press Alt+F1.

7. Log in to your user account. At the login prompt, type the username for the account and press Enter. You are then prompted for a password. Type the password and press Enter. You're now working in the shell and the shell prompt will look something like the following:

```
[rusty@localhost rusty]$
```

The adduser and passwd commands are a fast and easy way to add new users to the system, assign a shell, and create a home directory. Our imaginary user rusty can now use the system. When rusty logs in, the bash shell will start because it is the default shell used by the passwd command. In addition, the home directory for the account is located at /home/rusty.

## Looking at the Shell Programs
One of the installation suggestions made in Hour 2, “Installing Linux-Mandrake,” was that you not have the X Window System start automatically when you boot the Linux operating system. If you followed this suggestion, when the system boots, you are presented with a text screen that asks for a login name and a password. After you enter this information, the system checks to see whether you are a properly authorized user and, if you are, it presents you with the shell prompt. An example of a shell prompt for the superuser on a Linux-Mandrake system is

```
[root@localhost /root]#
```

![](img/782ecfdc0b083a767896cc983e10427f_98_0.png)

If you are using one of the graphical desktop environments, such as KDE or GNOME, you can display the shell prompt by opening a terminal emulation program. Browse through the menu system to find a number of these terminal emulation programs. They have various names, such as XTerm, GNOME terminal, Eterm, and Konsole.

The shell prompt is your gateway to the Linux kernel and enables you to work with any program, command, or utility installed on the system. But wait...the shell can do much more for you. The shell keeps track of the work you've performed on the computer. It enables you to use shortcuts to request programs and commands. It also helps you automate routine tasks, such as file backups. You do this by writing scripts that the shell can read at specified times and then pass the instructions to the operating system.

New Term
A shell program is the user interface to the computer system for the Linux operating system. This interface accepts commands from the user and translates it into a language that the operating system (more specifically, the Linux kernel) can understand. The shell can also be used to write programs, automate job control, and provide a scripting mechanism to customize the way the system works.

You will find that the shell program is one of the most important programs installed on your Linux system. Even if you do use one of the graphical interfaces designed for the X Window System, you might still need to type commands at the shell prompt to start or stop a program. To give you a model for viewing the shell's position in the system and gaining an understanding of why it is so important, you can think of the Linux operating system as a stack:

- The kernel (the core of the operating system) is on the bottom of the stack, making use of the modules and kernel routines compiled in it to run the computer and manage the peripherals that you have attached.
- The shell program sits on top of the kernel: it accepts commands from the user, processes the ones it can, and interprets the rest to pass on to the kernel for execution.
- At the top of the stack is the applications layer. The shell manages the launching of applications in this layer and passes information between the applications and the kernel as necessary.

Figure 5.1 illustrates how this process operates. In step 1, the user types a command after the shell prompt and sends it to the shell. The shell first determines whether the command is one of its built-in commands or if it is an application program. If the command is an application program, it must be located in one of the directories listed in the shell's search path. If the command is found, the shell interprets the command (in step 2) and sends it to the kernel. The kernel then tells the shell (in step 3) to launch the application.
