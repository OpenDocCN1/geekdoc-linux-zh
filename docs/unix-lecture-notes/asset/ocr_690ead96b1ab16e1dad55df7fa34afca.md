```
void save_buffer ( const char path[], Buffer buf, char *statusstr )
{
    char newline = '\n';
    int fd;
    //char statusstr[80];

    fd = creat(path, 0644);
    if ( fd != -1 ) {
        sprintf(statusstr,
            "%s\n" "%dL %dC written",
            path, buf.num_lines+1, buf.size);
        write(fd, buf.text, strlen(buf.text));
        if ( buf.text[buf.size-1] != '\n' )
            write(fd, &newline, 1);
        close(fd);
    }
    else
        exit(1);
}
/********************************************************************************/

void update_buffer_index( Buffer *buffer )
{
    int totalchars = 0;
    int i = 0;

    while ( i < buffer->cur_line ) {
        totalchars += buffer->line_len[i];
        i++;
    }
    totalchars += buffer->index_in_cur_line;
    buffer->index = totalchars;
}

/********************************************************************************/

void get_lastline_in_win( Buffer buffer, Window win, int *lastline )
{
    int totallines = 0;
    int i;
    int max_possible = win.rows-1; /* rows less status line */

    i = win.line_at_top;
    while ( i < buffer.num_lines ) {
        if ( buffer.line_len[i] <= win.cols )
            totallines++;
        else
            totallines += (int) ceil((double)buffer.line_len[i]/win.cols);
        if ( totallines > max_possible )
            break;
        else {
            i++;
        }
    }
}
```