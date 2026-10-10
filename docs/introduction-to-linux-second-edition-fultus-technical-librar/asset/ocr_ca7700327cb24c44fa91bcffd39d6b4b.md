| Key or key combination | Function |
| --- | --- |
| Ctrl+D | Log out of the current shell session, equal to typing `exit` or `logout`. |
| Ctrl+E | Move cursor to the end of the command line. |
| Ctrl+H | Generate backspace character. |
| Ctrl+L | Clear this terminal. |
| Ctrl+R | Search command history, see Section 3.3.3.4. |
| Ctrl+Z | Suspend a program, see Chapter 4. |
| ArrowLeft and ArrowRight | Move the cursor one place to the left or right on the command line, so that you can insert characters at other places than just at the beginning and the end. |
| ArrowUp and ArrowDown | Browse history. Go to the line that you want to repeat, edit details if necessary, and press Enter to save time. |
| Shift+PageUp and Shift+PageDown | Browse terminal buffer (to see text that has 'scrolled off' the screen). |
| Tab | Command or filename completion; when multiple choices are possible, the system will either signal with an audio or visual bell, or, if too many choices are possible, ask you if you want to see them all. |
| TabTab | Shows file or command completion possibilities. |

# Table 2.2. Key combinations in Bash

The last two items in the above table may need some extra explanations. For instance, if you want to change into the directory `directory_with_a_very_long_name`, you are not going to type that very long name. No. You just type on the command line `cd dir`, then you press **Tab** and the shell completes the name for you, if no other files are starting with the same three characters. Of course, if there are no other items starting with "d", then you might just as well type `cd d` and then **Tab**. If more than one file starts with the same characters, the shell will signal this to you, upon which you can hit **Tab** twice with short interval, and the shell presents the choices you have:

```
your_prompt> cd st
starthere     stuff           stuffit
```