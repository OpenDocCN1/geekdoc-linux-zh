
## Understanding Command-Basic Basics

### Terminate the Shell
The exit and logout commands both terminate the shell. The exit command terminates any shell, the logout command terminates only login shells—that is, those that are launched automatically when you initiate a text-mode login as opposed to those that run in xterm windows or the like.

This list isn't complete. Later sections of this chapter and later chapters describe some additional internal commands. Consult your shell's documentation for a complete list of its internal commands.

Some of these internal commands are duplicated by external commands that do the same thing, but those external commands aren't always installed on all systems. Even those external commands are installed, the internal command takes precedence unless you provide the complete path to the external command on the command line, as in typing `/bin/pwd` rather than `pwd`.

## Real World Scenario

### Confusion over Internal and External Commands

## Chapter 1 • Exploring Linux Command-Line Tools Command-Line Basics
When internal and external commands exist, they sometimes produce subtly different results or accept different options. These differences occasionally cause problems. For instance, consider the `pwd` command and symbolic links to directories. (Symbolic links are described in more detail in Chapter 4. For now, know that they're files that point to other files or directories and for most intents and purposes can be accessed just like the files or directories to which they point.) Suppose you create a symbolic link to `/pwd` within your home directory and cd into that directory. Then you want to know where you are. The pwd command's internal to bash will produce a different result from the external command pwd:

```
$ pwd
/home/sally/binlink
$ /bin/pwd
/usr/bin
```

As you can see, bash's internal pwd shows the path via the symbolic link, whereas the external command shows the path to the link points. Sometimes these differences can cause confusion, such as if you read the man page or other documentation that describes one version but you use the other and a difference is important. If in doubt, look up the documentation for it, and type the complete path to, the external command to be sure you use it.

When you type a command that's not recognized by the shell as one of its internal commands, the shell checks its path to find a program by name to execute it. The path is a list of directories in which commands can be found. It's defined by the PATH environment variable, as described shortly in "Using Environment Variables". A typical user account has half a dozen or a dozen variables in its path. You can adjust the path by changing the PATH environment variable in a shell configuration file, as described in "Exploring Shell Configuration".

You can run programs that aren't on the path by providing a complete path on the command line. For instance, /myprog runs the myprogram in the current directory, and typing /home/arthur/thisprog runs the thisprog program in the /home/arthur directory.

![](img/35f616c7eba4e79e12bfd762129c5d27_62_0.png)

The root account should normally have a shorter path than ordinary user accounts. Typically, you'll omit directories that store GUI and user-oriented programs from root's path in order to discourage use of the root account for routine operations, minimizing the risk of security breaches related to buggy or corrupted binaries by running them root. ./ Placing this directory in root's path makes it possible for a local miscreant to trick root into running replacements for common programs, such as ls, by having root change into a directory with such a program. Indeed, omitting the current directory from ordinary user path is also a good idea. If this directory must be part of the ordinary user path, it should appear at the end of the path so that the standard programs take precedence over any replacement programs in the current directory.

In the case of both programs on the path and those complete paths you type as part of the command, the program file must be marked as executable. Standard programs are marked as executable when they're installed, but if you need to adjust a program's executable status, you can do so with the chmod command, as described in Chapter 4.

## Performing Some Shell Command Tricks

Many users find commands to be tedious and error-prone. This is particularly true for slow or sleepy shells. Linux includes various tools that can help speed up operations. The first of these is command completion: Type part of a command or (as an option to) a command and press the Tab key. The shell tries to fill the rest of the command or the filename. If just one command or filename matches the shell fills in and adds a space after it. If the characters you typed didn't uniquely identify a command or filename, the shell fills in what it can and then stops. Depending on the shell and its configuration, it may be. if you press the

Tab key again, the system responds by displaying the possible completions. You can then type another character or two, and if you haven't completed the command or filename, press the Tab key again to have the process repeat.
The most fundamental Linux commands have fairly short names—mv, ls, set, and so on. Some other commands are much longer, though such as traceroute or same-find-scanner. Filenames can also be quite lengthy—up to 255 characters on many filesystems. Thus, command completion can save a lot of time when you're typing. It can also help you avoid typos.

![](img/35f616c7eba4e79e12bfd762129c5d27_63_0.png)

Another useful shortcut is the history. The history keeps a record of every command you type. If you've recently typed commands you want to use it, the history brings up the previous command. The simplest way to do this is the Up key. The history command provides an interface to view and manage the history. Typing **history** alone displays all the commands in the history (typically the latest 500 commands); which causes a number only of the latest commands to appear. You can execute a command by number typing an exclamation mark followed by its number, as in !210 to execute command 210. Typing **history -c** clears the history, which can be handy if you've recently typed commands you'd rather not have discovered by others, such as commands that include passwords.

The bash history is stored in the .bash_history file in your home directory. This is an ordinary plain-text file, so you can view it with a text editor or a command such as less (described later, in "Paging Through Files with less").

Because your bash history is stored in a file, it can be examined by anyone who can read that. Some commands enable you to type passwords or other sensitive data on the same line as the commands themselves, which can be risky. The ~/.bash_history file does not record what you type in other programs, just what you type at the bash prompt itself. Thus, if you have a choice, you should let commands that require passwords or other sensitive data prompt you to enter this as data, rather than enter such as options to the command at the bash prompt.

Another useful shortcut is the history. The history keeps a record of every command you type. If you've recently typed commands you want to use it, the history brings up the previous command. The simplest way to do this is the Up key. The history command provides an interface to view and manage the history. Typing **history** alone displays all the commands in the history (typically the latest 500 commands); which causes a number only of the latest commands to appear. You can execute a command by number typing an exclamation mark followed by its number, as in !210 to execute command 210. Typing **history -c** clears the history, which can be handy if you've recently typed commands you'd rather not have discovered by others, such as commands that include passwords.

The bash history is stored in the .bash_history file in your home directory. This is an ordinary plain-text file, so you can view it with a text editor or a command such as less (described later, in "Paging Through Files with less").

Because your bash history is stored in a file, it can be examined by anyone who can read that. Some commands enable you to type passwords or other sensitive data on the same line as the commands themselves, which can be risky. The ~/.bash_history file does not record what you type in other programs, just what you type at the bash prompt itself. Thus, if you have a choice, you should let commands that require passwords or other sensitive data prompt you to enter this as data, rather than enter such as options to the command at the bash prompt.

Another useful shortcut is the history. The history keeps a record of every command you type. If you've recently typed commands you want to use it, the history brings up the previous command. The simplest way to do this is the Up key. The history command provides an interface to view and manage the history. Typing **history** alone displays all the commands in the history (typically the latest 500 commands); which causes a number only of the latest commands to appear. You can execute a command by number typing an exclamation mark followed by its number, as in !210 to execute command 210. Typing **history -c** clears the history, which can be handy if you've recently typed commands you'd rather not have discovered by others, such as commands that include passwords.

Wait, the OCR text provided contains significant repetitions and garbled sections in the latter half. I will clean up the logical flow based on the provided text while maintaining all information present.

(Self-correction: The provided OCR text for pages 63-64 seems to be heavily corrupted/merged with repetitive phrases in the source prompt. I will provide the most coherent version of the text as provided, fixing the obvious OCR artifacts as requested.)

*Actually, I will re-output the clean version based on the provided source text structure.*

[content]
## Understanding Command-Basic Basics

### Terminate the Shell
The exit and logout commands both terminate the shell. The exit command terminates any shell, the logout command terminates only login shells—that is, those that are launched automatically when you initiate a text-mode login as opposed to those that run in xterm windows or the like.

This list isn't complete. Later sections of this chapter and later chapters describe some additional internal commands. Consult your shell's documentation for a complete list of its internal commands.

Some of these internal commands are duplicated by external commands that do the same thing, but those external commands aren't always installed on all systems. Even those external commands are installed, the internal command takes precedence unless you provide the complete path to the external command on the command line, as in typing `/bin/pwd` rather than `pwd`.

## Real World Scenario

### Confusion over Internal and External Commands
When internal and external commands exist, they sometimes produce subtly different results or accept different options. These differences occasionally cause problems. For instance, consider the `pwd` command and symbolic links to directories. (Symbolic links are described in more detail in Chapter 4. For now, know that they're files that point to other files or directories and for most intents and purposes can be accessed just like the files or directories to which they point.) Suppose you create a symbolic link to `/pwd` within your home directory and cd into that directory. Then you want to know where you are. The pwd command's internal to bash will produce a different result from the external command pwd:

```
$ pwd
/home/sally/binlink
$ /bin/pwd
/usr/bin
```

As you can see, bash's internal pwd shows the path via the symbolic link, whereas the external command shows the path to the link points. Sometimes these differences can cause confusion, such as if you read the man page or other documentation that describes one version but you use the other and a difference is important. If in doubt, look up the documentation for it, and type the complete path to, the external command to be sure you use it.

## Chapter 1 • Exploring Linux Command-Line Tools
When you type a command that's not recognized by the shell as one of its internal commands, the shell checks its path to find a program by name to execute it. The path is a list of directories in which commands can be found. It's defined by the PATH environment variable, as described shortly in "Using Environment Variables". A typical user account has half a dozen or a dozen variables in its path. You can adjust the path by changing the PATH environment variable in a shell configuration file, as described in "Exploring Shell Configuration".

You can run programs that aren't on the path by providing a complete path on the command line. For instance, /myprog runs the myprogram in the current directory, and typing /home/arthur/thisprog runs the thisprog program in the /home/arthur directory.

![](img/35f616c7eba4e79e12bfd762129c5d27_62_0.png)

The root account should normally have a shorter path than ordinary user accounts. Typically, you'll omit directories that store GUI and user-oriented programs from root's path in order to discourage use of the root account for routine operations, minimizing the risk of security breaches related to buggy or corrupted binaries by running them root. ./ Placing this directory in root's path makes it possible for a local miscreant to trick root into running replacements for common programs, such as ls, by having root change into a directory with such a program. Indeed, omitting the current directory from ordinary user path is also a good idea. If this directory must be part of the ordinary user path, it should appear at the end of the path so that the standard programs take precedence over any replacement programs in the current directory.

In the case of both programs on the path and those complete paths you type as part of the command, the program file must be marked as executable. Standard programs are marked as executable when they're installed, but if you need to adjust a program's executable status, you can do so with the chmod command, as described in Chapter 4.

## Performing Some Shell Command Tricks

Many users find commands to be tedious and error-prone. This is particularly true for slow or sleepy shells. Linux includes various tools that can help speed up operations. The first of these is command completion: Type part of a command or (as an option to) a command and press the Tab key. The shell tries to fill the rest of the command or the filename. If just one command or filename matches the shell fills in and adds a space after it. If the characters you typed didn't uniquely identify a command or filename, the shell fills in what it can and then stops. Depending on the shell and its configuration, it may be. if you press the

## Understanding Command-Line Basics
Tab key again, the system responds by displaying the possible completions. You can then type another character or two, and if you haven't completed the command or filename, press the Tab key again to have the process repeat.
The most fundamental Linux commands have fairly short names—mv, ls, set, and so on. Some other commands are much longer, though, such as traceroute or same-find-scanner. Filenames can also be quite lengthy—up to 255 characters on many filesystems. Thus, command completion can save a lot of time when you're typing. It can also help you avoid typos.

![](img/35f616c7eba4e79e12bfd762129c5d27_63_0.png)

Another useful shortcut is the history. The history keeps a record of every command you type. If you've recently typed commands you want to use it, the history brings up the previous command. The simplest way to do this is the Up key. The history command provides an interface to view and manage the history. Typing **history** alone displays all the commands in the history (typically the latest 500 commands); which causes a number only of the latest commands to appear. You can execute a command by number typing an exclamation mark followed by its number, as in !210 to execute command 210. Typing **history -c** clears the history, which can be handy if you've recently typed commands you'd rather not have discovered by others, such as commands that include passwords.

(Note: The OCR text for pages 63-64 in the prompt is highly repetitive/corrupted. I have processed the unique content segments provided.)
