# Part I Getting Started

respectively. If you prefer to keep your fingers on the keyboard, use h (left), l (right), j (down), or k (up) to move the cursor.

+   w \u2014 Moves the cursor to the beginning of the next word.
+   b \u2014 Moves the cursor to the beginning of the previous word.
+   0 (zero) or `\u2014 Moves the cursor to the beginning of the current line.
+   $ \u2014 Moves the cursor to the end of the current line.
+   H \u2014 Moves the cursor to the upper-left corner of the screen (first line on the screen).
+   M \u2014 Moves the cursor to the first character of the middle line on the screen.
+   L \u2014 Moves the cursor to the lower-left corner of the screen (last line on the screen)

Now that you know how to input text and move around, the only other editing you need to know is how to delete text. Here are a few v1 commands for deleting text:

+   x \u2014 Deletes the character under the cursor.
+   X \u2014 Deletes the character directly before the cursor.
+   dw \u2014 Deletes from the current character to the end of the current word.
+   d$ \u2014 Deletes from the current character to the end of the current line.
+   d0 \u2014 Deletes from the previous character to the beginning of the current line.

If you feel pretty good about creating text and moving around the file, you may want to wrap things up. Use the following keystrokes for saving and quitting the file:

+   :ZZ \u2014 Save the current changes to the file and exit from v1.
+   :zw \u2014 Save the current file but continue editing.
+   :zq \u2014 Same as ZZ.
+   :q \u2014 Quit the current file. This works only if you don't have any unsaved changes.
+   :q! \u2014 Quit the current file and *don't* save the changes you just made to the file.

> **TIP** If you've really trashed the file by mistake, the `:q!` command is the best way to exit and abandon your changes. The file reverts to the most recently changed version. So, if you just did a `:w`, you are stuck with the changes up to that point. If you just want to undo a few bad edits, press `u` to back out of changes.

You have learned a few v1 editing commands. I describe more commands in the following sections. However, before I do, here are a few tips to smooth out your first trials with v1:

+   **[Esc]** \u2014 Remember that `[Esc]` gets you back to Command mode. (I've watched people press every key on the keyboard trying to get out of a file.) `[Esc]` followed by `ZZ` gets you out of input mode, saves the file, and exits.
+   **u** \u2014 Press `u` to undo the previous change you made. Continue to press `u` to undo the change before that, and the one before that. (With the traditional v1 editor, u undoes a single command and t returns what you just undid.)

158