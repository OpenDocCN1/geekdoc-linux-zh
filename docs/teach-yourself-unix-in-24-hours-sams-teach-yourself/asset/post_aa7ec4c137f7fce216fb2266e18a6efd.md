
arguments Not any type of domestic dispute, arguments are the set of options and filenames specified to UNIX commands. When you use a command such as vi test.c, all other than the command name itself (vi) are arguments, or parameters to the program.

i-list See i-node.

i-node The UNIX file system is like a huge notebook of sheets of information. Each file is like an index tab, indicating where the file starts in the notebook and how many sheets are used. The tabs are called i-nodes, and the list of tabs (the index to the notebook) is the i-list.

command Each program in UNIX is also known as a command: the two words are interchangeable.

man page Each UNIX command comes with some basic online documentation that describes its function. This online documentation for command is called a man page. Usually, the man pages list the command-line flags and some error conditions.

multitasking A multitasking computer is one that actually run more than one program, or task, at a time. By contrast, personal computers lock you into a single program that you must exit before you launch another.

multiuser Computers intended to have more than a single person working on them simultaneously are designed to support multiple users, hence the term multiuser. By contrast, personal computers are almost always single-user because someone else can't be running a program or editing a file while you are using the computer for your own work.

pathname UNIX is split into a wide variety of different directories and subdirectories, often across multiple hard disks and even multiple computers. The system doesn't search laboriously through the entire mesh you request a program, the set of directories you reference is stored as your search path, and the location of any specific command is known as its pathname.

shell To interact with UNIX, you type in commands to the command-line interpreter, which is known in UNIX as the shell, or command shell. It's the underlying environment in which you work with the UNIX system.

# Questions

Each hour concludes with a set of questions for you to contemplate. Here's a warning front: Not all of the questions have a definitive answer. After all, you are learning about a multichoice operating system!

- 1. Name the three multi concepts that are at the heart of UNIX's power.

- 2. UNIX is more like a grid of streets, picking you from point A to point B, or a directed highway with only one option? How does this compare with other systems you've used?

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_32_0.png)

- 3. Systems that support multiple users always ask you to say who you are when you begin using the system. What's the most important thing to remember when you're done using the system?

- 4. If you're used to graphical interfaces, try to think of a few tasks that you feel are more easily accomplished by moving icons than by typing commands. Write those tasks on a separate paper, and in a few days, pull that paper out and see if you still feel that way.

- 5. Think of a few instances in which you needed to give a person written instructions. Was that easier than giving spoken instructions or drawing a picture? Was it harder?

# Preview of the Next Hour

In the next hour, you learn how to log in to the system at the login prompt (login:), how to log out of the system, how to use the password command to change your password, how to use the id command to find out who the computer thinks you are, and lots more!

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_33_0.png)

# Hour 2

# Getting onto the System and Using the Command Line

This is the second hour of UNIX lessons, so it's time you logged in to the system and tried some commands. This hour focuses on teaching you the basics of interacting with your UNIX machine.

# Goals for This Hour

In this hour, you learn how to

- Log in and log out of the system
- Change passwords with passwd
- Choose a memorable and secure password
- Find out who the computer thinks you are
- Find out who else is on the system

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_34_0.png)

# Task 2.1: Logging In and Out of the System

- Find out what everyone is doing on the system
- Check the current date and time
- Look at a month and year calendar
- Perform some simple commands with UNIX

This had introduces a lot of commands, so it's very important that you have a similar approach, or you which you can work through all examples. Most examples have been taken from a Sun workstation Solaris, a variant of UNIX V Release 4, and have been double-checked on a BSD-based system. Any variance between the two is noted, and if you have a UNIX system available, odds are that it's based on either AT&T System V or Berkeley UNIX.

DESCRIPTION Because UNIX is a multiuser, you need to start by finding a terminal, computer, or other way to access the system. I use a Macintosh and a model to dial up various systems by telephone. You might have a terminal directly connected to the UNIX computer on your desk or in your office, or you might have the UNIX system itself on your desk. Regardless of how you connect to the UNIX system, the first thing you'll see on the screen is:

4.3BSD DYNIX (mentor.utech.edu) 5:38pm on Fri, 7 Feb 1997

login:
The first line indicates what UNIX of the system is running (DYNIX is UNIX on Sequel commands), the actual name of the computer system, and the current date and time.
The second line is asking for your login, your account name.

- 1. Connect your terminal or PC to the UNIX system until the point where you see a login prompt (login:) on your screen similar to that in the preceding example. Use the phone and modem to dial up the computer if you need to.
It would be nice if computers could keep track of users by simply using for names that if I could enter Taylor at the login prompt. Also, like the Internal Revenue Service, Department of Motor Vehicles, and many other agencies, UNIX—rather than using names—assign each user a unique identifier. This identifier is called an account name, has eight characters or fewer, and is usually based on the first or last name, although it can be any combination of letters and numbers. I have two account names, or logins, on the systems I use: taylor and, on another machine where someone already had that account name, taylor.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_35_0.png)

# Getting onto the System and Using the Command Line

- 2. You should know your account name on the system. Perhaps your account name is on a paper with your initial password, both assigned by the UNIX system. If you do not have this information, you need to track it down before you go further. Some accounts might not have an initial password; that means you won't have to enter it the first time you go into the system. In a few minutes, you will learn how you can give yourself the password of your choice by using a UNIX command passwd`.

- 3. At the login prompt, enter your account name. Be particularly careful to use lowercase letters unless specified otherwise by your administrator.

```
login: taylor
Password: own```

Once you've entered your account name, the system moves the cursor to the next line and prompts for your password. When you enter your password, the system won't echo it (that is, it won't display it) on the screen. That's okay. Lack of an echo doesn't mean anything is broken; instead, it is a security measure to ensure that if people are looking over your shoulder, they can't learn your secret password by watching your screen.

- 4. If you enter your login or your password incorrectly, the system complains with an error message:

```
login: taylor
Password:
Login incorrect
Login:
```

| Most systems give you three or four attempts to get both your login and password correct, try again. Don't forget to enter your account name at the login prompt each time. |

- 5. Once you've successfully entered your account name and password, you are shown some information about the system, some news for users, and an indication of whether you have electronic mail. This will vary; the specifics here's an example of what I see when I log in to my account:

```
login: taylor
Password:
Last login: Fri Feb 7 17:00:23 on ttyAe
You have mail.
%
```
