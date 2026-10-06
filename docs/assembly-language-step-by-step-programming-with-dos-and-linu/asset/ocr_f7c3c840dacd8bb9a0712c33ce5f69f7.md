And finally, it's possible to delete the entire cursor line with a control keystroke:

Ctrl-Y deletes the entire line containing the cursor.

The line beneath the cursor moves up to take the place of the deleted line, pulling the rest of the file behind it.

A warning for those of you with thick fingers: The T and Y characters are right next to one another on the keyboard. In a late-night frenzy at the keyboard you may find yourself reaching for Ctrl-T to delete a word or hit Ctrl-T instead, losing the entire line irretrievably. I've done this enough that I simply broke myself of the habit of using Ctrl-T at all.

# Undoing Changes to a Line

NASM-IDE's editor keeps a backup copy of each line while you're working on it, and retains that copy as long as the cursor remains within the line. Therefore, if you delete a word or some other portion of the line, or add something to a line by mistake, you can undo those changes to the line as long as you haven't yet left the line. Once you leave the line even momentarily, the editor throws away the backup copy, and Undo is no longer possible.

Ctrl-Q/L restores a line to its condition before you entered it.

One drawback is the undo feature will not restore a line deleted partially with Ctrl-Q/Y or entirely with the Ctrl-Y command. Once a line is deleted, the cursor (by necessity) leaves the line, and so the editor does not retain the backup copy of the line. Be careful how you use Ctrl-Y!

# Marking Text Blocks

Several kinds of operations, it's useful to be mark a text block. You might want to copy the text to the clipboard, or delete the block of text entirely. A logical pointer embedded invisibly in your text called a marker is used to specify the beginning and end of a text block. There are only two of these markers, and in consequence only one block may be marked within a given file at any time. These block markers are named B and K, after the commands that position them in your file. (You can try and remember them with: B and K are on opposite ends of the work block and the markers mark opposite ends of a block of text.)