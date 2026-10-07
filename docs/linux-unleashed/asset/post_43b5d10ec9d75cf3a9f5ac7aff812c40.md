
At the adduser prompt, enter the login name that you want to create. It is advisable to use all lowercase letters to avoid confusion. Do not exceed the eight-character limit at this point. (Although a mixed case login can be useful for confusing people trying to hack into your system, it causes problems when your system tries to talk to others over a network.)

For our sample user account in this chapter, let’s create the user **fido**. (After all, as the joke goes, “On the Internet, no one knows if you’re a dog!”) Of course, you can substitute your choice on the screen in place of fido (unless you really like our login name).

```
Enter login name for new account (^C to quit): **fido**
Editing information for new user [fido]
Full Name:
```

After entering the login name, a status message from the adduser utility usually appears, followed by a set of questions about the new user and the type of environment to present the account with when the user logs in. (The exact order of questions may be different, but usually most of the same information is requested.)

In the example previously shown, the adduser routine is waiting for the user’s real name. At this prompt, type the full name of the user. Uppercase, lowercase, mixed case, and spaces are fine. This information is not mandatory but is used by the system for some other tasks. Other users can also identify you with this name when you are on a network.

```
Full Name: **Fido Dog**
GID [100]:
```

The system is waiting for you to provide a GID or *Group Id*, which is discussed in more detail in Chapter 35, “Users and Logins.” The last part of the prompt, [100], means that it’s suggesting a GID of 100. This is the default choice and is good for most systems unless you are part of a larger network which has a naming policy in effect. For most users, the default is a great way to start and you can always change it later if you need to.

### Tip

In this adduser utility and many other Linux programs, default choices are presented in square brackets. Simply press the Enter key to accept the default, or type the new value if you don’t want to accept the default value.

Sometimes (as you will see later in the adduser utility) you are given two choices—usually y for yes and n for no—separated by a / or | character. The uppercase letter is the default choice which you can select by pressing Enter. The other choice must be typed explicitly. In the following examples, yes is always the default choice: [Y/n], [Y;n], [Yn].

After the Group ID has been given, the adduser program wants even more information:

```
GID [100]:
Checking for an available UID after 100
First unused uid is 101
UID [101]:
```

The adduser utility does not echo your Group ID choice to the screen if you simply press Enter. This can be a little disconcerting if you're not used to it, especially if you look back and try to figure out what you've done. If you don't see anything, the default value is used. Most Linux commands don't echo what you have done, so this is a good time to get used to it.

The adduser utility now asks for a User ID or UID. In this case, Linux suggests a default value of 101. Again, the default is fine in this case, so simply press Enter. You can pick any number that isn't already in use, but there's not much point in changing either the GID or UID unless you have specific organizational reasons to do so.

### NOTE

The User ID is used by Linux whenever it is referring to something you have done. The operating system is designed to use a number rather than the full login name because it takes up less room and is easier to manipulate. The User ID is important and each login on the system has its own unique number. By convention, UIDs of less than 100 (500 on some versions) are special system UIDs; root's UID is 0. Regular users get UIDs starting at 100 (or 500).

### NOTE

A few versions of Linux, such as Caldera's OpenLinux, don't bother asking you any questions at all when you use the adduser command. The adduser routine just finds the next GID and UID and assumes default values for all the rest of the information, too. While this is fast and easy, it does make configuring a login with nonstandard characteristics a bit more difficult.

The adduser utility then shows two more prompts asking for the user's home directory and the shell:

```
Home Directory [/home/fido]:
Shell [/bin/bash]:
```

Choose the default values for Home Directory and Shell. You'll see more about directories in Chapter 9, “File and Directory Permissions,” and look at different shells in Chapter 11, “bash,” Chapter 12, “pdksh,” and Chapter 13, “tcsh.” The default values are suitable for most user IDs.

As a last step, the adduser program asks for a password for the new user. At the prompt, enter a suitable password. If you press Enter without typing anything else, the password is set to the same string as the login or a null password, depending on the version of Linux. These two approaches are not recommended, however, because they are easy to guess. Even a simple password is better than none.

