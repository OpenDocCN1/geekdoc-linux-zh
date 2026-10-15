```
window -- the last character in the last visible line. The first char
is the start of the line at the top of the screen. */
lastchar = buffer.line_start[lastline] + buffer.line_len[lastline];
firstchar = buffer.line_start[win->line_at_top];

/* Prepare to redraw the window. First clear the screen. */
write(1,CLEAR_SCREEN, !CLEAR_SCREEN);

/* Do the redraw */
moveto(0,0);
for ( i = firstchar; i < lastchar; i++ )
    write(1,&buffer.text[i],1);
}
```

The **redraw_buffer()** function could be more efficient. It is written for clarity. The problem is that the line containing the insertion might have grown long enough that it wrapped and part of it is no longer in the visible region of the window. It could also be that the inserted character is outside of the visible region because the cursor was at the right margin and the new character is in the next row of the screen. In these cases, the entire window must be redrawn because the starting line and ending line have changed. In other cases it is not necessary to redraw the entire window, but for simplicity, the entire window is always redrawn.

Redrawing the buffer requires determining whether the current line and the index of the cursor in that line are outside of the visible region. This is accomplished in a few steps:

+   1. getting the index of the last visible line in the window,
+   2. getting the index of the text line containing the insertion position,
+   3. comparing the line of the insertion point to the top line and last line computed above, and if out of bounds, resetting the line at the top of the window so that the insertion point is visible,
+   4. calculating the first and last characters of the buffer that delimit the visible characters in the window, and
+   5. moving to the upper left corner and redrawing all characters from the first to the last.

# Cursor Movement

One of the primary challenges in managing the cursor is that, at any given time, the program must be able to map the cursor position to a position in the text buffer, and vice versa.

The program will always make sure that it knows the current line and the current index in the line as the cursor moves around on the screen. In fact, the cursor movement operations will actually update these variables, and from those recalculate the cursor position. This needs explanation. Text lines may be longer than the screen width. When this happens, they wrap onto two or more lines. In vi, when the cursor is moved upward or downward, it “jumps” over wrapped lines. In other words, it moves from one text line to another, not from one screen row to another. Our simplevi program emulates this behavior. Therefore, when the user presses an arrow key up or down, it will move to the preceding or following text line. To make this possible, it will increment or decrement the cur_line member of the buffer as needed, and possibly adjust the index in cur_line variable, as will be explained below. But this implies that the index member is no longer synchronized with