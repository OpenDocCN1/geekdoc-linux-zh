
called a **bitmap**—that must be translated by graphics software, commonly called a graphics viewer, which transforms a complex array of bits into an image.

## Executable Program Files

Many programmers develop source code for their programs by writing text files; then they compile these files to convert them to executable program files. **Executable program files** contain pure binary or machine language that the computer can immediately use or execute.

## Using Editors

Editors let you create and edit ASCII files. UNIX normally includes the two editors vi and Emacs. They are **screen editors**: they display the text you are editing one screen at a time and let you move around the screen to change and add text. You can also use a line editor to edit text files. A **line editor** lets you work with only one line or group of lines at a time. Although line editors do not let you see the context of your editing, they are useful for general tasks such as searching, replacing, and copying blocks of text.

## Using the vi Editor

The vi editor is so called because it is visual—it immediately displays on screen the changes you make to text. It is also a **modal editor**; that is, it works in two modes: insert mode and command mode. **Insert mode** lets you enter text; **command mode** lets you enter commands to perform editing tasks, such as moving through the file and deleting text.

Now you're ready to write your first memo using the vi editor. To do so, you complete the following tasks:

- Create a new file in the vi editor
- Insert, edit, and delete text
- Search and replace text
- Add text from other files
- Copy, cut, and paste text
- Print a file
- Save a file and exit vi

## Creating a New File in the vi Editor

Start by creating a file called temp to hold your first memo summarizing the basic features of text files. To start vi and with a new file, you type vi followed by the new file's name.

### The UNIX Editors

To enter vi and create a new file:

- After the $ command prompt, type `vi temp` and press Enter. This starts vi and begins editing a new file called temp. Your screen should look similar to Figure 3-2.

![](img/6d8286a85e2d8ad63e16f1801102da59_88_0.png)

Figure 3-2: vi editor's opening screen

In the upper-left corner of your screen, you see the cursor, shown in Figure 3-2 as a solid block. The cursor indicates your current location in the file.

Note: The line containing the cursor is the current line. Lines containing tildes (~) are not part of the file; they indicate lines on the screen only, not lines of text in the file.

### Inserting Text

When you start the vi editor, you're in command mode. This means that the editor interprets anything you type on the keyboard as a command. Before you can insert text in your new file, you must use the i (insert) command.

**To insert text in the Temp file:**

1. Type `i`. Like most vi commands, the `i` command does not appear (or echo) on your screen. The command switches you from command mode to insert mode; you don't need to press Enter to signal the command's completion.
2. Type the text shown in Figure 3-3.

![](img/6d8286a85e2d8ad63e16f1801102da59_89_0.png)

Figure 3-3: Inserting text with the vi editor

If you need to delete characters, press Backspace. Press Enter at the end of each line to move to the next line.

Note: In insert mode, every character you type appears on the screen. To switch to command mode, press Esc.

### Repeating a Change

Use the repeat ( . ) command to repeat the most recent change you made. Because you just inserted text, the repeat command repeats the insertion, duplicating the inserted text. You can add the next item in your memo by repeating the previous line and then editing it.

**To repeat your last edit command:**

1. Press ESC to switch to command mode.
2. Type `.` (period).

The vi editor inserts the last text you typed below the current line. Your screen should look similar to the one in Figure 3-4.

![](img/6d8286a85e2d8ad63e16f1801102da59_90_0.png)

Figure 3-4: Repeating a command in the vi editor

Now you're ready to edit the text you just inserted. Start by moving the cursor around the screen and then deleting unnecessary text.

### Moving the Cursor

You can move the cursor when you are in command mode. Start by moving around the screen to get a feel for the commands, and then move to the particular line you want to edit.

**To move the cursor around the screen:**

1. Press ESC to make sure you are in command mode.
2. Press the arrow keys to move up, down, left, and right one character at a time.
3. Type `H` to move the cursor to the upper-left corner of the screen.
   Note: Make sure you type capital letters as indicated in these steps.
4. Type `L` to move the cursor to the last line on the screen.
5. Type `G` to go to the beginning of the last line. This is the go to command. You can include a number before the `G` to indicate which line you want to move to.
6. Type `2G` to move to the beginning of the second line.

In addition to these commands, you can use other commands to move the cursor. Table 3-1 summarizes the vi editor's cursor movement keys.

| Key | Movement |
| :--- | :--- |
| h or left arrow | Left one character position |
| l or right arrow | Right one character position |
| k or up arrow | Up one line |
| j or down arrow | Down one line |
| H | Upper-left corner of the screen |
| L | Last line on the screen |
| nG | Go to the line specified by a number, n |
| w | Forward one word |
| b | Back one word |
| 0 (zero) | To the beginning of the current line |
| $ | To the end of the current line |
| Ctrl+U | Up one-half screen |
| Ctrl+D | Down one-half screen |
| Ctrl+F or Pg down | Forward one screen |
| Ctrl+B or Pg up | Back one screen |

Table 3-1: vi editor's cursor movement keys

Remember that cursor movement keys only work in command mode.

Note: Using the letter keys to move the cursor dates back to the days when UNIX used teletype terminals that had no arrow keys. Designers of vi chose the letter keys because of their relative position on the keyboard.

### Deleting Text

Now that you know how to insert text and move around a file, you are ready to delete text. To do so, move to a character and then type `x` to delete that character. You can also combine many delete commands with cursor movement commands to delete more than one character. Table 3-2 summarizes the most common delete commands.

| Command | Purpose |
| :--- | :--- |
| x | Delete the character at the cursor |
| dd | Delete the current line |
| dw | Delete the word starting at the cursor. If the cursor is in the middle of the word, delete from the cursor to the end of the line. |
| d$ or D | Delete from the cursor to the end of the line |
| d0 | Delete from the cursor to the start of the line |

Table 3-2: vi editor's delete commands

Now you can use the delete commands and the cursor movement keys to edit text you inserted in your memo.

**To edit the temp file by deleting text:**

1. Press Esc to make sure you are in command mode.
2. Type `1G` to move to the first line of the file. You want to delete this line.
3. To delete the first line, type `dd`.
   Your file should now look like Figure 3-5.

![](img/6d8286a85e2d8ad63e16f1801102da59_92_0.png)

Figure 3-5: Memo after deleting first line

4. Press `w` to go to the next word, “contains.”
5. Type `dw` to delete the current word (so the line now reads “Text lines”), and then type `i` to enter insert mode.
6. Type `consists` of between “Text” and “lines.” Be sure to include the extra “s.”
7. Press the arrow keys to move the cursor to the extra “s” in “consistss,” and then press ESC to switch to command mode.
8. To delete the current character (the extra “s”), type `x`. Your memo should now look like the one in Figure 3-6.

![](img/6d8286a85e2d8ad63e16f1801102da59_93_0.png)

Figure 3-6: Memo after editing

Now you want to edit the sentence, “Files contain text” by deleting the last word.

9. Press the arrow keys to move to the sentence, “Files contain text,” and then move to the first “c” in “contain.”
10. Type `d$` to delete the text from the cursor to the end of the line, and then type `i` to switch to insert mode.
11. Type `consist of words.` to complete the sentence.

Now you can edit the next sentence by replacing the first word.

12. Press the arrow keys to move to the next line in the file, move to the initial character in the word “lines,” and then press ESC to switch back to command mode.
13. Type `d0` to delete the text from the cursor to the beginning of the line, and then type `i` to enter insert mode.
14. Type `Words form` to insert that text at the beginning of the sentence.
15. Your completed memo should look like the one in Figure 3-7.
