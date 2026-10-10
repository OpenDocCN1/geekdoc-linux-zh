
## Introduction to Linux

  typing and memorizing locations of commands. So the path naturally contains a lot of directories containing bin somewhere in their names, as the user below demonstrates. The echo command is used to display the content ("$") of the variable PATH:

```
roger:-> echo $PATH
/opt/local/bin:/usr/X11R6/bin:/usr/bin:/usr/sbin:/bin
```

  In this example, the directories /opt/local/bin, /usr/X11R6/bin, /usr/bin, /usr/sbin and /bin are subsequently searched for the required program. As soon as a match is found, the search is stopped, even if not every directory in the path has been searched. This can lead to strange situations. In the first example below, the user knows there is a program called sendsms to send an SMS message, and another user on the same system can use it, but she can't. The difference is in the configuration of the PATH variable:

```
[jenny@blob jenny]$ sendsms
bash: sendsms: command not found
[jenny@blob jenny]$ echo $PATH
/bin:/usr/bin:/usr/bin/X11:/usr/X11R6/bin:/home/jenny/bin
[jenny@blob jenny]$ su - tony
Password:
tony:~$ which sendsms
sendsms is /usr/local/bin/sendsms

tony:~$ echo $PATH
/home/tony/bin:/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/usr/bin/X11:/usr/sbin:/bin
```

  Note the use of the su (switch user) facility, which allows you to run a shell in the environment of another user, on the condition that you know the user's password.

  A backslash indicates the continuation of a line on the next, without an Enter separating one line from the other.

  In the next example, a user wants to call on the wc (word count) command to check the number of lines in a file, but nothing happens and he has to break off his action using the Ctrl+C combination:

```
jumper:-> wc -l test

(Ctrl-C)
jumper:-> which wc
wc is /home/jumper/bin/wc

jumper:-> echo $PATH
/home/jumper/bin:/usr/local/bin:/usr/local/sbin:/usr/X11R6/bin:/usr/bin:/usr/sbin:/bin:/sbin
```

  The use of the **which** command shows us that this user has a *bin*-directory in his home directory, containing a program that is also called *wc*. Since the program in his home directory is found first when searching the paths upon a call for *wc*, this “home-made” program is executed, with input it probably doesn’t understand, so we have to stop it. To resolve this problem there are several ways (there are always several ways to solve a problem in UNIX/Linux): one answer could be to rename the user’s *wc* program, or the user can give the full path to the exact command he wants, which can be found by using the *-a* option to the **which** command.

  If the user uses programs in the other directories more frequently, he can change his path to look in his own directories last:

```
jumper:~$ export PATH=/usr/local/bin:/usr/local/sbin:/usr/X11R6/bin:/usr/bin:/usr/sbin:/bin:/sbin:/home/jumper/bin
```

### Changes are not permanent

  Note that when using the *export* command in a shell, the changes are temporary and only valid for this session (until you log out). Opening new sessions, even while the current one is still running, will not result in a new path in the new session. We will see in Section 7.2 how we can make these kinds of changes to the environment permanent, adding these lines to the shell configuration files.

### 3.2.2 Absolute and relative paths

  A path, which is the way you need to follow in the tree structure to reach a given file, can be described as *starting from* the trunk of the tree (the */* or root directory). In that case, the path starts with a slash and is called an absolute path, since there can be no mistake: only one file on the system can comply.

  In the other case, the path doesn’t start with a slash and confusion is possible between *~/bin/wc* (in the user’s home directory) and *bin/wc* in */usr*, from the previous example. Paths that don’t start with a slash are always relative.

  In relative paths we also use the *.* and *..* indications for the current and the parent directory. A couple of practical examples:

- When you want to compile source code, the installation documentation often instructs you to run the command **./configure**, which runs the *configure* program located in the current directory (that came with the new code), as opposed to running another *configure* program elsewhere on the system.
- In HTML files, relative paths are often used to make a set of pages easily movable to another place:
  
  `<img alt="Garden with trees" src="../images/garden.jpg">`
  
  Notice the difference one more time:

```
theo:--> ls /mp3
ls: /mp3: No such file or directory
theo:-->ls mp3/
oriental/  pop/  sixties/
```

### 3.2.3 The most important files and directories

#### 3.2.3.1 The kernel

  The kernel is the heart of the system. It manages the communication between the underlying hardware and the peripherals. The kernel also makes sure that processes and daemons (server processes) are started and stopped at the exact right times. The kernel has a lot of other important tasks, so many that there is a special kernel-development mailing list on this subject only, where huge amounts of information are shared. It would lead us too far to discuss the kernel in detail. For now it suffices to know that the kernel is the most important file on the system.

#### 3.2.3.2 The shell

##### 3.2.3.2.1 What is a shell?

  When I was looking for an appropriate explanation on the concept of a *shell*, it gave me more trouble than I expected. All kinds of definitions are available, ranging from the simple comparison that "the shell is the steering wheel of the car", to the vague definition in the Bash manual which says that "bash is an sh-compatible command language interpreter," or an even more obscure expression, "a shell manages the interaction between the system and its users". A shell is much more than that.

  A shell can best be compared with a way of talking to the computer, a language. Most users do know that other language, the point-and-click language of the desktop. But in that language the computer is leading the conversation, while the user has the passive role of picking tasks from the ones presented. It is very difficult for a programmer to include all options and possible uses of a command in the GUI-format. Thus, GUIs are almost always less capable than the command or commands that form the backend.

  The shell, on the other hand, is an advanced way of communicating with the system, because it allows for two-way conversation and taking initiative. Both partners in the communication are equal, so new ideas can be tested. The shell allows the user to handle a system in a very flexible way. An additional asset is that the shell allows for task automation.

##### 3.2.3.2.2 Shell types

  Just like people know different languages and dialects, the computer knows different shell types:

- **sh** or Bourne Shell: the original shell still used on UNIX systems and in UNIX related environments. This is the basic shell, a small program with few features. When in POSIX-compatible mode, **bash** will emulate this shell.
- **bash** or Bourne Again Shell: the standard GNU shell, intuitive and flexible. Probably most advisable for beginning users while being at the same time a powerful tool for the advanced and professional user. On Linux, **bash** is the standard shell for common users. This shell is a so-called *superset* of the Bourne shell, a set of add-ons and plug-ins. This means that the Bourne Again Shell is compatible with the Bourne shell: commands that work in sh, also work in bash. However, the reverse is not always the case. All examples and exercises in this book use bash.
- **csh** or C Shell: the syntax of this shell resembles that of the C programming language. Sometimes asked for by programmers.
- **tcsh** or Turbo C Shell: a superset of the common C Shell, enhancing user-friendliness and speed.
- **ksh** or the Korn shell: sometimes appreciated by people with a UNIX background. A superset of the Bourne shell; with standard configuration a nightmare for beginning users.

  The file `/etc/shells` gives an overview of known shells on a Linux system:

```
mia:~$ cat /etc/shells
/bin/bash
/bin/sh
/bin/tcsh
/bin/csh
```

  **Fake Bourne shell**

  Note that /bin/sh is usually a link to Bash, which will execute in Bourne shell compatible mode when called on this way.

  Your default shell is set in the `/etc/passwd` file, like this line for user *mia*:

```
mia:L2N0qdlPrHwE:504:504:Mia Maya:/home/mia:/bin/bash
```

  To switch from one shell to another, just set under the name of the new shell in the active terminal. The system finds the directory where the name occurs using the PATH settings, and since a shell is an executable file (program), the current shell activates it.
