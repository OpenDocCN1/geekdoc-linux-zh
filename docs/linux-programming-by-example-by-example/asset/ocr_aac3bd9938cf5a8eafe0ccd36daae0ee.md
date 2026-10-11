startup errors. Functions that change a terminal’s status, such as *cbreak* or *noecho*, should be called after *initscr* returns. The first call to *refresh* after *initscr* will clear the screen. If the call succeeds, *initscr* returns a pointer to *stdscr*, which you can save for later use; otherwise, the call returns NULL and exits the program, printing a useful error message to the display.

If your program will send output to or receive input from more than one terminal, use the *newterm* function call instead of *initscr*. For each terminal with which you expect to interact, call *newterm* once.

*newterm* returns a pointer to a C data structure of type *SCREEN* (another ncurses-defined type), which is used when referring to that terminal. Before you can send output to or receive input from such a terminal, you must make it the current terminal. The *set_term* call accomplishes this. Pass as *set_term*’s argument the pointer to the *SCREEN* (returned by a previous *newterm* call) that you want to make the current terminal.

# Example

![](bbox=[0.04, 0.32, 0.15, 0.42])

# Example

This program, *initcurs*, shows the standard ncurses initialization and termination idioms, using *initscr* and *endwin*. Figure 11.3 shows the window this program creates.

```
```C
/*
 * initcurs.c curses initialization and termination
 */
#include <stdlib.h>
#include <curses.h>

int main(void)
{
	if((initscr() == NULL) {
	perror("initscr");
	exit(EXIT_FAILURE);
	printw("This is an ncurses window\n");
	refresh();
	sleep(3);


	printw("Going bye-bye now\n");
	refresh();
	sleep(3);
```
```