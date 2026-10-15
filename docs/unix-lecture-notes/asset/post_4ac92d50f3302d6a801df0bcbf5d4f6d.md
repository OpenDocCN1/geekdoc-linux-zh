
and this is a subsequence of the lines in the buffer. The smallest index of this sequence is stored as a member of the window to facilitate redrawing the buffer during scrolling operations and insertions. The last line index is recalculated rather than storing it. It could also be stored to save running time. Finally, because the erase character is a terminal setting, its value is stored within the window object (a window is really a terminal), and will be determined at program startup by querying the terminal driver. The window object is defined by

```
typedef struct _window
{
    unsigned short rows;
    unsigned short cols;
    int            line_at_top;
    char           erase_char;
} Window;
```

The window is divided into two regions: the line at the bottom of the screen and everything above it. The bottom line is reserved by the application for writing status messages and for *lastline mode*, which is explained below. The text is never allowed to be written onto the window's last line.

## The Cursor

The cursor is simple: it is a structure with a row and column index, representing a position in a two-dimensional array whose upper-left corner is position (0,0). The cursor is defined by

```
typedef struct _cursor
{
    int r;
    int c;
} Cursor;
```

Although the cursor position is in zero-based two-dimensional coordinates, the ANSI escape sequences use a 1-based set of coordinates: the upper-left corner of the screen is (1,1). Therefore, the cursor functions must account for this difference. For example, the function to move the cursor to a new row and column position is

```
void moveto(int line, int column)
{
    char seq_str[20];
    sprintf(seq_str, "\033[%d;%dH", line+1, column+1);
    write(1, seq_str, strlen(seq_str));
}
```

Some of the cursor functions are relatively simple. When *simplevi* is in input mode and a character is typed on the keyboard, three things must happen:

- the character must be inserted into the text buffer;
- the cursor must be advanced to the next insertion point (because echo is controlled by the application, not by the terminal driver), and
- the window must be redrawn to account for the inserted character.

The function to advance the cursor is in the listing below.

## Listing 5.1: advance_cursor

```
void advance_cursor( Cursor *cursor, Window win, char ch)
{
    if ( ch == '\n' ) {
        cursor->r++;
        cursor->c = 0;
    }
    else {
        cursor->c++;
        if ( cursor->c == win.cols ) { /* wrap the line */
            cursor->c = 0;
            cursor->r++;
        }
    }
}
```

The function checks which character was typed. If a newline, it advances the cursor to the next line at column 0, and if not, it checks whether it has to account for wrapping the line: if the cursor is at the right margin, it also advances to the next line, column 0.

## Inserting a Character

When the program is in input mode and the use enters a character to be inserted into the buffer, four actions must be taken:

- 1. physically inserting the character into the buffer, provided no overflow occurs,
- 2. advancing the cursor to the next logical position in the window,
- 3. redrawing the buffer contents to the screen, which may cause the cursor's logical position to change, and
- 4. physically moving the cursor to the final screen position.

The first step is implemented by the insert() function in Listing 5.2 below.

## Listing 5.2: insert()

```
int insert( Buffer *buf, Window win, char c )
{
    int i;

    if ( ( c == '\n' ) && ( MAXLINES == buf->num_lines ) )
        return OUT_OF_LINES;
    else if ( buf->size == BUFSIZ )
        return OUT_OF_MEM;
```

```c
if ( c == win.erase_char ) {
    /* Not implemented -- just ignore it */
    return UNHANDLEDCHAR;
}

for ( i = buf->size; i > buf->index; i-- )
    buf->text[i] = buf->text[i-1];
buf->text[buf->index] = c;
buf->size++;
buf->index++;
buf->line_len[buf->cur_line]++;

/* the first character sets line count to 1 */
if ( buf->size == 1 ) buf->num_lines++;

if ( c == '\n' ) {
    /* Save the length of the line being split by the newline */
    int temp = buf->line_len[buf->cur_line];

    /* The new length of current line is the current index position + 1. */
    buf->line_len[buf->cur_line] = buf->index_in_cur_line + 1;

    /* Increase number of lines */
    buf->num_lines++;

    /* Shift all line starts and lengths upwards in the array, but
       add 1 to the line starts since they are 1 character further
       than before because of the new newline. Do this from the last line
       down to cur_line+1, which is the line just after the split
       line. */
    for ( i = buf->num_lines-1; i > buf->cur_line+1; i-- ) {
        buf->line_len[i] = buf->line_len[i-1];
        buf->line_start[i] = buf->line_start[i-1]+1;
    }

    /* Set the start of the new line created here. It is the sum of the
       start of cur_line plus the length of cur_line. */
    buf->line_start[buf->cur_line+1] = buf->line_start[buf->cur_line]
                                      + buf->line_len[buf->cur_line];

    /* advance to new line */
    buf->cur_line++;
    /* The length of the newly created line is the number
       of characters that were to the right of the current
       index position. */
    buf->line_len[buf->cur_line] = temp - buf->line_len[buf->cur_line-1];
    buf->index_in_cur_line = 0;
}
else if ( isprint(c) ) { /* non-newline character */
    buf->index_in_cur_line++;  /* advance index in line */
    /* increment all line starts after this line */
    for ( i = buf->cur_line+1; i < buf->num_lines; i++ )
        buf->line_start[i]++;
}
```
