![](bbox=[0.11, 0.03, 0.89, 0.41])

Figure 11.6:
String output in a window.

# *Miscellaneous Output*

The next and last group of output routines to consider are a hodgepodge of calls that draw borders and lines, clear and set the background, control output options, move the cursor, and send formatted output to an ncursees window. ncursees' "miscellaneous" output routines comprise a wide variety of calls. The most common ones are discussed in this section.

To begin with, to set a window's background property, use the set background call, `bkgd`, prototyped as follows:

```
int bkgd (const chtype ch);
```

`ch` is a logically ORed combination of the character you want to display and one or more of the video attributes previously listed. To obtain the current background setting, call

```
chtype getbkgd (WINDOW *win);
```