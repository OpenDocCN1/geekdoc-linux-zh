# UNIX User’s Handbook
vi

# Modes and Notations in vi

| Mode or Notation | Description |
| :--- | :--- |
| Command Mode | You are issuing commands such as moving the cursor or deleting text rather than inserting or changing text, when in command mode. You can switch to insert mode by issuing an insert mode command such as i insert or a for add text. |
| for Insert Mode | You are in insert mode when changing or inserting more than one character of text. You can switch to command mode by pressing the escape key. |
| `:` (colon commands) | Commands that start with a `:` are complete by pressing the return key. |
| control (^) commands | When a command uses the control (^) key, you press and hold down the control key and then press the next key, that is part of the command. For instance, ^g means press and hold control and then g to get the status on the file you are editing. |
| file for the name of a file | Many commands require you to specify the name of a file. For instance, in the command vi file, you would substitute the name of the file you wish to edit for file. |
| char for the name of a character | Many commands require you to specify a single character. For instance, in the command tchar, you would substitute the character you wish to search for in place of char. |
| cursor command for a cursor movement command | Many commands require you to specify a cursor command to execute. For instance, in the command d<cursor command>, you would substitute for <cursor command> the command you wish to execute. |
| string for a character string | Many commands require you to specify a character string. For instance, in the command /<string>, you would substitute for <string> the character string for which you wish to search. |

# Starting a vi Session

| Command | Description |
| :--- | :--- |
| vi file | Edit file. |
| vi-r file | Edit last saved version of file after a crash. |
| vi-R file | Edit file in read-only mode. |
| vi +n file | Edit file and place cursor on line n. |
| vi + file | Edit file and place cursor at last line. |
| vi file1 file2 file3 ... | Edit file1 through file3, and after saving changes in file1, you can move to file2 by entering :n. |
| vi +/<string> file | Edit file and place cursor at the beginning of the line containing <string>. |

# Cursor Control Commands in vi

| Command | Cursor Movement |
| :--- | :--- |
| h or ^h | Move left one character. |
| j or ^j or ^n | Move down one line. |
| k or ^p | Move up one line. |
| l or space | Move right one character. |
| G | Go to the last line of the file. |
| nG | Go to line number n. |