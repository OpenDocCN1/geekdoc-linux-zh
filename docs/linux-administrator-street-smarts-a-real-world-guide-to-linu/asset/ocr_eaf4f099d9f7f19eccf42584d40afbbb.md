# ## Editing Commands

Frequently, after finding a command in the history, you want to edit it. The bash shell, like many shells, provides editing features modeled after those of the Emacs editor:

**Move within the line** Press `Ctrl+A` or `Ctrl+E` to move the cursor to the start or end of the line, respectively. The left and right arrow keys will move within the line a character at a time. `Ctrl+B` and `Ctrl+F` will do the same, moving backward and forward within a line. Pressing `Ctrl` plus the left or right arrow keys will move backward or forward a word at a time, as will pressing `Esc` and then B or F.

**Delete text** Pressing `Ctrl+D` or the Delete key deletes the character under the cursor, while pressing the Backspace key deletes the character to the left of the cursor. Pressing `Ctrl+K` deletes all text from the cursor to the end of the line. Pressing `Ctrl+X` and then Backspace deletes all the text from the cursor to the beginning of the line.

**Transpose text** Pressing `Ctrl+T` transposes the character before the cursor with the character under the cursor. Pressing `Esc` and then T transposes the two words immediately before (or under) the cursor.

**Change case** Pressing `Esc` and then U converts text from the cursor to the end of the word to uppercase. Pressing `Esc` and then L converts text from the cursor to the end of the word to lowercase. Pressing `Esc` and then C converts the letter under the cursor (or the first letter of the next word) to uppercase, leaving the rest of the word unaffected.

**Invoke an editor** You can launch a full-fledged editor to edit a command by pressing `Ctrl+X` followed by `Ctrl+E`. The bash shell attempts to launch the editor defined by the `$FCEDIT` or `$EDITOR` environment variable or Emacs as a last resort. (Environment variables are described later in this phase.)

These editing commands are just the most useful ones supported by bash; consult its man page to learn about many more obscure editing features. In practice, you're likely to make heavy use of command and filename completion, command history, and perhaps a few editing features.

Try editing your previous command by pulling it out of the history and then changing it. For instance, you might add the `-l` option to the command that did not use it or verify the presence of another file, such as `/usr/bin/who`.

# ## Getting Help

Linux provides a text-based help system known as `man`. This command's name is short for manual, and its entries (its man pages) provide succinct summaries of what a command, file, or other feature does. For instance, to learn about `man` itself, you would type `man man`. The result is a description of the `man` command.

The `man` utility uses the `less` pager to display information. When you're done, press Q to exit from `less` and the `man` page it's displaying.

Some programs have moved away from `man` pages to `info` pages. The basic purpose of `info` pages is the same as that for `man` pages, but `info` pages use a hypertext format so that