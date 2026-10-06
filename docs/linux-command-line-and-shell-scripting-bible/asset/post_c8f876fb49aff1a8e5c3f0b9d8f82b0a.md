
# Part I The Linux Command Line

Almost all Linux distributions create an alias name (see Chapter 5) vi to point to vim:

```
$ alias vi
alias vi='vim'
```

This section walks through the basics of using the vim editor to edit your text script files.

# The basics of vim

The vim editor works with data in a memory buffer. To start the vim editor, just type the vim command (or vi if there's an alias) and the name of the file you want to edit:

```
$ vimprog.c
```

If you start without a filename, or if the file doesn't exist, vim opens a new buffer area for editing. If you specify an existing file on the command line, vim will read the entire contents of the file into a buffer area, where it is ready for editing, as shown in Figure 7-1.

The vim editor detects the terminal type for the session (see Chapter 2) and uses a full-screen mode to use the entire console window for the editor area.

# FIGURE 7-1

The vim main window

![](img/adcbcf1053b52dbf22f3aa187738232f_203_0.png)

# Working with Editors

The initial vim edit window shows the contents of the file (if there are any) along with a message line at the bottom of the window. If the file contents don't take up the entire screen, vim places a tilde on lines that are not part of the file (as shown in Figure 7-1).

The message line at the bottom indicates information about the edited file, depending on the status of the file, and the default settings in your vim installation. If the file is new, the message [New File] appears.

The vim editor has two modes of operation:

- Normal mode
- Insert mode

When you first open a file (or start a new file) for editing, the vim editor enters normal mode. In normal mode, the vim editor interprets keystrokes as commands (more on those later).

In insert mode, vim inserts every key you type at the current cursor location in the buffer. To enter insert mode, press the i key. To get out of insert mode and go back to normal mode, press the Escape key for the keyboard.

In normal mode, you can move the cursor around the text area by using the arrow keys (as long as your type is detected properly by vim). If you happen to be on a flaky connection that doesn't have the arrow keys defined, hope is not lost. The vim includes commands for moving the cursor:

- h to move left one character.
- j to move down one line (the next line in the text).
- k to move up one line (the previous line in the text).
- l to move right one character

Moving around large text files by line can be tedious. Fortunately, vim provides a few commands to help things along:

- PageDown (or Ctrl-f) to move forward one screen of data
- PageUp (or Ctrl-b) to move backward one screen of data
- G to move to the last line in the buffer
- num G to move to the line number num in the buffer.
- gg to move to the first line in the buffer

The vim editor has a special feature within normal mode called command line mode. The command line provides an interactive command line where you can enter additional commands to control the actions in vim. To get command line mode, press the colon key in normal mode. The cursor moves to the message line, and a colon appears, waiting for you to enter a command.

# Part I The Linux Command Line

Within the command line mode are several commands for saving the buffer to the file, and exiting vim:

- q to quit if no changes have been made to the buffer data
- q! to quit and discard any changes made to the buffer data
- w filename to save the file under a different filename
- wq to save the buffer data to the file and quit

After seeing just a few basic vim commands you might understand why some people absolutely hate the vim editor. To be able to use vim to its fullest, you must know plenty of obscure commands. However, once you get a few of the basic commands down, you can quickly edit files from the command line, no matter what environment you're in.

# Editing data

While in insert mode, you can insert data into the buffer; however, sometimes you need to remove data after you've already entered it into the buffer. In normal mode, the vim editor provides several commands for editing the data in the buffer. Table 7-1 lists some common editing commands for vim.

Some of the editing commands also allow you to use a numeric modifier to indicate how many times to perform the command. For example, the command 2x deletes two characters, starting from the current cursor position, and the command 5d deletes five lines, starting at the line from the cursor position.

> Be careful when trying to use the PC keyboard Backspace or Delete keys in the vim editor. The vim editor recognizes the Delete key as the functionality of the x command, deleting the character at the current cursor location. Usually, the vim editor doesn't recognize the Backspace key.

# Copy and paste

A standard feature of modern editors is the ability to copy or cut data, then paste it elsewhere in the document. The vim editor provides a way to do this.

Cutting and pasting is relatively easy. You've already seen the commands in Table 7-1 that can remove data from the buffer. However, when vim removes data, it actually keeps stored in a separate register. You can retrieve that data using the p command.

For example, you can use the dd command to delete a line of text, then move the cursor to the location in the buffer where you place it, then use the p command. The p command inserts the text after the line at the current cursor position. You can do this with any command that removes text.

Copying text is a little trickier. The copy command in vim is y (for yank). You can use the same command with y as the d command (yw to yank to the end of a line). After you yank the text, move the cursor to the location where you want to place the text, and use the p command. The yanked text now appears at that location.

# TABLE 7-1
# vim Editing Commands

| Command | Description |
|---|---|
| x | Delete the character at the current cursor position. |
| dd | Delete the line at the current cursor position. |
| dw | Delete the word at the current cursor position. |
| d$ | Delete to the end of the line from the current cursor position. |
| J | Delete the line break at the end of the line at the current cursor position. |
| a | Append data after the current cursor position. |
| A | Append data to the end of the line at the current cursor position. |
| r char | Replace a single character at the current cursor position with char. |
| R text | Overwrite the data at the current cursor position with text, until you press Escape. |

Yanking is tricky when you cannot see what happened, since you're not affecting the text that you yank. You never know for sure what yanked until you paste it somewhere. But there's another feature in vim that helps us out with yanking.

The visual mode highlights text as you move the cursor. Use visual mode to select text to yank for pasting. To enter visual mode, move the cursor to the location where you want to start yanking, and press v. You will notice that the text at the cursor position is now highlighted. Next, move the cursor to cover the text you want to yank (you can even move down to yank more than one line of text). As you move the cursor, vim highlights text in the yank area. After you've covered the text you want to copy, press the y to activate the yank command. Now that you've covered the text in the register, just move the cursor to where you want to paste, and use the p command.

# Search and substitute

You can easily search for data in the buffer using the vim search command. To enter a search string, press the forward slash (/) key. The cursor goes to the message line, and displays a forward slash. Enter the text you want to find, and press the Enter key. The vim editor responds with one of three actions:

- If the word appears after the cursor location, it jumps to the first location where the text appears.
- If the word does not appear after the cursor location, it wraps around the end of the file to the first location in the file where the text appears (and indicates this with a message).
- It produces an error message stating that the text was not found in the file.
