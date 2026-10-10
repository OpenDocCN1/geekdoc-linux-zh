
## Example 10.3 Copying Text Line by Line in vi

Sancho has heard that repeating the last line in a stanza is a poetic and songwriting technique used for emphasis, and he wants to see whether it works in “Fleas.” So, in Command mode, he moves the cursor to the line he wants to copy (there is the cursor—just below the O in the second line):

```text
You chase your tail, you drag your butt
Oh, but you suffer, my dear old mutt!
```

He presses `yy`. The line is copied into buffer 0 (the default buffer), but the original line remains on the screen. Also, the cursor stays where he placed it.

Now, he moves the cursor to the line below which he wants to place the yanked line, which is still in the buffer. (In this case, because he just wants to repeat the last line of the stanza, the cursor is already in the correct location. So he keeps it where it is.)

```text
You chase your tail, you drag your butt
Oh, but you suffer, my dear old mutt!
```

Then, he presses `p`. The yanked copy of the original line appears below the line where he had left the cursor. Now, the cursor is on the newly placed (in other words, the copied) line.

```text
You chase your tail, you drag your butt
Oh, but you suffer, my dear old mutt!
Oh, but you suffer, my dear old mutt!
```

“No,” he concludes, “it was okay the way it was.”

## The Undo Buffer

If you are deleting, moving, or copying text, the most recent buffer you have put a text string into is the undo buffer, whether you have specified it (such as the `2` or `3` or `c` in the multiple-move example) or whether it is the default `0` buffer (if you have not specified one).

Using the multiple-move example, after you have cut the three text strings, the undo buffer is the `c` buffer, not the `2` or `3` buffer. The only action you would be able to undo with the `u` command is `^c^d`. To undo your last command, simply press `u`. If you have made several changes on one line and you want to undo all of those changes and you have not moved off that line yet, press `U`.

## Executing Linux/UNIX Commands in vi

Suppose that while you are working in vi, you realize that you need to exit vi to run a command. But you do not really want to exit vi, run the command, and then re-enter vi. What is your solution? Using the exclamation point (`!`) command within vi creates an appropriate shell to execute the chosen command, prompts you for the command, executes it, and displays the results.

Here, we will show how to copy a file while remaining in the vi editor instead of having to exit vi, use the `cat` command on the file, write down the information, re-enter vi, and type the information in the file.

To copy the contents of one source file into a target file, enter the following:

```bash
$ vi targetfilename<Enter>
```

You will see the contents of `targetfilename` on the terminal screen.

Press Esc to enter Command mode.

Move the cursor down to where you want to add the information from `sourcefilename`.

Now, list the contents of the directory where `sourcefilename` resides:

```bash
:!ls /directorypath<Enter>
```

vi will respond with the following:

```text
[No write since last change]
"-  - other files and directories - " RFL_trip_laundry
Hit ENTER or type command to continue _
```

Type the following:

```bash
:!r /directorypath/sourcefilename<Enter>
```

vi will respond with

```text
"*sourcefilename" Line count, Character count
Hit ENTER or type command to continue _
```

To complete the procedure, press Enter to insert the contents of the `sourcefilename` file into `targetfilename`. By default, the text from `sourcefilename` will be inserted just below where you left your cursor in `targetfilename` before you pressed `<: !ls etc.>`.

If beforehand, line numbering had been set to On in the `targetfilename` file, you could have inserted a line number before `:r /directorypath/sourcefilename` to tell the vi editor to place the contents of `sourcefilename` there instead. (Line numbering is discussed later in this chapter; the line numbering command is described in Table 10.3.)

By the way, this method is a common technique for dumping the output of the `date` command into letters, memos, and other documents.

Please note that when you are prompted with *Hit ENTER or type command to continue*, if you need to run a series of commands without returning to vi after the execution of the first command, type

```bash
:sh
```

Then, you can run all your commands in the shell. When you want to exit the shell and return to vi, press Ctrl-D.

## Example 10.4 Executing Linux/UNIX Commands from vi

