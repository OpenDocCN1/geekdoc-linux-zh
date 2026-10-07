# Chapter 1: SETTING UP 21

gram runs other programs (which describes almost all shell programs), your shell program needs to have its PATH set correctly so that the shell can find these other programs.

PATH is a list of directories, separated by colons (: ) that the shell will search for executable files, including the shell scripts that you will be learning to write in this book. If it's not already there, you will need to add ~/ bin to this list. (Remember, the tilde (~) is automatically taken by the shell to mean the pathname to your home directory.) If there was no PATH= command in your ~/.profile, you could accomplish this by adding the following line to that file:

```
PATH="~/bin:$PATH"
```

More concisely, you can combine this with the export command:

```
export PATH=$~/bin:$PATH
```

![](bbox=[0.068, 0.433, 0.115, 0.545])

The shell looks through the directories in your PATH in the left-to-right order that they appear in the variable's value string. The previous command tells the shell to prepend your bin directory to this list, means that if you put a program in ~/bin that has the same name as another command in the system, your program will run instead of the system's command. This is generally a good thing, but not always. Imagine if you unwittingly create a program with the same name as one of the ones that with the system, then tried to run someone's script that uses that program. If your bin directory was before the system's bin directory and PATH is exported, the script wouldn't work right. For this reason, many people append directories to the value established in /etc/profile, using a command in ~/.profile, like the:

```
export PATH=$~/bin
```

You might also consider adding dot (.) to your PATH. It represents the current working directory, no matter what cd command(s) you might have executed to change to other directories. That can be convenient when you are developing programs in a directory that you set up for development work, but it can expose you to certain security risks if you are running your system as the superuser.

![](bbox=[0.068, 0.923, 0.115, 0.933])