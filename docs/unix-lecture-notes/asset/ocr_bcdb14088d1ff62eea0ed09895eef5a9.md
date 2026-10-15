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
```