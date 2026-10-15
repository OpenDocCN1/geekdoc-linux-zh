

if ( str[i] == ' ' )
    state = 4;
else
    state = 5;
    i++;
    break;
case 4:
    if ( str[i] == ' ' )
        state = 4;
    else if ( isalnum(str[i]) || str[i] == '_' ) {
        filename = &(str[i]);
        state = 6;
    }
    else
        state = 5;
    i++;
    break;
case 5:
    badchar = 1;
    sprintf(statusstr, "\033[7m: %s Not an editor command\033[27m", str);
    return -1;
case 6:
    filename = &(str[i-1]);
    while ( ( i < len ) && ( isalnum(str[i]) || str[i] == '_' ) )
        i++;
    str[i] = '\0';
    done = 1;
    break;
case 7:
    if ( str[i] == ' ' )
        state = 7;
    else {
        badchar = 1;
        sprintf(statusstr,
            "\033[7m: %s Not an editor command\033[27m", str);
        return -1;
    }
    i++;
}
if ( foundwrite ) {
    if ( filename != NULL )
        save_buffer( filename, buf, statusstr );
    else {
        sprintf(statusstr,
            "\033[7m: %s Not an editor command\033[27m", str);
        return -1;
    }
}
if ( foundquit )
    return 1;
else
    return 0;
}

/*************************************************************************/
int do_lastline_mode( Buffer buf, Window win, Cursor curs )
{
    char tempstr[MAXCHARS];
    char statusstr[MAXCHARS];
    char c;
    int i = 0;
    int status;
    int in_lastline_mode = 1;

    while ( in_lastline_mode ) {
        read( STDIN_FILENO, &c, 1);
        if ( c == '\n' ) {
            tempstr[i] = '\0';
            status = parse_lastline(tempstr, strlen(tempstr), buf, statusstr);
            in_lastline_mode = 0;
            write_status_message( statusstr, curs);
            statusstr[0] = '\0';
        }
        else if ( c == win.erase_char ) {
            write(1,BACKSPACE,1);
            if ( i > 0 )
                i--;
            else
                in_lastline_mode = 0;
        }
        else {
            tempstr[i++] = c;
            write(1,&c,1);
        }
    }
    return status;
}
/*************************************************************************/

void handle_escape_char( Buffer *buf, Window *win, Cursor *curs )
{
    char c;

    read(STDIN_FILENO, &c, 1);
    if ( c == 91 ) {
        read(STDIN_FILENO, &c, 1);
        switch ( c ) {
            case KEY_UP:
                moveUp(buf, win, curs );
                break;
            case KEY_DOWN:
                moveDown(buf, win, curs );
                break;
            case KEY_RIGHT:
                moveRight(buf, win, curs );
                break;
case KEY_LEFT:
    moveLeft(buf, win, curs );
    break;
}
}
/********************************************************************************/
void set_erase_char(int termfd, Window *win )
{
    struct termios cur_tty;
    tcgetattr(termfd, &cur_tty);

    win->erase_char = cur_tty.c_cc[VERASE];
}
/********************************************************************************/
void modify_termios(int fd, int echo, int canon )
{
    struct termios cur_tty;
    tcgetattr(fd, &cur_tty);

    if ( canon )
        cur_tty.c_lflag |= ICANON;
    else
        cur_tty.c_lflag &= ~ICANON;
    if ( echo )
        cur_tty.c_lflag |= ECHO;
    else
        cur_tty.c_lflag &= (~ECHO & ~ECHOE);

    cur_tty.c_lflag &= ~ISIG;
    cur_tty.c_cc[VMIN]  = 1;
    cur_tty.c_cc[VTIME] = 0;

    tcsetattr(fd, TCSADRAIN, &cur_tty);
}
/********************************************************************************/
void save_restore_tty(int fd, int action)
{
    static struct termios original_state;
    static int            retrieved = FALSE;

    if ( RETRIEVE == action ){
        retrieved = TRUE;
        tcgetattr(fd, &original_state);
    }
    else if (retrieved && RESTORE == action ) {
        tcsetattr(fd, TCSADRAIN, &original_state);
    }
    else
        fprintf(stderr, "Illegal action to save_restore_tty().\n");
}

/********************************************************************************
                                窗口函数
********************************************************************************/
void init_window( int fd, Window *win )
{
    struct winsize size;

    if (ioctl(fd, TIOCGWINSZ, &size) < 0) {
        perror("TIOCGWINSZ error");
        return;
    }
    win->rows = size.ws_row;
    win->cols = size.ws_col;
    win->line_at_top = 0;
    set_erase_char( fd, win);
}
/********************************************************************************/
void write_status_message( const char *message, Cursor curs )
{
    write(1, PARK, IPARK);
    write(1, CLEAR_LINE, ICLEAR_LINE);
    write(1, message, strlen(message));
    moveto(curs.r, curs.c);
}
/********************************************************************************/
void moveto(int line, int column )
{
    char seq_str[20];

    sprintf(seq_str, "\033[%d;%dH", line+1, column+1);
    write(1, seq_str, strlen(seq_str));
}
/********************************************************************************
                                缓冲区函数
********************************************************************************/
void init_buffer( Buffer *buffer)
{
    buffer->num_lines      = 0;
    buffer->cur_line       = 0;
    buffer->line_len[0]    = 0;
    buffer->line_start[0]  = 0;
    buffer->size           = 0;
    buffer->index_in_cur_line = 0;
    buffer->index          = 0;
}
/********************************************************************************/

