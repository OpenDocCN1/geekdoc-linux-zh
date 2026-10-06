# Chapter 28 ♦ Programming Environments and Interfaces 773

```
mvaddstr(stdscr, 1, 1, "INPUT: *");
refresh();
```

```
/* read characters until newline read */
noecho();
while ((c = getch()) != '\n') {
    ++;
    getyx(stdscr, y, x);
    /* at the right margin */
    if (x == 79) {
        mvaddch(stdscr, c);
    } else {
        waddch(stdscr, c);
        refresh();
    }
}
echo();
refresh();
```

```
/* print the character count */
getmaxyx(stdscr, maxy, maxx);
mwprintw(stdscr, maxy - 2, 1, "characters read: %d\n", i + 1);
curs_set(0);
refresh();
```

```
/* time to look at the screen */
sleep(3);
```

```
/* shutdown ncurses */
endwin();
```

```
return 0;
```

The first things you notice is that nreadkey.c is about twice as long as readkey.c. The additional code addresses the need to set up the screen, position the cursor, and so forth. To see if the additional code is worth it, compile nreadkey.c using the following command:

```
$ gcc nreadkey.c -lcurses -o nreadkey
```

To run the program, type ./nreadkey. Figure 28-5 shows the result after typing the same text as typed for readkey.c earlier.

Ncurses-based programs can also read input piped from stdin. Figure 28-6 shows the results of the command cat /etc/passwd | ./nreadkey.