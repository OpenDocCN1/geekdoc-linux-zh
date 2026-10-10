
## 代码示例与分析

```c
97          y = new_y;
98      }
99      break;
100     case GDK_BUTTON_PRESS:
101         if (event->button.button == 1)
102             gnome_canvas_item_raise_to_top (item);
103         x = event->button.x;
104         y = event->button.y;
105         break;
106     default:
107         break;
108     }
109     return (0);
110 }
111 gint eventDelete(GtkWidget *widget,
112                 GdkEvent *event,gpointer data) {
113     return(FALSE);
114 }
115 gint eventDestroy(GtkWidget *widget,
116                  GdkEvent *event,gpointer data) {
117     gtk_main_quit();
118     return (0);
119 }
```

Lines 4 and 5 include the files that hold the definition of the two images to be displayed. As described in Chapter 7, you can create XPM formatted images from another form for the purpose of compiling them directly inside your program.

Line 37 creates a GdkImLibImage by calling gdk_imlib_create_image_from_xpm(). The image is added to the canvas with the call to gnome_canvas_item_new() on line 38. The GdkImLibImage is passed as the “image” argument. The values for x and y specify the anchor point for the image within the canvas window, and the value of anchor determines which part of the image is placed at that point. The example uses GTK_ANCHOR_CENTER to place the center of the image at the anchor point. You can have it anchored at the center of one of its sides, or at one of the corners, by using one of the values from Table 9-1. There is a longer form for each of the names in the table—for example, the name GTK_ANCHOR_NORTH_EAST is the same as GTK_ANCHOR_NE.

Even though the image itself has a built-in size, it is required that you supply both height and width values. The image is scaled to fit the dimensions you specify, so if you don’t want it to scale the image automatically, you need to pass the same dimension values as those defined in the original image. Two of the three images in this example are displayed in their “actual” size, but the image that has its height and width values set on lines 69 and 70 is rescaled to the larger size automatically, as shown in Figure 9-5.

### Table 9-1
**Anchor Points that Attach an Image to a Canvas**

| Name | Anchor the Image by... |
| --- | --- |
| GTK_ANCHOR_CENTER | ...its center |
| GTK_ANCHOR_E | ...the middle of its right edge |
| GTK_ANCHOR_N | ...the middle of its top edge |
| GTK_ANCHOR_NE | ...its upper-right corner |
| GTK_ANCHOR_NW | ...its upper-left corner |
| GTK_ANCHOR_S | ...the middle of its bottom edge |
| GTK_ANCHOR_SE | ...its lower-right corner |
| GTK_ANCHOR_SW | ...its lower-left corner |
| GTK_ANCHOR_W | ...the middle of its left edge |

![](img/8bcc1ba72831c7d67cfc8b395deab95f_299_0.png)

Once your image is added to the canvas, you can delete it if you wish because GnomeCanvasItem creates its own (possibly rescaled) copy. The image created on line 37 is deleted on line 49. The other image, the one created on line 51, is not deleted until it is used in the creation of two GnomeCanvasItems. It is deleted with the call to gdk_pixmap_destroy_image() on line 75.

The callback function dragEvent() essentially is the same as the one in the previous example. In this version, the left button is selected to raise an item to the top of the display stack (by checking the button number on line 101). The left button is also the selected button for moving the item around the canvas (by checking the state bit on line 90).

## Canvas Text

Text can be used as an item displayed on a canvas. A text item has much of the same capabilities as any other item. The following example creates three text items and positions them on a canvas.

```c
/** canvastext.c **/
#include <gnome.h>

gint eventDelete(GtkWidget *widget,
              GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
              GdkEvent *event, gpointer data);
static gint dragEvent(GnomeCanvasItem *item,
                 GdkEvent *event, gpointer data);

#define WIDTH 600
#define HEIGHT 75

int main(int argc, char *argv[]) {
    GtkWidget *app;
    GtkWidget *canvas;
    GnomeCanvasGroup *rootGroup;
    GnomeCanvasItem *item;

    gnome_init("canvastext", "1.0", argc, argv);
    app = gnome_app_new("canvastext",
                        "Gnome Canvas Text");
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
                      GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy",
                      GTK_SIGNAL_FUNC(eventDestroy), NULL);

    canvas = gnome_canvas_new();
    gtk_widget_set_usize(canvas, WIDTH, HEIGHT);
    gnome_canvas_set_scroll_region(GNOME_CANVAS(canvas),
                         0.0, 0.0, WIDTH, HEIGHT);
    rootGroup = gnome_canvas_root(GNOME_CANVAS(canvas));
    gnome_app_set_contents(GNOME_APP(app), canvas);

    item = gnome_canvas_item_new(rootGroup,
                                 gnome_canvas_text_get_type(),
                                 "text", "This is on the left.",
                                 "x", (double)(WIDTH / 2),
                                 "y", (double)25,
                                 "anchor", GTK_ANCHOR_E,
                                 NULL);

    gtk_signal_connect(GTK_OBJECT(item), "event",
                       (GtkSignalFunc)dragEvent, NULL);

    item = gnome_canvas_item_new(rootGroup,
                                 gnome_canvas_text_get_type(),
                                 "text", "and this is on the right.",
                                 "x", (double)(WIDTH / 2),
                                 "y", (double)25,
                                 "anchor", GTK_ANCHOR_W,
                                 NULL);
    gtk_signal_connect(GTK_OBJECT(item), "event",
                       (GtkSignalFunc)dragEvent, NULL);

    item = gnome_canvas_item_new(rootGroup,
                                 gnome_canvas_text_get_type(),
                                 "text", "These larger red letters"
                                         " go all the way across.",
                                 "font", "12x24",
                                 "x", (double)(WIDTH / 2),
                                 "y", (double)50,
                                 "fill", "red",
                                 "anchor", GTK_ANCHOR_CENTER,
                                 NULL);
    gtk_signal_connect(GTK_OBJECT(item), "event",
                       (GtkSignalFunc)dragEvent, NULL);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

static gint dragEvent(GnomeCanvasItem *item,
                      GdkEvent *event, gpointer data) {
    static gint x;
    static gint y;
    gint new_x;
    gint new_y;

    switch(event->type) {
    case GDK_MOTION_NOTIFY:
        if(event->button.state & 0x00000100) {
            new_x = event->button.x;
            new_y = event->button.y;
            gnome_canvas_item_move(item,
                                   (double)(new_x - x),
                                   (double)(new_y - y));
            x = new_x;
            y = new_y;
        }
        break;
    case GDK_BUTTON_PRESS:
        if(event->button.button_num == 1)
            gnome_canvas_item_raise_to_top(item);
        x = event->button.x;
        y = event->button.y;
        break;
    default:
        break;
    }
    return(0);
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

The first of the three text items is created by the call to gnome_canvas_item_new() on line 36. The text itself is specified as a character string. You specify x and y coordinates and use an anchor to specify how the text is to be positioned in relation to the point used to define the text item's location. The possible anchor positions are listed in Table 9-1 (in the previous section). The first text item is attached to the point by its right side (that is, the East end).

Defined on line 46, the second text item uses the same anchor point as the first one, but it is attached to the point by its left side (that is, its West end). The two lines of text are thus joined together to look like a single line, as shown in Figure 9-6.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_302_0.png)

**Figure 9-6:** Text appearing as an item on a canvas

The third text item is defined on line 56. The text is to a point that is 50 pixels from the top of the canvas and in the horizontal center of the window. Using the anchor to attach the text to the point by its center results in centered text. The color of the text and the name of the font are specified.
