
No where could I find a description of where the Highland Inn was originally located on Cache Lake.

If it is no trouble, could you kindly let me know such that I need not wait until next year when I visit your lodge?

Regards, MacKenzie Elizabeth

Keep in mind that the text being searched is case sensitive; to perform a case-insensitive search, use the -i option to the grep command:

```bash
[root@server1 ~]# grep "algonquin park" project4
[root@server1 ~]# grep -i "algonquin park" project4
room this year while vacationing in Algonquin Park - I
I have been reading on the history of Algonquin Park but
[root@server1 ~]#
```

Another important note to keep in mind regarding text tools such as grep is that they match only patterns of text; they are unable to discern words or phrases unless they are specified. For example, if you want to search for the lines that contain the word “we”, you can use the following grep command:

```bash
[root@server1 ~]# grep "we" project4
Hi there, I hope this day finds you well.
Unfortunately we were not able to make it to your dining
[root@server1 ~]#
```

However, notice from the preceding output that the first line displayed does not contain the word “we”; the word “well” contains the text pattern “we” and is displayed as a result. To display only lines that contain the word “we”, you can type the following to match the letters “we” surrounded by space characters:

```bash
[root@server1 ~]# grep " we" project4
Unfortunately we were not able to make it to your dining
[root@server1 ~]#
```

All of the previous grep examples did not use regular expression metacharacters to search for text in the project4 file. Some examples of using regular expressions (see Table 3-4) when searching this file are shown throughout the remainder of this section.

To view lines that contain the word “tote” or “the” or “tie”, you can enter the following command:

```bash
[root@server1 ~]# grep "t.e" project4
especially wished to see the model of the Highland Inn
and the train station in the dining room.
I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
[root@server1 ~]#
```

To view lines that start with the word “I,” you can enter the following command:

```bash
[root@server1 ~]# grep "^I" project4
I have been reading on the history of Algonquin Park but
I need not wait until next year when I visit your lodge?
[root@server1 ~]#
```

To view lines that contain the text “lodge?” or “lake,” you need to use an extended regular expression and the egrep command, as follows:

```bash
[root@server1 ~]# egrep "(lodge|lake)" project4
Inn was originally located on Cache Lake.
I need not wait until next year when I visit your lodge?
[root@server1 ~]#
```

## Editing Text Files

Recall that text files are the most common type of file modified by Linux users and administrators. Most system configuration is stored in text files, as is commonly accessed information such as e-mail and program source code. Consequently, most Linux distributions come with an assortment of text editors, and many more are available for Linux systems via the Internet. Text editors come in two varieties: editors that can be used on the command line, including vi (vim), nano, and Emacs, and editors that can be used in a GUI environment, including Emacs (graphical version) and gedit.

### The vi Editor

The vi editor (pronounced “vee eye”) is one of the oldest and most popular visual text editors available for UNIX operating systems. Its Linux equivalent (known as vim, which is short for “vi improved”) is therefore standard on almost every Linux distribution. Although the vi editor is not the easiest of the editors to use when editing text files, it has the advantage of portability. A Fedora Linux user who is proficient in using the vi editor will find editing files on all other UNIX and Linux systems easy because the interface and features of the vi editor are nearly identical across Linux and UNIX systems. In addition, the vi editor supports regular expressions and can perform over 1000 different functions for the user.

To open an existing text file for editing, you can type `vi filename` (or `vim filename`), where filename specifies the file to be edited. To open a new file for editing, simply type `vi` or `vim` at the command line:

```bash
[root@server1 ~]# vi
```

The vi editor then runs interactively and replaces the command-line interface with the following output:

![](img/c27875544958897d817484d558c208c8_136_0.png)
![](img/c27875544958897d817484d558c208c8_137_0.png)

The tilde ~ characters on the left indicate the end of the file; they are pushed further down the screen as you enter text. The vi editor is called a bimodal editor because it functions in one of two modes: command mode and insert mode. The vi editor opens command mode, in which you must use the keyboard to perform functions, such as deleting text, copying text, saving changes to a file, and exiting the vi editor. To insert text into the document, you must enter insert mode by typing one of the characters listed in Table 3-5. One such method to enter insert mode is to type the i key on the keyboard while in command mode; the vi editor then displays -- INSERT -- at the bottom of the screen and allows the user to enter a sentence such as the following:

