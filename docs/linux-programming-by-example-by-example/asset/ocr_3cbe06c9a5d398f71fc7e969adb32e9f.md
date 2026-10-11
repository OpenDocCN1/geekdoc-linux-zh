where `win` is the window in question. Complete descriptions of functions that set and get window backgrounds can be found in the `curs_bkgd(3)` manual page.

At least 11 ncurses functions draw boxes, borders, and lines in ncurses windows. The `box` call is the simplest; it draws a box around a specified window using one character for vertical lines and another for horizontal lines. Its prototype is listed here:

```
int box(WINDOW *win, chtype verch, chtype horch);
```

`verch` sets the pseudo-character used to draw vertical lines and `horch` sets the same for horizontal lines.

The `box` call is actually a macro, and is shorthand for the more general `wborder` function:

```
int border(WINDOW *win, chtype ls, chtype rs, chtype ts, chtype bs,
           chtype tl, chtype tr, chtype bl, chtype br);
```

The arguments are as follows:

+   * `ls`—Left side
+   
+   * `rs`—Right side
+   
+   * `ts`—Top side
+   
+   * `bs`—Bottom side
+   
+   * `tl`—Top-left corner
+   
+   * `tr`—Top-right corner
+   
+   * `bl`—Bottom-left corner
+   
+   * `br`—Bottom-right corner

Both the `box` and the `wborder` calls draw an outline on the window along its left, right, top, and bottom margins.

Use the `hline` function to draw a horizontal line of arbitrary length on the current window; `vline`, similarly, draws a vertical line of arbitrary length.

```
int hline(chtype ch, int n);
int vline(chtype ch, int n);
```

By following ncurses' function naming convention, you can also specify a window in which to draw lines using the functions listed here:

```
int whline(WINDOW *win, chtype ch, int n);
int wvline(WINDOW *win, chtype ch, int n);
```