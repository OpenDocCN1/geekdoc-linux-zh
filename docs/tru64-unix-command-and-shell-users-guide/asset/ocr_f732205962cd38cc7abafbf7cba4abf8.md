# Example 1-1: Typical Login Screen (cont.)

2 The date and time of your last login.

Note this information whenever you log in, and tell your system administrator if you have not logged in at the time specified. A wrong date and time might indicate that someone has been breaking into your system.

3 Messages from the administrator

Your system administrator may set messages that each user receives each time a login is accomplished. These messages may describe planned system updates, operational schedules, or other information of general interest. These messages are called the message of the day and are stored in the file /etc/motd. You may redisplay these messages at any time by displaying this file.

4 Whether you have mail messages waiting to be read.

Briefly, mail is a program that lets you send and receive electronic mail. The system displays the message You have mail when there are mail messages for you that are waiting to be read. If you have no mail messages, this line does not appear.

# 1.2 Logging Out

When you are ready to end your work session, log out of the system. Logging out leaves the operating system running for other users and also ensures that no one else can use your work environment.

To log out, perform the following steps:

+   1. Make sure that the shell prompt is displayed.
+   2. Press Ctrl/D. If Ctrl/D does not work, enter the exit command.

The system displays the login prompt or login screen. On some systems, a message may also be displayed.

At this point, you or another user may log in.

# 1.3 Using Commands

Operating system commands are programs that perform tasks on the operating system. The operating system has a large set of commands that are described in the remaining chapters of this book and in the related reference pages.

Entering a command is an interactive process. When you enter a command, the shell interprets that command, and then gives an appropriate response — that is, the system either runs the program or displays an error message.

A shell reads every command you enter and directs the operating system to do what is requested. Therefore, the shell is a command interpreter.