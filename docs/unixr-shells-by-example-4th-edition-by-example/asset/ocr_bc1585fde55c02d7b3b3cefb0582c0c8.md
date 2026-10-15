# 9.19 Printing the Values of Variables in the TC Shell

# 9.19.1 The echo Command

The built-in echo command prints its arguments to standard output. The echo allows the use of numerous escape sequences that are interpreted and displayed as tabs, newlines, form feed, and so on. Table 9.21 lists the echo options and escape sequences.

The TC shell uses the style of both BSD and SVR4, but allows you to modify the behavior of the echo command by using the built-in echo_style variable; for example, set echo_style=bsd. See Table 9.22, and the manual page for echo.

Table 9.21 echo Options and Escape Sequences

Option | Meaning
--- | ---
-n | Suppresses newline at the end of a line of output

Escape Sequences
\a | Alert (bell)
\b | Backspace
\c | Print the line without a newline
\f | Form feed
\n | Newline
\r | Return
\t | Tab
\v | Vertical tab
\\ | Backslash
\nnn | The character whose ASCII code is nnn (octal)

Table 9.22 The echo_style Variable (SVR4 and BSD)

System | Behavior
--- | ---
bsd | If the first argument is -n, the newline is suppressed
both | Both -n and escape sequences are in effect (the default)
none | Recognizes neither sysv or bsd
sysv | Expands escape sequences in echo strings