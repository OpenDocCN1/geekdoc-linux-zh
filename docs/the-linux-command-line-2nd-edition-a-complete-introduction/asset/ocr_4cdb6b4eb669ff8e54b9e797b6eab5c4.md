> Note: Besides the normal (0) and bold (1) character attributes, text may also be given underscore (4), blinking (5), and inverse (7) attributes as well. In the interests of good taste, many terminal emulators refuse to honor the blinking attribute, however.

# Moving The Cursor

Escape codes can be used to position the cursor. This is commonly used to provide a clock or some other kind of information at a different location on the screen, such as an upper corner each time the prompt is drawn. Here is a list of the escape codes that position the cursor:

Table 13-4: Cursor Movement Escape Sequences

| Escape Code | Action |
|---|---|
| \033[ l ; c H | Move the cursor to line l and column c |
| \033[ n A | Move the cursor up n lines |
| \033[ n B | Move the cursor down n lines |
| \033[ n C | Move the cursor forward n characters |
| \033[ n D | Move the cursor backward n characters |
| \033[ 2 J | Clear the screen and move the cursor to the upper left corner (line 0, column 0) |
| \033[ K | Clear from the cursor position to the end of the current line |
| \033[ s | Store the current cursor position |
| \033[ u | Recall the stored cursor position |

Using the codes above, we'll construct a prompt that draws a red bar at the top of the screen containing a clock (rendered in yellow text) each time the prompt is displayed. The code for the prompt is this formidable looking string:

```
PS1="\033[s\033[0;0H\033[0;41m\033[K\033[1;33m\t\033[0m\033[u]\033[u\h \W\$ "
```

Let's take a look at each part of the string to see what it does: