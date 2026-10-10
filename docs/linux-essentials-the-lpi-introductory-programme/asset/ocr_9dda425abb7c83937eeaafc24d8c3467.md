to open the “file browser”, which will offer you an interactive choice of existing files. (Incidentally, this also works when saving a file using Ctrl+O.)

**Cutting and pasting** You may use the Ctrl+K command to remove (“cut”) the line containing the cursor and store it in a buffer (*Caution*: Nano will always remove all of the line, no matter where inside the line the cursor is actually positioned). Ctrl+U will then insert (“paste”) the content of the buffer again—either in the same place, if you have pressed Ctrl+K inadvertently or simply wanted to copy the line rather than move it, or elsewhere in your text.

*Insertions always happen where the cursor is positioned.* Hence if the cursor is in the middle of a line when you hit Ctrl+U, the line from the buffer becomes the right-hand part of that line, and whatever was to the right of the cursor on the original line becomes a new line.

You can move several consecutive lines to the buffer by pressing Ctrl+K a number of times in a row. These lines will then be inserted again *en bloc*.

If you want to cut just part of a line, position the cursor at the corresponding point and press Ctrl+^ (Alt+a on keyboards like some German ones that expect you to type a character to be adorned with a circumflex after you press “^”). Then move the cursor to the end of the material to be cut—Nano helpfully highlights the part of your text that you have selected for cutting—and move the region to the buffer using Ctrl+K. Do note that the character under the cursor itself is *not cut!* Afterwards you can press Ctrl+U as above to insert the buffer content elsewhere.

**Searching text** If you press Ctrl+W, Nano uses the status line to ask you for a piece of text. The cursor then jumps to the next occurrence of that piece of text in your document, starting at its current position. This makes it convenient to locate specific places in your text.

**Online help** You can use Ctrl+G to display Nano’s internal help screen, which explains the basics of the editor as well as various keyboard commands (there are many more than who have explained here). Leave the help screen again using Ctrl+X.

These are the most important features of GNU Nano. Practice makes perfect—do feel free to experiment, you will not be able to damage anything.

Back to the topic of vi (you may remember—the editor of Linux gurus). If you are game for an adventure, then ensure that the vi editor is installed on your system (this is the go-to implementation of vi today; hardly anybody uses the original BSD vi on Linux), start the *vi tutor* program, and spend an exciting and instructional half hour with the interactive introduction to vi. (Depending on your Linux distribution, you may have to install *vi tutor* as a separate package. When in doubt, ask your system administrator or somebody else knowledgeable.)

# ## Exercises

**3.6 [I2]** Start GNU Nano and enter some simple text—something like

```
Roses are red,
Violets are blue,
Linux is brilliant,
I know this is true.
```

Save this to a file called `roses.txt`