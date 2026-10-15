
## EXPLANATION (CONTINUED)

- 3. `ls !:3` reads: go to the last command on the history list and get the fourth word (words start at 0) and pass it to the `ls` command as an argument. (`file3` is the fourth word.)
- 4. The bang (`!`) with the dollar sign (`$`) refers to the last argument of the last command on the history list. The last argument is `c`.
- 5. The caret (`^`) represents the first argument after the command. The bang (`!`) with the `^` refers to the first argument of the last command on the history list. The first argument of the last command is `a`.
- 6. The asterisk (`*`) represents all arguments after the command. The `!` with the `*` refers to all of the arguments of the last command on the history list.
- 7. The last command from the history list is printed but not executed. The history list is updated. You could now perform caret substitutions on that line.

## 13.5.4 Command-Line Editing

The bash shell provides two built-in editors, emacs and vi, that allow you to interactively edit your history list. When you use the editing features at the command line, whether in vi or emacs mode, the readline functions determine which keys will perform certain functions. For example, if using emacs, Ctrl-P allows you to scroll upward in the command-line history, whereas if using vi, the k key moves upward through the history list. Readline also controls the arrow keys, cursor movement, changing, deleting, inserting text, and redoing or undoing corrections. Another feature of readline is the completion feature previously discussed in "Command and Filename Completion" on page 783.

This allows you to type part of a command, filename, or variable, and then, by pressing the Tab key, the rest of the word is completed. There are many more features provided by the Readline library designed to help manipulate text at the command line.

The emacs built-in editor is the default built-in editor and is modeless, whereas the vi built-in editor works in two modes, one to execute commands on lines and the other to enter text. If you use UNIX, you are probably familiar with at least one of these editors. To enable the vi editor, add the set command listed below and put this line in your `~/.bashrc` file. To set vi, type what's shown in the following example, at either the prompt or in the `~/.bashrc` file.

### EXAMPLE 13.34

```bash
set -o vi
```

### EXPLANATION

Sets the built-in vi editor for command-line editing of the history list.

- 4. If the `set -o` (editor) has not been set, but the `EDITOR` variable has been set to either emacs or vi, then bash will use that definition.

To switch to the emacs editor, type:

### EXAMPLE 13.35

```bash
set -o emacs
```

### EXPLANATION

Sets the built-in emacs editor for command-line editing of the history list.

### The vi Built-In Editor

To edit the history list, go to the command line and press the Esc key. Then press the K key if you want to scroll upward in the history list, and the J key to move downward, just like standard vi motion keys. When you find the command that you want to edit, use the standard keys that you would use in vi for moving left and right, deleting, inserting, and changing text. (See Table 13.8.) After making the edit, press the Enter key. The command will be executed and added to the bottom of the history list.

### Table 13.8 vi Commands

| Command | Function |
| --- | --- |
| Moving Through the History File | |
| Esc k or + | Move up the history list |
| Esc j or - | Move down the history list |
| G | Move to first line in history file |
| 5G | Move to fifth command in history file |
| /string | Search upward through history file for string |
| ?string | Search downward through history file for string |
| Moving Around on a Line | |
| h | Move left on a line |
| l | Move right on a line |
| b | Move backward a word |
| e or w | Move forward a word |
| ^ or 0 | Move to beginning of first character on the line |
| $ | Move to end of line |

- 5. vi is case-sensitive; an uppercase J and a lowercase j are different commands.
