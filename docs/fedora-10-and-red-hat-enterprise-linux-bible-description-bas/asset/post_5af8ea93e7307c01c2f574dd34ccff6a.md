
# Part I: Getting Started in Fedora RHEL

- Metacharacters — These are characters that have special meaning to the shell. Metacharacters can be used to direct the output of a command to a file (>), pipe the output to another command (|), or run a command in the background (&), to name a few characters, which are discussed later in this chapter.

To save you time, there are shell features that you want to remember, recall previous commands, and edit commands. You can create aliases that allow you to type a short command to run a longer one. The shell stores previously entered commands in a history list, which you can display and show with you can recall commands. This is discussed in the remainder of this section.

Unless you specifically change another shell, the bash shell is the one you use with Fedora or RHEL. The bash shell contains most of the powerful features available in other shells. Although the description in this chapter steps through many shell features, you can learn more about the bash shell by typing `man bash`. For other ways to learn about the shell, refer to the sidebar "Getting Help with Using the Shell."

## Locating commands

If you know the directory that contains the command you want to run, one way to run it is to type the full path to that command. For example, you run the `date` command from the `/bin` directory by typing:

```
$ /bin/date
```

Of course, this can be inconvenient, especially if the command resides in a directory with a long name. The better way is to have commands stored in well-known directories, and add those directories to your shell's PATH environment variable. The path consists of a list of directories that are checked sequentially for the command you enter. To see your current path, type the following:

```bash
$ echo PATH
/usr/kerberos/bin:/usr/local/bin:/usr/bin:/usr/sbin:/sbin:/usr/local/bin:/home/chris/bin
```

The results show the default path for a regular Linux user. Directories in the path list are separated by colons. Most commands that use Linux are stored in the `/bin,/usr/local/bin` directories. The last directory shown is the bin directory in the user's home directory (In Fedora and RHEL systems, the `/usr/kerberos/bin` directory precedes others so that if you are not running authentication with Kerberos, the Kerberos versions of many network clients are used instead of the regular Linux versions.)

> TIP: If you want to add your commands or shell scripts, place them in the bin directory in your home directory (such as /home/chris/bin for the user named chris). This directory is automatically added to your path (although you type mkdir $HOME/bin to create it). As long as you add the command to your bin with execute permission (described in the "Understanding file permissions" section), you can immediately begin using the command by simply typing the command name at your shell prompt. There are always security concerns when adding new commands. This is in why your local bin directory appears after the system bin directories in your PATH. Be careful when adding commands and read the section on "Understanding file permissions" carefully.

## Getting Help with Using the Shell

When you start using the shell, it can be intimidating. All you see is a prompt. How do you know which commands are available, which options use, or how to use more advanced features? Fortunately, lots of help is available. Here are some places you can look to supplement what you learn in this chapter:

- Check the PATH — Type echo PATH. You see a list of the directories containing commands immediately accessible to you. Listing the contents of these directories (with the ls command) displays most standard Linux commands.
- Use the help — Some commands are built into the shell, so they do not appear in a directory. The help command lists those commands and shows options available with each of them.(Type help | less to page through the list.) For help with a particular built-in command, type help command, replacing command with the name that interests you. The help command works with the shell only.
- Use --help — Many commands include a --help option that you can use to get information about how the command is used. For example, type date --help | less. The output shows not only options, but also format you can use with the date command.
- Use the man — To learn more about a particular command, type man command.(Replace command with the command you want). The command name is short for manual. A description of the command and its options appears on the screen.
- Use the info — Command descriptions that aren't available on man pages are often avail for the info facility. Type info command to see a text-based interface for stepping through information on the command.

Also note administrative commands are in your path. These directories include /sbin and /usr/sbin.

## Part I: Getting Started in Fedora and RHEL

The path directory order is important. Directories are checked from left to right. So, in example, if there is a command foo located in both the /bin and /usr/bin directories, the one in /bin is executed. To have the other foo command run, you type either the full path to command or change your PATH variable. (Changing the PATH and adding directories to it is described later in this chapter).

Not all the commands that you run are located in directories in your PATH. Some commands are built into the shell. Other commands can be overwritten by aliases that define any commands and options that you want to run. There are also ways of defining a function that consists of a series of commands. Here is the order in which the shell checks for the commands you use:

1. Aliases — Names set by the alias command that represents a particular command and a set of options. (Type alias to see what aliases are. Often, aliases allow you to define a short name for a long, complicated command. Some users use aliases to map a command name from another operating system to the similar utility in Linux.
2. Reserved word — Words that are reserved by the shell for special use. Many of these are words that you would use in programming-type functions, such as do, while,
3. Function — A set of commands that are executed within the current shell.
4. Built-in command — A command that is built into the shell.
5. File system command — This is a command that is stored in and executed from the computer's file system. These are the commands that are indicated by the value of the PATH variable.

To find out where a particular command is taken from, you can use the type command. (If you are using a shell other than bash, use the which command instead.) For example, if to find out where the bash shell is located, type the following:

```bash
$ type bash
bash /bin/bash
```

Try these few words with the type command to see other locations: which, case, and return.

> TIP: When you run a command and receive an error message that the command was not found or permission was denied. In the first case, check that you spelled the command correctly. In the second case, the command may be in the PATH, but not executable. Adding execute permissions to a command is described later in this chapter.

# Chapter 4: Using Linux Commands

## Rerunning commands

It's annoying, after typing a long or complex command, to learn you mistyped something. Fortunately, some features let you recall and edit command lines. The shell history is a list of the commands you have entered. Using the history command, you can view your previous commands. Then, using various shell features, you can recall individual lines and change them. The rest of this section describes how to edit commands, how to complete parts of lines, and how to work with the history.

## Command-line editing

If you type something wrong on a command line, the bash shell ensures that you don't have to delete the entire line and start over. Likewise, you can recall a previous command line and change it.

By default, the bash shell uses command-line editing that is based on emacs. So, if you are familiar with emacs, you probably know most of the keystrokes described here.

> TIP: If you prefer the vi command for editing command lines, you can easily make that happen. set -o vi to the .bashrc file in your home directory. The next time you open a shell, you can use vi commands (as described in the tutorial later in this chapter) to edit your lines.

To do editing, you can use a combination of control keys, meta keys, and arrow keys. For example, Ctrl-f means to hold the Control key and Alt+f means to hold the Alt key and f. (Instead of the Alt key, your keyboard may use a meta key or the Esc key instead. On a Windows keyboard, you can sometimes use the Windows key.)

To try a bit of command-line editing, typing the following command:

```bash
$ /usr/bin | sort -f | less
```

This list counts the contents of the /usr/bin directory, sorts the contents in alphabetical order (regardless of upper- and lowercase), and pipes the output to less. Now, suppose you want to change /usr/bin to /bin. You can use the following steps to change the command from the shell:

- Press Ctrl+a. This moves the cursor to the beginning of the command line.
- Press Ctrl+f or the right arrow (→) key. Repeat this command a few times to position the cursor under the first slash (/).
- Press Ctrl+d. Type this command four times to delete /usr.
- Press Enter. This executes the command line.
