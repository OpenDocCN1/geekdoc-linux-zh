
Line 61 calls the function `fillString()`, defined on line 101, to list the method used for filling regions of the window. Table 11-3 lists the fill functions, in terms of the fields in the `GdkGCValues` struct, and describes how each uses the pixmaps. The default is `GDK_SOLID` to fill the region with a solid color.

### Table 11-3 Functions Used for Filling Regions

| Function | Description |
| :--- | :--- |
| GDK_SOLID | Every pixel in the area is painted the foreground color. The pixmaps have no effect. |
| GDK_TILED | The tile pixmap is copied to the destination in such a way that it fills the entire area. The upper-left corner of the tile pixmap is positioned at the upper-left corner of the area to be filled. If the pixmap is too small, it is repeated both vertically and horizontally until the entire area is filled. |
| GDK_STIPPLED | The stipple pixmap is used as a mask to paint the area. The stipple pixmap must have a depth of one—that is, one bit per pixel. Where a stipple bit is set to 1, the foreground color is drawn. Where a stipple bit is set to 0, the pixel is left unchanged. |
| GDK_OPAQUE_STIPPLED | The stipple pixmap is used as a mask to paint the area. The stipple pixmap must have a depth of one—that is, one bit per pixel. Where a stipple bit is set to 1, the foreground color is drawn. Where a stipple bit is set to 0, the background color is drawn. |

Line 62 displays the subwindow mode by calling the function `subwindowString()`, defined on line 111. If the setting is `GDK_CLIP_BY_CHILDREN`, any drawing to the window does not occur in the regions covered by any child windows. (In other words, this window cannot cover a child window.) The other option is `GDK_INCLUDE_INFERIORS`, which directs the drawing to ignore any child windows and simply draw right over them. (In other words, this window covers its child windows).

Lines 64 through 67 display the x and y origin points for tiling, stippling, and clipping. The default for all of these values is zero. The default has tiling begin by laying the first tile in the upper-left corner of the window—at coordinate point (0,0) of the drawable (not of a figure being drawn on it). The settings can be used to position the first tile to fit with the figure being drawn, as in the examples later in this chapter. Another reason you might want to do this is for symmetry. For example, if you have a window that is 200 pixels wide and you are using a tile that is 75 pixels wide, you may want to set the horizontal origin of tiling to -25 causing the tile trimming to be the same on both sides of the window. The origin of the clip mask can be repositioned the same way.

Line 68 displays whether or not pixel-copying failure (due to an obscured window) should generate an interrupt. When copying pixels from a window onto the screen, the copy may fail partially or completely if the originating window is partially or completely obscured. This is a consequence of the application being responsible for updating the window---the server is not required to keep a copy of obscured pixels. A `GdkEventExpose` event is issued when the copy fails, and a `GdkEventNoExpose` event is issued if it succeeds.

Lines 70 through 76 display the settings that control line drawing. The line width is measured as the number of pixels, with zero being the default of a single-pixel width. While a line of width 0 and 1 show up alike on the display, a line defined as a width of 0 can be displayed only as a solid line. A nonzero width line can be drawn as a solid line, or it can be in one of several dashed forms, as shown in the function `lineStyleString()` on line 119. A line that is wider than one pixel can have one of four different styles at its end, and one of three different styles where two lines join at an angle. I provide examples of these styles later in this chapter.

The output from this program varies from one system to another because of differences in graphic capabilities. Also the default black color, white color, font size, and line styles may differ. The following is an example of typical output:

```
foreground RGB: 62900 49151 35864 (0x00007FFF)
background RGB: 24744 2055 0 (0x00000001)
font id: 33554437 ascen: 11 descen: 3
pixel drawing function: copy
fill method: solid
subwindow mode: clip by children
tiling/stripping origin: (0,0)
clipping origin: (0,0)
graphics exposures: False
line width: 0
line style: solid
cap style: not last
join style: miter
```

## Setting the Color of a Widget

