file or put itself in the mode you want, you can set the mode manually by pressing Esc+x and then typing the name of the mode you want to switch to. The major mode of the current buffer is listed between parentheses in the mode line. Table 6.10 lists some of the major modes available.

# **TABLE 6.10** Some XEmacs Major Modes

| Mode | Description |
| :--- | :--- |
| fundamental-mode | This is the default mode when you start XEmacs. It has no special features or key bindings. |
| nroff-mode | This mode is for editing `nroff` files before they are formatted. It redefines some indentation commands. |
| tex-mode | This mode is for editing LaTeX source files. It adds commands for inserting quotes, braces, and other characters. It will also help nicely format the file for printing. |
| outline-mode | This mode is for editing outlines. It allows you to make parts of the text invisible so that you can see the overall structure of the document. |
| c-mode | This mode is for editing C source files. It redefines commands for indentation and performs syntax highlighting—a very useful feature. |
| c++-mode | This is similar to c-mode but for C++ source files. |
| lisp-mode | This mode is for editing Lisp source files. |
| fortran-mode | This mode is for editing Fortran source files. It adds special commands for moving around and indentation. |
| asm-mode | This mode is for editing assembly source files. |

> **Tip**
> 
> You can get information about the mode you are in by selecting Mode under the Commands and Keys menu item of the help menu.

# # Minor Modes

Minor modes provide optional features that you can turn on and off as you like. You can have any number of minor modes active with any major mode. You turn minor modes on and off using the same command as for major modes. If the mode is turned off, then issuing the command will turn it on. Issuing the same command will turn it off again. In short, the command simply toggles the minor mode on and off. Some of the active minor modes are listed next to the major mode on the mode line. Table 6.11 lists some of the minor modes available.