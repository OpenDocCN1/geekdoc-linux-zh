
# history, fc

## 497

```
s/oldchars/replacements/
```Substitute replacements for oldchars. oldchars is a string that may contain embedded blank spaces, whereas previous-word in the event designator ^oldchars`replacements` may not.

t
Remove all leading path-name components, leaving the tail.

&
Repeat the previous substitution.

g
Apply the change to the first occurrence of a match in each word by prefixing the modifiers (for example, g&).

p
Print the new command, but do not execute it.

q
Quote the substituted words, escaping further substitutions.

x
Like q, but break into words at each shell character, Tab, or newline.

Unless preceded by a g, the modification is only applied to the first string that matches oldchars, an error results if no string matches.

The left-hand side of substitutions are character strings, not regular expressions. You can use any character as the delimiter in place of /. A backslash escapes the delimiter character & in the right-hand side is replaced by the text from the left-hand side. You can escape the & with a backslash. A null oldchars uses the previous string from oldchars or from a contextual string $. You can omit the rightmost delimiter if a newline immediately follows replacements; similarly, you can omit the rightmost ? in a context.

Without an event specification, a history reference refers to the previous or to previous history reference on the command line (if any).

## Kern Shell

When you use fc -e - [old-new] [command], the command is reexecuted after the substitution old-new performed. If you specify no command argument, the most recent command typed at this terminal is executed.

When you use fc [-e editor] [-nrl] [first [last]], a range of commands from first to last is selected from the last HISTSIZE commands that were typed at the terminal. A string is used to specify the arguments first and last as a number or a string. A negative number is used as an offset to the current command number. If you use -1 flag, the commands are listed on standard output. Otherwise, the -e editor is invoked on a file containing these keyboard commands. If you do not specify editor; then the value of the variable EDIT (default /bin/ed) is used as the editor. When editing is complete, the command (s) is executed. If you do not specify last, the value is set to first. If you do not specify first, the default is the previous command for editing and the -n option reverses the order of the commands, and the -s suppresses commands when listed. (See k1 for more information about command-editing.)

## HISTFILE
If this variable is set when the shell is invoked, the value is the path name of the file that is used to store the command history.

## HISTSIZE
If this variable is set when the shell is invoked, the number of previously entered commands that are accessible by this shell is greater than equal to this number. The default is 128.

## 498 Command Reentry

The text of the last HISTSIZE(default 128) commands entered from the terminal device is saved in a history file. The file $HOME/.sh_history is used if the HISTFILE variable is not set or if the file name is not writable. A shell can access the commands of all interactive shells that use the same HISTFILE. to list or edit portion of this file. Use fc or by giving the first character or characters of the command. You can select the portion of the file to be edited or listed. You can specify a specific command or a range of commands. If you do not specify an editor as an argument to fc, then the value of FCEDIT is used. If FCEDIT is not defined, then /bin/ed is used. The command(s) is printed and reexecuted on leaving the editor. The editor name - is used to skip the editing phase and of the form old-new to modify the command before execution. For example, if r is aliased to fc -r bad-good it reexec the most recent command that starts with the letter c, replacing the first occurrence of the string bad with the string good.

Using the fc built-in command within a compound command removes the command from the history file.

## Options

- -e editor Use the editor named by editor to edit the commands. The editor string is a command name, subject to searching the PATH variable. The value in the FCEDIT variable is used as a default when you do not specify -e. If FCEDIT is not unset, ed is used as the editor.
- -h Display the history list without leading numbers. Use this option to produce files suitable for sourcing with the -h option to the csh built-in source(1) command.
- -1 List the commands instead of invoking an editor on them. Write the commands in the sequence indicated by the first and last operands, as affected by -r, with each command preceded by the command number. Suppress command numbers when listing with -1.
- -r Reverse the order of the commands listed (with -1) or edited.
- -s Reexecute the command without invoking an editor.

## Operands

- first last Choose the commands to list or edit. The number of previous commands that can be accessed is determined by the value of the HISTSIZE variable. The value of first or last is both one of the following:
- +[number] A positive number representing a command number; you can display command numbers with the -l option.
- -number A negative decimal number representing the command that was executed number of commands previously. For example, -1 is the previous command.
- string A string indicating the most recently entered command that begins with string. If you do not also specify the old=new operand with -s, the string form of the first operand cannot contain an embedded equal sign.
- old=new Replace the first occurrence of string old in the command to be reexecuted by the new string.

When you use the synopsis form with -s:

- * If you omit first, use the previous command. For the synopsis, forms without -s.
- * If you omit last, last defaults to the previous command when -l is specified; otherwise, it defaults to first.
- * If you omit both first and last, list the previous 16 commands or edit the previous command (based on the -1 option).
- * If you specify both first and last, edit or list all of the commands from first to last. When editing multiple commands, the editor presents all of the commands at one time, each command starting on a new line. If first represents a new command after last, the commands are listed or edited in reverse sequence, equivalent to using -r. For example, the following commands on the first line are equivalent to the corresponding commands on the second:

```
fc -r 10 20
fc
30 40
fc 20 10
fc -r
40 30
```

When you use a range of commands, you can specify first or last values that are in the history list; fc substitutes the value representing the oldest or newest command in the list, appropriate. For example, if the history list has 10 commands, numbered 1 to 10, the following command edits all 10 commands.

```
fc -1
fc 1 99
```

## Output

When you use the -1 option to list commands, the format of each command in the list is as follows:

```
line-number command
```

If you specify both the -1 and -n options, the format of each command is:

```
"\t%s\n\", command
```

If the command consists of more than one line, the lines after the first are displayed as:

```
"\t%s\n\", continued-command
```

## Examples

### C Shell

The following C shell examples show various ways to use the history event designators.

```
castle% history
1 cd /etc
2 vi passwd
3 date
4 cd
5 du
6 ls -t
7 history
castle% !da
date
Mon Jan 18 17:53:28 WST 1999
castle% !!
date
Mon Jan 18 17:53:34 WST 1999
castle% !5
du
262 ./SCCS
336
castle% !ls ma*
ls -t malloc.c
malloc.o
malloc.c
```

### Korn Shell

The following example shows the various ways to use the fc event designators.

```
$ fc -l
1 cd /etc
2 vi passwd
3 date
4 cd
5 du
6 ls -t
7 $ fc -e - d
du
262 ./SCCS
336
$ fc -e - da
date
Mon Jan 18 17:59:52 WST 1999
$ !!
ksh:!: not found
$ alias !=-fc -e -
$ !
alias='fc -e -'
$ !5: not found
du .
```
