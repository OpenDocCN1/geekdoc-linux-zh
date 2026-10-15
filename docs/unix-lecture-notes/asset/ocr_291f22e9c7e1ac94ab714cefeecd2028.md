```
sprintf(curs_str, "Cursor: [%d,%d]  line index: %d  win topline: %d "
"buf #lines: %d",
        cursor.r+1, cursor.c+1, line_number, win.line_at_top,
        buf.num_lines );
write(1, PARK, IPARK);
write(1, CLEAR_LINE, ICLEAR_LINE);
write(1, curs_str, strlen(curs_str));
moveto(cursor.r, cursor.c);
}
/********************************************************************************/
void moveUp( Buffer *buf, Window *win, Cursor *curs )
{
    /* if buf->cur_line == 0, we cannot go up further */
    if ( buf->cur_line > 0 ) {
        buf->cur_line--;

        if ( buf->index_in_cur_line >= buf->line_len[buf->cur_line] ) {
            buf->index_in_cur_line = buf->line_len[buf->cur_line]-1;
        }

        if ( buf->cur_line >= win->line_at_top ) {
            get_cursor_at(*buf, *win, buf->index_in_cur_line, buf->cur_line, curs );
        }
        else {
            win->line_at_top = buf->cur_line;
            get_cursor_at(*buf, *win, buf->index_in_cur_line, buf->cur_line, curs );
            scroll_buffer(*buf, *win );
        }
        moveto(curs->r, curs->c);
    }
}
/********************************************************************************/
void moveDown( Buffer *buf, Window *win, Cursor *curs )
{
    int lastline;

    if ( buf->cur_line < buf->num_lines-1 ) {
        buf->cur_line++;
        /* Check whether the cursor would be past the rightmost character
           of the now current line. If so, position it just past the rightmost
           character. */
        if ( buf->index_in_cur_line >= buf->line_len[buf->cur_line] ) {
            buf->index_in_cur_line = buf->line_len[buf->cur_line]-1;
        }

        get_lastline_in_win( *buf, *win, &lastline );

        if ( buf->cur_line > lastline ) {
            /* Need to scroll */
            win->line_at_top += buf->cur_line - lastline;

```