| Command | Purpose |
| --- | --- |
| i | This command inserts text at the current cursor position. All characters typed after i will be inserted. To exit this mode, press the Escape key. |
| a | This command will append text after the current cursor position. All characters typed after a will be inserted. To exit this mode, press the Escape key. |
| h, j, k, l | These keys move the cursor in various directions. They move the cursor left, down, up, and right, respectively. |
| $ | This key moves the cursor to the end of the current line. |
| :1 | This key moves the cursor to the first line. |
| :$ | This key moves the cursor to the last line. |
| dd | Pressing the d key twice deletes the line the cursor is on. |
| x | Pressing the x key deletes the character the cursor is on. |
| u | The lowercase u will undo the previous command. |
| U | This command will undo changes to the current line. |
| p | This command will paste the last deleted text at the cursor position. This is much like the Ctrl key and the v key being pressed simultaneously in most Windows programs. |
| q! | This command will discard all of your changes and exit the vi editor. |
| zz | This command will save all of your changes and exit the vi editor. |


You will need to keep in mind that while you are inserting text, you will need to type a carriage return at the end of each line. Otherwise, your text will be one very, very, very long line. Unfortunately the vi editor does support automatic word wrapping.

You might think the vi editor seems a bit complex and has a number of archaic commands. You are correct. It might seem curious then that this editor is so popular. However, it is popular among Linux aficionados because it has been around for a long time and has been in widespread use. Of course, proponents of the vi editor would argue that, with its plethora of commands, it is also quite a powerful text editor.

# ## Pico

If you thought the vi editor was a bit too complex, it is quite possible that you will find Pico more to your liking. Pico is a simple text editor. The first thing you will notice when you launch Pico is that the main commands are displayed at the bottom of the screen and that context-sensitive help is provided. This means that you don't have to memorize any commands. This may be the single most important advantage of Pico over vi. The commands you need are shown at the bottom of the screen. When you open a file with Pico, you should see something much like Figure 21.7, where one of the scripts from the preceding chapter is shown open for editing.