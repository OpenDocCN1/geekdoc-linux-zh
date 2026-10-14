
## What Exactly Are Commands?

A command can be one of four things:

- **An executable program** like all those files we saw in `/usr/bin`. Within this category, programs can be *compiled binaries*, such as programs written in C and C++, or programs written in *scripting languages*, such as the shell, Perl, Python, Ruby, and so on.
- **A command built into the shell itself.** bash supports a number of commands internally called *shell builtins*. The cd command, for example, is a shell builtin.
- **A shell function.** *Shell functions* are miniature shell scripts incorporated into the *environment*. We will cover configuring the environment and writing shell functions in later chapters, but for now just be aware that they exist.
- **An alias.** An *alias* is a command that we can define ourselves, built from other commands.

## Identifying Commands

It is often useful to know exactly which of the four kinds of commands is being used, and Linux provides a couple of ways to find out.

## type—Display a Command's Type

The type command is a shell builtin that displays the kind of command the shell will execute, given a particular command name. It works like this:

```
type command
```

where *command* is the name of the command you want to examine. Here are some examples:

```
[me@linuxbox ~]$ type type
type is a shell builtin
[me@linuxbox ~]$ type ls
ls is aliased to 'ls --color=tty'
[me@linuxbox ~]$ type cp
cp is /bin/cp
```

Here we see the results for three different commands. Notice that the ls command (taken from a Fedora system) is actually an alias for the ls command with the --color=tty option added. Now we know why the output from ls is displayed in color!

## which—Display an Executable's Location

Sometimes more than one version of an executable program is installed on a system. While this is not very common on desktop systems, it's not unusual on large servers. To determine the exact location of a given executable, the which command is used:

```
[me@linuxbox ~]$ which ls
/bin/ls
```

which works only for executable programs, not builtins or aliases that are substitutes for actual executable programs. When we try to use which on a shell builtin (for example, cd), we get either no response or an error message:

```
[me@linuxbox ~]$ which cd
/usr/bin/which: no cd in (/opt/jre1.6.0_03/bin:/usr/lib/qt-3.3/bin:/usr/kerberos/bin:/opt/jre1.6.0_03/bin:/usr/lib/ccache:/usr/local/bin:/usr/bin:/bin:/home/me/bin)
```

This is a fancy way of saying "command not found."

## Getting a Command's Documentation

With this knowledge of what a command is, we can now search for the documentation available for each kind of command.

## help—Get Help for Shell Builtins

bash has a built-in help facility for each of the shell builtins. To use it, type help followed by the name of the shell builtin. For example:

```
[me@linuxbox ~]$ help cd
cd [-L|-P] [dir]
Change the current directory to DIR. The variable $HOME is the default DIR.
The variable CDPATH defines the search path for the directory containing DIR.
Alternative directory names in CDPATH are separated by a colon (:). A null directory name is the same as the current directory, i.e. "..". If DIR begins with a slash (/), then CDPATH is not used. If the directory is not found, and the shell option "cdable_vars" is set, then try the word as a variable name. If that variable has a value, then cd to the value of that variable. The -P option says to use the physical directory structure instead of following symbolic links; the -L option forces symbolic links to be followed.
```

A note on notation: When square brackets appear in the description of a command's syntax, they indicate optional items. A vertical bar character indicates mutually exclusive items. An example is the cd command above: cd [-L|-P] [dir].

This notation says that the command cd may be followed optionally by either a -L or a -P and further, optionally followed by the argument dir.

While the output of help for the cd command is concise and accurate, it is by no means a tutorial, and as we can see, it also seems to mention a lot of things we haven’t talked about yet! Don’t worry. We’ll get there.

## --help—Display Usage Information

Many executable programs support a --help option that displays a description of the command’s supported syntax and options. For example:

```
[me@linuxbox ~]$ mkdir --help
Usage: mkdir [OPTION] DIRECTORY...
Create the DIRECTORY(ies), if they do not already exist.

    -Z, --context=CONTEXT (SELinux) set security context to CONTEXT
Mandatory arguments to long options are mandatory for short options too.
    -m, --mode=MODE      set file mode (as in chmod), not a=rwx - umask
    -p, --parents        no error if existing, make parent directories as needed

    -v, --verbose        print a message for each created directory
        --help           display this help and exit
        --version        output version information and exit
Report bugs to <bug-coreutils@gnu.org>.
```

Some programs don’t support the --help option, but try it anyway. Often it results in an error message that will reveal the same usage information.

## man—Display a Program’s Manual Page

Most executable programs intended for command-line use provide a formal piece of documentation called a manual or man page. A special paging program called man is used to view them, like this:

```
man program
```

where program is the name of the command to view.

Man pages vary somewhat in format but generally contain a title, a synopsis of the command’s syntax, a description of the command’s purpose, and a listing and description of each of the command’s options. Man pages, however, do not usually include examples, and they are intended as a reference, not a tutorial. As an example, let’s viewing the man page for the ls command:

```
[me@linuxbox ~]$ man ls
```

On most Linux systems, man uses less to display the manual page, so all of the familiar less commands work while displaying the page.

The "manual" that man displays is broken into sections and covers not only user commands but also system administration commands, programming interfaces, file formats, and more. Table 5-1 describes the layout of the manual.
