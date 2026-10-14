# Table 13-4: Cursor Movement Escape Sequences

| Escape Code | Action |
|---|---|
| `\033[1;ch` | Move the cursor to line 1 and column c. |
| `\033[nA` | Move the cursor up n lines. |
| `\033[nB` | Move the cursor down n lines. |
| `\033[nC` | Move the cursor forward n characters. |
| `\033[nD` | Move the cursor backward n characters. |
| `\033[2J` | Clear the screen and move the cursor to the upper-left corner (line 0, column 0). |
| `\033[K` | Clear from the cursor position to the end of the current line. |
| `\033[s` | Store the current cursor position. |
| `\033[u` | Recall the stored cursor position. |

Using these codes, we’ll construct a prompt that draws a red bar at the top of the screen containing a clock (rendered in yellow text) each time the prompt is displayed. The code for the prompt is this formidable looking string:

```
PS1="\[\033[s\033[0;41m\033[K\033[1;33m\t\033[0m\033[u\]\u@\h \W\$ "
```

Table 13-5 takes a look at each part of the string to see what it does.

# Table 13-5: Breakdown of Complex Prompt String

| Sequence | Action |
|---|---|
| `\[` | Begins a non-printing character sequence. The real purpose of this is to allow bash to correctly calculate the size of the visible prompt. Without this, command line editing features will improperly position the cursor. |
| `\033[s` | Store the cursor position. This is needed to return to the prompt location after the bar and clock have been drawn at the top of the screen. *Be aware that some terminal emulators do not honor this code.* |
| `\033[0;0H` | Move the cursor to the upper-left corner, which is line 0, column 0. |
| `\033[0;41m` | Set the background color to red. |