The cursor should now be positioned on the space between the words new and text.

The i command starts inserting text at the character just before the cursor. That is why you have to remember to press the Space bar to insert a space between words if the cursor was positioned at the first character in a word when you started to insert text.

Another command that is used to insert text is the append (a) command. In contrast to the insert command, the a command adds (or appends) the characters you type just after the cursor position. To see how the a command works, use the cursor movement keys to move to the letter u in the word You, and type:

```
a
, too, Escape
```

The vi text editor appended the text you typed to the end of the word You. The cursor should now be positioned on the second comma.

The o command opens a new line below the line with the cursor and lets you insert text at the start of that new line. To add a sentence to the end of this file, move the cursor to the last line of the file by pressing the Return key three times:

```
Return
Return
Return
```

The cursor should be positioned at the word will. To open a new line below the current line and automatically put vi into the input mode, type:

```
o
```

Enter the sample text shown below (including pressing the Return key where indicated), and press the Escape key to return to command mode when you are finished.

```
New text can be easily entered Return
while in input mode. Escape
```

Your screen should now look like this:

```
You, too, can use this new text file
to experiment with vi.
The examples shown here
will teach you the basics of vi.
New text can be easily entered
while in input mode.
~
```