The following program uses numeric values for red, green, and blue to create a color in the form of a `GdkColor` object. Then the color is inserted as the foreground into a graphics context (a `GdkGC` object). The graphics context is used to fill a rectangular area. A timer causes rectangles of different colors to be painted continuously to the window. Please note that the color, size, and location of each rectangle are random.

```c
1 /* flasher.c **/
2 #include <gnome.h>
3
4 gint eventDelete(GtkWidget *widget,
                   GdkEvent *event,gpointer data);
5 gint eventDestroy(GtkWidget *widget,
                   GdkEvent *event,gpointer data);
6 gint drawRandomRectangle(gpointer data);
7
8 #define WIDTH 400
9 #define HEIGHT 300
10 #define INTERVAL 30
11
12 int main(int argc, char *argv[])
13 {
14     GtkWidget *app;
15     GtkWidget *area;
16
17     gnome_init("flasher","1.0",argc,argv);
18     app = gnome_app_new("flasher","Creating Colors");
19     gtk_signal_connect(GTK_OBJECT(app),"delete_event",
                GTK_SIGNAL_FUNC(eventDelete),NULL);
20     gtk_signal_connect(GTK_OBJECT(app),"destroy",
                GTK_SIGNAL_FUNC(eventDestroy),NULL);
21
22     area = gtk_drawing_area_new();
23     gtk_widget_set_usize(area,WIDTH,HEIGHT);
24     gnome_app_set_contents(GNOME_APP(app),area);
25     gtk_timeout_add(INTERVAL,drawRandomRectangle,area);
26
27     gtk_widget_show_all(app);
28     gtk_main();
29     exit(0);
30 }
31
gint drawRandomRectangle(gpointer data)
32 {
33     static GdkColormap *colormap = NULL;
34     static GdkGC *gc = NULL;
35     GdkColor color;
36     GtkWidget *widget = GTK_WIDGET(data);
37     gint x = 20;
38     gint y = 20;
39     gint width = 40;
40     gint height = 40;
41
42     if(colormap == NULL) {
         colormap = gdk_colormap_get_system();
```

```c
48     gc = gdk_gc_new(widget->window);
49 }
50
51 color.red += ((double)rand() * 0xFFFF) / RAND_MAX;
52 color.green += ((double)rand() * 0xFFFF) / RAND_MAX;
53 color.blue += ((double)rand() * 0xFFFF) / RAND_MAX;
54 gdk_color_alloc colormap,&color;
55
56 gdk_gc_set_foreground(gc,&color);
57
58 x = ((double)rand() * WIDTH) / RAND_MAX - (WIDTH/4);
59 y = ((double)rand() * HEIGHT) / RAND_MAX - (HEIGHT/4);
60 width = ((double)rand() * (WIDTH/2)) / RAND_MAX;
61 height = ((double)rand() * (HEIGHT/2)) / RAND_MAX;
62
63 gdk_draw_rectangle(widget->window,
64 gc,
65 TRUE,
66 x,y,
67 width,height);
68 return(TRUE);
69 }
70
71 gint eventDelete(GtkWidget *widget,
72 GdkEvent *event,gpointer data) {
73 return(FALSE);
74 }
75
76 gint eventDestroy(GtkWidget *widget,
77 GdkEvent *event,gpointer data) {
78 gtk_main_quit();
79 return(0);
79 }
```

Lines 26 through 29 create the drawing area that is used to display the rectangles, and attaches the function `drawRandomRectangle()` to a timer. The interval value, defined on line 12, is set to 30 milliseconds. The area widget is passed to the callback function as the data. The function `drawRandomRectangle()`, beginning on line 35, uses the random number generator in the creation of a color and draws one rectangle.

The system color map is retrieved by the call to `gdk_colormap_get_system()` on line 47. The local variable color map is defined as static, so it is only necessary for the color map to be retrieved the first time the function is called. The call to `gdk_gc_new()` on line 48 creates a new graphics context that is suitable for drawing to that particular window.

There is a reason that a specific window is used in the call to `gdk_gc_new()` that creates a new graphics context. There are constraints of sizes, pixel depths, and so on that can vary from one window to the next. This happens quite often in X because any one program may have windows open simultaneously on two or more workstations.
