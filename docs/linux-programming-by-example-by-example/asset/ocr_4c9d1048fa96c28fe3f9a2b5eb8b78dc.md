```
/* set up stdscr */
mvwprintw(2, 1, "*** WINDOW 1 ***\n\n");
keypad(stdscr, TRUE);
box(stdscr, ACS_VLINE, ACS_HLINE);
refresh();

/* set up the new window */
if((win = newwin(10, 40, 10, 10)) == NULL) {
    perror("newwin");
    exit(EXIT_FAILURE);
} else {
    keypad(win, TRUE);
    mvwprintw(win, 2, 1, "*** WINDOW 2 ***\n\n");
    box(win, ACS_VLINE, ACS_HLINE);
    wrefresh(win);
}

/* set the event mask for all events */
mask = mousemask(ALL_MOUSE_EVENTS, NULL);
/* decode events until user presses [q/Q] */
while((toupper(ch = getch())) != 'Q') {
    if(ch == KEY_MOUSE) {
        getmouse(&event);
        if(wenclose(win, event.y, event.x)) {
            mvwprintw(win, 3, 1,
                "event detected in window 2\n");
            mvwprintw(win, 4, 1,
                "coords were (%d,%d)\n", event.y, event.x);
        }
        else if(wenclose(stdscr, event.y, event.x)) {
            mvwprintw(3, 1,
                "event detected in window 1\n");
            mvwprintw(4, 1,
                "coords were (%d,%d)\n", event.y, event.x);
        }
    }
    box(stdscr, ACS_VLINE, ACS_HLINE);
    box(win, ACS_VLINE, ACS_HLINE);
```