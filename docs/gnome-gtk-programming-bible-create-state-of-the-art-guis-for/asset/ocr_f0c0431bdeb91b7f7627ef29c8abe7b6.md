| Option Name | Description |
| :-- | :-- |
| `POPT_CFLAG_PRE` | **Used with `POPT_ARG_CALLBACK` to call the callback before the parse** |
| `POPT_CFLAG_POST` | **Used with `POPT_ARG_CALLBACK` to call the callback after the parse** |

This all may seem to be a bit more complicated than necessary, but the complications are necessary only when we are doing something very special with the arguments. In almost every case, it is simply a matter of creating an array of option descriptions, a place to store the input values, and a single function call. The following program defines and accepts five command-line arguments.

```
1 /** readparm.c **/
2 #include <gnome.h>
3 
4 int toolbarParm = FALSE;
5 char *titleParm = NULL;
6 char *backgroundParm = NULL;
7 int widthParm = 100;
8 int heightParm = 50;
9 
10 struct poptOption opt[] = {
11   {
12     "title",'t',
13     POPT_ARG_STRING,
14     &titleParm,0,
15     "The text to appear on the title bar",
16     "TITLE"
17   },{
18     "width",'w',
19     POPT_ARG_INT,
20     &widthParm,0,
21     "The width of the window",
22     "WIDTH"
23   },{
24     "height",'h',
25     POPT_ARG_INT,
26     &heightParm,0,
27     "The height of the window",
28     "HEIGHT"
29   },{
30     "toolbar",'T',
31     POPT_ARG_NONE,
32     &toolbarParm,0,
33     "Display the toolbar",
34     NULL
```