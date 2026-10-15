```
starting at the computed firstchar until the lastchar. The cursor has to be moved to the upper left-hand corner before starting.
The caller is responsible for restoring the previous cursor position.
*/

int i;
int lastline;
int lastchar;
int firstchar = buf.line_start[win.line_at_top];

get_lastline_in_win( buf, win, &lastline );
lastchar = buf.line_start[lastline] + buf.line_len[lastline];

write(1, CLEAR_SCREEN, ICLEAR_SCREEN);
moveto(0,0);
for ( i = firstchar; i < lastchar; i++ )
    write(1,&buf.text[i], 1 );
}
/**********************************************************************/
int line_in_buffer( Buffer buf, Window win, int pos )
{
    int i = 0;

    while ( i < buf.num_lines )
        if ( buf.line_start[i] <= pos )
            i++;
        else
            break;
    /* If the inserted character is a newline, add
       the extra line */
    if ( ( buf.text[pos] == '\n' ) )
        i++;
    return i-1;
}
/**********************************************************************/
int insert( Buffer *buf, Window win, char c )
{
    int i;

    if ( ( c == '\n' ) && ( MAXLINES == buf->num_lines ) )
        return OUT_OF_LINES;
    else if ( buf->size == BUFSIZ )
        return OUT_OF_MEM;

    if ( c == win.erase_char )
        return UNHANDLEDCHAR;

    for ( i = buf->size; i > buf->index; i-- )
        buf->text[i] = buf->text[i-1];
    buf->text[buf->index] = c;
    buf->size++;
    buf->index++;
}
```