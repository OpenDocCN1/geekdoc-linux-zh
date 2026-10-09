# Moving the Cursor

You need to be able to move the cursor on the screen so you can delete, insert, and correct text. While vi`m` is in Command mode, the RETURN key, the SPACE bar, and the ARROW keys move the cursor. If you prefer to keep your hand closer to the center of the keyboard, if your terminal does not have ARROW keys, or if the emulator you are using does not support them, you can use the h, j, k, and l (lowercase “el”) keys to move the cursor left, down, up, and right, respectively.

# Deleting Text

+   *   x (Delete character)
+   *   dw (Delete word)
+   *   dd (Delete line)

You can delete a single character by moving the cursor until it is over the character you want to delete and then giving the command x. You can delete a word by positioning the cursor on the first letter of the word and then giving the command dw (Delete word). You can delete a line of text by moving the cursor until it is anywhere on the line and then giving the command dd.

# Undoing Mistakes

+   *   u (Undo)

If you delete a character, line, or word by mistake or give any command you want to reverse, give the command u (Undo) immediately after the command you want to undo. The vi`m` editor will restore the text to the way it was before you gave the last command. If you give the u command again, vi`m` will undo the command you gave before the one it just undid. You can use this technique to back up over many of your actions. With the compatible parameter (page 269) set, however, vi`m` can undo only the most recent change.

+   *   :redo (Redo)

If you undo a command you did not mean to undo, give a Redo command: CONTROL-R or :redo (followed by a RETURN). The vi`m` editor will redo the undone command. As with the Undo command, you can give the Redo command many times in a row.

# Entering Additional Text

+   *   i (Insert)
+   *   a (Append)

When you want to insert new text within existing text, move the cursor so it is on the character that follows the new text you plan to enter. Then give the i (Insert) command to put vi`m` in Input mode, enter the new text, and press ESCAPE to return vi`m` to Command mode. Alternatively, you can position the cursor on the character that precedes the new text and use the a (Append) command.

+   *   o/O (Open)

To enter one or more lines, position the cursor on the line above where you want the new text to go. Give the command o (Open). The vi`m` editor opens a blank line below the line the cursor was on; puts the cursor on the new, empty line; and goes into Input mode. Enter the new text, ending each line with a RETURN. When you are finished entering text, press ESCAPE to return vi`m` to Command mode. The O command works in the same way o works, except it opens a blank line *above* the line the cursor is on.

# Correcting Text

To correct text, use dd, dw, or x to remove the incorrect text. Then use i, a, o, or O to insert the correct text.