The $= subcommand is an easy way to find out how many lines are in the buffer. The ed $ symbol has no relationship to the shell prompt ($).

# B.4.2 Changing Your Position in the Buffer

You can change your position in the buffer (change your current line) in one of two ways:

+   - Specify a line number (an absolute position)
+   - Move forward or backward relative to your current line

To move the current line to a specific line, enter the line number; ed displays the new current line. In the following example, the first line of a file becomes the current line:

```
1
The only way to stop
```

Pressing Return advances one line through the buffer and displays the new current line, as the following example shows:

```
appending is to enter a

line that contains only

a dot.

?
```

When you try to move beyond the last line of the buffer, ed returns ?, an error message. You cannot move beyond the end of the buffer.

To set the current line to the last line of the buffer, enter $.

To move the current line backward through the buffer one line at a time, enter minus signs (-) one after the other, as the following example shows:

```
- line that contains only
- appending is to enter a
- The only way to stop
- ?_
```

When you try to move beyond the first line in the buffer, you receive the ? message. You cannot move beyond the top of the buffer.