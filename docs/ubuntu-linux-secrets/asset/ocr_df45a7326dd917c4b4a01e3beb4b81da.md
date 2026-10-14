Within the Command Line mode are several commands for saving the buffer to the file and for exiting vim:

+   - q to quit if no changes have been made to the buffer data
+   - q! to quit and discard any changes made to the buffer data.
+   - w filename to save the file under a different filename
+   - wq to save the buffer data to the file and quit

After seeing just a few basic vim commands you might understand why some people absolutely hate the vim editor. To be able to use vim to its fullest, you must know plenty of obscure commands. However, once you get a few of the basic vim commands down, you can quickly edit files directly from the command line, no matter what type of environment you're in.

# Editing Data

While in Insert mode, you can insert data into the buffer; however, sometimes you need to add or remove data after you've already entered it into the buffer. While in Normal mode, the vim editor provides several commands for editing the data in the buffer. Table 6-2 lists some common editing commands for vim.

| Table 6-2: vim Editing Commands |
| Command | Description |
| x | Delete the character at the current cursor position |
| dd | Delete the line at the current cursor position |
| dw | Delete the word at the current cursor position |
| d$ | Delete to the end of the line from the current cursor position |
| J | Delete the line break at the end of the line at the current cursor position |
| a | Append data after the current cursor position |
| A | Append data to the end of the line at the current cursor position |
| r char | Replace a single character at the current cursor position with char |
| R text | Overwrite the data at the current cursor position with text, until you press Esc |

Some of the editing commands also allow you to use a numeric modifier to indicate how many times to perform the command. For example, the command 2x deletes two characters starting from the current cursor position, and the command 5dd deletes five lines starting at the line from the current cursor position.

> Be careful when trying to use the PC keyboard Backspace or Delete keys while in the vim editor. The vim editor usually recognizes the Delete key because of the functionality of the x command, which deletes the character at the current cursor location. Usually, the vim editor doesn't recognize the Backspace key for deletions but instead uses it as a back arrow key.