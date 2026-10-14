You can also start vi followed by various options, and the name of a file to edit, as in the following example:

```
vi exercise
```

The text of the file appears in the vi “window.” If a file does not yet exist, it is created. The sign “~” indicates lines that do not exist yet. The cursor is on the first line.

# Use the Editor vi

You can move the cursor with the k, j, h, and l keys (k—one line up, j—one line down, h—to the left, l—to the right) or by using the arrow keys (Up-arrow, Down-arrow, Left-arrow, Right-arrow).

# Learn the Working Modes

In contrast to many other editors, vi is mode-oriented. When vi is first started, it is in command mode. Anything you enter in this mode is considered a command. You must switch to input mode before you can type any text. This can be frustrating to users who are unfamiliar with vi.

In addition to switching modes, you must learn which keys perform which actions because you cannot use the mouse. However, the number of commands needed for everyday work is fairly small, and you can get used to them quickly.

To enter text, you must first switch the editor to insert mode by typing i (insert) or pressing the Insert key. At the bottom of the screen, you see the message --INSERT--.

Press Esc once to take you back to the command mode. From command mode, you can switch to command-line mode by entering “:”. The cursor jumps to the last line after “:” and waits for a command entry.

A command will only be carried out in command-line mode after you press Enter. Then you are automatically back in command mode.

The following is a summary of the available modes:

+   - *Command mode*—When vi starts, it is automatically in this mode. In command mode, vi can be given commands. The command `i` puts it into insert mode and the command `:` switches it to command-line mode.
+   - *Insert mode*—In this mode, vi accepts all input as text. Return to command mode with Esc.
+   - *Command-line mode*—In this mode, vi accepts commands from the command line. Pressing Enter causes the command to be executed and automatically returns vi to the command mode.