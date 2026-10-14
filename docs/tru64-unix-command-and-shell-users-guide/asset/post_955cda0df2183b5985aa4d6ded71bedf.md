
### Example 1-1: Typical Login Screen (cont.)

- 2. The date and time of your last login.

  Note this information whenever you log in, and tell your system administrator if you have not logged in at the time specified. A wrong date and time might indicate that someone has been breaking into your system.

- 3. Messages from the administrator

  Your system administrator may set messages that each user receives each time a login is accomplished. These messages may describe planned system updates, operational schedules, or other information of general interest. These messages are called the message of the day and are stored in the file /etc/motd. You may redisplay these messages at any time by displaying this file.

- 4. Whether you have mail messages waiting to be read.

  Briefly, mail is a program that lets you send and receive electronic mail. The system displays the message You have mail when there are mail messages for you that are waiting to be read. If you have no mail messages, this line does not appear.

## 1.2 Logging Out

When you are ready to end your work session, log out of the system. Logging out leaves the operating system running for other users and also ensures that no one else can use your work environment.

To log out, perform the following steps:

- 1. Make sure that the shell prompt is displayed.
- 2. Press Ctrl/D. If Ctrl/D does not work, enter the exit command.

The system displays the login prompt or login screen. On some systems, a message may also be displayed.

At this point, you or another user may log in.

## 1.3 Using Commands

Operating system commands are programs that perform tasks on the operating system. The operating system has a large set of commands that are described in the remaining chapters of this book and in the related reference pages.

Entering a command is an interactive process. When you enter a command, the shell interprets that command, and then gives an appropriate response — that is, the system either runs the program or displays an error message.

A shell reads every command you enter and directs the operating system to do what is requested. Therefore, the shell is a command interpreter.

```
$ man date
```

Commands can have options that modify the way a command works. These options are called flags and immediately follow the command name. Most commands have several flags. If you use flags with a command, arguments follow the flags on the command line.

For example, suppose that you use the -f flag with the man command. This flag displays a one-line description of a specified command. To display a one-line description of the date command, you would enter:

```
$ man -f date
```

While a command is running, the system does not display the shell prompt because the control passes to the program you are running. When the command completes its action, the system displays the shell prompt again, indicating that you can enter another command.

In addition to using the commands provided with the system, you can also create your own personalized commands. Refer to Section 7.10.1 for information about creating these special commands.

## 1.4 Stopping Command Execution

If you enter a command and then decide that you do not want it to complete executing, enter Ctrl/C. The command stops executing, and the system displays the shell prompt. You can now enter another command.

Depending upon the command, partial completion of the command may have varied results (referred to as an unknown state). To see the result of stopping a command during execution, enter Ctrl/C after executing commands such as ls -l to list files in a directory or cat filename to view a file on the screen.

## 1.5 Setting Your Password

Your user name is public information and generally does not change. Your password, on the other hand, is private.

In most instances, when your system account is established, the system administrator assigns a password that is common to new users. On some systems, this new user password is valid for only one login to allow you access to the system to establish your own password. After getting familiar with the system, select your own password to protect your account from unauthorized access. In addition, change your password periodically to protect your data from unauthorized access.

To set your password, use the passwd command. If your account does not have a password, use the passwd command to set one. For information on passwd procedures, see Section 1.5.2. If your system is part of a networked
