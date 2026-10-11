![](bbox=[0.1, 0.07, 0.9, 0.43])

Figure 11.2:
getmaxyx returns a window's maximum
number of lines and columns.

# ### Function Naming Conventions

Although many `ncurse`s functions are defined to use `stdscr` by default, there will be many situations in which you want to operate on a window other than `stdscr`. `ncurse`s uses a systematic and consistently applied naming convention for routines that can apply to any window. Functions that can operate on an arbitrary window are prefixed with the character 'w' and take a (WINDOW *) variable as their first argument.

For example, the `move` call, which moves the cursor on `stdscr`, can be replaced by `wmove`, which moves the cursor on a specific window.

> **NOTE**
> Actually, most of the functions that apply to `stdscr` are pseudo-functions. They are `#defined` preprocessor macros that use `stdscr` as the default window in calls to the window-specific functions. This is an implementation detail with which you need not trouble yourself, but it may help you better understand the `ncurse`s library. A quick `grep '#define' /usr/include/ncurses.h` will reveal the extent to which `ncurse`s uses macros and will also serve as a good example of preprocessor usage.

Likewise, many `ncurse`s input and output functions have forms that combine a move and an I/O operation in a single call. These functions prepend `mv` to the function name and the desired (y, x) coordinates to the argument list. So, for example, a `move` followed by `addchstr` can be combined to create `mvaddchstr`.

You have probably surmised by now that functions also exist that combine an I/O and a move directed to a specific window. So, `wmove` and `waddchstr` are the same as `wvwaddchstr`.

This sort of shorthand permeates `ncurse`s. The convention is simple and makes for fewer lines of code.