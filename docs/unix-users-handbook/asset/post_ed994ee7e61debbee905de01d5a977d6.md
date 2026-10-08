
![](img/75f39fc91296b889c0653851accdfd46_447_0.png)

The bottom line in Figure 8-1 is the message line in vi. After invoking vi, the message line indicates the name of the file, the number of lines, and the number of characters in the file. Different messages appear on the message line, depending on the command you issue, as we see in upcoming examples. If a tilde appears on any lines in the file, as it does in the two lines above the message line in wisdom, it means that not enough lines exist to fill up the screen. The cursor is the dark box that appears at line 1 in Figure 8-1.

We can specify several file names and after saving the first file move on to the second file by entering :n, and continue going through the list of files in this way. Or we can specify a file and position the cursor on the last line in the file. The default is for the cursor to appear over the first character in the file, as shown in Figure 8-1.

Table 8-1 shows some of the ways we can start a vi session.

### Table 8-1 Starting a vi Session

| Command | Description |
| :--- | :--- |
| vi file | Edit file. |
| vi -r file | Edit last saved version of file after a crash. |
| vi -R file | Edit file in read-only mode. |
| vi + n file | Edit file and place cursor at line n. |
| vi + file | Edit file and place cursor on last line. |
| vi file1 file2 file3 ... | Edit file1 through file3, and after saving changes in file1, you can move to file2 by entering :n. |
| vi +string file | Edit file and place cursor at the beginning of the line containing string. |

Figure 8-2 shows editing wisdom and placing the cursor at line 5 with the command vi +5 wisdom.

![](img/75f39fc91296b889c0653851accdfd46_448_0.png)

![](img/75f39fc91296b889c0653851accdfd46_448_1.png)

Figure 8-2 Editing the File **wisdom** and Placing Cursor at Line 5 with vi +5 **wisdom**

Figure 8-3 shows editing wisdom and placing the cursor at the last line of the file with the command vi + wisdom.

![](img/75f39fc91296b889c0653851accdfd46_448_2.png)

Figure 8-3 Editing the File **wisdom** and Placing Cursor at Last Line with vi + **wisdom**

![](img/75f39fc91296b889c0653851accdfd46_449_0.png)

Figure 8-4 shows editing wisdom and placing the cursor at the line containing task with vi +/task wisdom.

![](img/75f39fc91296b889c0653851accdfd46_449_1.png)

Figure 8-4 Editing the file **wisdom** and Placing Cursor at Line Containing *task* with vi +/task **wisdom**

## Cursor Control Commands

A key skill to develop in **vi** is getting the cursor to the desired position. You do this in *command mode*. You have a variety of ways to move the cursor around the screen. Table 8-2 summarizes some of the more commonly used cursor movements.

Table 8-2 Cursor Control Commands in **vi**

| Command | Cursor Movement |
| :--- | :--- |
| h or ^h | Move left one character. |
| j or ^j or ^n | Move down one line. |
| k or ^p | Move up one line. |
| l or space | Move right one character. |
| G | Go to the last line of the file. |
| nG | Go to line number n. |
| G$ | Go to the last character in the file. |
| 1G | Go to the first line in the file. |
| w | Go to the beginning of the next word. |
| W | Go to the beginning of next word, ignore punctuation. |
| b | Go to the beginning of the previous word. |
| B | Go to the start of previous word, ignore punctuation. |
| L | Go to the last line of the screen. |
| M | Go to the middle line of the screen. |
| H | Go to the first line of the screen. |
| e | Move to the end of the next word. |
| E | Move to the end of the next word, ignore punctuation. |
| ( | Go to the beginning of the sentence. |
| ) | Go to the end of the sentence. |
| { | Go to the beginning of the paragraph. |
| } | Go to the beginning of the next paragraph. |
| 0 or \| | Go to the first column in the current line. |
| n\| | Go to column n in the current line. |
| ^(caret) | Go to the first non-blank character in the current line. |
| $ | Go to the last character in the current line. |
| + or return | Go to the first character in the next line. |
| - | Go to the first non-blank character in the previous line. |

![](img/75f39fc91296b889c0653851accdfd46_451_0.png)

I know that the fact that you have to remember these commands in order to get the cursor to the desired position may seem a little strange at first, but this is the way vi works. Let’s use **wisdom** to show how some of these cursor movements work. Figures 8-5 and 8-6 show some cursor movements. Like all of the upcoming figures, Figures 8-5 and 8-6 show **wisdom** before a command is entered on the left and the result after the command is entered on the right. The command issued appears in the middle. Some of the commands in upcoming figures use the *enter* and *escape* keys.

![](img/75f39fc91296b889c0653851accdfd46_452_0.png)

Figure 8-5 Examples of Cursor Movement in vi (h, j, k, and l)

![](img/75f39fc91296b889c0653851accdfd46_453_0.png)

![](img/75f39fc91296b889c0653851accdfd46_453_1.png)

![](img/75f39fc91296b889c0653851accdfd46_453_2.png)

![](img/75f39fc91296b889c0653851accdfd46_453_3.png)

Figure 8-6 Examples of Cursor Movement in vi (G, w, b, and e)

## Adding Text in vi

Now that we know how to move around the cursor, let's do something with it. You need to first learn about cursor movement, because the commands for adding text take place relative to the position of the cursor. Table 8-3 summarizes some commands for adding text.

Table 8-3 Adding Text In vi

| Command | Insertion Action |
| :--- | :--- |
| a | Append new text after the cursor. |
| A | Append new text after the end of the current line. |
| i | Insert new text before the cursor. |
| I | Insert new text before the beginning of the current line. |
| o | Open a line below the current line and insert. |
| O | Open a line above the current line and insert. |
| :r file | Read *file* and insert after the current line. |
| :nr file | Read *file* and insert after line *n*. |
| escape | Get back to command mode. |
| ^v char | Ignore special meaning of *char* when inserting. This is for inserting special characters. |

Let's now look at some examples for adding text into **wisdom** in Figure 8-7.

![](img/75f39fc91296b889c0653851accdfd46_455_0.png)

Figure 8-7 Examples of Adding Text in vi

## Deleting Text in vi

We also need to learn about cursor movement before learning how to delete text, because the commands for deleting text take place relative to the position of the cursor. Table 8-4 summarizes some commands for deleting text.

Table 8-4 Deleting Text In vi

| Command | Deletion Action |
| :------ | :-------------- |
| x | Delete the character at the cursor. You can also put a number in front of x to specify the number of characters to delete. |
| nx | Delete n characters beginning with the current. |
| X | Delete the previous character. You can also put a number in front of X to specify the number of previous characters to delete. |
| nX | Delete previous n characters. |
| dw | Delete to the beginning of the next word. |
| ndw | Delete the next n words beginning with the current. |
| dG | Delete lines to the end of the file. |
| dd | Delete the entire line. |
| ndd | Delete n lines beginning with the current. |
| db | Delete the previous word. |
| ndb | Delete the previous n words beginning with the current. |
| :n,md | Deletes lines n through m. |
| D or d$ | Delete from the cursor to the end of the line. |
| d*cursor_command* | Delete text to the *cursor_command*. **dG** would delete from the current line to the end of the file. |
| ^h or backspace | While inserting, delete the previous character. |
| ^w | While inserting, delete the previous word. |

Let’s now look at some examples for deleting text from **wisdom** in Figures 8-8 and 8-9.
