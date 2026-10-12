
## 278 Appendix A = NCurses Library Reference

```c
char bgchar;
int bgcolor.x;
short fore_back;
char colors[8] = { "Black"
```

Sample output:

Background `ctype` is `0x200120`

Background character is `0x20` or `' '`

Background color is `1`

Foreground color is White

Background color is Blue

## Appendix A ■ NCurses Library Reference 279

Other attributes found:

Bold

## Also See

`bkdget()`, `attr_get()`, `pair_content()`, Appendix C

## `getch()`

The `getch()` function reads a single character input from the keyboard.

## Man Page Formats

```
int getch(void);
int wget(WINDOW *win);
int mvgetch(int y, int x);
int mvgetch(WINDOW *win, int y, int x);
```

## Format Reference

The function has no arguments; refer to the entries for `w`, `mv`, and `mvw` elsewhere in this appendix for more information on the `win`, `y`, and `x` arguments.

## Return Value

Under typical operation, `getch()` returns an `int` value equal to the key pressed, such as a specific character, symbol, control code, and so on.

When the `keypad()` function is TRUE for a specific window, a `getch()` call referencing that window can also return special keys on the keyboard. Refer to Appendix D for a list of these keys.

When the `nodelay()` function is TRUE for a specific window, `getch()` calls referencing that window return ERR when a key is not waiting in the input queue. Otherwise the `int` key is returned as normal.

## Notes

It is not necessary to call `refresh()` after the `getch()` function as `getch()` naturally echoes its input to the screen. Also see `echo()`.

The functions listed in Table A-6 affect the behavior and return value of `getch()`. (Refer to each entry elsewhere in this appendix for details.)

## 280 Appendix A Ncurses Library Reference

Ncurses has only one input queue; therefore, it may seem bizarre that `wget()` has an argument. This argument isn’t used to direct input from a particular window, but rather for the selective application of specific input filters. The functions that apply such filtering are `intrflush()`, `keypad()`, `meta()`, `nodelay()`, and `timeoutout()`, as listed in Table A-6.

The `wget()` also functions which window is checked for changes and that window is then refreshed. For example, by specifying `wget(two)`, you get a character from the keyboard and refresh the window.

To apply a window-specific input modification to `wget()`, use `strscr`, the standard screen.

**Table A-6:** Ncurses functions that affect input

| FUNCTION ON/OFF | DESCRIPTION |
|---|---|
| `cbreak()`<br>`nocbreak()` | Disables text line buffering and erase/kill character processing |
| `echo()`<br>`noecho()` | Controls display (echo) of its text as input |
| `halfdelay()` | Similar to break mode, with a timeout value |
| `intrflush(win, TRUE)`<br>`intrflush(win, FALSE)` | Activates text flush on interrupt key input |
| `keypad(win, TRUE)`<br>`keypad(win, FALSE)` | Allows special keyboard keys to be input; refer to Appendix D |
| `meta(win, TRUE)`<br>`meta(win, FALSE)` | Determines whether 7 or 8 bits of keyboard input are read |
| `nodelay(win, TRUE)`<br>`nodelay(win, FALSE)` | Transforms get() into a nonblocking call |
| `timeout(win, TRUE)`<br>`timeout(win, FALSE)` | Controls a delay after Esc key |
| `raw()`<br>`noraw()` | Disables all keyboard buffering and key traps; enters raw mode text processing |
| `qiflush()`<br>`qiflush()` | Flushes input on the SUSP, QUIT, and INTR keys |
| `timeout(delay)` | Similar to break (and halfdelay) mode but with a timeout value |
| `typeahead()` | Enables/disables typeahead on refresh |

## Appendix A ■ NCurses Library Reference 281

`echo()`/`nocho()` functions control whether `get()` displays its input on the screen. Normally, `get()` displays each character typed as input; `refresh()` is required.

To turn `get()` into a non-blocking call (meaning `getch()` does not wait for a key, use `nodelay()`).

To read alphanumeric keys on the keyboard, use `keypad()` function. Input modification functions that are not window-specific apply to all input for `getch()`, as well as `getstr()`.
