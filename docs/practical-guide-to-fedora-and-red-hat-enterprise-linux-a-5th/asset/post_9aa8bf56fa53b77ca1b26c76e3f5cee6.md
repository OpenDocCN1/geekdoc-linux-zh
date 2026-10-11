
In the `films` directory every file that starts with `dar` has `k_` as the next characters, so `bash` cannot extend the line further without making a choice among files. You are left with the cursor just past the `_` character. At this point you can continue typing the pathname or press `TAB` twice. In the latter case `bash` beeps, displays your choices, redisplay the command line, and again leaves the cursor just after the `_` character.

```
$ cat films/dar<TAB> (beep) cat films/dark_
```

When you add enough information to distinguish between the two possible files and press `TAB`, `bash` displays the unique pathname. If you enter `p` followed by `TAB` after the `_` character, the shell completes the command line:

```
$ cat films/dark_p<TAB> passage
```

Because there is no further ambiguity, the shell appends a `SPACE` so you can finish typing the command line or just press `RETURN` to execute the command. If the complete pathname is that of a directory, `bash` appends a slash (`/`) in place of a `SPACE`.

## VARIABLE COMPLETION

When typing a variable name, pressing `TAB` results in *variable completion*, where `bash` tries to complete the name of the variable. In case of an ambiguity, pressing `TAB` twice displays a list of choices:

```
$ echo $HO<TAB>
HOME    HOSTNAME    SHOSTTYPE
$ echo $HOM<TAB>E
```

### Pressing RETURN executes the command

Pressing `RETURN` causes the shell to execute the command regardless of where the cursor is on the command line.

### .inputrc: CONFIGURING READLINE

The Bourne Again Shell and other programs that use the Readline Library read the file specified by the `INPUTRC` environment variable to obtain initialization information. If `INPUTRC` is not set, these programs read the `~/.inputrc` file. They ignore lines of `.inputrc` that are blank or that start with a pound sign (`#`).

## VARIABLES

You can set variables in `.inputrc` to control the behavior of the Readline Library using the following syntax:

```
set variable value
```

Table 9-11 (next page) lists some variables and values you can use. See *Readline Variables* in the `bash` man or info page for a complete list.

| Variable | Effect |
| --- | --- |
| editing-mode | Set to vi to start Readline in vi mode. Set to emacs to start Readline in emacs mode (the default). Similar to the set -o vi and set -o emacs shell commands (page 326). |
| horizontal-scroll-mode | Set to on to cause long lines to extend off the right edge of the display area. Moving the cursor to the right when it is at the right edge of the display area shifts the line to the left so you can see more of the line. You can shift the line back by moving the cursor back past the left edge. The default value is off, which causes long lines to wrap onto multiple lines of the display. |
| mark-directories | Set to off to cause Readline not to place a slash (/) at the end of directory names it completes. Normally it is on. |
| mark-modified-lines | Set to on to cause Readline to precede modified history lines with an asterisk. The default value is off. |

## KEY BINDINGS

You can specify bindings that map keystroke sequences to Readline commands, allowing you to change or extend the default bindings. As in **emacs**, the Readline Library includes many commands that are not bound to a keystroke sequence. To use an unbound command, you must map it using one of the following forms:

```
keyname: command_name
"keystroke_sequence": command_name
```

In the first form, you spell out the name for a single key. For example, **CONTROL-u** would be written as **control-u**. This form is useful for binding commands to single keys.

In the second form, you specify a string that describes a sequence of keys that will be bound to the command. You can use the **emacs**-style backslash escape sequences to represent the special keys **CONTROL (\C)**, **META (\M)**, and **ESCAPE (\e)**. Specify a backslash by escaping it with another backslash: `\\`. Similarly, a double or single quotation mark can be escaped with a backslash: `"` or `'`.

The **kill-whole-line** command, available in **emacs** mode only, deletes the current line. Put the following command in **.inputrc** to bind the **kill-whole-line** command (which is unbound by default) to the keystroke sequence **CONTROL-r**.

```
control-r: kill-whole-line
```

Give the command **bind -P** to display a list of all Readline commands. If a command is bound to a key sequence, that sequence is shown. Commands that can use in vi mode start with vi. For example, **vi-next-word** and **vi-prev-word** move the cursor to the beginning of the next and previous words, respectively. Commands that do not begin with vi are generally available in **emacs** mode.

Use **bind -q** to determine which key sequence is bound to a command:

```
$ bind -q kill-whole-line
kill-whole-line can be invoked via "^C-r".
```

You can also bind text by enclosing it within double quotation marks (*emacs* mode only):

```
"QQ": "The Linux Operating System"
```

This command causes *bash* to insert the string **The Linux Operating System** when you type **QQ**.

## CONDITIONAL CONSTRUCTS

You can conditionally select parts of the *inputrc* file using the $if directive. The syntax of the conditional construct is

```
$if test[=value]
    commands
[$else
    commands]
$endif
```

where *test* is *mode*, *term*, or *bash*. If *test* equals *value* or if *test* is *true*, this structure executes the first set of *commands*. If *test* does not equal *value* or if *test* is *false*, it executes the second set of *commands* if they are present or exits from the structure if they are not present.

The power of the $if directive lies in the three types of tests it can perform.

1. You can test to see which mode is currently set.

   ```
   $if mode=vi
   ```

   The preceding test is *true* if the current *Readline* mode is *vi* and *false* otherwise. You can test for *vi* or *emacs*.

2. You can test the type of terminal.

   ```
   $if term=xterm
   ```

   The preceding test is *true* if the *TERM* variable is set to *xterm*. You can test for any value of *TERM*.

3. You can test the application name.

   ```
   $if bash
   ```

   The preceding test is *true* when you are running *bash* and not another program that uses the *Readline* Library. You can test for any application name.

These tests can customize the *Readline* Library based on the current mode, the type of terminal, and the application you are using. They give you a great deal of power and flexibility when using the *Readline* Library with *bash* and other programs.

The following commands in **.inputrc** cause CONTROL-y to move the cursor to the beginning of the next word regardless of whether bash is in vi or emacs mode:

```
$ cat ~/.inputrc
  set editing-mode vi
  if mode=vi
    "\C-y": vi-next-word
  else
    "\C-y": forward-word
  endif
```

Because *bash* reads the preceding conditional construct when it is started, you must set the editing mode in **.inputrc**. Changing modes interactively using *set* will not change the binding of CONTROL-y.

For more information on the Readline Library, open the *bash* man page and give the command */^READLINE*, which searches for the word READLINE at the beginning of a line.

### If Readline commands do not work, log out and log in again

The Bourne Again Shell reads ~/.inputrc when you log in. After you make changes to this file, you should log out and log in again before testing the changes.

## ALIASES

An *alias* is a (usually short) name that the shell translates into another (usually longer) name or (complex) command. Aliases allow you to define new commands by substituting a string for the first token of a simple command. They are typically placed in the ~/.bashrc startup files so that they are available to interactive subshells.

The syntax of the *alias* builtin is

```
alias [name=value]
```

No SPACES are permitted around the equal sign. If *value* contains SPACES or TABS, you must enclose *value* between quotation marks. An alias does not accept an argument from the *command line* in *value*. Use a function (page 335) when you need to use an argument.

An alias does not replace itself, which avoids the possibility of infinite recursion in handling an alias such as the following:

```
$ alias ls='ls -F'
```

You can nest aliases. Aliases are disabled for noninteractive shells (that is, shell scripts). To see a list of the current aliases, give the command *alias*. To view the alias for a particular name, use *alias* followed by the name and nothing else. You can use the *unalias* builtin to remove an alias.
