
# Understanding Command-Line Basics

In Exercise 1.1, you'll experiment with your shell's completion and command-editing tools.

# EXERCISE 1.1

## Editing Commands

To experiment with your shell's completion and command-editing tools, follow these steps:

1. Log in as an ordinary user.
2. Create a temporary directory by typing `mkdir test`. (Directory and file manipulation commands are described in more detail in Chapter 4.)
3. Change into the test directory by typing `cd test`.
4. Create a few temporary files by typing `touch one two three`. This command creates three empty files named one, two, and three.
5. Type `ls -t`, and without pressing the Enter key, press the Tab key. The system may beep at you or display two. If it doesn't display three, press the Tab key again, and it should. This reveals that two or three is a valid completion to your command, because these are the two files in the test directory whose filenames begin with the letter t.
6. Type `h`, and again without pressing the Enter key, press the Tab key. The system should complete the command `ls -1 three`, at which point you can press the Enter key to execute it. (You'll see information on the file.)
7. Press the Up arrow key. You should see the `ls -1 three` command appear on the command line.
8. Press `Ctrl+A` to move the cursor to the beginning of the line.
9. Press the Right arrow key once, and press `es` (without pressing the Enter key). The command line should now read less -1 three.
10. Press the Right arrow key once, and press the Delete key three times. The command should now read less three. Press the Enter key to execute the command. (Note that you can do so even though cursor isn't at the end of the line.) This invokes the `less` pager on the three file. (The `less` pager is described more fully later, in “Paging Through Files with `less`”) Because this file is empty, you'll see a mostly empty screen.
11. Press the Q key to exit the less pager.

# Exploring Shell Configuration

Shells, like many Linux programs, are configured through files that hold configuration options in a plain-text format. The bash configuration files are actually bash shell scripts, which are described more fully in Chapter 9. For now, you should know that the ~/.bashrc and ~/.profile files are the main user configuration files for bash, and /etc/bash.bashrc and /etc/profile are the main configuration files.

Even without knowing much about shell scripting, you can make simple changes to these files. Edit them in your favorite text editor, and whatever needs changing. For instance, you can add directories to the PATH environment variable, which takes a colon-delimited list of directories.

![](img/35f616c7eba4e79e12bfd762129c5d27_66_0.png)

> Be careful when changing your bash configuration, particularly the global bash configuration files. Save a backup of the original file before making changes, and test your changes immediately by logging in using another virtual terminal. If you spot a problem, revert to your saved copy until you learn the cause and create a working file.

# Using Environment Variables

Environment variables are like variables in programming languages—they hold data referred to by the variable name. Environment variables differ from programs' internal variables in that they're part of the environment of a program, and other programs, such as the shell, can modify this environment. Programs rely on environment variables to set information that can apply to many different programs. For instance, many text-based programs need to know the capabilities of the terminal you use. This information is conveyed by TERM environment variable, which is likely to hold a value such as xterm or Linux. Programs that need to position the cursor, display color text, or perform other tasks that depend on terminal-specific capabilities can customize their output based on this information.

Chapter 9 describes environment variables and their manipulation in more detail. For the moment, you should know that you can set them in bash by using an assignment (=) operator followed by the export command:

```
$ NNTPSERVER=news.abigis.com
$ export NNTPSERVER
```

You can combine these two commands into a simple form:

$ export NNTPSERVER=news.abigisp.com

Either method sets the NNTPSERVER environment variable to news.abigisp.com. (When setting an environment variable, you omit the dollar sign, but subsequent references include a dollar sign to identify the environment variable as such.) Thereafter, programs that need this information can refer to the environment variable. In fact, you can do so from the shell yourself, using the echo command:

$ echo NNTPSERVER
news.abigisp.com

Some environment variables, including the $TERM environment variable, are set automatically when you log in. If a program uses environment variables, its documentation should say so. The NNTPSERVER variable is used by some Usenet news clients, which enable participation in a type of online discussion group that predates Web forums.

You can also view the entire environment by typing env. The result is likely to be several dozens of environment variables and their values. Chapter 9 describes what many of these variables are in detail.

To delete an environment variable, use the unset command, which takes the name of an environment variable (without the $ sign) as an option. For instance, unset NNTPSERVER removes the NNTPSERVER environment variable.

# Getting Help

Linux provides a text-based help system as man. This command's name is short for manual, and its entries (man pages) provide succinct summaries of what a command, file, or other does. For instance, to learn about man, you can type man man. The result is a description of the man command.

The man uses the less pager to display information. This program displays text page at a time. Press the spacebar to move forward a page, Esc by V to move back a page, the arrow keys to move up or down a line at a time, the slash (/) key to search for text, and so on. (Type man to learn all the details, or consult the upcoming section "Paging Through Files with less.") When you are done, Press Q to exit less and the man page its displaying.

Man pages are organized into several sections, which are summarized in Table 1.1. Sometimes a keyword has entries in multiple sections; for instance, passwd has entries under both section 1 and section 5. In most cases, man returns the entry in the lowest-numbered section, but you can force the issue by preceding the keyword with the section number.

![](img/35f616c7eba4e79e12bfd762129c5d27_67_0.png)

# TABLE 1.1 Manual sections

| Section number | Description |
| --- | --- |
| 1 | Executable programs and shell commands |
| 2 | System calls provided by the kernel |
| 3 | Library calls provided by program libraries |
| 4 | Device files (usually stored in /dev) |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous (macro packages, conventions, and so on) |
| 8 | System administration commands (programs run or exclusively by root) |
| 9 | Kernel routines |
