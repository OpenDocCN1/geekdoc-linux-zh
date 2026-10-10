# **Figure 7-8:** The XPM figure to be converted to a cursor

In the following example, two of the XPM colors (B and W) are selected to represent the visible pixel locations. The other colors (r, y, and blank) all become transparent. The window with its cursor is shown in Figure 7-9.

![](bbox=[0.12, 0.26, 0.56, 0.38])

```
```
1 /** xpmcursor.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
			  GdkEvent *event, gpointer data);
5 gint eventDestroy(GtkWidget *widget,
			  GdkEvent *event, gpointer data);
6 GdkCursor *newCursorFromXPM(char *xpm[],
			 char blackLetter, GdkColor *blackColor,
			 char whiteLetter, GdkColor *whiteColor,
			 gint xHot, gint yHot);
7
8 #include "sancha.xpm"
9
10 GdkColor green = {0, 0x0000, 0xFF, 0x0000};
11 GdkColor black = {0, 0x0000, 0x0000, 0x0000};
12
13 int main(int argc, char *argv[])
14 {
15 	GtkWidget *topLevel;
16 	GdkCursor *cursor;
17
18 	gnome_init("xpmcursor", "1.0", argc, argv);
19 	topLevel = gtk_window_new (GTK_WINDOW_TOPLEVEL);
20 	gtk_window_set_default_size (GTK_WINDOW (topLevel), 150, 150);
21
22 	gtk_signal_connect (GTK_OBJECT (topLevel), "delete_event",
			   GTK_SIGNAL_FUNC (eventDelete), NULL);
23 	gtk_signal_connect (GTK_OBJECT (topLevel), "destroy",
			   GTK_SIGNAL_FUNC (eventDestroy), NULL);
24
25 	gtk_widget_show_all (topLevel);
26```
```