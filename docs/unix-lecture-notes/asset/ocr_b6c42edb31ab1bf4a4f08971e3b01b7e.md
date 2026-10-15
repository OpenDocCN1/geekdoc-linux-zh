```
finished = update_from_input(&speed, &dir);
    input_ready = 0;
    }
    else
        pause();
    clear();
    endwin();
    return 0;
}

/********************************************************************************/
/*                              SIGIO Signal Handler                           */
/********************************************************************************/

/* Handler called when aio_read() has stuff to read */
void on_input(int signo)
{
    input_ready = 1;
}

/* First check for any error codes, and if ok, then get the return code */
int update_from_input( int *speed, int *dir )
{
    int c;
    int is_changed = 0;
    char *cp = (char *) kbcbuf.aio_buf;      /* cast to char * */
    char msg[40];
    int finished=0;

    /* check for errors */
    if ( aio_error(&kbcbuf) != 0 )
        perror("reading failed");
    else
        /* get number of chars read */
        if ( aio_return(&kbcbuf) == 1 ) {
            c = *cp;
            /*nodelay = 0; */
            switch (c) {
                case 'Q':
                case 'q':
                    finished = 1;                      /* quit program */
                    break;
                case ',':
                    *dir = (*dir == LEFT)? RIGHT:LEFT;  /* reverse direction */
                    break;
                case 'f':
                    if ( 1000/( *speed ) > 2 ) {        /* if interval > 2 */
                        *speed = *speed + 2;           /* increase */
                        is_changed = 1;
                    }
                    break;
                case 's':
```