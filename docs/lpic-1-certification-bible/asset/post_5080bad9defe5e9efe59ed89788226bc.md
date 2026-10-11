
# CHAPTER 14
## Using Shells and Scripts

### EXAM OBJECTIVES

**Exam 102 General Linux, Part 2**

- **1.7 Text editing, Processing, Printing**
  - Perform basic file editing operations using vi. Edit text files using vi. Includes vi navigation, basic modes, inserting, editing and deleting text, finding text, and copying text.
- **1.9 Shells, Scripting, Programming, Compiling**
  - Customize and use the shell environment. Customize your shell environment: set environment variables (e.g. PATH) at login or when spawning a new shell; write bash functions for frequently used sequences of commands. Involves editing these files in your home directory: `.bash_profile | .bash_login | .profile ; .bashrc ; .bash_logout ; .inputrc`
  - Customize or write simple scripts. Customize existing scripts (like paths in scripts of any language), or write simple new (ba)sh scripts. Besides use of standard sh syntax (loops, tests), be able to do things like: command substitution and testing of command return values, test of file status, and conditional mailing to the superuser. Make sure the correct interpreter is called on the first (#!) line, and consider location, ownership, and execution- and suid-rights of the script.

### CHAPTER PRE-TEST

- Which file is executed when a user logs out?
- How many named buffers does vi have?
- Which file customizes the readline?
- Which command tells vi to insert text?
- How many modes does vi have?
- Which command is used to make a variable usable by subprocesses?
- Which variable specifies the prompt when given after an incomplete command?
- Which command is used to read user input from a shell script?
- What is the first line of a shell script?
- Which commands are used to set shell options that change the features of bash?

Most Linux distributions now ship with easy-to-use, point-and-click GUI tools, but they are not always the best to use or the best available. The other way to configure the system is by manually editing the configuration files using a text editor. Several text editors exist. Some of the most popular are vi, emacs, Joe, Pico, and ae. The best editor is often hotly debated on the Internet, and the choice is up to your personal preference. But, the vi editor is usually installed by default with most Linux distributions and other UNIX systems. Given that, it is well worth the time invested to learn it. Never know; you may find that it is your favorite editor after all. Later in the chapter we go over writing shell scripts to help ease the network administrators' burden. These scripts can be used to automate tasks and reduce repetitive work. Linux also uses many different scripts to start up and configure the system. These are covered and their functions are explained.

### Using vi

**1.7 Text editing, Processing, Printing**

**Objective:** Perform basic file editing operations using vi. Edit text files using vi. Includes vi navigation, basic modes, inserting, editing and deleting text, finding text, and copying text.

William Joy originally wrote vi, pronounced *cee eye*, at the University of Berkeley in California. It is a text mode editor with a command set that not everyone is fond of; however, with a little experience that command set becomes second nature. Several clones of vi exist that add functionality or even a graphical interface, but you can never be sure to find them on a system. So, it is best to learn using the basic vi editor.

### Text editing practices

There are a couple of best practices to remember when editing text files that are worth repeating. First, be sure to have a backup copy of any file that you are editing, especially important configuration files. Copy the original to another file for safekeeping, remembering to reset the file permissions as necessary so those stay the same as well.

When editing a file for the first time we usually rename the original to the same name but with a .dist extension. This signifies that it is the version that shipped with the distribution. After that, we normally add a date extension.

Save early and save often. Network connections drop, lines are accidentally deleted, or important configuration options are overwritten. Be sure to save your work often so that you do not have to start over in case of such an accident.

### Opening files for editing

To have vi open a file for editing, use the following command:

```bash
vi filename
```

If no filename is specified, vi opens with a blank slate, and you can specify the filename later when saving. Be sure that you have read and write permissions to the file, or you will not be able to save changes and may find that out after spending a lot of time editing the file. If you know which line needs to be edited in a file, you can jump straight to that line using the following syntax:

```bash
vi +10 filename
```

This tells vi to start editing the file at line 10. Another option for quickly jumping to a point in the file is to specify a search string to start at. This is done with the following syntax:

```bash
vi +/telnet inetd.conf
```

This would start vi, open the `inetd.conf` file, and then jump to the first instance of the string `telnet`.

There are three modes in vi. They are as follows:

- Command mode
- Insert mode
- Last line mode

When vi starts up, it defaults to command mode. When in command mode, you can move the cursor around, enter commands, delete and append text, or enter insert mode. To return to command mode you press the Esc key. When in insert mode, all you can do is insert text and use the Delete key to remove mistyped text. You cannot move the cursor around the document. You must go back to command mode for that. The last line mode is used to enter complex commands. To enter last line mode you type a colon from command mode. After the command is completed you are returned to command mode.

> **Caution** Remember that in vi the commands are case-sensitive. `j` is different from `J`.

### Exiting vi and saving files

Exiting vi is done from the last line mode, so the commands start with a colon from command mode.

- **Saving without closing** — To save the current file, you would use the `:w` command. You should do this often in case of big mistakes or system problems.
- **Saving and closing** — To exit vi and save the changes to the file, you can either use the `:wq` command or just `ZZ`.
- **Closing without saving** — If you need to redo the changes you have made to a file, you should exit vi without saving your changes. This is done with the `:q!` command. The exclamation overrides the requirement to save the file before you can exit.

> **Exam Tip**
> In vi, to save a file without closing, use the `:w` command. To exit and save changes, use `:wq` or `ZZ`. To exit without saving, use `:q!`.

### Moving the cursor

vi is a text mode editor, so mouse support isn't available. This is sometimes daunting to new users, but is easily overcome. vi offers numerous shortcuts to quickly move through files, so users are not bogged down in simple cursor movements.

In most cases you can just use the arrow keys to move around the document. But, not all systems have these keys, and sometimes terminal emulation incompatibilities cause them not to function as expected. The cursor movement keys are shown below, diagramming their function:

![](img/96d9ccd181675a8ae8b6a1146c919d2b_549_0.png)

The `-` key can be substituted for `k`, and the `+` key for `j`. You should learn these keys even if you plan to always use the arrow keys. Many other applications use the vi cursor movement keys since they are popular and well known. By themselves, the keys move the cursor one line or character. To move more, you can use a number, such as `4j` to move down four lines.

To move around the file more quickly, you can use the full-page and half-page commands. These are `Ctrl+f` and `Ctrl+b` to move forward and backward a page, and `Ctrl+d` and `Ctrl+u` to move forward and backward half of a page.

You can also use line numbers to move around the file. To display the number of the current line you would use the `Ctrl+g` command. To move to a specific line you would use the `nG` command, where `n` is the line number.

There are many other commands to move the cursor around. Most of these are shown in Table 14-1. Remember that you can cause a command to repeat by putting a number in front of it.
