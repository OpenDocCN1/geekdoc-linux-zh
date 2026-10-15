```
char gridchar[REPEATS] = GRIDCHARS;
int rowshift, colshift;
int ch;

initscr(); /* Initialize screen */
noecho(); /* turn off character echo */

/* Make sure that the window is wide enough for message at the bottom.*/
length = strlen(MESSAGE);
if ( length > COLS - 2 ) {
 endwin();
 printf("This program needs a wider window.\n");
 exit(1);
}

/* Calculate the amount by which we shift each window when we draw it */
rowshift = (LINES - NUMROWS)/5;
colshift = (COLS - NUMCOLS)/5;

/* In this loop, we create a new window, fill it with a grid of a unique
characters
*/
for ( j = 0; j < REPEATS; j++ ) {
 /* Create a new window at an offset from (0,0) determined by the
 row and column shift. */
 windows[j] = newwin(NUMROWS, NUMCOLS, rowshift*j, colshift*j);
 if ( NULL == windows[j] ) {
 endwin();
 fprintf(stderr, "Error creating window\n");
 exit(1);
 }

 /* Draw each grid row as a string into windows[j] */
 for ( i = 0; i < NUMROWS; i++ ) {
 for ( k = 0; k < NUMCOLS; k++ ) {
 wmove(windows[j], i, k);
 if ( ERR == waddch(windows[j], gridchar[j]) )
 /* Ignore the error; it means we are in the
 bottom right corner of the window and the
 cursor was advance to a non-window position
 */
 ;
 }
 }
 /* Update the virtual screen with this window's content */
 wnoutrefresh(windows[j]);
}
/* Now send the virtual screen to the physical screen */
doupdate();

/*Create a window to hold a message and put it in the bottom row */
msgse_win = newwin(1, COLS, LINES-1, 0);
/* Write the message into the window; mywaddstr positions the cursor */
```