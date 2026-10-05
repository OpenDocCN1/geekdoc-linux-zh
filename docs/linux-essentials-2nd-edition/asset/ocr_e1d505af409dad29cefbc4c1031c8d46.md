You can move forward or backward through the file, move to a specific line, and search for information. Table 6.3 summarizes the most common ways of moving about a document using less.

# TABLE 6.3 less file-navigation commands

| Keystroke | Action |
|---|---|
| h or H | Displays help using less. |
| Page Down, spacebar, Ctrl, V, or Ctrl+F | Moves down one screen in the document. |
| Page Up, Esc+V, b, or Ctrl+B | Moves up one screen in the document. |
| Down arrow, Enter, Ctrl+N, e, or Ctrl+E, or Ctrl+j | Moves down one line in the document. |
| Up arrow, y, Ctrl+Y, P, or Ctrl+K | Moves up one line in the document. |
| xg, x<, or Esc+< | Goes to line x in the document—for instance, typing 10g displays the document's 100th line. If x is omitted, the default is 1. |
| xG, x>, or Esc+> | Goes to line x in the document. If x is omitted, the default is last. |
| xp or x% | Goes to the point x percent through the document—for instance, typing 50p goes to the document's halfway point. |
| /pattern | Searches forward for pattern in the document, starting at the current location. For instance, typing /BUGS searches for the string BUGS. |
| ?pattern | Performs a backward search, locating instances of pattern before the current location. |
| n or / | Repeats the previous search. |
| q, 0, :q, or ZZ | Quits from the less pager. |

> An earlier pager was known as more, but less adds features. This peculiar name is an example of geek humor.

The notation Esc+V refers to pressing the Esc key followed by the V key.