
![](img/8bcc1ba72831c7d67cfc8b395deab95f_352_0.png)

Figure 10-9: Trimmed pixmaps with strings and a polygon

The pixmap starts out as XPM-formatted data in the file logo.xpm and is included in the program on line 4. The call to `gdk_pixmap_create_from_xpm_d()` on line 56 converts the XPM data into a GdkPixmap.

The call to `gdk_draw_pixmap()` on line 60 draws the entire pixmap to the drawing area. The first three arguments specify the window of the drawing area, the GdkGC to be used for drawing, and the GdkPixmap to be drawn. Inside the function, the actual drawing is achieved by copying a rectangle of pixels from the pixmap to the window, so the last six arguments are the x and y source location, the x and y destination location, and the height and width of the rectangular area to be copied. On line 60, the objective is to draw the entire pixmap, so the source coordinates are (0,0). To place it in the upper-left corner of the drawing area, the destination coordinates are also (0,0). The height and width values are the ones defined in the XPM data.

> Note
> It may seem odd to you that the call to `gdk_draw_pixmap()` requires a graphics context, because all the sizes and colors are defined by the pixmap and the other arguments. It turns out that there is some hidden information inside the GdkGC object that is needed by the low-level function XCopyArea(), which copies pixels from one place to another.

The call to `gdk_draw_pixmap()` on line 67 uses the same pixmap as input, but only copies a small section of it. On line 70, the upper-left corner of the rectangle to be copied is set to (70,60). The upper-left corner of the destination rectangle is defined on line 71 to be (210,50). Line 72 sets the width of the rectangle to 90 pixels and the height to 50 pixels. As a result, only the area immediately surrounding the beak is copied to the window.

In a drawing area, you can draw right over the top of things that are there already. On line 73, there is a call to `gdk_draw_string()` that places the "Beak" text directly on top of the pixmap placed there earlier.

Lines 79 through 89 copy the right-foot section of the source bitmap to the drawing area, and then, using another string, adds a tag noting that it is the right foot. Lines 91 through 100 add an annotation to the left foot. The call to `gdk_draw_string()` draws the text. The call to `gdk_draw_polygon()` uses the set of points defined on line 45 to draw a filled arrow pointing from the text to the foot.

Lines 102 and 103 return the pixmap and the font to the system. The callback routine builds them from scratch each time it is called, so there is no need to keep it—besides, failure to return it can cause memory leaks. In a real application, it makes more sense to store both of these in static variables so they can be used again without requiring a complete rebuild.

## Resizing the Drawing Area

The drawing area may be resized, depending on the rules applied to it by its containing widget. If you ignore the size change, your drawing can leave spaces or be clipped on the right and bottom. However, you can have your drawing resize itself to fit the new window configuration.

> It may not be worth the effort to write the code that resizes the drawing. To make a drawing resizable, you need to calculate all the coordinates as a ratio of width and height of the window. Some things, such as XPM image data and text fonts, don’t rescale easily. Also, a change in the aspect ratio changes circles to ellipses and squares to rectangles.

The following example draws rectangles based on the height and width of the window, and allows for these values to change.

