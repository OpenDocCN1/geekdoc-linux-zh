
# Part I: Getting Started in Fedora and RHEL

- **Forward Search (Alt+n)** — After you press these keys, you are asked to enter a string to do a forward search. Type a string, and press Enter to see the most recent command line that includes that.
- **Beginning of History List (Alt+<)** — Brings you to the first entry of the history list.
- **End of History List (Alt+>)** — Brings you to the end of the history list.

Another way to work with your history list is to use the `fc` command. Type `fc` followed by a history line number, and the command is opened in a text editor. Make the changes that you want. When you exit the editor, the command runs. You can also give a range of numbers (for example, `fc 100 105`). All the commands open in your text editor, and then run one after the other when you exit the editor.

The history list is stored in `.bash_history` file in your home directory. Up to 1000 history commands are stored for you by default. Note that this serves as a history of your commands, something the root or other users may not want to expose.

# Connecting and expanding commands

A truly powerful feature of the shell is the capability to redirect the input and output of commands and from other files. To allow commands to be string together, the shell uses metacters. As noted earlier, a metacharacter is a typed character that has special meaning to the shell for connecting commands or requesting expansion.

# Piping commands

The pipe (`|`) metacharacter connects the output of one command to the input of another command. This lets you work on some data, and then have the command deal with the results. Here is an example of a command line that includes pipes:

```bash
$ cat /etc/passwd | sort | cut -f1-5 -d | less
```

This lists the contents of the `/etc/passwd` file and pipes the output to the `sort` command. The `sort` command takes the users name and begins each line of the `/etc/passwd` file.

Pipes are an excellent illustration of how UNIX, the predecessor of Linux, was created as an operating system made up of building blocks. A standard practice in UNIX is to connect utilities in different ways to get different jobs done. For example, before the days of graphical word processors, users created plain-text files that included macros to indicate formatting. To see how document reality appeared, they used a command such as the following:

```bash
$ gunzip < /usr/share/man/man/grep.1.gz | nroff -c -man | less
```

# Chapter 4: Linux Commands 159

In this example, the contents of the grep man page (grep.gz) are directed as input to the gunzip command to be unzipped. The output from gunzip is piped to the nroff command to format the page using the manual (-man). The output is piped to the less command to display the output. The file being displayed is in plain text, you could have substituted any number of options with the text before displaying it. You could sort the contents, change or delete some of the content, or bring in text from other documents. The key is that, instead of all these features in one program, you get results from piping and redirecting input multiple commands.

# Sequential commands

Sometimes you may want a sequence of commands to run, with one command completing the next command begins. You can do this by typing several commands on the same command line and separating them with semicolons (;).

```bash
$ date ; troff -me verylargdocument | lpr ; date
```

In this example, I was formatting a huge document and wanted to know how long it would take. The first command (date) showed the date and time before the formatting started. The troff formatted the document and piped the output to the printer. When the formatting was done, the date and time was printed again (so I knew when the troff completed).

# Background commands

Some commands can take a while to complete. Sometimes you may not want to tie up your shell waiting for a command to finish. In those cases, you can have the commands run in the background using the ampersand (&).

Text formatting (such as nroff and troff, described earlier) are examples of commands that are often run in the background to format a large document. You may want to create your own shell scripts that run in the background to continue continuously for certain events to occur, such as the hard disk filling or particular users logging in.

Here is an example of a command running in the background:

```bash
$ troff -me verylargdocument | lpr &
```

There are other ways to manage background and foreground processes (described in the “Managing background and foreground processes” section).

# Expanding commands

With command substitution, you can have the output of a command interpreted by the shell instead of the command itself. In this way, you can have the standard output of a command become an argument for another command. The two forms of command substitution are

$ $(command) or `command` . (The first case is the preferred method.)

The command in this case can include options, metacharacters, and arguments. Here is an example of using command substitution:

```bash
$ vi $(find /home | grep xxyzy)
```

In this line, the command substitution is done before the vi command is run. First, the find command starts at the /home directory and prints out all files and directories below that point in the system. This output is piped to the grep command, which filters out all files except for those that include the string xxyzy. Finally, the vi command opens all filenames (one at a time) to that xxyzy.

This particular example might be useful if you knew that you wanted to edit a file for which you know the name but not the location. As if the string was uncommon, you could find and open every instance of a filename beside a point you chose in the file system.

# Expanding arithmetic expressions

There may be times when you want to pass arithmetic results to a command. There are two forms you can use to expand an arithmetic expression and pass to the shell:
$[expression] or $(expression) . Here is an example:

```bash
$ echo "$(2008 - 1957) years old."
I am 51 years old.
```

In this example, the shell interprets the arithmetic expression (2008–1957), and then passes information to the echo command. The echo command displays the text, with the results of the arithmetic (51) inserted.

# Expanding variables

Environment variables store information within the shell can be expanded using the dollar ($) metacharacter. When you expand an environment variable on a command line, the value of the variable is printed instead of the variable name, as follows:

```bash
$ echo $USER
```

Using environment variables

When you start a shell (by logging in or opening a window), a lot of environment variables are already set. Here are some variables that are either set when you use or can be set by you:

- **BASH**: Contains the full path of the bash command. This is usually /bin/bash
- **BASH_VERSION**: A number of the current version of bash.
- **EUID**: This is the effective user ID of the current user. It is assigned when the shell starts, based on the user's entry in /etc/passwd.
- **FCEDIT**: If set, this variable indicates the text editor used by the fc command to edit history commands. If this variable is not set, the vi command is used.
- **HISTFILE**: The location of your history file. It is typically located at $HOME/.bash_history.
- **HISTFILESIZE**: The number of history entries that can be stored. After this is reached, the oldest commands are discarded. The default value is 1000.
- **HOSTCMD**: This returns the number of the current command in the history list.
- **HOME**: This is your home directory. It is your working directory each time you log in or type cd with any options.
- **HOSTTYPE**: A value that describes the computer architecture which the Linux system is running. For Intel-compatible PCs, the value is i386, i486, i586, i686, or x86. For AMD 64-bit and Intel EM64 machines, the value is x64. There is also ppc and pp64, for Apple computers (PowerPC 32-bit and 64-bit).
- **MAIL**: This is the location of your mailbox file. It is typically your user name in the /var/mail/ directory.
- **OLDPWD**: The directory that was the working directory before you changed to the current working directory.
- **OSTYPE**: A name identifying the current operating system. For Fedora and RHEL, the OSTYPE value is either linux or linux-gnu, depending on the type of shell you are using. (Bash can run on other operating systems as well.)

To see the environment variables currently assigned, type any variable name by preceding it with a dollar sign ($). For example:

```bash
$ echo $USER
```

This command prints the value of USER, which holds your user name. Substitute any other variable name for USER to print its value.
