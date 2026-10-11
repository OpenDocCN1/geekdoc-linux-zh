# String Input

The `getstr` function, declared as

```
int getstr(char *str);
```

repeatedly calls `getch` until it encounters a newline or carriage return (which will not be part of the returned string). The characters input are stored in `str`. Because `getstr` performs no bounds checking, you should use `getnstr` instead, which takes an additional argument specifying the maximum number of characters to store. Regardless of whether you use `getstr` or `getnstr`, the receiving buffer `str` must be large enough to hold the string received plus a terminating null character, which must be added programmatically. `getnstr`'s prototype follows:

```
int getnstr(char *str, int n);
```

`getnstr` copies a maximum of `n` characters from `stdscr` to `n` buffer to which `str` points. Input beyond a count of `n` causes a beep.

`scanw` obtains formatted input from the keyboard in the manner of `scanf(3)` and family. In fact, ncurses passes the received characters as input to `sscanf(3)`, so input that does not map to available arguments in the format field goes to the bit bucket. As usual, `scanw` has variants for movement operations (the "mv" prefix) and variants that apply to specific windows (the "w" prefix). In addition, the `scanw` family of functions includes a member for dealing with variable length argument lists, `vws canw`. The relevant prototypes are as follows:

```
int scanw(char *fmt [, arg] . . . );
int vws canw(WINDOW *win, char *fmt, va_list varglist);
```

The manual pages `curs_getch(3)`, `curs_getstr(3)`, and `curs_scanw(3)` fully document these routines and their various permutations.

# Example

![](bbox=[0.04, 0.6, 0.12, 0.67])

# Example

```
```
/*
 * cursgstr.c - ncurses string input functions
 */
#include <stdlib.h>
#include <curses.h>
#include <errno.h>
#include <string.h>
#include "utilfcns.h"

#define BUFSSZ 20
```
```