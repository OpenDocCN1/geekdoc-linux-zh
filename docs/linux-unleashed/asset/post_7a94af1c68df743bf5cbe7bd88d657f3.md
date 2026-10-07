
## Online Help Available in Linux

Linux has help facilities available online. If you forget the exact use of a command, which option means what, or if you’re looking for the right command to use, the answer might be available straight from Linux. The two help facilities we will try out are the `bash` shell’s `help` command and the `man` command, which is available on almost all UNIX systems, including Linux.

### The Linux Man Pages

The "man" in "man pages" stands for "manual." (As usual, the creators of UNIX shortened a long but descriptive word to a shorter, cryptic one!) Typing `man <command>` lets you view the manual pages dealing with a particular command.

Try typing `man passwd` to see what the Linux manual has to say about the `passwd` command.

The general layout of a man page is as follows:

```
COMMAND(1)                Linux Programmer's Manual           COMMAND(1)

NAME
        command - summary of what command does

SYNOPSIS
        <complete syntax of command in the standard Linux form>

DESCRIPTION
        More verbose explanation of what "command" does.

OPTIONS
        Lists each available option with description of what it does

FILES
        lists files used by, or related to, command

SEE ALSO
        command_cousin(1), command_spouse(1), etc.

BUGS
        There are bugs in Linux commands??

AUTHOR
        J. S. Goobly (goobly@hurrdly-gurdly.boondocks)

Linux 1.0         22 June 1994                   1
```

The man page for `passwd` is actually quite understandable. Be warned, however, that man pages are often written in a very formal and stylized way that sometimes bears little resemblance to English. This is done not to baffle people, but to cram a great deal of information into as short a description as possible. For example, try entering `man ls`. Notice how many options are available for `ls` and how long it takes to explain them.

Although it can take practice (and careful reading!) to understand man pages, once you get used to them the first thing you’ll do when you encounter an unfamiliar command is call up the man page for that command.

### Finding Keywords in Man Pages

Sometimes you know what you want to do, but you don’t know which command you should use to do it. Use the keyword option by typing `man -k <keyword>`, and the `man` program returns the name of every command whose `name` entry (which includes a very brief description) contains that keyword.

For instance, you can search on `manual`:

```
darkstar:~$ man -k manual
darkstar:~$ man 5 passwd
```

You have to be careful to specify your keyword properly, though! Using `directory` as your keyword isn’t too bad, for example, but using `file` gives you many more entries than you will want to wade through.

> **NOTE**
> You may have noticed that commands seem to be followed by numbers in brackets, usually `(1)`. This refers to the manual section. Back in the days when UNIX manuals came in printed, bound volumes, normal commands were in Section 1, files used by administrators were in Section 5, programming routines were described in Section 3, and so on. Therefore, some man pages are not about commands at all, but rather about files or system calls used in Linux! If a particular entry shows up in more than one section, `man` will show you the lowest-numbered entry by default. You can see higher-numbered entries by specifying the section number. For instance, Section 5 has a manual entry on the `passwd` file. To see this rather than the manual entry for the `passwd` command, type `man 5 passwd`.

In general, `man <n> <entry>` will find the man page for `<entry>` in Section `<n>`.

### The bash Shell help Facility

When you type a command at the prompt, the shell program takes what you’ve written, interprets it as necessary, and passes the result to the Linux operating system. Linux then performs the actions requested of it. Many Linux commands require Linux to find and start up a new program. However, the shell itself can perform a number of functions.

These functions can be simple, often-used commands, so that the overhead of starting up separate programs is eliminated or they can be facilities that make the shell environment friendlier and more useful. One of these facilities is the **help** command, which provides information on the built-in functions of the **bash** shell.

Type **help** at the prompt. You will see at least some of the following:

```
GNU bash, version 1.14.15(1)
Shell commands that are defined internally. Type 'help' to see this list.
Type 'help name' to find out more about the function 'name'.
Use 'info bash' to find out more about the shell in general.
```

A star (*) next to a name means that the command is disabled.

```
%[DIGITS | WORD] [&] . [filename] : [arg...] alias [ name[=value] ... ] bg [job_spec] bind [-lvd] [-m keymap] [-r filena break [N] builtin [Shell-builtin [arg ...]] case WORD in [PATTERN [; PATTERN]. cd [dir] command [-pvV] [command [arg ...]] continue [n] declare [-frx] name[=value] ... dirs [-1] echo [-nE] [arg ...] enable [-n] [name ...] eval [arg ...] exec [-] file [redirection ...] exit [n] export [-n] [-f] [name ...] or exp fc [-e name] [-nlr] [first] [last fg [job_spec] for NAME [in WORDS ... ;] do COMMA function NAME { COMMANDS ; } or NA getopt optstring name [arg] hash [-r] [name ...] help [pattern ...] history [n] [ -awrn] [filename] if COMMANDS; then COMMANDS; [elif jobs [-lnp] [jobspec ...] | jobs - kill [-S sigspec | -sigspec] [pid let [arg ...] local name[=value] ... logout popd [+n ! -n] pushd [dir | +n ! -n] pwd read [-r] [name ...] readonly [-n] [-f] [name ...] or r return [n] select NAME [in WORDS ... ;] do CO set [--abefhknoutvXhDCP] [-o opti shift [n] source filename suspend [-f] test [expr] times trap [arg] [signal_spec] type [-all] [-type ! -path] [name typeset [-frxij] name[=value] ... ulimit [-SHacdmtfnpuv [limit]] umask [-S] [mode] unalias [-a] [name ...] unset [-f] [-v] [name ...] until COMMANDS; do COMMANDS; done variables - Some variable names an wait [N] while COMMANDS; do COMMANDS; done { COMMANDS }
```

You will have to pipe the output of **help** to **more** (**help** ! **more**) to keep the first part from scrolling off your screen.

### Wildcards: * and ?

In many a late-night card game, jokers are shuffled into the deck. The jokers are *wild-cards* that can become any card of your choice. This is obviously very useful! Linux also has wildeards. They are more useful than jokers in a card game.

Linux has several wildcards. Wildcards are used as a convenient and powerful shortcut when specifying files (or directories) that a command is to operate on. We will briefly look at the two most popular wildcards: * and ?. (There are quite a few more wildcards supported by Linux, but they are seldom used and would only complicate the issue at this point.)

The most commonly used wildcard is *, which stands in for any combination of one or more characters. For example, `c*` matches all filenames that begin with c. You can see this for yourself by typing `ls /bin/c*`. What happens if you type `ls /bin/c**t` at the command line? How about `ls /bin/*t` at the command line?

The ? wildcard is more restrictive than *. It stands in only for any *one* character. You can see this by comparing `ls/bin/d*` with `ls/bin/d?`.

> NOTE
> Wildcards can only be used to match filenames and directory names. You can't, for example, type `pass*` at the Linux prompt and expect Linux to run the `passwd` program for you.

> WARNING
> Be very careful when using wildcards with dangerous commands, such as the ones used to permanently delete files! A good check is to run `ls` with the wild-cards you plan to use and examine the resulting list of files to see whether the wildcard combination did what you expected it to do. Also double-check that you typed everything correctly *before* pressing the Enter key!

## Environment Variables

When you log in, Linux keeps a number of useful data items in the background ready for the system to use. The actual data is held in something called an *environment variable*, whose name is often descriptive or mnemonic. In fact, this is no different from the way
