# 3.1.1 Positioning the Cursor

The main cursor movement keys in edit mode are provided by the up, down, left and right arrow keys, if your keyboard supports them. If your keyboard does not properly support the arrow keys then the same effect can be achieved with the following keys:

+   - k up;
- j down;
- h left;
- l right.

Remember, again, that vi was written to run on a system which could support almost any kind of terminal. And some terminal types, especially older ones, just don't have arrow keys or any other special keys for that matter, other than the standard typewriter keyboard layout.

As well as these four commands, which only move the cursor by one line or one character at a time, vi also has commands to move the cursor by greater distances:

+   - Ctrl-f move forward one page in the file (page down);
- Ctrl-b move backward one page in the file (page up).

In fact, these commands move by just under a page to give some degree of continuity as you read through a file.

Once you have the page of interest on the screen you can quickly move the cursor round it with the commands:

+   - H move the cursor to the home (top) line on the screen;
- M move the cursor to the middle line on the screen;
- L move the cursor to the last line on the screen.

Again, note the case of these letters. In the case of the H and L commands, they may be preceded by a number, which will move the cursor that many lines into the screen. So, the command 2H will position the cursor on the second line of the screen, while the command 3L will move the cursor to the third line from the bottom of the screen.

When you get to the right line in the file, positioning the cursor at the correct point on that line is easy:

+   - w move right to the start of the next word;
- e move right to the end of the next word;
- b move left to the start of the previous word;
- 0 (zero) move cursor left to the start of the line;
- ^ move to the first non-whitespace character on the line;
- $ move cursor right to the end of the line.

When the w, e or b commands reach the end (or start) of a line they will wrap around onto the next (or previous) line.