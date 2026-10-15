# 6.4.3 Building Programs

All programs using NCurses must include the <ncurses.h> header file and the standard C I/O library header file <stdio.h>. The header file <ncurses.h> is often just a symbolic link to <curses.h>, so they are often interchangeable. Because the NCurses library is not in the linker’s standard set of libraries, you have to build explicitly with -lncurses in the command (following all files that reference NCurses symbols):

```
$ gcc -o myprog myprog.c -lncurses
```

# 6.4.4 A Core Repertoire of Functions

This is not intended to be a comprehensive tutorial on NCurses. For that you should consult any of the several on-line reference manuals or tutorials. The objective here is to explain the underlying concepts of the core library and to describe many of the functions that it provides. Below is a collection of the most important, and basic, representative functions for terminal configuration, cursor movement, output and input.

# Configuration Functions

+   initscr() Initialize the curses library and create a logical screen.
+   endwin() Turn off curses and reset the screen.
+   wrefresh(win) Draw what is in the logical window win into the physical display. Remember that refresh() is the same as wrefresh(stdscr).
+   clear() Clear the screen.
+   keypad(stdscr,TRUE) Enable use of function and keypad keys (arrows, F1, ...)

# Output and Cursor Movement

+   move(r,c) Move the cursor to screen position (r,c).
+   getyx(win,y,x) Get the current cursor position. This is a macro so y and x do not have to be passed by address.
+   addch(c) Draw character c on the screen at the current cursor position, advancing the cursor to the end of the character. If c is a tab, newline, or backspace, the cursor is moved appropriately within the window. It wraps if it reaches the right margin.
+   addstr(str) Draw the character string str on the screen at the current cursor position, advancing the cursor to the end of the string. It is equivalent to calling addch() for every character in the string.
+   addnstr(str, n) Like addstr(), except that at most n characters of str will be written. If n is -1, then the entire string will be added, up to the maximum number of characters that will fit on the line, or until a terminating null is reached. Thus, addstr(str) is the same as addnstr(str,-1).