```c
/** configure.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget,
   GdkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget,
   GdkEvent *event,gpointer data);
gboolean eventDraw(GtkWidget *widget,
   GdkEvent *event,gpointer data);
gboolean eventConfigure(GtkWidget *widget,
   GdkEventConfigure *event,gpointer data);

static int width = 20;
static int height = 20;

int main(int argc,char *argv[])
{
   GtkWidget *app;
   GtkWidget *area;

   gnome_init("configure","1.0",argc,argv);
   app = gnome_app_new("configure","Resizing Rectangles");
   gtk_signal_connect(GTK_OBJECT(app),"delete-event",
     GTK_SIGNAL_FUNC(eventDraw),NULL);
   gtk_signal_connect(GTK_OBJECT(app),"destroy",
     GTK_SIGNAL_FUNC(eventDestroy),NULL);

   area = gtk_drawing_area_new();
   gtk_widget_set_usize(area,width,height);
   gnome_app_set_contents(GNOME_APP(app),area);

   gtk_signal_connect(GTK_OBJECT(area),"expose-event",
     GTK_SIGNAL_FUNC(eventDraw),NULL);
   gtk_signal_connect(GTK_OBJECT(area),"configure-event",
     GTK_SIGNAL_FUNC(eventConfigure),NULL);

   gtk_widget_show_all(app);
   gtk_main();
   exit(0);
}

gboolean eventDraw(GtkWidget *widget,
   GdkEvent *event,gpointer data) {
   gint xDelta = width / 5;
   gint yDelta = height / 5;

   gdk_draw_rectangle(widget->window,
     widget->style->white_gc,
     TRUE,
     0,0,
     width,height);

   gdk_draw_rectangle(widget->window,
     widget->style->black_gc,
     TRUE,
     xDelta,yDelta,
     width - (2 * xDelta),height - (2 * yDelta));

   xDelta *= 2;
   yDelta *= 2;
   gdk_draw_rectangle(widget->window,
     widget->style->white_gc,
     TRUE,
     xDelta,yDelta,
     width - (2 * xDelta),height - (2 * yDelta));

   return(TRUE);
}

gboolean eventConfigure(GtkWidget *widget,
   GdkEventConfigure *event,gpointer data) {
   width = event->width;
   height = event->height;

   return(TRUE);
}

gint eventDelete(GtkWidget *widget,
   GdkEvent *event,gpointer data) {
   return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
   GdkEvent *event,gpointer data) {
   gtk_main_quit();
   return(0);
}
```

Lines 28 through 30 create a drawing area and insert it into the main window of the application. Whenever this main window is resized, the drawing area also is resized. The callback routines are connected to the drawing area on lines 32 through 35. The "expose-event" calls `eventDraw()` whenever the figure needs to be drawn. The "configure-event" calls `Configure()` whenever the drawing area changes its height or width.

The rectangles are drawn by the callback function `eventDraw()` beginning on line 41. The values of xDelta and yDelta, used to size and position the rectangles, are calculated as fractional values of the height and width. The call to `gdk_draw_rectangle()` on line 46 uses the width and height values to clear the entire drawing area to a white background. Using the fractional values, a black rectangle is drawn on line 52 and a white one is drawn inside it on line 60. Because all dimensions are calculated from the size of the window itself, the figure is drawn to fit. Figure 10-10 shows the appearance of the window in four different sizes and shapes.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_355_0.png)

**Figure 10-10: Rectangles reshaped to fit the window**

The callback function `eventConfigure()` on line 68 is called whenever the window configuration changes. Lines 71 and 73 retrieve the new height and width values and store them until the next time the figure is drawn. There is no need to do anything else because an "expose-event" always follows a "configure-event", and `eventDraw()` is called to render the figure.

## Drawing to Memory and Animation

There are times when it is convenient to write graphics to a location in memory instead of directly to a window. One such example is when doing animation because the first step in creating a new frame is to clear the old frame. If this is done directly on the window, the animation flickers with each frame. Fortunately, it is possible to draw to a pixmap and then use it to update the entire window all at once.

The following program performs the simple animation of dropping balls from the top of the window and bouncing them off the bottom. Each ball continues to bounce lower and lower until it finally disappears off the left or right side of the window.

```c
/** animation.c **/
#include <gnome.h>
#include <math.h>

static struct ballStruct {
	double x;
	double y;
	double xVelocity;
	double yVelocity;
} ball[5];

gint eventDelete(GtkWidget *widget,
	GdkEvent *event,gpointer data);
gint eventDestroy(GtkWidget *widget,
	GdkEvent *event,gpointer data);
gint nextFrame(gpointer data);
void newBall(struct ballStruct *b);
void nextBall(struct ballStruct *b);
gint nextFrame(gpointer data);

#define WIDTH 400
#define HEIGHT 300
#define GRAVITY 0.8
#define RADIUS 5
#define DIAMETER (RADIUS * 2)
#define INTERVAL 30

int main(int argc,char *argv[])
{
	int i;
	GtkWidget *app;
	GtkWidget *area;

	gnome_init("animation","1.0",argc,argv);
	app = gnome_app_new("animation",
		"Drawing Area Animation");
	gtk_container_set_border_width(GTK_CONTAINER(app),20);
```
