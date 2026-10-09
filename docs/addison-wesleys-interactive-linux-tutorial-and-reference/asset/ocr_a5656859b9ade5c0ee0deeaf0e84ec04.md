# Edit and Undo Commands

| | | |
|---|---|---|
| `:e filename` | (1) open an existing file named *filename*. (2) create a new file named *filename*. |
| `:! filename` | open or create a file even though changes to the current file have not been saved |
| `:w` | save the current file |
| r | replace character under the cursor and return to command mode |
| R | replace characters; remain in input mode until ` <Esc> ` |
| u | undo last change |
| U | undo all changes to current line |
| x | delete character under cursor |
| X | delete character to left of cursor |

# Command Structure

The most effective way to remember many of *vi’s* commands is *not* to remember individual commands but to remember the *command structure* instead. This command structure is presented in Figure12-37.

| Command List | Object List |
|---|---|
| w | small word forward |
| `< < > >` W | big word forward |
| change b | small word back |
| B | big word back |
| `) | sentence forward |
| `< d>` `(` | sentence back |
| delete | | |
| `}` | paragraph forward |
| `{ | paragraph back |
| `$ | to end of line |
| `< y>` 0 | to beginning of line |
| yank k | current line and line above |
| j | current line and line below |
| n[object] | affect n objects |

Figure 12-37 vi’s Command Structure