```
Password [fido]:

Information for new user [fido]:
Home directory: [/home/fido] Shell: [/bin/bash]
uid: [501] gid: [100]

Is this correct? [y/N]:
```

The adduser program now verifies that you are happy with all the information you have entered. If you are, type y for yes, and press Enter. The default value (shown by the capital letter) is N for no. If you choose the default, you are telling the script that the information displayed is not correct, and you have to start the whole process over again.

When you answer y to the question Is this correct?, the adduser program creates the new user's directory and adds the user information to the system configuration files. You may see the following information appear on the screen as the adduser utility does its work. When the utility has finished, you see the Linux shell prompt again:

```
Adding login [fido] and making directory [/home/fido]

Adding the files from the /etc/skel directory:
./.kermrc -> /home/fido/.kermrc
./.less -> /home/fido/.less
./.lessrc -> /home/fido/.lessrc
./.term -> /home/fido/.term
./.term/termrc -> /home/fido/.term/termrc
darkstar:~#
```

We will look at how to remove unwanted users from your /etc/passwd file in Chapter 35, “Users and Logins.”

## Logging Out

Now that you have created a new user, you can use it in the next couple of chapters to explore Linux. To finish with your session as root, log out of the system by typing logout:

```
darkstar:~# logout

Welcome to Linux 1.2.13
darkstar login:
```

You see the login prompt display again. At this point, you can log back in as root or as the new user you have just created.

Some systems allow you to log out with the Ctrl+D sequence. If the shell you are using supports Ctrl+D as a logout command, the login prompt reappears. Otherwise, you may see a message such as this:

```
Use "logout" to leave the shell.
```

If you have used other UNIX systems before, you may be used to using Ctrl+D to log out. The default shell used by Linux does not support Ctrl+D unless the key mappings are changed to allow it. Some versions of Linux also allow the logoff command to be used with most shells.

## Trying Out Your New Login

Now you can try out your new login. We can also look at some of the interesting features and capabilities of Linux.

At the login prompt, type the login name you have just created. If you were conscientious and assigned a nonzero-length password to your new login, enter the password when prompted.

You should now see the following (or something similar to it):

```
darkstar login: fido
Password: 
Last login: Sun Dec 11 19:14:22 on tty1
Linux 1.2.13 (POSIX).

Quiet! I hear a hacker....
darkstar:~$
```

The messages for the most part are the same as when you logged in as root. Some sys-tems don't show you anything except the shell prompt, but you can change that. Note that your prompt looks different from the root prompt or the pound sign. The $ prompt indicates that you are a regular user running under the bash shell (which was the default choice presented by the adduser program). Also, there is no You have mail message (because you have no mail).

![](img/e8e6b47ac20475e23d48b4c476f5d891_157_0.png)

To see an example of the difference between the root login and a regular user login, type **adduser** at the shell prompt and press **Enter**.

```
darkstar:~$ adduser
bash: adduser: command not found
```

The message you get looks somewhat cryptic. However, it has a typical Linux error mes-sage structure, so it's worth making a little effort now to understand it.

### Linux Error Messages

First of all, in the error message shown previously there's quite a bit of information. The program that is giving you the message is your shell, *bash*. It therefore announces itself with *bash*:, somewhat like the character in a play script. Next is the shell’s “mono-” “logo.” Being the “strong and silent” type of character, *bash*'s monologue is very terse and to the point. It declares the program that is causing problems (adduser) and the spe-cific problem with this program: the command (adduser) can't be found.

If the error message were expanded into real English, it would read something like this: “Hi, I'm *bash*. You know that adduser command you gave me? I looked everywhere for adduser but I couldn't find it, so I couldn't perform whatever actions adduser would have specified.” With time, you will get quite good at understanding Linux error mes-sage grammar.

### Search Paths

Why can root find adduser, but an ordinary user cannot? Linux has many directories, and each directory can hold many files (one of which can be the elusive adduser). In theory, Linux could go search through the entire file system until it found adduser. But if root accidentally mistyped adduser as asuser, Linux would have to rummage
