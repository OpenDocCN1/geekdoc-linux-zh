
to give to the interval timer must be 1000/k ms. Since speed contains the current number of chars per second for moving the object, the interval to give to the timer is 1000/speed, since the set_timer() function (defined in Listing 6.11) is expecting the interval expressed in milliseconds.

As a concrete example, if speed = 10, then the timer must expire every 1000/10 = 100 milliseconds, in order that we can move the object 10 times per second. If speed is increased by 2, to 12 chars/second, then the interval must be 1000/12 ≈ 83 milliseconds, so that the timer will expire every 83 milliseconds.

4. We make sure we avoid a division by zero, by preventing the user from decrementing speed below 1, which is achieved by making sure 1000/speed ≤ 500. We set an upper bound on the speed simply because high speeds are not easy to watch.

The logic of redrawing is now in the signal handler, move_msg(), shown below:

### Listing 6.14: move_msg()

```c
void move_msg(int signum)
{
    static int row = ROW;
    static int col = 0;
    char msg[40];
    mvaddstr(row, col, BLANK);   /* erase old string */
    col += dir;                  /* advance one column */
    move(row, col);              /* move to new location */
    if ( RIGHT == dir ) {
        addstr( MESSAGE );       /* add forward string */
        if ( col+strlen(MESSAGE) >= COLS-1 )
            dir = LEFT;          /* reverse if hitting edge */
    }
    else {
        addstr( REVMSGE );      /* add reverse string */
        if ( col <= 0 )
            dir = RIGHT;         /* reverse if hitting edge */
    }
    refresh();
}
```

Note that

- The handler uses static variables, a.k.a. globals, making it non-reentrant.
- It makes calls to several functions that are not safe.

However, because this is a SIGALRM handler, and the time intervals are extremely long relative to the length of the code, it is essentially impossible for a SIGALRM signal to be delivered while the handler is running. That is why it is effectively safe. Of course you can send it multiple Ctrl-C's and it will be unsafe for them.

If the signal handler were installed using the signal() system call, the handler would have to reset itself by calling signal() immediately. We use the sigaction() call instead. If the user were allowed to speed up the animation enough, the SIGALRM signals might arrive so fast that they would arrive before the handler has finished executing. In this case, the handler's behavior would be unsafe. By using sigaction(), we can make sure that signals are blocked while the program is executing inside the handler.

The program without the main processing loop from Listing 6.13 is below.

### Listing 6.15: Main program of bouncestr.c

```c
#include <stdio.h>
#include <string.h>
#include <curses.h>
#include <signal.h>
#include "timers.h"

#define INITIAL_SPEED 50
#define RIGHT 1
#define LEFT -1
#define ROW 12
#define MESSAGE "0000000=>"
#define REVMSGE "<=0000000"
#define BLANK "        "

int dir; /* Global variable to store direction of movement */
int speed; /* Current speed in chars/second */

int main()
{
    int finished;
    int is_changed;
    int c;

    /* Set up signal handling */
    struct sigaction newhandler; /* for installing handlers */
    sigset_t blocked; /* to set mask for handler */

    newhandler.sa_handler = move_msg; /* name of handler */
    newhandler.sa_flags = SA_RESTART; /* flag is just RESTART */
    sigemptyset(&blocked); /* clear all bits of blocked set */
    newhandler.sa_mask = blocked; /* set this empty set to be the mask */

    if ( sigaction(SIGALRM, &newhandler, NULL) == -1 ) { /* try to install */
        perror("sigaction");
        return (1);
    }

    /* Prepare the terminal for the animation */
    initscr(); /* initialize the library and screen */
    cbreak(); /* turn off line buffering and editing */
    noecho(); /* turn off echo */
    clear(); /* clear the screen */
    curs_set(0); /* hide the cursor */

    /* Initialize the parameters of the program */
    dir = RIGHT;
    finished = 0;
```
