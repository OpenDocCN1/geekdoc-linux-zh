
/* Initialize the parameters of the program */
dir = RIGHT;
finished = 0;
speed = INITIAL_SPEED ;
input_ready = 0;

/* Turn on keyboard signals */
fcntl(0, F_SETOWN, getpid());
fd_flags = fcntl(0, F_GETFL);
fcntl(0, F_SETFL, (fd_flags|O_ASYNC));

/* Start the real time interval timer with delay interval size */
set_timer( ITIMER_REAL, 1000/speed, 1000/speed );

/* Put a message in bottom row with current speed. */
mvaddstr(LINES-1, 0, "Current speed:");

/* Put the message into the first position and start */
mvaddstr(ROW, 0, MESSAGE);

while( !finished ) {
    if ( input_ready ) {
        c = getch();
        finished = update_from_input(c, &speed, &dir);
        input_ready = 0;
    }
    else
        pause();
}
clear();
endwin();
return 0;
}

/********************************************************************************/
int update_from_input( int c, int *speed, int *dir )
{
    int is_changed = 0;
    char mssge[40];
    switch (c) {
    case 'Q':
    case 'q':
        return 1;                         /* quit program */
    case ' ': 
        *dir = (LEFT == *dir )? RIGHT:LEFT;  /* reverse direction */
        break;
    case 'f':
        if ( 1000/( *speed ) > 2 ) {        /* if interval > 2 */
            *speed = *speed + 2;          /* increase */
            is_changed = 1;
        }
        break;
case 's':
    if (1000/(*speed) < 500 ) {        /* if interval <= 500 */
        *speed = *speed - 2 ;           /* decrease */
        is_changed = 1;
    }
    break;
}
if ( is_changed ) {
    set_timer( ITIMER_REAL, 1000/(*speed), 1000/(*speed) );
    sprintf(mssge, "Current speed: %d (chars/sec)", (*speed));
    mvaddstr(LINES-1, 0, mssge);
}

move( LINES-1, COLS-12);
sprintf(mssge, "Last Char:%c", c);
addstr(mssge);
refresh();
return 0;
}
/********************************************************************************/
void on_input(int signum)
{
    input_ready = 1;
}
/********************************************************************************/
void on_alarm(int signum)
{
    static int row = ROW;
    static int col = 0;

    mvaddstr( row, col, BLANK );   /* erase old string */
    col += dir;                    /* advance one column */
    move( row, col );              /* move to new location */
    if ( RIGHT == dir ) {
        addstr( MESSAGE );         /* add forward string */
        if ( col+strlen(MESSAGE) >= COLS-1 )
            dir = LEFT;            /* reverse if hitting edge */
    }
    else {
        addstr( REVMSSGE );        /* add reverse string */
        if ( col <= 0 )
            dir = RIGHT;           /* reverse if hitting edge */
    }
    refresh();
}

## 6.12.4 The bouncestr.c Program Using AIO

The AIO interface is a POSIX interface that provides asynchronous I/O. Whereas setting the O_ASYNC flag on a file descriptor causes a signal to be sent when data is available to be read, using the AIO interface causes a signal to be sent when the data has actually been read and placed into a user buffer. The aio_read() call is an asynchronous read. In essence, it places a read request in the I/O device driver's queue and returns immediately, as indicated in the man page:

```
#include <aio.h>
int aio_read(struct aiocb *aiocbp);
```

```
The aio_read() function requests an asynchronous
"n = read(fd, buf, count)"
with fd, buf, count given by aiocbp->aio_fildes, aiocbp->aio_buf,
aiocbp->aio_nbytes, respectively. The return status n can be retrieved upon completion using aio_return(3).
```

```
The data is read starting at the absolute file offset aiocbp->aio_offset, regardless of the current file position. After this request, the value of the current file position is unspecified.
```

```
The “asynchronous” means that this call returns as soon as the request has been enqueued; the read may or may not have completed when the call returns. One tests for completion using aio_error(3).
```

When the request is satisfied, the driver sends a SIGIO signal. The signal handler can process the input and then issue a new aio_read() call to get more data.

The program must

- create a buffer to store the input data, and
- fill an aiocb structure with appropriate values before issuing the first read.

An aiocb structure has the following members:

```
int          aio_fildes    //File descriptor.
off_t        aio_offset    // File offset.
volatile void *aio_buf     //Location of buffer.
size_t       aio_nbytes    //Length of transfer.
int          aio_reqprio   //Request priority offset.
struct sigevent aio_sigevent // Signal number and value.
int          aio_lio_opcode //Operation to be performed.
```

A program does not have to assign a value to the aio_reqprio member, but all others must be initialized. The following function, setup_aio_buffer(), demonstrates how to set up a read of a single character at a time into a buffer named input. It is given a pointer to an aiocb structure and fills its members with the required data. The main program can then give the address of this structure to the aio_read() function.
