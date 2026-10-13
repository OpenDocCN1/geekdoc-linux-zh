
### TABLE 8.2 continued

| Cursor Movement | Command |
|---|---|
| Scroll forward one screen | Ctrl+F |
| Scroll backward one screen | Ctrl+B |
| Scroll forward one-half screen | Ctrl+D |
| Scroll backward one-half screen | Ctrl+U |
| Go to end of the file | G |
| Go to line 10 | 10G |

## Inserting and Deleting Text

Press the Escape key. Did the system beep? If it did, you're in Command mode and you're ready to give the command to insert some text. Well, that is, after you move the cursor to the place where you want the text inserted. After the cursor is in position, press the i key (use lowercase) and begin typing the text. To move the cursor to a new location, press Escape and use the cursor commands to move around. You'll find more ways to insert text in Table 8.3.

### TABLE 8.3 Inserting Text into a File

| To Insert Text | Use This Command |
|---|---|
| Before the character cursor | i |
| At the beginning of the line | I |
| After the cursor | a |
| To the end of the line | A |
| On a new line below the cursor | o |
| On a new line above the cursor | O |
| Overwrite existing text | R |

There are several commands that will delete text, whether you need to delete a single character or a block of text. The basic command for deleting text is d followed by one of the cursor movement symbols to show what should be deleted. A few commands used to delete text are shown in Table 8.4.

### TABLE 8.4 Deleting Text from the Buffer Area

| To Delete | Use This Command |
|---|---|
| From the cursor to the end of a word | dw |
| The three words following the cursor | 3dw |
| From the cursor to the end of a line | d$ |
| From the cursor to the beginning of a line | d0 |
| From the cursor to the end of a paragraph | d} |
| The line on which the cursor rests | dd |
| Current line and 3 following lines | 4dd |
| The character under the cursor | x |
| The character to the left of the cursor | X |
| Undo unwanted changes | u |

## Copying Text

Organizing a document involves quite a bit of moving text around. To move text around in vi, you must first yank the text, move the cursor to the new location for the text, and then paste the text in the new location.

### New Term

When you yank text, you are selecting it (although you might not see the text highlighted on the screen) and making a copy of the selected text. The yanked text is stored in an unnamed buffer. This unnamed buffer is a temporary holding pen where only the last piece of yanked text is kept.

To yank text, move the cursor to the beginning of the text that you want to copy, press the y key followed by the cursor movement command (found in Table 8.2) that will move the cursor to the end of the text. For example, to copy the text from the cursor position to the end of the line, press y$. To position the cursor in the place where you want to copy the text, use the cursor movement commands. After the cursor is in place, paste the text by pressing p. The text will be copied on the line below the cursor.

![](img/782ecfdc0b083a767896cc983e10427f_165_0.png)

> If you want to move text, first delete the text to be moved (use one of the commands found in Table 8.4). Then move the cursor to the place where you want to paste the text and press the p key.

## Searching and Replacing Text

One final way to edit your text file is to find a word or a group of words quickly and to replace those words with other words. You might need to replace text to give more meaning to your document. Or, information might need to be updated and you have to search for an old version number of a software application and replace it with the new version number. You might also want to search the file to locate places in the document that need to be double-checked.

When you want to search for a specific word, press Escape to enter Command mode, type a slash (/) character, type the word for which you are searching, and then press Enter. For example, to find all instances of the word “fox” in the file, type /fox and press Enter. The vi text editor starts the search from the cursor location and looks for the first instance of the word “fox.” When a match is found, the cursor is placed on the first letter of the word. To find the next occurrence of “fox,” type / and press Enter.

If you need to look for a word and then replace it with another word, the command is quite different. If you want to find all instances of the word “fox” and replace them with the word “dog,” press the Escape key to enter Command mode, type :%s/fox/dog/g, and press Enter. This command makes the search-and-replace procedure automatic. The colon (:) character tells vi that you are about to type a command, the %s parameter tells vi to search the entire file, and the g parameter tells vi to replace all instances of the word “fox” with the word “dog.” When vi has finished replacing the text, a message similar to the following appears at the bottom of the screen:

```
3 substitutions on 3 lines
```

If you want to replace only the first match found by vi, do not use the g parameter. So, to replace only the first occurrence of the word “fox,” type :%s/fox/dog and press Enter.

![](img/782ecfdc0b083a767896cc983e10427f_166_0.png)

> You’ll find the same type of command line history list as you saw in Hour 6. After you type the colon (:) character, press the up-arrow key. The last command you typed in vi will appear on the command line. You can use the Backspace key to make any changes.

![](img/782ecfdc0b083a767896cc983e10427f_166_1.png)

## Task: Configuring vi

There are a number of options within vi that you can set to control the editing environment. These options are enabled and disabled with the :set command, and range from listing line numbers along the left side of the screen to displaying the cursor position. Table 8.5 shows some of the configuration changes you can make. To enable any of these options, press Escape to enter Command mode, type the option (as shown in Table 8.5), and press Enter. For example, to display line numbers along the left side of the screen, use the :set number option. Then, to disable an option, type no before the option. So, when you want to turn off line numbering, use the :set nonumber command.

### TABLE 8.5 Control the Editing Environment with Configuration Settings

| Option | Description |
|---|---|
| :set backup | Keep a copy of a file after overwriting a file |
| :set incsearch | Show matches for partially typed search commands |
| :set lines=X | Change the number of lines displayed on the screen at one time (X is the number of lines) |
| :set number | Show line numbers along the left side of the screen |
| :set ruler | Show the cursor position in the status line |
| :set scroll=X | Number of lines to scroll the window at a time (X is the number of lines) |
| :set visualbell | Use a visual signal (displays as ^[ on the status line) instead of a beep |

When you change options with the :set command, the configuration change is only temporary. When you close the program, the configuration changes are not stored. The next time you use vi, the default configuration will be used. To change the default configuration, you will need to edit the .vimrc file. Here's how to use vi to change the default configuration of the program:

- 1. Find the configuration file in your home directory. At the shell prompt, type `ls -a` and press Enter. You should see a file named `.vimrc` or `.exrc` in your home directory.
- 2. Make a backup copy of the `.vimrc` file. Type `cp .vimrc .vimrc.original` and press Enter.
- 3. Open the configuration file in vi. Type `vi .vimrc` and press Enter. A sample `.vimrc` file is shown in Figure 8.3.

### FIGURE 8.3
Edit and add options to change the default settings for vi.

Delete 'no' to activate an option

![](img/782ecfdc0b083a767896cc983e10427f_168_0.png)

Insert new default settings

- 4. Use the j key to read the configuration file line by line. You should read this file so that you understand the current vi configuration.
- 5. Change vi so that it automatically makes a backup of any file you accidentally overwrite. Scroll down to the section that reads:
  
  `'Some options deactivate by default (remove the no).`
  `set nobackup`
  `set nohlsearch`
  `set noincsearch`
  
  Change the set nobackup option so that it reads:
  
  `set backup`
- 6. Change the default configuration so that line numbers display in each open file. Type the following (starting on a blank line):
  
  `'Display line numbers to the left of the text`
  `set number`
- 7. Save the file and exit vi. Type :wq and press Enter.
- 8. Open a file in vi to see the configuration changes. Figure 8.4 shows an example of a file that uses line numbers.
