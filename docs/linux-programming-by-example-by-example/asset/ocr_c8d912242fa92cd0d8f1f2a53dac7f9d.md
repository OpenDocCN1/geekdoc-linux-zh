# ### Subwindows

ncurses has two functions for creating subwindows, subwin and derwin:

```
WINDOW *subwin(WINDOW *orig, int nlines, int ncols, int begin_y, int begin_x);
WINDOW *derwin(WINDOW *orig, int nlines, int ncols, int begin_y,
int begin_x);
```

subwin and derwin create and return a pointer to a window with ncols columns and nlines rows, positioned in the center of the parent window orig. The child window's upper-left corner is positioned at begin_y, begin_x relative to the screen, not the parent window. derwin behaves like subwin except that the child window is positioned at begin_y, begin_x relative to the parent window orig, not the screen.

# #### Example

![](bbox=[0.04, 0.32, 0.14, 0.38])

# ### Example

This program creates a child window, writes some text into it, and then moves it across the parent window, thus illustrating how subwindows can be managed independently of their parents.

```
/*
 * subwin.c - curses utility routines
 */
#include <stdlib.h>
#include <curses.h>
#include <errno.h>
#include <unistd.h>
#include "utilfcs.h"

int main(void)
{
    WINDOW *win;
    int ymax, xmax, n = 0;

    app_init();

    wbkgd(stdscr, 'X');
    wrefresh(stdscr);
    if ((win = subwin(stdscr, 10, 10, 0, 0)) == NULL)
        err_quit("subwin");
    wbkgd(win, ' ');
    wprintw(win, "\n#SUBWINDOW\n");
```