![](img/c27875544958897d817484d558c208c8_137_1.png)

| Key | Description |
| :--- | :--- |
| i | Changes to insert mode and places the cursor before the current character for entering text |
| a | Changes to insert mode and places the cursor after the current character for entering text |
| o | Changes to insert mode and opens a new line underneath the current line for entering text |
| I | Changes to insert mode and places the cursor at the beginning of the current line for entering text |
| A | Changes to insert mode and places the cursor at the end of the current line for entering text |
| O | Changes to insert mode and opens a new line above the current line for entering text |
| Esc | Changes back to command mode while in insert mode |

**Table 3-5** Common keyboard keys used to change to and from insert mode

When in insert mode, you can use the keyboard to type text as required, but when finished you must press the Esc key to return to command mode to perform other functions via keys on the keyboard. Table 3-6 provides a list of keys useful in command mode and their associated functions. After you are in command mode, to save the text in a file called samplefile in the current directory, you need to press the : character (by pressing the Shift and ; keys simultaneously) to reach a : prompt where you can enter a command to save the contents of the current document to a file, as shown in the following example and in Table 3-7.

```text
This is a sample sentence.
~
~
~
~
~
~
~
:w samplefile
```

As shown in Table 3-7, you can quit the vi editor by pressing the : character and entering q!, which then returns the user to the shell prompt:

```text
This is a sample sentence.
~
~
~
~
~
~
~
:q!
[root@server1 ~]# _
```

The vi editor also offers some advanced features to Linux users, as explained in Table 3-7. Examples of some of these features are discussed next, using the project4 file shown earlier in this chapter. To edit the project4 file, simply type `vi project4` and view the following screen:

```text
Hi there, I hope this day finds you well.
Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
```

| Key | Description |
| :--- | :--- |
| w, W | Moves the cursor forward one word to the beginning of the next word |
| e, E | Moves the cursor forward one word to the end of the next word |
| b, B | Moves the cursor backward one word |
| 53G | Moves the cursor to line 53 |
| G | Moves the cursor to the last line in the document |
| 0, ^ | Moves the cursor to the beginning of the line |
| $ | Moves the cursor to the end of the line |
| X | Deletes the character the cursor is on |
| 3x | Deletes three characters starting from the character the cursor is on |
| dw | Deletes one word starting from the character the cursor is on |
| d3w, 3dw | Deletes three words starting from the character the cursor is on |
| dd | Deletes one whole line starting from the line the cursor is on |
| d3d, 3dd | Deletes three whole lines starting from the line the cursor is on |
| d$ | Deletes from cursor character to the end of the current line |
| d^, d0 | Deletes from cursor character to the beginning of the current line |
| yw | Copies one word (starting from the character the cursor is on) into a temporary buffer in memory for later use |
| y3w, 3yw | Copies three words (starting from the character the cursor is on) into a temporary buffer in memory for later use |
| yy | Copies the current line into a temporary buffer in memory for later use |
| y3y, 3yy | Copies three lines (starting from the current line) into a temporary buffer in memory for later use |
| y$ | Copies the current line from the cursor to the end of the line into a temporary buffer in memory for later use |
| y^, y0 | Copies the current line from the cursor to the beginning of the line into a temporary buffer in memory for later use |
| p | Pastes the contents of the temporary memory buffer underneath the current line |
| P | Pastes the contents of the temporary memory buffer above the current line |
| J | Joins the line underneath the current line to the current line |
| Ctrl+g | Displays current line statistics |
| u | Undoes the last function (undo) |
| . | Repeats the last function (repeat) |
| /pattern | Searches for the first occurrence of pattern in the forward direction |
| ?pattern | Searches for the first occurrence of pattern in the reverse direction |
| n | Repeats the previous search in the forward direction |
| N | Repeats the previous search in the reverse direction |

**Table 3-6** Key combinations commonly used in command mode
