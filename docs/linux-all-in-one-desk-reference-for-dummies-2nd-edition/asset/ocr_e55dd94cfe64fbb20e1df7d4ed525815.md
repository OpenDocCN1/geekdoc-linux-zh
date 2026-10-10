The current line is marked by the cursor, which appears as a small black rec-
tangle. The cursor appears on top of a character.

When using vi, you work in one of three modes:

+   ✦  **Visual command mode** is what you get by default. In this mode, anything
+   that you type is interpreted as a command that applies to the line con-
+   taining the cursor. The vi commands are similar to the ed commands.

+   ✦  **Colon command mode** is for reading or writing files, setting vi options,
+   and quitting vi. All colon commands start with a colon (:). When you
+   enter the colon, vi positions the cursor on the last line and waits for
+   you to type a command. The command takes effect when you press
+   Enter.

+   ✦  **Text input mode** is for typing text. You can enter input mode with the
+   command a (insert after cursor), A (append at end of line), or i (insert
+   after cursor). After entering lines of text, you have to press Esc to leave
+   input mode and re-enter visual command mode.

One problem with all these modes is that you cannot easily tell the current
mode that vi is in. You may begin typing only to realize that vi is not in
input mode, which can be frustrating.

![](bbox=[0.14, 0.51, 0.21, 0.58])

If you want to make sure that vi is in command mode, just press Esc a few
times. (Pressing Esc more than once doesn't hurt.)

To view online help in vi, type **:help** while in colon command mode. When
you're done with help, type **:q** to exit the Help screen and return to the file
you're editing.

The vi editor initially positions the cursor on the first character of the first
line — and one of the handiest things you can know is how to move the
cursor around. To get a bit of practice, try the commands shown in Table 5-2.

**Table 5-2**  Cursor Movement Commands in vi
| Key | Does the Following |
|---|---|
| ↓ | Moves the cursor one line down |
| ↑ | Moves the cursor one line up |
| ← | Moves the cursor one character to the left |
| → | Moves the cursor one character to the right |
| W | Moves the cursor one word forward |
| B | Moves the cursor one word backward |
| Ctrl+D | Moves down half a screen |
| Ctrl+U | Scrolls up half a screen |