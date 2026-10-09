CONTROL-f to move one character forward. As in vim, you can precede these movements with counts. To use a count you must first press ESCAPE; otherwise, the numbers you type will appear on the command line.

Like vim, emacs provides word and line movement commands. To move backward or forward one word on the command line, press ESCAPE-b or ESCAPE-f, respectively. To move several words using a count, press ESCAPE followed by the number and the appropriate escape sequence. To move to the beginning of the line, press CONTROL-a to move to the end of the line, press CONTROL-e; and to move to the next instance of the character c, press CONTROL-<CONTROL-f followed by c.

You can add text to the command line by moving the cursor to the position you want to enter text and typing. To delete text, move the cursor just to the right of the characters you want to delete and press the erase key (page 123) once for each character you want to delete.

# CONTROL-D can terminate your screen session

> caution If you want to delete the character directly under the cursor, press CONTROL-d. If you enter CONTROL-d at the beginning of the line, it might terminate your shell session.

If you want to delete the entire command line, press the line kill key (page 123). You can press this key while the cursor is anywhere in the command line. Use CONTROL-k to delete from the cursor to the end of the line.

# READLINE COMPLETION COMMANDS

You can use the TAB key to complete words you are entering on the command line. This facility, called completion, works in both vi and emacs editing modes. Several types of completion are possible, and which one you use depends on which part of a command line you are typing when you press TAB.

# COMMAND COMPLETION

If you are typing the name of a command, pressing TAB initiates command completion, in which bash looks for a command whose name starts with the part of the word you have typed. If no command starts with the characters you entered, bash beeps. If there is one such command, bash completes the command name. If there is more than one choice, bash does nothing in vi mode and beeps in emacs mode. Pressing TAB a second time causes bash to display a list of commands whose names start with the prefix you typed and allows you to continue typing the command name.

In the following example, the user types bz and presses TAB. The shell beeps (the user is in emacs mode) to indicate that several commands start with the letters bz. The user enters another TAB to cause the shell to display a list of commands that start with bz followed by the command line as the user has entered it so far:

```
$ bz TAB (beep) TAB
bzc\* bzdff bzip2 bzless
bzcmp bzgrep bzip2recover bzmore
$ bz■
```