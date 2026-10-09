
# File Globbing Examples

- Use the `ls` command just to list them all (by default, it lists them by name in alphabetical order):

```
$ ls
cinque dieci due nove otto quattro sei sette tre uno
```

- Now let's group them in a number of different ways, using the metacharacters we just mentioned. First, list all the files that start with the letter s:

```
$ ls s*
sei sette
```

- Next, use the `?` metacharacter to select all files whose name consists of exactly three characters:

```
$ ls ???
due sei tre uno
```

- Next, select all the files whose name starts with a vowel:

```
$ ls [aeiou]*
otto uno
```

- Next, select all the files whose name starts with any character in the range a to f:

```
$ ls [a-f]*
cinque dieci due
```

- Finally, select all the files whose name *does not* start with a vowel. The exclamation operator must be within the square parentheses.

```
$ ls [!aeiou]*
cinque dieci due nove quattro sei sette tre
```

## How It Works

We've used the `ls` command here to demonstrate file globbing, because the output from `ls` shows the effects of the globbing very clearly. However, you should note that we can use file globbing with any command that expects filename or directory-name arguments. Let's look at each of the globbing expressions here.

We used the expression `s*` to match all files that begin with the letter s:

```
$ ls s*
```

This expression matches the file names `sei` and `sette`, and would even match a file called `s` if there were one, because the `*` matches any string of any length (including the 0-length string).

To match filenames with exactly three characters, we use a `?` to represent each character:

```
$ ls ???
```

We used the expression `[aeiou]*` to pick up all filenames starting with a vowel. The `*` works in the same way as in the `s*` example, matching any string of any length, so files matching this expression begin with a character a, e, i, o, or u, followed by any other sequence of characters:

```
$ ls [aeiou]*
```

A similar approach applies for the expression `[a-f]*`, except that we use a hyphen (-) within the parentheses to express any one of the characters in a range:

```
$ ls [a-f]*
```

Using a range implies that the characters have an assumed order. In fact, this encompasses all alphanumeric characters, with numbers (0-9) preceding letters (a-z). (Hence the expression `[0-z]*` would match all filenames that start with either a number or a letter.)

Finally, we use the exclamation mark (!) within the square parentheses to negate the result of the vowel-matching expression, thereby arriving at all filenames that start with a consonant:

```
$ ls [!aeiou]*
```

# Aliases

Aliases are our first step toward customizing Bash. In its simplest form, an alias functions as an abbreviation for a commonly used command. In more complex cases, aliases can define completely new functionality. An alias is easily defined using the notation `<alias_name>=<alias_value>`. When we need it, we invoked it using `<alias_name>` – the shell substitutes `<alias_name>` with `<alias_value>`.

In fact, the standard Red Hat Linux 9 shell already has several aliases defined. We could list the existing aliases using the `alias` command:

```shell
$ alias
alias 1='ls -d .* --color=tty'
alias 11='ls -l --color=tty'
alias 1s='ls --color=tty'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
```

Some of the common aliases include aliases for the `ls` command, to include our favorite options. If you use the `ls` command without any options then it would simply print the list of files and sub-directories under the current working directory. However, in this case the `ls` command is aliased to itself, with the `--color` option, which allows `ls` to indicate different file types with different colors.

Aliases may be defined for the lifetime of a shell by specifying the alias mapping at the command line or in a startup file (discussed in a later section) so that the aliases are available every time the shell starts up.

# Environment Variables

Like aliases, **environment variables** are name-value pairs that are defined either on the shell prompt or in startup files. A process may also set its own environment variables programmatically (that is, from within the program, rather than declared in a file or as arguments).

Environment variables are most often used either by the shell or by other programs to communicate settings. Some programs communicate information through environment variables to programs that they spawn. There are several environment variables set for us in advance. To list all of them that are currently set, you can use the `env` command, which should display an output similar to that below:

```shell
$ env
HOSTNAME=localhost.localdomain
SHELL=/bin/bash
TERM=xterm
HISTSIZE=1000
USER=deepakt

MAIL=/var/spool/mail/deepakt
PATH=/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/deepakt/bin
...
```

As you can see, the `PATH` variable is one of the environment variables listed here. As we described earlier in this chapter, Bash uses the value of the `PATH` variable to search for commands. The `MAIL` variable, also listed here, is used by mail reading software to determine the location of a user's mailbox.

## System-defined Variables and User-defined Variables

We may set our own environment variables or modify existing ones:

```
$ echo $PATH
PATH=/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/deepakt/bin
$ export MYHOME=/home/deepakt
$ export PATH=$PATH:SMYHOME/mybin
$ echo $PATH
PATH=/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:/home/deepakt/bin:/home/
deepakt/mybin
```

While user-defined variables (also known as local variables) can be set as `MYHOME=/home/deepakt`, these variables will not be available to any of the commands spawned by this shell. For local variables to be available to child processes spawned by a process (the shell in this case), we need to use the `export` command. However, to achieve persistence for variables even after we log out and log back in, we need to save these settings in startup files.

Environment variables are defined either interactively or in a startup file such as `.bashrc`. These variables are automatically made available to a new shell. Examples of environment variables are `PATH`, `PRINTER`, and `DISPLAY`.

However, local variables do not get automatically propagated to a new shell when it is created. The `MYHOME` variable is an example of a local variable.

The `echo` command, followed by the name of a variable prefixed with a dollar ($) symbol, prints the value of the environment variable.

# I/O Redirection

Earlier in the chapter, we referred to the file system and how we can use file system commands to manipulate files and directories and process management commands such as `ps` to manage processes. The shell provides us with a powerful set of operators that allow us to manage input, output, and errors while working with files and processes.

## I/O Streams

If a process needs to perform any I/O operation, it has to happen through an abstraction known as an I/O stream. The process has three streams associated with it – standard input, standard output, and standard error. The process may read input from its standard input, write its output to standard output, and write error messages to its standard error stream.

By default, the standard input is associated with the keyboard; output and error are associated with the terminal, in our case mostly an *xterm*. Sometimes, we may not want processes to write to or read from a terminal; we may want the process to write to another location, such as a file. In this case we need to associate the process's standard output (and possibly the standard error) with the file in question. The process is oblivious to this, and continues to read from the standard input and write to the standard output, which in this case happens to be the files we specify. The I/O redirection operators of the shell make this redirection of the streams from the terminal to files extremely simple.

## The < Operator

The `<` *operator* allows programs that read from the standard input to read input from a file. For instance, let us consider the *wc* (word count) program, which reads input from the keyboard (until a *Ctrl-D* is encountered) and then prints the number of lines, words, and characters that were input:

```
$ wc -l
12345
67890
12345
^D
3
```

*Note that we've used the -l option here, which has wc print the number of lines only.*

Now consider a case in which we have the input to *wc* available in a file, called `31linefile.txt`. In this case the following command will produce the same result:

```
$ wc -l < 31linefile.txt
3
```

In this case the standard input is redirected from the keyboard to the file.

## The > Operator

The `>` *operator* is similar to the `<` operator. Its purpose is to redirect the standard output from the terminal to a file. Let us consider the following example:

```
$ date > date.txt
```

The `date` command writes its output to the standard output, which is usually the terminal. Here, the `>` operator indicates to the shell that the output should instead be redirected to a file.

When we write the file out to the terminal (using the `cat` command), we can see the output of the `date` command displayed:

```
$ cat date.txt
Tue Jan 14 23:03:43 2003
```
