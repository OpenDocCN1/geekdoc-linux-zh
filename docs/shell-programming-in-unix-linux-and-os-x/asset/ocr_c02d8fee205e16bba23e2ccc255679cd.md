# Table 14.1 Basic vi Line Edit Commands

| Command | Meaning |
| --- | --- |
| h | Move one character. |
| l | Move right one character. |
| b | Move left one word. |
| w | Move right one word. |
| 0 | Move to start of line. |
| $ | Move to end of line. |
| x | Delete character at cursor. |
| dw | Delete word at cursor. |
| rc | Change character at cursor to c |
| a | Enter input mode and enter text after the current cursor. |
| i | Enter input mode and insert text before the current cursor. |
| k | Get previous command from history. |
| j | Get next command from history. |
| /string | Search history for the most recent command containing string; if string is null, the previous string will be used. |

It seems like a lot, but don't get too anxious: j and k to move up and down your history list, h and l to move around the command line, i to insert and Enter to invoke are all you really need to get going with command editing in vi mode.

# The emacs Line Edit Mode

Not a fan of the vi editor but prefer emacs, an editor much beloved by the open source developer community? The shell has a line edit mode for you too. After turning on the emacs line editor, you won't notice anything different because you'll type in and execute commands exactly as:

```
$ set -o emacs
$ echo hello
hello
$ pwd
/users/pat
$
```

This time, however, to use the emacs line editor you will enter emacs commands, emacs commands are either control characters—characters typed by holding down the Ctrl key and pressing another character—or they are characters preceded by the Esc key. You may enter