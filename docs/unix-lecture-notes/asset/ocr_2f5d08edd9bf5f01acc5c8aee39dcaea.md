```
/* This will wrap across the screen */
move(LINES/2,0);
for ( i == 1; i <= 8; i++ ) {
    addstr( pattern );
    addch( ' ' );
}

/* Park the cursor at bottom */
move(LINES-1,0);
addstr("Type any char to quit:");
refresh(); /* not needed */

/* Wait for the user to type something, otherwise
   the screen will clear. */
getch();
endwin();
return 0;
}
```

# Comments

+   1. NCurses has a predefined constant, LINES, that contains the number of rows in the terminal window, and a constant COLS that stores the number of columns.
+   2. Notice too that the program calls refresh() each time it changes the screen. This is unnecessary, because addstr() forces the refresh automatically.
+   3. If you delete the call to getch(), you will not see anything, and if you delete the call to endwin(), the screen will not be restored.

The next program draws a grid of periods centered on the screen.

# Listing 6.3: drawgrid.c

```
#define CENTERY (LINES/2 -2)   /* The middle line in terminal */
#define CENTERX (COLS/2 -2)   /* The middle column in terminal */
#define NUMROWS (LINES/2)
#define NUMCOLS (COLS/2)

int main()
{
    int r, c;
    char MESSAGE[] = "Press any character to exit:";
    int length, i, j;
    length = strlen(MESSAGE);

    initscr();   /* Initialize screen */
    clear();     /* Clear the screen */
    noecho();    /* turn off character echo */

    char grid[NUMROWS][NUMCOLS];
```