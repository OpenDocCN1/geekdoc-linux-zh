then, using the `printf` semantics discussed a moment ago, `mcdecli.c` writes each key/value pair to stdout.

As noted, `mcdecli.c` is designed to be used from a shell script, so it performs a single operation and displays its output simply. Appropriate shell code is required to format its input or output. Also be aware that input containing spaces must be surrounded by strong or weak quotes. For example, to add a key of "Joan Armatrading" and a value of "Greatest Hits," the correct invocation would be

$ ./mcdecli -a "Joan Armatrading" "Greatest Hits"

After performing the requested operation, `mcdecli.c` closes the database and exits. The `usage` function reminds the user how to invoke the program properly.

The support routines for the ncurses-based user interface are defined in `mcdecscr.h`. It is listed here:

```
```
/*
 * mcdecscr.h - Screen-handling for music CD database
 */
#ifndef MCDESCR_H_          /* Guard against multiple inclusion */
#define MCDESCR_H_

#include <curses.h>

/*
 * Initialize the curses subsystem. Return 0 if successful or -1
 * on error.
 */
int init_scrn(void);

/*
 * Shut down the curses subsystem. No return value.
 */
void close_scrn(void);

/*
 * (Re)Draw the main screen. No return value.
 */
void draw_scrn(void);
```
```