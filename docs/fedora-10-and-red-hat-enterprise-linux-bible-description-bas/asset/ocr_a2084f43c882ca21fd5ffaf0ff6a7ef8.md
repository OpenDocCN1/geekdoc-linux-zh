# Part I: Getting Started in Fedora and RHEL

+   - **Forward Search (Alt+n)** — After you press these keys, you are asked to enter a string to do a forward search. Type a string, and press Enter to see the most recent command line that includes that.
- **Beginning of History List (Alt+<)** — Brings you to the first entry of the history list.
- **End of History List (Alt+>)** — Brings you to the end of the history list.

Another way to work with your history list is to use the `fc` command. Type `fc` followed by a history line number, and the command is opened in a text editor. Make the changes that you want. When you exit the editor, the command runs. You can also give a range of numbers (for example, `fc 100 105`). All the commands open in your text editor, and then run one after the other when you exit the editor.

The history list is stored in `.bash_history` file in your home directory. Up to 1000 history commands are stored for you by default. Note that this serves as a history of your commands, something the root or other users may not want to expose.

# Connecting and expanding commands

A truly powerful feature of the shell is the capability to redirect the input and output of commands and from other files. To allow commands to be string together, the shell uses metacters. As noted earlier, a metacharacter is a typed character that has special meaning to the shell for connecting commands or requesting expansion.

# Piping commands

The pipe (`|`) metacharacter connects the output of one command to the input of another command. This lets you work on some data, and then have the command deal with the results. Here is an example of a command line that includes pipes:

```
$ cat /etc/passwd | sort | cut -f1-5 -d | less
```

This lists the contents of the `/etc/passwd` file and pipes the output to the `sort` command. The `sort` command takes the users name and begins each line of the `/etc/passwd` file

Pipes are an excellent illustration of how UNIX, the predecessor of Linux, was created as an operating system made up of building blocks. A standard practice in UNIX is to connect utilities in different ways to get different jobs done. For example, before the days of graphical word processors, users created plain-text files that included macros to indicate formatting. To see how document reality appeared, they used a command such as the following:

```
$ gunzip < /usr/share/man/man/grep.1.gz | nroff -c -man | less
```