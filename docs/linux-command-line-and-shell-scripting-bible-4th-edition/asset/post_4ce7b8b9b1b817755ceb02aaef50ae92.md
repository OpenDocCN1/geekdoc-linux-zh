
Within the Ex mode are several commands for saving the buffer to the file and exiting vim:

-   q to quit if no changes have been made to the buffer data
-   q! to quit and discard any changes made to the buffer data
-   w *filename* to save the file under a different filename
-   wq to save the buffer data to the file and quit

After seeing just a few basic vim commands, you might understand why some people loathe the vim editor. To use vim to its fullest, you must know plenty of obscure commands. However, after you get a few of the basic vim commands down, you can quickly edit files directly from the command line, no matter what type of environment you're in. Due to its enormous functionality and despite its steep learning curve, the vim editor maintains its popularity. It is still considered one of the top 10 text editors.

### Editing data

While in command mode, the vim editor provides several commands for editing the data in the buffer. *Table 10-1* lists some common editing commands for vim.

TABLE 10-1 vim Editing Commands

| Command | Description |
| :--- | :--- |
| x | Deletes the character at the current cursor position. |
| dd | Deletes the line at the current cursor position. |
| dw | Deletes the word at the current cursor position. |
| d$ | Deletes to the end of the line from the current cursor position. |
| J | Deletes the line break at the end of the line at the current cursor position (joins lines). |
| u | Undoes the previous edit command. |
| a | Appends data after the current cursor position. |
| A | Appends data to the end of the line at the current cursor position. |
| `r char` | Replaces a single character at the current cursor position with *char*. |
| `R text` | Overwrites the data at the current cursor position with *text*, until you press Esc. |

Some of the editing commands also allow you to use a numeric modifier to indicate how many times to perform the command. For example, the command 2x deletes two characters, starting from the current cursor position, and the command 5dd deletes five lines, starting at the line from the current cursor position.

### NOTE

Be careful when trying to use the keyboard Backspace or Delete key while in the vim editor’s command mode. The vim editor usually recognizes the Delete key only as the functionality of the x command, deleting the character at the current cursor location. Usually, the vim editor doesn’t recognize the Backspace key in command mode as a deleting action, but instead as a method to move the cursor back one space.

### Copying and pasting

A standard editor feature is the ability to cut or copy data and paste it elsewhere in the document. The vim editor provides a way to do this. Cutting and pasting is relatively easy. You’ve already seen the commands in Table 10-1 that can remove data from the buffer. However, when vim removes data, it actually keeps it stored in a separate area. While in command mode, that data is retrievable by using the p command.

For example, use the dd command to delete a line of text, move the cursor to the buffer location where you want to place it, and then use the p command. The p command inserts the text after the line at the current cursor position. You can do this with any command that removes text while in command mode.

Copying text is a little bit trickier. The copy command in vim is `y` (for yank). You can use the same second character with `y` as with the `d` command (`yw` to yank a word, `y$` to yank to the end of a line). After you yank the text, move the cursor to the location where you want to place the text and use the `p` command. The yanked text now appears at that location.

Yanking is tricky in that you can't see what happened because you're not affecting the text that you yank. You never know for sure what you yanked until you paste it somewhere. But there's another feature in vim that helps you out with yanking.

While in command mode, the *visual mode* highlights text as you move the cursor. You use visual mode to select text to yank for pasting. To enter visual mode, move the cursor to the location where you want to start yanking, and press `v`. Notice that the text at the cursor position is now highlighted. Next, move the cursor to cover the text you want to yank (you can even move down lines to yank more than one line of text). As you move the cursor, vim highlights the text in the yank area. After you've covered the text you want to copy, enter `y` to activate the yank command. Now that you have the text in the register, just move the cursor to where you want to paste and use the `p` command.

### Searching and substituting

You can easily search for data in the buffer using the vim search command. To enter a search string, press the forward slash (`/`) key. The cursor goes to the message line, and vim displays a forward slash. Enter the text you want to find, and press the Enter key. The vim editor responds with one of three actions:

-   If the word appears after the current cursor location, it jumps to the first location where the text appears.
-   If the word doesn't appear after the current cursor location, it wraps around the end of the file to the first location in the file where the text appears (and indicates this with a message).
-   It produces an error message stating that the text was not found in the file.

If the word appears, to continue searching for the same word, press the forward slash character and then press the Enter key, or you can use n, which stands for next.

### NOTE

Are you more familiar with writing scripts and programs on a Microsoft Windows platform with an integrated development environment (IDE)? If so, Microsoft's Visual Studio Code is available on Linux. (We'll wait a minute for you to reread that last sentence.) Yes, Microsoft offers Visual Studio for Linux. Find information for installing it on your particular Linux distribution at code.visualstudio.com/docs/setup/linux. If desired, you can add the VSCodeVim plugin to Visual Studio, and have all the vim commands at your fingertips.

The substitute command, performed within Ex mode, allows you to quickly replace (substitute) one word for another in the text. To get to the substitute command, you must be in command-line mode. The format for the substitute command is `:s / old / new /`. The vim editor jumps to the first occurrence of the text *old* and replaces it with the text *new*. You can make a few modifications to the substitute command to replace more than one occurrence of the text:

-   `:s / old / new / g` to replace all occurrences of *old* in a line
-   `: n , m s / old / new / g` to replace all occurrences of *old* between line numbers *n* and *m*
-   `:%s / old / new / g` to replace all occurrences of *old* in the entire file
-   `:%s / old / new / gc` to replace all occurrences of *old* in the entire file, but prompt for each occurrence

As you can see, for a console mode text editor, vim contains quite a few advanced features. Because nearly every Linux distribution includes it, it's a good idea to at least know the basics of the vim editor so that you can always edit scripts, no matter where you are or what you have available.

### Navigating the nano Editor

In contrast to vim, which is a complicated editor with powerful features, nano is a simple editor. For individuals who need a simple console mode text editor that is easy to navigate, nano is the tool to use. It's also a great text editor for those who are just starting on their Linux command-line adventure.

The nano text editor is a clone of the Unix systems' Pico editor. Although Pico also is a light and simple text editor, it is not licensed under the GPL. Not only is the nano text editor licensed under the GPL, it is also part of the GNU project.

The nano text editor is installed on most Linux distributions by default. Everything about the nano text editor is easy. To open a file at the command line with nano, enter

```
$ nano myprog.c
```

If you start nano without a filename, or if the file doesn't exist, nano simply opens a new buffer area for editing. If you specify an existing file on the command line, nano reads the entire contents of the file into a buffer area, where it is ready for editing, as shown in Figure 10-2.
