
When `Ctrl+r` is typed, the shell replaces the current line with the prompt `^R`:

```
$ _                         Ctrl+r test       $ ^Rtest_
```

The search is initiated when Enter is pressed.

```
$ ^Rtest_                   Enter             $ echo this is a test_
```

To execute the command that is displayed as a result of the search, Enter must be pressed again.

```
$ echo this is a test_       Hit Enter again
this is a test
$ _
```

To continue the search through the command history, keep typing `Ctrl+r` followed by an Enter.

Bash handles `Ctrl+r` a little differently. When you type `Ctrl+r`, Bash replaces the current line with ``(reverse-i-search)`':``

```
$ _                         Ctrl+r             (reverse-i-search)`': _
```

As you type text, the line is updated inside the `_` with the text you typed, and the rest of the line is updated with the matching command:

```
(reverse-i-search)`': _                         c       (reverse-i-search)`c': echo this is a test
(reverse-i-search)`c': echo this is a test   d       (reverse-i-search)`cd': cd /tmp
```

Note how Bash highlights the matching part of the command by placing the cursor on it. As with the Korn shell, the command is executed by pressing Enter.

When you’ve found the command in the history (either by `Ctrl+p`, `Ctrl+n`, or `Ctrl+r`), you can also edit the command using the other emacs commands already discussed. As with the vi edit mode, you won’t actually change the command in the history but are editing a copy of the command, which will then be entered in the history list when you press Enter.

Table 14.2 summarizes the basic emacs line edit commands.

## Table 14.2 Basic emacs Line Edit Commands

| Command | Meaning |
|---|---|
| `Ctrl+b` | Move left one character. |
| `Ctrl+f` | Move right one character. |
| `Esc f` | Move forward one word. |
| `Esc b` | Move back one word. |
| `Ctrl+a` | Move to start of line. |
| `Ctrl+e` | Move to end of line. |
| `Ctrl+d` | Delete current character. |
| `Esc d` | Delete current word. |
| `erase char` | (User-defined erase character, usually # or Ctrl+h), delete previous character. |
| `Ctrl+p` | Get previous command from history. |
| `Ctrl+n` | Get next command from history. |
| `Ctrl+r string` | Search history for the most recent command line containing `string`. |

## Other Ways to Access Your History

There are several other ways to access your command history that are worth noting if you don’t find that either the vi or emacs line edit modes work for you.

### The `history` Command

The easiest way to access your command history is actually to just type in the command `history`:

```shell
$ history
507   cd shell
508   cd ch15
509   vi int
510   ps
511   echo $HISTSIZE
512   cat $ENV
513   cp int int.sv
514   history
515   exit
516   cd shell
517   cd ch16
518   vi all
519   run -n5 all
520   ps
521   lpr all.out
522   history
```

The numbers to the left are relative command numbers (command number 1 would be the first, or oldest, command in your history).

Be aware that the history command differs between the Korn and Bash shells: The Korn shell history command writes your last 16 commands to standard output while Bash will list your entire command history, even if it’s 500 or 1000 lines long.

If you’re running Bash and don’t want to be inundated with commands, you can specify the number of commands to display as an argument:

```shell
$ history 10
  513   cp int int.sv
  514   history
  515   exit
  516   cd shell
  517   cd ch16
  518   vi all
  519   run -n5 all
  520   ps
  521   lpr all.out
  522   history 10
$
```

### The `fc` Command

The `fc` command allows you to start up an editor on one or more commands from your history or to write a list of history commands to your terminal. In the latter form, which is indicated by giving the `-l` option to `fc`, it is like typing in `history`, only more flexible (you can specify a range of commands to be listed). For example, the command

```shell
fc -l 510 515
```

writes commands 510 through 515 to standard output, and the command

```shell
fc -n -l -20
```

writes the last 20 commands to standard output, but omits the command numbers (`-n`). Suppose that you’ve just executed a long command and decide that it would be nice to turn that command line into a shell program called runx. You can use `fc` to get the command from your history and I/O redirection to write that command to a file:

```shell
fc -n -l -1 > runx
```

That’s the letter l followed by the number -1 to get the most recent command (current minus one). `fc` is described in full detail in Appendix A.

### The `r` Command

A simple Korn shell command allows you to re-execute previous commands using even fewer keystrokes. Type in the `r` command, and the Korn shell re-executes your last command:

```shell
$ date
Thu Oct 24 14:24:48 EST 2002
$ r
date
Thu Oct 24 14:25:13 EST 2002
$
```

*Re-execute previous command*

When you type the `r` command, the Korn shell redisplays the previous command and then immediately executes it.

If you give `r` the name of a command as an argument, the Korn shell re-executes the most recent command from your history that begins with the specified pattern:

```shell
$ cat docs/planA
...
$ pwd
/users/steve
$ r cat                 Rerun last cat command
cat docs/planA
$
```

Once again, the Korn shell redisplays the command line from its history before automatically re-executing it.

The final form of the `r` command allows you to substitute the first occurrence of one string with the next. To re-execute the last `cat` command on the file `planB` instead of `planA` you could type:

```shell
$ r cat planA=planB
cat docs/planB
...
$
```

or even more simply, you could have typed:

```shell
$ r cat A=B
cat docs/planB
...
$
```

Bash has a similar history shortcut command. `!string` lets you search your history and `!!` re-executes the previous command:

```shell
$ !!
cat docs/planB
...
$ !d
date
Thu Oct 24 14:39:40 EST 2002
$
```

No spaces can occur between `!` and `string`.

The `fc` command can be used with the `-s` option to do the same thing with any POSIX-compliant shell (the `r` command is actually an alias to the `fc` command in the Korn shell—more on that later in this chapter):

```shell
$ fc -s cat
cat docs/planB
...
$ fc -s B=C
cat docs/planC
...
$
```

## Functions

Bash and the Korn shell both have function features not available in the POSIX standard shell. Let's have a look.

### Local Variables

Both Bash and Korn shell functions can have local variables, making recursive functions possible. These variables are defined with the `typeset` command, as in `typeset i j`.

If a variable of the same name already exists, it is saved when the `typeset` is executed and restored when the function exits.

After using the shell for a while, you may develop a set of functions that you like to use during your interactive work sessions. A good place to define such functions is inside your `ENV` file so that they will be defined whenever you start up a new shell.

### Automatically Loaded Functions

The Korn shell allows you to set up a special variable called `FPATH` that is similar to your `PATH` variable. If you try to execute a function that is not yet defined, the Korn shell searches the colon-delimited list of directories in `FPATH` for a file that matches the function name. If it finds such a file, it executes it in the current shell with the expectation that somewhere in the file is a definition for the specified function.

## Integer Arithmetic

Both Bash and the Korn shell support evaluating arithmetic expressions without arithmetic expansion. The syntax is similar to `$((...))` but without the dollar sign. Because expansion is not performed, the construct can therefore be used by itself as a command:

```shell
$ x=10
$ ((x = x * 12))
$ echo $x
120
$
```
