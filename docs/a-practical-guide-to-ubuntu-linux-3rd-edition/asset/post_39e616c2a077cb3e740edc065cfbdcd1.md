
## EDITING AND REEXECUTING PREVIOUS COMMANDS

You can use **fc** to edit and reexecute previous commands.

`fc [-e editor] [first [last]]`

When you call **fc** with the `-e` option followed by the name of an editor, **fc** calls the editor with event(s) in the Work buffer, assuming the editor you specify is installed. By default, **fc** invokes the **nano** editor. Without *first* and *last*, it defaults to the most recent command. The next example invokes the **vim** editor to edit the most recent command:

```
$ fc -e vi
```

The **fc** builtin uses the stand-alone **vim** editor. If you set the **FCEDIT** variable, you do not need to use the `-e` option to specify an editor on the command line. Because the value of **FCEDIT** has been changed to `/usr/bin/emacs` and **fc** has no arguments, the following command edits the most recent command using the **emacs** editor (part of the **emacs** package; not installed by default):

```
$ export FCEDIT=/usr/bin/emacs
$ fc
```

If you call it with a single argument, **fc** invokes the editor on the specified command. The following example starts the editor with event 1029 in the Work buffer. When you exit from the editor, the shell executes the command:

```
$ fc 1029
```

As described earlier, you can identify commands with numbers or by specifying the first few characters of the command name. The following example calls the editor to work on events from the most recent event that begins with the letters **vim** through event 1030:

```
$ fc vim 1030
```

### Clean up the **fc** buffer

*caution* When you execute an **fc** command, the shell executes whatever you leave in the editor buffer, possibly with unwanted results. If you decide you do not want to execute a command, delete everything from the buffer before you exit from the editor.

## REEXECUTING COMMANDS WITHOUT CALLING THE EDITOR

You can reexecute previous commands without using an editor. If you call **fc** with the `-s` option, it skips the editing phase and reexecutes the command. The following example reexecutes event 1029:

```
$ fc -s 1029
lpr letter.adams01
```

The next example reexecutes the previous command:

```
$ fc -s
```

When you reexecute a command, you can tell fc to substitute one string for another. The next example substitutes the string `john` for the string `adams` in event 1029 and executes the modified event:

```
$ fc -s adams=john 1029
lpr letter.john01
```

## USING AN EXCLAMATION POINT (!) TO REFERENCE EVENTS

The C Shell history mechanism uses an exclamation point to reference events. This technique, which is available under `bash`, is frequently more cumbersome to use than `fc` but nevertheless has some useful features. For example, the `!!` command reexecutes the previous event, and the shell replaces the `!$` token with the last word on the previous command line.

You can reference an event by using its absolute event number, its relative event number, or the text it contains. All references to events, called event designators, begin with an exclamation point (!). One or more characters follow the exclamation point to specify an event.

You can put history events anywhere on a command line. To escape an exclamation point so that the shell interprets it literally instead of as the start of a history event, precede the exclamation point with a backslash (\) or enclose it within single quotation marks.

## EVENT DESIGNATORS

An event designator specifies a command in the history list. See Table 9-8 below for a list of event designators.

You can reexecute the previous event by giving a `!!` command. In the following example, event 45 reexecutes event 44:

```
44 $ ls -l text
-rw-rw-r--    1 max group  45 2010-04-30 14:53 text
45 $ !!
ls -l text
-rw-rw-r--    1 max group  45 2010-04-30 14:53 text
```

The `!!` command works whether or not your prompt displays an event number. As this example shows, when you use the history mechanism to reexecute an event, the shell displays the command it is reexecuting.

A number following an exclamation point refers to an event. If that event is in the history list, the shell executes it. Otherwise, the shell displays an error message. A negative number following an exclamation point references an event relative to the current event. For example, the command `!-3` refers to the third preceding event. After you issue a command, the relative event number of a given event changes (event `–3` becomes event `–4`). Both of the following commands reexecute event 44:

```
51 $ !44
ls -l text
-rw-rw-r--    1 max group  45 2010-04-30 14:53 text
52 $ !-8
ls -l text
-rw-rw-r--    1 max group  45 2010-04-30 14:53 text
```

*!string* event text When a string of text follows an exclamation point, the shell searches for and executes the most recent event that *began* with that string. If you enclose the string within question marks, the shell executes the most recent event that *contained* that string. The final question mark is optional if a RETURN would immediately follow it.

```
68 $ history 10
59  ls -l  text*
60  tail text5
61  cat text1 text5 > letter
62  vim.tiny letter
63  cat letter
64  cat memo
65  lpr memo
66  pine zach
67  ls -l
68  history
69 $ !l
ls -l
...
70 $ !lpr
lpr memo
71 $ !?letter?
cat letter
...
```

**Table 9-8 Event Designators**

| Designator | Meaning |
| :--- | :--- |
| `!` | Starts a history event unless followed immediately by SPACE, NEWLINE, =, or (. |
| `!!` | The previous command. |
| `!n` | Command number *n* in the history list. |
| `!-n` | The *nth* preceding command. |
| `!string` | The most recent command line that started with *string*. |
| `!?string[?]` | The most recent command that contained *string*. The last ? is optional. |
| `!#` | The current command (as you have it typed so far). |
| `!(event)` | The *event* is an event designator. The braces isolate *event* from the surrounding text. For example, `!(3)` is the third most recently executed command followed by a 3. |

## Optional Word Designators

A *word designator* specifies a word (token) or series of words from an event. (Table 9-9 on page 338 lists word designators.) The words are numbered starting with 0 (the first word on the line—usually the command), continuing with 1 (the first word following the command), and ending with *n* (the last word on the line).

To specify a particular word from a previous event, follow the event designator (such as `!14`) with a colon and the number of the word in the previous event. For example, `!14:3` specifies the third word following the command from event 14. You can specify the first word following the command (word number 1) using a caret (`^`) and the last word using a dollar sign ($). You can specify a range of words by separating two word designators with a hyphen.

```
72 $ echo apple grape orange pear
apple grape orange pear
73 $ echo !72:2
echo grape
grape
74 $ echo !72:^
echo apple
apple
75 $ !72:0 !72:$_
echo pear
pear
76 $ echo !72:2-4
echo grape orange pear
grape orange pear
77 $ !72:0-$_
echo apple grape orange pear
apple grape orange pear
```

As the next example shows, `!$` refers to the last word of the previous event. You can use this shorthand to edit, for example, a file you just displayed with cat:

```
$ cat report.718
...
$ vim.tiny !$
vim.tiny report.718
...
```

If an event contains a single command, the word numbers correspond to the argument numbers. If an event contains more than one command, this correspondence does not hold true for commands after the first. In the following example, event 78 contains two commands separated by a semicolon so the shell executes them sequentially; the semicolon is word number 5.

```
78 $ !72 ; echo helen zach barbara
echo apple grape orange pear ; echo helen zach barbara
apple grape orange pear
helen zach barbara
79 $ echo !78:7
echo helen
helen
80 $ echo !78:4-7
echo pear ; echo helen
pear
helen
```