Don Quixote is producing a staff notice called `Knight_Laundry`, a list of the minimal protective and other clothing that knights-errant should take with them on their travels. He has already created an up-to-date list of such materials in the `RFL_trip_laundry` file, which we saw in Figure 10.2 (were you wondering when you would see that list again?). To copy that file into his `Knight_Laundry` notice, he enters the following:

```bash
$ vi Knight_Laundry<Enter>
```

He sees, so far, that the `Knight_Laundry` file reads like the following on the screen:

```text
All RFL knights-errant should obtain the
following beforehand and bring it with them
on their Noble Deeds Division missions:
""-" blank line - ""
```

He presses Esc to enter Command mode. Then, he moves the cursor down to the blank line below “ . . Noble Deeds Division missions:”, where he wants to append the information from `RFL_trip_laundry`.

Now, he lists the contents of the directory where `RFL_trip_laundry` is located:

```text
:ls<Enter>
[No write since last change]
"-  - other files and directories - " RFL_trip_laundry
Hit ENTER or type command to continue _
```

He types

```text
:r RFL_trip_laundry<Enter>
"RFL_trip_laundry" 6 lines, 40 characters
Hit ENTER or type command to continue _
```

Finally, now he presses Enter to insert the contents of the `RFL_trip_laundry` file into `Knight_Laundry`. By default, the text is inserted just below where Don Quixote had left cursor in that file (in other words, on the blank line below “ . . . Noble Deeds Division missions:”). So, `Knight_Laundry` now resembles Figure 10.4.

![](img/cae5c706c216875d12d4b7d28144cc71_340_0.png)

> Figure 10.4 Executing Linux/UNIX commands from vi.

## Options for Changing vi Functions

You can change several appearance and behavior characteristics of vi to make it more useful or convenient. We list some of them in this section, and we also discuss how you change characteristics.

The two basic approaches to changing vi characteristics are to:

- Set default options that remain in place after you close the current session (with the hidden `.exrc` file).
- Specify options for single-session use.

When you invoke vi, it searches for your own specific default characteristics in a hidden file called `.exrc` in the current directory. If vi finds an `.exrc` file, it follows whatever default specifications are listed there. If it does not find the `.exrc` file in the current directory, it checks your home directory for it. Please note, though, that a `.exrc` file might not even exist. If no one has specifically configured vi to alter its default behavior, then there is no need for `.exrc`.

At any rate, have a look in your current directory and/or home directory for a hidden `.exrc` file. If you cannot locate one, you can actually use vi to create one. Invoke vi with `.exrc` as its argument (in other words, to create `.exrc`), get into Insert mode, and enter any of the options listed in Table 10.4 or in any other vi information source. We have only listed a dozen or so options in Table 10.4; there are many more. Some affect the way text is presented; others facilitate editing (especially for new users).

If you want to invoke any of the Table 10.4 options on the fly while you are already in a vi session, then simply press Esc to get into Command mode and then type a colon (`:`) followed by the option as you see it in Table 10.4. We must provide a note of clarification, though: when you list any of the Table 10.4 options in the `.exrc` file, do *not* put a colon at the beginning of any of them. Again, the colon is used *only* when you are doing an interactive-style specification in Command mode when you are already in a vi session.

You can also set options for a specific session rather than every time you invoke vi. For example, to number lines as you enter text, go to Command mode and type the following:

```bash
:set nu
```

At the end of the session, you will (naturally) leave vi. The next time you invoke the vi editor, though, line numbering will be off as usual (unless you or someone else has entered `set nu` in the `.exrc` file). Table 10.4 lists common options.

### Table 10.4 vi Customizing Options

| OPTION | DESCRIPTION |
| :--- | :--- |
| set all | Display all settings |
| set | Display settings different from the default settings |
| set ai | Turn on autoindent |
| set noai | Turn off autoindent |
| set nu | Turn on line numbering |
| set nonu | Turn off line numbering |
| set list | Display nonprintable characters |
| set nolist | Hide nonprintable characters |
| set showmode | Show the current mode of operation |
| set noshowmode | Hide the current mode of operation |
| set ts=4 | Set tabs to four character jumps |
| set ic | Ignore case sensitivity |
| set noic | Set case sensitivity |
| set wrapmargin | Set the margin for automatic word wrapping from one line to the next; a value of 0 turns off word wrapping |
