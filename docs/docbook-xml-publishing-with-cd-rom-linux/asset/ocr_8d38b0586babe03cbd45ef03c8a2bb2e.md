After you've moved around a little bit, try editing the text a little. The following keys delete, cut, paste, and otherwise message text. Remember, you have to press the Esc key to return to command mode.

+   - Insert mode.

+   - Append mode. Insertion begins next to the cursor, rather than where the cursor is placed.

+   - Deletes the character that the cursor is currently on.

+   - Deletes n characters.

+   - Deletes the entire line that the cursor is on.

+   - Deletes n characters.

+   - Deletes a sentence, not the entire line.

+   - Deletes a word.

+   - Changes a word. This deletes the word that the cursor is currently on and places you in insert mode so that you can replace the word.

+   - Yanks a line. This copies the current line so that it can be pasted later.

+   - Yanks a number of lines.

+   - Pastes below the current line.

+   - Pastes above the current line.

+   - Joins two lines of text.

+   - Repeats last command.

+   - Undoes last command.

7. After a little editing, you're ready for the next step, to save the buffer that you're working on to a file. To write a new file, or to save an existing file, use the last line mode of Vim. Entering last line mode is similar to command mode. Press the Esc key if you're not already in command mode, and type a colon (:) to enter the last line mode. The commands for saving files work only in the last line mode:

+   - w filename Writes to a new file.

+   - wfilename Overwrites an existing file.

+   - wq filename Writes to a file and quits vi.

+   - wq Writes to a file and quits vi, if a filename is already assigned.

+   - q Quits without saving.

+   - q Quits.

![](bbox=[0.805, 0.563, 0.953, 0.613])