# ## Non-Standard Icons

You can get your icons from anywhere. Just about any graphic you have can be used as a toolbar icon. Once you convert it to an XPM file, you can compile it directly into the program or load it at runtime. The toolbar in the following program mixes the three different methods of generating the icons in a toolbar.

```
```c
1  /** toolbarcustom.c **/
2  #include <gnome.h>
3
4  static char *module[] = {
5     "25 24 2 1",
6     " c None",
7     "B c Black",
8     "",
9     "                B",
10    "               B       *",
11    "               B B        *",
12    "  B B                 B B B        *",
13    "    B       B   B B B",
14    "  B B B   B B B B B B B B",
15    "  B B B   B B B B B B B B  *",
16    "  B B B   B B B B B B B B *",
17    "  B B B   B B B B B B B B *",
18    "  B B B B B B B B B B B B B B *",
19    "  B B B B B B B B B B B B B B *",
20    "  B B B B B B B B B B B B B B *",
21    "  B B B B B B B B B B B B B B *",
22    "  B B B   B B B B B B B B *",
23    "  B B B B B B B B B B B B *",
24    "  B B B B B B B B B B B B *",
25    "  B B B B B B B B B B B",
26    "  B B B     B B B B B   B",
27    "  B B B       B B B",
28    "    B B B       B B B",
29    "      B",
30    "      B",
31    "        B",
32  };
33
34 gint eventDelete (GtkWidget *widget,
35                GdkEvent *event, gpointer data);
36 gint eventDestroy (GtkWidget *widget,
37                GdkEvent *event, gpointer data);
38
39 static GnomeUIInfo toolbarFile[] = {
40    { GNOME_APP_UI_ITEM, "Redeks",
41      "Create a new file", NULL, NULL, NULL,
42      GNOME_APP_PIXMAP_FILENAME, "redeks.xpm",
43      0,0,NULL },
44    { GNOME_APP_UI_ITEM, "Open",
45      "Open an existing file", NULL, NULL, NULL,
```
```