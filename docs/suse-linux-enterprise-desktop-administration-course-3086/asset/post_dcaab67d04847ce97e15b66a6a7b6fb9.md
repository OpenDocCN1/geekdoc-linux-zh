
## Locating Files

- Log in to tty1 as the root user.

- Use the which command to locate the who, grep, and cp executable files. What directories are each file in? Type `echo $PATH` and press Enter to view the PATH variable. Are these directories listed? Use the which command to find the file called `file1` in your home directory. Why were you not successful?

- Use the appropriate find command to perform the following actions. For each action, write down the command that you used.
  1. Find all files on the system called “hosts”.
  2. Find all files under the /etc directory and subdirectories that are larger than 100K in size.
  3. Find all files in the /etc directory and subdirectories that are less than 2K in size.
  4. Find all symbolic links underneath the /usr directory.
  5. Find all files in the /usr directory and subdirectories that were modified less than 1 day ago.
  6. Find all files in the /tmp directory and subdirectories that are owned by the root user.

## File Linking

- Log in to tty1 as the gecko user and copy the file `/etc/issue` to your current directory. Next, perform a long listing of the issue file in your current directory. Is it hard linked? Is it soft linked? How can you tell?

- Create a hard link to issue called `hardissue`. Next, do a long listing of both files. What are their sizes? What are their modification dates? What are their link counters? Why? Next, use the `ls --li` command to view their inodes. Are they the same? Remove the file `hardissue`. Was issue removed as well? What is the link count of issue now? Explain.

- Create a soft link to issue called `softissue`. Next, do a long listing of both files. What are their sizes? What are their modification dates? What are their link counts? What is the file type of `softissue`? What does the filename of softissue indicate? Next, use the `ls --li` command to view their inodes. Are they the same? Explain.

![](img/9129877170834ca9d5fdac5319bf5f12_256_0.png)

## Work with the Linux Shell and Command Line

In this section, you learn about the basic features of the bash shell. In addition, you are introduced to some important administration commands.

### Objectives

- Objective 1—Get to Know the bash Shell
- Objective 2—Get to Know Common Command-Line Tasks
- Objective 3—Understand Command Syntax and Special Characters
- Objective 4—Get to Know Linux Text Editors

## Objective 1—Get to Know the bash Shell

You cannot communicate directly with the operating system kernel. You need to use a program that serves as an interface between the user and operating system.

In the operating systems of the UNIX family, this program is called the shell.

The shell accepts a user’s entries, interprets them, converts them to system calls, and delivers system messages back to the user, making it a command interpreter.

To understand the bash shell, you need to know the following:

- Types of Shells
- bash Configuration Files
- Completion of Commands and Filenames
- History Function

### Types of Shells

UNIX has a whole series of shells, most of which are provided by Linux in freely usable versions. The following are examples of some popular shells:

- The Bourne shell (/bin/sh; symbolic link to /bin/bash)
- The Bourne Again shell (/bin/bash)
- The Korn shell (/bin/ksh)
- The C shell (/bin/csh; symbolic link to /bin/tcsh)
- The TC shell (/bin/tcsh)

These shells differ in the functionality they provide.

Every shell can be started like a program and you can switch at any time to a different shell. For example, you can switch to the C shell by entering tcsh; you can switch to the Korn shell by entering ksh.

Unlike most other programs, the shell does not terminate on its own. You need to enter the exit command to return to the previous shell.

A shell is started at a text console right after a user logs in. This is called the login shell. Which shell is started for which user is defined in the user database.

The standard Linux shell is bash, so we only cover the bash shell in this objective.

### bash Configuration Files

To customize bash for an interactive session, you need to be familiar with the configuration files and the order in which they are processed.

To understand how shells work, you need to know the difference between the following:

- Login Shells
- Nonlogin Shells

**Login Shells** A login shell is started whenever a user logs in to the system. By contrast, any shell started from within a running shell is a nonlogin shell. The only differences between these two are the configuration files read when starting the shell.

