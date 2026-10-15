
but sh (the original Bourne shell) and ksh (the Korn shell) are used on a few UNIX systems. Shell scripts are typically used for light tasks such as automating a sequence of commands or assembling several filters to process data.

The shell is always available, so shell scripts are relatively portable and have few dependencies other than the commands they invoke. Whether or not you choose the shell, the shell may choose you: most environments include a hefty complement of existing sh scripts, and those scripts frequently need to be read, understood, and tweaked by administrators.

For more sophisticated scripts, it’s advisable to jump to a real programming language such as Perl or Python, both of which are well suited for administrative work. These languages incorporate a couple of decades’ worth of language design advancements relative to the shell, and their text processing facilities (invaluable to administrators) are so powerful that sh can only weep and cower in shame.

The main drawback to Perl and Python is that their environments can be a bit fussy to set up, especially when you start to use third-party libraries that have compiled components. The shell skirts this particular issue by having no module structure and no third-party libraries.

This chapter takes a quick look at bash, Perl, and Python as languages for scripting, along with regular expressions as a general technology.

## 2.1 SHELL BASICS

Before we take up shell scripting, let’s review some of the basic features and syntax of the shell. The material in this section applies to all major shells in the sh lineage (including bash and ksh, but not csh or tcsh), regardless of the exact platform you are using. Try out the forms you’re not familiar with, and experiment!

### Command editing

We’ve watched way too many people edit command lines with the arrow keys. You wouldn’t do that in your text editor, right?

If you like emacs, all the basic emacs commands are available to you when you’re editing history. <Control-E> goes to the end of the line and <Control-A> to the beginning. <Control-P> steps backward through recently executed commands and recalls them for editing. <Control-R> searches incrementally through your history to find old commands.

If you like vi, put your shell’s command-line editing into vi mode like this:

```
$ set -o vi
```

As in vi, editing is modal; however, you start in input mode. Type <Esc> to leave input mode and “i” to reenter it. In edit mode, “w” takes you forward a word, “b”

finds the next X in the line, and so on. You can walk through past command history entries with <Esc> k. Want emacs editing mode back again?

```
$ set -o emacs
```

### Pipes and redirection

Every process has at least three communication channels available to it: “standard input” (STDIN), “standard output” (STDOUT), and “standard error” (STDERR). The kernel sets up these channels on the process’s behalf, so the process itself doesn’t necessarily know where they lead. They might connect to a terminal window, a file, a network connection, or a channel belonging to another process, to name a few possibilities.

UNIX has a unified I/O model in which each channel is named with a small integer called a file descriptor. The exact number assigned to a channel is not usually significant, but STDIN, STDOUT, and STDERR are guaranteed to correspond to file descriptors 0, 1, and 2, so it’s safe to refer to these channels by number. In the context of an interactive terminal window, STDIN normally reads from the keyboard and both STDOUT and STDERR write their output to the screen.

Most commands accept their input from STDIN and write their output to STDOUT. They write error messages to STDERR. This convention lets you string commands together like building blocks to create composite pipelines.

The shell interprets the symbols <, >, and >> as instructions to reroute a command’s input or output to or from a file. A < symbol connects the command’s STDIN to the contents of an existing file. The > and >> symbols redirect STDOUT; > replaces the file’s existing contents, and >> appends to them. For example, the command

```
$ echo "This is a test message." > /tmp/mymessage
```

stores a single line in the file /tmp/mymessage, creating the file if necessary. The command below emails the contents of that file to user johndoe.

```
$ mail -s "Mail test" johndoe < /tmp/mymessage
```

To redirect both STDOUT and STDERR to the same place, use the >& symbol. To redirect STDERR only, use 2>.

The find command illustrates why you might want to handle STDOUT and STDERR separately because it tends to produce output on both channels, especially when run as an unprivileged user. For example, a command such as

```
$ find / -name core
```

usually results in so many “permission denied” error messages that genuine hits get lost in the clutter. To discard all the error messages, you can use

```
$ find / -name core 2> /dev/null
```
