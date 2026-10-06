# Chapter 4: Using Linux Commands 149

Although most Linux users have a preference for one shell or another, when you know how to use one shell, you can quickly learn any of the others by occasionally referring to the shell's man page (for example, type man bash). The bash shell is roughly compatible with the sh shell.

# Using the Shell in Linux

When you type a command in a shell, you can also include other characters that change or add to how the command works. In addition to the command itself, these are some of the other items that you can use on a command line:

+   **Options** — Most commands have one or more options you can add to change their behavior. Options typically consist of a single letter, by a dash. You can also combine several options after a single dash. For example, the command -la lists the contents of the current directory. The -l asks for a detailed (list) of information, and the -a asks for files beginning with a dot (.) listed. When a single option of a word, it is usually preceded by a double dash (--). For example, to use help on many commands, you would enter --help on the command line. Here's an example of help information for the ls command (Output is piped to the less command) through it, type q to quit:

```
$ ls --help | less
Usage: ls [OPTION]... [FILE]
List information about the FILE (the current directory by default).
Sort entries alphabetically if none of the -cftUSUX nor --sort.
```

Mandatory arguments are mandatory for long options are for short options too
-a, --all do not hide entries starting with .
-A, --almost-all do not list implied . and .

+   **Arguments** — Many commands also accept arguments after any options are entered. An argument is an extra piece of information, such as a filename, that can be used by the command. cat /etc/passwd displays the contents of the /etc/passwd file on your screen. In case, /etc/passwd is the argument.

+   **Environment variables** — The shell stores information that may be useful to the user's shell session in what are called environment variables. Examples of environment variables include $SHELL (which identifies the shell you are using), $PS1 (which defines your shell prompt), and $MAIL (which identifies the location of your mailbox).

> TIP: You can check your environment variables at any time. Type **declare** to list the current environment variables. Or you can type echo $VALUE, where VALUE is replaced by the name of a particular environment variable you want to list.