A login shell is also started whenever a user logs in through an X display manager. Therefore, all subsequent terminal emulation programs run nonlogin shells.

The following files are read when starting a login shell:

1. `/etc/profile`—A systemwide configuration file read by all shells. It sets global configuration options. This configuration file will be read not only by the bash, but also by other shells.
   `~/.profile`—A file created for each new user by default on the SUSE Linux Enterprise Desktop. Any user-specific customizations can be stored in it.
2. `/etc/bash.bashrc`—Some useful configurations for the bash shell are made. For example:
   - Appearance of the prompt
   - Colors for the `ls` command
   - Aliases

For your own systemwide bash configurations, use the file `/etc/bash.bashrc.local`, which is imported from `/etc/bash.bashrc`.

`~/.bashrc`—A configuration file in which users store their customizations.

### Nonlogin Shells

Only the files `/etc/bash.bashrc`, `/etc/bash.bashrc.local`, and `~/.bashrc` are read when a nonlogin shell is started.

Like most other Linux distributions, SUSE Linux Enterprise Desktop has a default setup that ensures users do not see any difference between a login shell and a nonlogin shell. In most cases, this is achieved by also reading the `~/.bashrc` file when a login shell is started.

If you change any settings and want them to be applied during the same shell session, the changed configuration file needs to be read in again.

The proper way to read in a changed configuration file and to apply the changes to the current session is by using the internal shell `source` command, as in the following example:

```bash
source ~/.bashrc
```

You can also use the “short form” of this command, which is included in many configuration files. It is used to read in other configuration files, as in the following (with a space between the period and the tilde):

- `. ~/.bashrc`

### Completion of Commands and Filenames

The bash shell supports a function of completing commands and filenames. Just enter the first characters of a command (or a filename) and press Tab. The bash shell completes the name of the command.

If more than one possibility exists, the bash shell shows all possibilities when you press Tab a second time. This feature makes entering long filenames very easy.

### History Function

bash stores the commands you enter so you have easy access to them again when needed later. By default, the commands are written in the `.bash_history` file in the user’s home directory. In SUSE Linux Enterprise Desktop, the size of this file is set to a maximum of 1,000 entries.

You can display the content of the file by using the history command.

You can display the commands stored in the history cache (one at a time) by using the arrow keys. **Up-arrow** shows the previous command; **Down-arrow** shows the next command. After finding the desired command, edit it as needed; then execute it by pressing Enter.

When browsing the entries of the history, you can also select specific commands. Typing one or several letters and pressing Page Up or Page Down displays the preceding or next command in the history cache beginning with this letter.

Enter part of the command (not necessarily the beginning of the command) and press Ctrl+r to search the history list for matching commands and display them. Searching starts with the last command executed.

## Objective 2—Get to Know Common Command-Line Tasks

Two features make working with the bash shell more powerful:

- Variables
- Aliases

## Variables

With shell and environment variables, you are able to configure the behavior of the shell and to adjust its environment to your own requirements.

The convention is to write variables such as PATH in uppercase letters. If you set your own variables, they should also be written in capitals for the sake of clarity.

Environment variables are used to control the behavior of a program that is started from a shell. Shell variables, on the other hand, are used to control the behavior of the shell itself.

Some important environment variables include the following:

- *PATH*—When a program is called up, the program is searched for in the directories specified here (each directory is separated by a “:” ). The order in which directories are listed is important because they are searched in turn.
- *HOME*—The user’s home directory.
- *USER*—The login name of the actual user.

To display the value of a shell or environment variable, enter `echo $variable`, as in the following:

```shell
gecko@da10:~ > echo $HOME
/home/gecko
```

To set the value of a variable or to create a new variable, use the syntax *variable=value*, as in the following:

```shell
da10:~ # MYVAR=myvalue
da10:~ # echo $MYVAR
myvalue
da10:~ #
```
