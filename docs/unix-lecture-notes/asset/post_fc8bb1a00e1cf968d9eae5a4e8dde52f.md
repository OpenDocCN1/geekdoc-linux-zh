
```
mvwaddstr(msgse_win,0,0, MESSAGE);
wrefresh(msgse_win);

while ( 1 ) {
    /*
        Read a character from the message window, not from stdscr. The
        call to wgetch forces a refresh on its window argument. If we
        refresh stdscr, our grids will disappear.
    */
    ch = wgetch(msgse_win);  /* wait for the user to type something */
    if ( ch === 'q' ) /* time to quit */
        break;
    /* Check if they typed a grid character */
    for ( j = 0; j < REPEATS; j++ ) {
        if ( ch === gridchar[j] ) {
            wmove(msgse_win,0,length);   /* move cursor to bottom */
            touchwin(windows[j]);        /* force the update */
            wrefresh(windows[j]);        /* refresh, bringing it forward */
            break;
        }
    }
}
clear();            /* clear the screen */
endwin();           /* delete curses window and quit */
return 0;
}
```

## 6.7 Adding Timing to Programs: Sleeps

To make images move or animate on the screen, the program has to control the rate at which images are changed or displayed, which implies their being able to access a time-of-day clock or a timer. You have already seen the sleep() system call. It is one method of controlling time. The problem with sleep() is that its base unit is a one-second interval, which is too coarse for most video. An alternative is the usleep() system call; usleep() has a granularity of one microsecond³. The problem with usleep() though is that it uses the real timer of the process, of which there is just one, so multiple simultaneous calls to usleep() will have unexpected results. Both sleep() and usleep() suffer from the fact that they may share the same timer as the alarm() system call. POSIX requires a call named nanosleep(), which has even finer granularity and is guaranteed not to interact with any other timers. Therefore, we will use nanosleep():

```
#include <time.h>
int nanosleep(const struct timespec *req, struct timespec *rem);
```

The timespec structure is defined by

```
struct timespec {
```

> ³This does not mean that it will be implemented accurately to within a microsecond. The implementation of the timer may be inaccurate for small intervals because of context-switching.

```
time_t tv_sec;    /* seconds */
long  tv_nsec;    /* nanoseconds */
};
```

The first argument specifies the amount of time that the caller should be suspended. The second argument can be used to store the amount of time remaining in case the caller is awakened by a signal. If it is a NULL pointer, it is ignored. For now we will pass a NULL pointer as the second argument.

The first example of animation alternates two images on the screen at regular intervals determined by the nanosleep() timer. It uses three functions defined in file faces.c :

```
void addsadface(int * y, int * x);    // Draws a "sad" face at (y,x)
void addhappyface(int * y, int * x);  // Draws a "happy" face at (y,x)
void eraseface(int * y, int * x);     // Erases face at (y,x)
```

that draw, respectively, a "sad face", a "happy face", and a blank face. The coordinates are initially the upper left corner of the rectangle enclosing the face. On return they store the upper right hand corner.

The main loop will repeatedly draw a face, park the cursor in the lower left-hand corner of the screen, call refresh(), and then sleep a bit. The sad and happy faces will alternate. The first version of the program, whose listing follows, uses a loop that runs forever and must be killed by the user's entering a Ctrl-C.

### Listing 6.8: animateface0.c

```
#include <stdio.h>
#include <curses.h>
#include <string.h>
#include <time.h>      /* for struct timespec */
#include "faces.h"    /* The set of face drawing functions */

int main(int argc, char* argv[])
{
    int r, c;
    int i = 0;
    char MESSAGE[] = "Type Ctrl-C to exit:";
    char BLANKS[] = "";
    int length;
    struct timespec sleeptime = {0,500000000};   /* 1/2 second */

    initscr();      /* Initialize curses library and the drawing screen */
    clear();        /* Clear the screen */

    /* Move to bottom of screen and post message to display */
    move(LINES-1,0);
    addstr(MESSAGE);

    /* Loop repeatedly until user types any character */
```
