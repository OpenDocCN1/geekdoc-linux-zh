
A password prompt appears if you are logged in as a regular user.
If you are logged in as the root user, then no password prompt displays.

3. If necessary, enter the password for the account that you are logging into.

### Note

You have changed accounts only for the command line you are using. If you are running a desktop, then you are still logged in with your original account in other windows.

4. If you changed accounts without running a command, repeat this process to return to your original account.

If you run a command, you return to your original account as soon as the command is carried out.

## 5 Getting to Know the Command Line

A command line is a text-based interface for interacting with your computer. You type a command, then press the Enter key to run it. If you have used DOS, then you have used a command line.

The command line is also known as the terminal, xterm, console, command shell, or shell. Some of these terms make technical distinctions, but, for most purposes, you can consider them identical.

This chapter explains the basics of using the Linux command line. It covers:

- Why Use the Command Line: An explanation of why you should learn to use the command line.
- Starting the Command Line: The different ways that you can open a command line.
- Navigating the Command Line: How you can move through directories and list files from the command line.
- Entering a Command: How a command is structured and how you run one.
- Using Command Line Shortcuts: Features of the Linux command line that save you time, effort, and typing.
- Finding Help for Commands: The on-line help systems for commands.

The rest of the manual also contains command line solutions to different computing tasks.

### Why Use the Command Line?

Most Windows and MacOS users work with a graphical desktop and ignore the command line. Increasingly, many Linux users are doing the same. However, you should learn how to use the command line for several reasons:

- Many useful tools can only be used from the command line.
- The command line gives you more flexibility and power, especially when you are working with multiple files.
- If you ever need to recover, you will do so from the command line. Maintenance work in single-user mode also requires familiarity with a command line.

These reasons are important enough that many Linux users work from the command line instead of the desktop.

If you have used DOS, you will find the Linux command line much easier and much more powerful. Not only does it have many shortcuts to save you time, but you can even choose the command line interface - the shell - that best suits your needs. This manual assumes that you are using BASH (Bourne Again Shell), the default for Progeny Debian and most other Linux distributions.

### Starting a Command Line

If your computer is not set-up to use a graphical desktop, it starts with the command line already running.

To start a command line while running a graphical desktop, do one of the following:

- Select the command line from the panel.

![](img/e36b94f8548b09d00212238f073b11d9_114_0.png)

- From the menu, select Programs > System > Eterm, GNOME Terminal or Regular xterm. A command line window opens.

![](img/e36b94f8548b09d00212238f073b11d9_114_1.png)

- Press Alt-F2 or select Run from the menu. A single line command window opens.

![](img/e36b94f8548b09d00212238f073b11d9_114_2.png)

- Right-click on the work space. Then select New > Terminal from the pop-up menu.

- Press Ctrl-Alt-F1 using the left-hand keys. A full screen command line opens.

To return to the desktop, press Alt-F7.

### Entering Commands

To new users, a command can look overwhelming. However, once you realize that all commands follow the same basic structure, you can start using them efficiently.

This section covers:

- Understanding the parts of a command.
- Understanding command structures.
- Entering multiple file names.
- Entering wild cards.
- Entering multiple commands.
- Combining commands.
- Running commands in the background.

#### Understanding the Parts of a Command

A command is sometimes a single word. However, a command may include:

- Options: variations on how the command is carried out. Options begin with one hyphen (-) if they were developed for UNIX or by unaffiliated programmers, or by two hyphens (--) if they were developed by the GNU Foundation. Because GNU commands are often complete words, they are often more user-friendly.
- Arguments: Fixed values that affect exactly what the command does, or how it does it.
- Directories or files: What the command affects. Some commands, such as cp (copy) need a source file (the file being worked with) and a target file (the one affected).
- Strings: A set of characters enclosed by double or single quotation marks. Often, a string contains a regular expression or wild card.

What a command does can vary greatly, depending on what options, arguments, and files are used. For example, if you simply type `date`, then the current date and time display. However, if you type `date 0707132101`, then your computer’s date is changed to 1:21 PM on July 7, 2001.

### Note

Commands, options, and arguments are often abbreviated descriptions of what they do. For example, `cp` copies a file, while `su` switches the user account you are using. Similarly, in some commands, the `-v` option is short for version, and lists the version number of the command. Knowing the full description is a useful way to memorize commands.

#### Understanding Command Structures

The parts of a command are always entered in the same order:

`COMMAND OPTIONS ARGUMENT FILES`

A typical command is `chgrp -Rv root /home/itang/ToDo`.

In this example:

- `chgrp` is the basic command. It is short for “change group.” It transfers the ownership of the file at the end of the command from one group of users to another.
- `-Rv` are two options:
    - `-R` (recursive) makes the command affect all files and sub-folders below the directory at the end of the command.
    - `-v` (verbose) makes the command list the files and folders as it changes them.

### Note

You only need one hyphen for both commands. However, you can enter `-R -v` if you prefer.

- `root` is an argument. In this case, it means that the ownership of the directory will be transferred to the root user.
- `/home/itang/ToDo` is the directory whose ownership is being changed. Originally, it belonged to the user `itang`, since it is in the home directory for that user. After the command is run, the `ToDo` directory will belong to the root user.

#### Understanding Common Options

Many options differ with each command. However, a few basic options are used reasonably consistently. Some may have slight variations, such as using upper or lower case letters. If you have any doubt about an option, check the help before using it.

### Common Command Options

| Option | What It Does |
| :--- | :--- |
| -d, --debug | Displays debugging information |
| -f, --force | Runs the command no matter what the consequences, such as over-writing existing files. |
| --help | Displays info help for the command |

### Common Command Options

| Option | What It Does |
| :--- | :--- |
| -i, --interactive or --ignore-case | Waits for confirmation before doing each part of the command (i, interactive).<br>Ignores the distinction between lower case and capital letters (ignore-case). |
| -R, -r, --recursive | Includes files and sub-directories of the directory name in the command. |
| -V, -v, --verbose | Displays what a command is doing so you can see its progress. |

### Entering Multiple File Names for a Command

The simplest way to have a command affect multiple files is to enter the file names with a space between them. Because this method specifies which files are affected by the command, it reduces the chances of accidentally applying the command to the wrong file.

For example, if a user called mary wanted to copy files called tasklist and notes to her backup directory, she would type:

```
cp /home/mary/tasklist notes /home/mary/backup/
```

### Entering Commands with Strings

Some commands use a string as an argument. A string is a combination of letters, numbers, characters and/or spaces inside single or double quotation marks.
