**Table 1.2** Python's String Escapes
| Escape | Meaning |
| :------- | :------- |
| \newline | Escape (i.e., ignore) the newline |
| \\ | Backslash (\) |
| \` | Single quote (') |
| \" | Double quote (" ) |
| \a | ASCII bell (BEL) |
| \b | ASCII backspace (BS) |
| \f | ASCII formfeed (FF) |
| \n | ASCII linefeed (LF) |
| \N{name} | Unicode character name |
| \r | ASCII carriage return (CR) |
| \t | ASCII tab (TAB) |
| \uhhhh | Unicode character with the given 16-bit hexadecimal value |
| \Uhhhhhhhh | Unicode character with the given 32-bit hexadecimal value |
| \v | ASCII vertical tab (VT) |
| \ooo | Character with the given octal value |
| \xhh | Character with the given hexadecimal value |

P*ython* strings are *sequences* where individual characters can be accessed by positional indexing, with the first character at index position 0. It is also possible to index from the end of the *string*, with the last character's index position being -1. For example:

```
>>> phrase = "The red balloon"
>>> phrase[0], phrase[5], phrase[-1]
('T', 'e', 'n')
```

Negative indexes are used to access characters from right to left, with the right most character position being -1, the one to the left of that at position -2, and so on.

Python sequences support *slicing*, which means that we can copy subsequences from a sequence. A slice has one, two, or three colon-separated components: the *start* (which defaults to index 0), the *end* (which defaults to the length of the sequence), and another one which we will ignore. Slices are taken from and including the *start* index up to but excluding the *end* index. Here are some examples:

```
>>> phrase = "The red balloon"
>>> phrase[:3]
```