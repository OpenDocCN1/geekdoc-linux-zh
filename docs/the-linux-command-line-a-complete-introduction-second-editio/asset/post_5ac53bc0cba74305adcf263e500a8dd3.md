
> The file managers in both GNOME and KDE provide an easy and automatic method of creating symbolic links. With GNOME, holding the CTRL-SHIFT keys while dragging a file will create a link rather than copying (or moving) the file. In KDE, a small menu appears whenever a file is dropped, offering a choice of copying, moving, or linking the file.

## Summing Up

We’ve covered a lot of ground here, and it will take a while for it all to fully sink in. Perform the playground exercise over and over until it makes sense. It is important to get a good understanding of basic file manipulation commands and wildcards. Feel free to expand on the playground exercise by adding more files and directories, using wildcards to specify files for various operations. The concept of links is a little confusing at first, but take the time to learn how they work. They can be a real lifesaver!

## 5 WORKING WITH COMMANDS

![](img/314a0280bc10c5c0d45be132de172677_82_0.png)

Up to this point, we have seen a series of mysterious commands, each with its own options and arguments. In this chapter, we will attempt to remove some of that mystery and even create our own commands. The commands introduced in this chapter are as follows:

- `type` — Indicate how a command name is interpreted
- `which` — Display which executable program will be executed
- `help` — Get help for shell builtins
- `man` — Display a command's manual page
- `apropos` — Display a list of appropriate commands
- `info` — Display a command's info entry
- `whatis` — Display one-line manual page descriptions
- `alias` — Create an alias for a command

## What Exactly Are Commands?

A command can be one of four different things.

- An executable program like all those files we saw in `/usr/bin`. Within this category, programs can be compiled binaries such as programs written in C and C++, or programs written in *scripting languages* such as the shell, Perl, Python, Ruby, and so on.
- **A command built into the shell itself.** bash supports a number of commands internally called *shell builtins*. The `cd` command, for example, is a shell builtin.
- **A shell function.** Shell functions are miniature shell scripts incorporated into the *environment*. We will cover configuring the environment and writing shell functions in later chapters, but for now, just be aware that they exist.
- **An alias.** Aliases are commands that we can define ourselves, built from other commands.

## Identifying Commands

It is often useful to know exactly which of the four kinds of commands is being used, and Linux provides a couple of ways to find out.

### type—Display a Command’s Type

The `type` command is a shell builtin that displays the kind of command the shell will execute, given a particular command name. It works like this:

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

Here we see the results for three different commands. Notice the one for `ls` (taken from a Fedora system) and how the `ls` command is actually an alias for the `ls` command with the `--color=tty` option added. Now we know why the output from `ls` is displayed in color!

### which—Display an Executable’s Location

Sometimes there is more than one version of an executable program installed on a system. While this is not common on desktop systems, it’s not unusual on larger servers. To determine the exact location of a given executable, the `which` command is used.

```
[me@linuxbox ~]$ which ls
/bin/ls
```

`which` works only for executable programs, not builtins or aliases that are substitutes for actual executable programs. When we try to use `which` on a shell builtin—for example, `cd`—we either get no response or get an error message.

```
[me@linuxbox ~]$ which cd
/usr/bin/which: no cd in (/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games)
```

This result is a fancy way of saying “command not found.”

## Getting a Command’s Documentation

With this knowledge of what a command is, we can now search for the documentation available for each kind of command.

### help—Get Help for Shell Builtins

bash has a built-in help facility available for each of the shell builtins. To use it, type `help` followed by the name of the shell builtin. Here’s an example:

```
[me@linuxbox ~]$ help cd
cd: cd [-L][-P [-e]] [-@] [dir]
Change the shell working directory.
```
