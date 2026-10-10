| Command | Description | |---|---| | Alt+d | Deletes the current word | | Alt+l | Converts the current word to lowercase | | Alt+r | Undoes line changes | | Alt+t | Transposes words | | Alt+u | Converts the current word to uppercase | | Ctrl+a | Goes to the beginning of the line | | Ctrl+b | Cursor goes backward one character on the line | | Ctrl+c | Aborts the command line | | Ctrl+d | Deletes the current character | | Ctrl+e | Goes to the end of the line | | Ctrl+f | Cursor goes forward one character on the line | | Ctrl+k | Deletes a line | | Ctrl+t | Transposes letters | | Ctrl+u | Deletes a line (but keeps a copy in the buffer) | | Ctrl+w | Deletes a word backward | | Ctrl+y | Pastes the buffer to the line | | Down arrow | Goes to the next (history) command line | | Left arrow | Cursor goes backward on the command line | | Right arrow | Cursor goes forward on the command line | | Tab | Expands the command line (help) | | Up arrow | Displays the previous (history) command line |

For example, you can use a simple shell script to launch a text-based application in an X11 terminal window like this:

```
```shell
#!/bin/sh
/usr/X11R6/bin/xterm -e $
```
```

Save these two lines in a text file, perhaps named `xi`, and then use the `chmod` command to make the file executable:

```
```shell
# chmod +x xi
```
```