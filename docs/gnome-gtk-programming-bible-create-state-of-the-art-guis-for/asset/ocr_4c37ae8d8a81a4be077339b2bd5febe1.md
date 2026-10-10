# ## A Dialog to Select Colors

There is a color-selection dialog box that enables the user to select a color. The following example program displays the dialog box and continuously updates its window to match the current setting in the dialog box.

```
```
1 /* selection.c **/
2 #include <gnome.h>
3
4 GtkWidget *makeColorBox();
5 void showColorSel(GtkWidget *widget,gpointer data);
6 void changeColor(GtkWidget *widget,
7       GtkColorSelection *colorSel);
8 void destroyColorSel(GtkWidget *widget,
       gpointer data);
10 void helpColorSel(GtkWidget *widget,gpointer data);
11
12 gint eventDelete(GtkWidget *widget,
13       GdkEvent *event,gpointer data);
14 gint eventDestroy(GtkWidget *widget,
       GdkEvent *event,gpointer data);
15
16 static GtkWidget *csDialog = NULL;
17 static GtkWidget *area;
18
19 int main(int argc,char *argv[])
20 {
21     GtkWidget *app;
22     GtkWidget *colorBox;
23
24     gnome_init("selection","1.0",argc,argv);
25     app = gnome_app_new("selection","Color Selection");
26     gtk_signal_connect(GTK_OBJECT(app),"delete_event",
27             GTK_SIGNAL_FUNC(eventDelete),NULL);
28     gtk_signal_connect(GTK_OBJECT(app),"destroy",
29             GTK_SIGNAL_FUNC(eventDestroy),NULL);
30
31     colorBox = makeColorBox();
32
33     gnome_app_set_contents(GNOME_APP(app),colorBox);
34     gtk_widget_show_all(app);
35     gtk_main();
36     exit(0);
37 }
38 GtkWidget *makeColorBox()
39 {
40     GtkWidget *colorbox;
41     GtkWidget *button;
42 }
```
```