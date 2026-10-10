The bitmap is stored as C source code in the file `stipple.xbm`. It contains height and width information along with an array of bits with one bit per pixel:

```
```
#define stipple_width 16
#define stipple_height 16
static unsigned char stipple_bits[] = {
    0x00, 0x20, 0xaa, 0x2a, 0x54, 0x25, 0xaa, 0x2a,
    0x54, 0x25, 0xaa, 0x2a, 0x54, 0x25, 0x00, 0x00,
    0xfc, 0x3f, 0x1c, 0x00, 0x9c, 0x7f, 0x3c, 0x00,
    0xef, 0xfc, 0x0e, 0x00, 0xce, 0x3f, 0x00, 0x20};
```
```

The following program uses stippling to draw two rectangles. One rectangle is drawn so that it is transparent — that is, the pixels corresponding to the 1 bits are drawn in the foreground color, while the ones corresponding to the 0 bits are not drawn. The second rectangle is drawn with the 1 bits being the foreground color and the 0 bits being the background color — all pixels are drawn so it is opaque.

```
```
1  /** stipple.c **/
2  #include <gnome.h>
3
4  #include "stipple.xbm"
5  #include "terminal.xpm"
6
7  gint eventDelete(GtkWidget *widget,
8                  GdkEvent *event,gpointer data);
9  gint eventDestroy(GtkWidget *widget,
10                 GdkEvent *event,gpointer data);
11  gboolean eventDraw(GtkWidget *widget,
12                   GdkEvent *event,gpointer data);
13
14 #define WIDTH 250
15 #define HEIGHT 420
16
17 int main(int argc,char *argv[])
18 {
19     GtkWidget *app;
20     GtkWidget *area;
21
22     gnome_init("stipple","1.0",argc,argv);
23     app = gnome_app_new("stipple","Stipple and Tile");
24     g_signal_connect(GTK_OBJECT(app),"delete_event",
25                     GTK_SIGNAL_FUNC(eventDelete),NULL);
26     g_signal_connect(GTK_OBJECT(app),"destroy",
27                     GTK_SIGNAL_FUNC(eventDestroy),NULL);
28
29     area = gtk_drawing_area_new();
30     gtk_widget_set_usize(area,WIDTH,HEIGHT);
31     gnome_app_set_contents(GNOME_APP(app),area);
32     g_signal_connect(GTK_OBJECT(area),"event",
33                     GTK_SIGNAL_FUNC(eventDraw),NULL);
34
35     gtk_widget_show_all(app);
```
```