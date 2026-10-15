```
```c
int main(int argc, char *argv[])
{
    int    r, c;
    char   MESSAGE[] = "Press any character to exit:";
    int    length;
    FILE *fp;        /* for writing window contents */

    length = strlen(MESSAGE);
    if ( argc < 2 ) {
        printf("usage: %s window-file\n", argv[0] );
        return 0;
    }

    fp = fopen(argv[1], "w");
    if ( NULL == fp ) {
        printf("Error opening %s for writing.\n", argv[1]);
        return 0;
    }

    initscr();       /* Initialize curses library and the drawing screen */
    clear();         /* Clear the screen */

    /* Move to bottom of screen and post message to display */
    move(LINES - 1, 0);
    addstr(MESSAGE);

    /* move to center of screen - width of face */
    r = CENTERY;
    c = CENTERX - 5;
    move(r, c);
    addhappyface(&r, &c);
    addhappyface(&r, &c);
    addhappyface(&r, &c);

    /* Park cursor at bottom at the right side of the message */
    move(LINES-1,length);
    refresh();

    /* Write the standard screen to a file */
    if ( ERR == putwin(stdscr, fp) ) {
        printf("Error saving window.\n");
    }

    fclose(fp);

    getch();         /* wait for the user to type something */
    clear();         /* clear the screen */
    endwin();        /* delete curses window and quit */
    return 0;
}
```
```

The next listing is of a program that can read any file created by an NCurses program that saved data using putwin(). It tries to open the file and display the window stored there. As getwin() returns a NULL pointer on failure, it checks that the returned pointer is not NULL before displaying the data.