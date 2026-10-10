
There is an example of using a pair of GtkAdjustment objects to control vertical and horizontal scroll bars in “The Layout Container” section in Chapter 5.

## GtkAlignment

This is a container widget that is capable of controlling the size of a single child widget. The scale values are from 0.0 to 1.0, indicating the maximum amount the child can expand to fill the space allocated to the GtkAlignment widget. The align values determine the x and y positions relative to the top left and bottom right corners of the GtkAlignment rectangle. The align values are from 0.0 to the top or left side, and 1.0 for the bottom or right side.

### Inheritance

GtkAlignment -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### Functions

```c
GtkType gtk_alignment_get_type(void)
GtkWidget *gtk_alignment_new(gfloat xalign, gfloat yalign, gfloat xscale, gfloat yscale)
void gtk_alignment_set(GtkAlignment *alignment, gfloat xalign, gfloat yalign, gfloat xscale, gfloat yscale)
```

The following code inserts a GtkButton widget into a GtkAlignment widget. The x alignment is set to 1.0, which keeps the button against the right edge. The y alignment is 0.5, keeping the widget vertically centered. The scale value is set to 0.15 in both directions, which limits the expansion of the button to no more than 15 percent of the area made available to it. Figure 21-2 shows the default size on the left where the GtkAlignment widget sized itself to the size that the button requested. The window on the right shows the result of expanding the window.

```c
static GtkWidget *makeWidget()
{
    GtkWidget *alignment;
    GtkWidget *button;
    button = gtk_button_new_with_label("The Button Label");
    alignment = gtk_alignment_new(1.0, 0.5, 0.15, 0.15);
    gtk_container_add(GTK_CONTAINER(alignment), button);
    return (alignment);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_563_0.png)

## GtkArrow

This is a simple arrowhead widget that points up, left, down, or right.

### Inheritance

GtkArrow -> GtkMisc -> GtkWidget -> GtkObject

### Functions

```c
GtkType gtk_arrow_get_type(void)
GtkWidget *gtk_arrow_new(GtkArrowType arrow_type, GtkShadowType shadow_type)
void gtk_arrow_set(GtkArrow *arrow, GtkArrowType arrow_type, GtkShadowType shadow_type)
```

### Enums

```c
typedef enum {
    GDK_ARROW_UP,
    GDK_ARROW_DOWN,
    GDK_ARROW_LEFT,
    GDK_ARROW_RIGHT
} GtkArrowType;

typedef enum {
    GTK_SHADOW_NONE,
    GTK_SHADOW_IN,
    GTK_SHADOW_OUT,
    GTK_SHADOW_ETCHED_IN,
    GTK_SHADOW_ETCHED_OUT
} GtkShadowType;
```

The following function creates the left-pointing arrow in Figure 21-3, drawn so that the shadowing makes it appear indented.

```c
static GtkWidget *makeWidget()
{
    GtkWidget *arrow;
    arrow = gtk_arrow_new(GTK_ARROW_LEFT, GTK_SHADOW_IN);
    return (arrow);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_564_0.png)

## GtkAspectFrame

This container widget wraps a single widget in a frame with a label, and imposes an aspect ratio on the child widget.

### Inheritance

GtkAspectFrame -> GtkFrame -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### Functions

```c
GtkType gtk_aspect_frame_get_type(void)
GtkWidget *gtk_aspect_frame_new(const gchar *label, gfloat xalign, gfloat yalign, gfloat ratio, gint obey_child)
void gtk_aspect_frame_set(GtkAspectFrame *aspect_frame, gfloat xalign, gfloat yalign, gfloat ratio, gint obey_child)
```

The following example encloses a GtkLabel inside a GtkAspectFrame. The Boolean value **obey_child** is set to TRUE, so the value of **ratio** is ignored; instead, the **ratio** value is derived from the label’s preferred size. Values of **xalign** and **yalign** set the preferred position as 60 percent of the distance from the top and the left. Figure 21-4 shows the widget as it first appears, and after it is resized. The window is stretched further horizontally than vertically. Essentially, the widget resized itself so that it is as large as possible, while maintaining the same aspect ratio (leaving 60 percent of the space on the left and 40 percent on the right).

```c
static GtkWidget *makeWidget()
{
    GtkWidget *aspectframe;
    GtkWidget *label;

    label = gtk_label_new("The Label Text");
    aspectframe = gtk_aspect_frame_new("Table", 0.6, 0.6, 1.0, TRUE);
    gtk_container_add(GTK_CONTAINER(aspectframe), label);
    return (aspectframe);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_565_0.png)

**Figure 21-4:** An aspect frame maintains the aspect ratio of child widgets

## GtkBin

This is a base class for a container widget that has only one child. This class contains code common to all widgets that contain only a single child widget.

### Inheritance

GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### Functions

```c
GtkType gtk_bin_get_type(void)
```

## GtkBox

This is the **base class** of GtkHBox and GtkVBox. It has the code necessary to maintain the contained list of widgets, but it does not position them.

### Inheritance

GtkBox -> GtkContainer -> GtkWidget -> GtkObject

### Functions

```c
GtkType gtk_box_get_type(void)
void gtk_box_pack_end(GtkBox *box, GtkWidget *child, gboolean expand, gboolean fill, guint padding)
void gtk_box_pack_end_defaults(GtkBox *box, GtkWidget *child)
void gtk_box_pack_start(GtkBox *box, GtkWidget *child, gboolean expand, gboolean fill, guint padding)
void gtk_box_pack_start_defaults(GtkBox *box, GtkWidget *child)
void gtk_box_query_child_packing(GtkBox *box, GtkWidget *child, gboolean *expand, gboolean *fill, guint *padding, GtkPackType *pack_type)
void gtk_box_reorder_child(GtkBox *box, GtkWidget *child, gint position)
void gtk_box_set_child_packing(GtkBox *box, GtkWidget *child, gboolean expand, gboolean fill, guint padding, GtkPackType pack_type)
void gtk_box_set_homogeneous(GtkBox *box, gboolean homogeneous)
void gtk_box_set_spacing(GtkBox *box, gint spacing)
```

### Enum

```c
typedef enum {
    GTK_PACK_START,
    GTK_PACK_END
} GtkPackType;
```

## GtkButton

This is a window with a text or pixmap label inside a frame. It can respond to the mouse.

### Inheritance

GtkButton -> GtkBin -> GtkContainer -> GtkWidget -> GtkObject

### Functions

```c
void gtk_button_clicked(GtkButton *button)
void gtk_button_enter(GtkButton *button)
GtkReliefStyle gtk_button_get_relief(GtkButton *button)
GtkType gtk_button_get_type(void)
void gtk_button_leave(GtkButton *button)
GtkWidget *gtk_button_new(void)
GtkWidget *gtk_button_new_with_label(const gchar *label)
void gtk_button_pressed(GtkButton *button)
void gtk_button_released(GtkButton *button)
void gtk_button_set_relief(GtkButton *button, GtkReliefStyle newrelief)
```

### Enum

```c
typedef enum {
    GTK_RELIEF_NORMAL,
    GTK_RELIEF_HALF,
    GTK_RELIEF_NONE,
} GtkReliefStyle;
```

### Signals

```c
"clicked"     void cb(GtkWidget *, gpointer)
"enter"       void cb(GtkWidget *, gpointer)
"leave"       void cb(GtkWidget *, gpointer)
"pressed"     void cb(GtkWidget *, gpointer)
"released"    void cb(GtkWidget *, gpointer)
```

The GtkButton object was used throughout the book, so there are examples of it in almost every chapter. In particular, see Chapters 3 and 4.

## GtkButtonBox

This is the base class that holds the common functions for GtkHButtonBox and GtkVButtonBox. These are container widgets specifically designed to manage a collection of buttons. GtkButtonBox has a number of control functions that you can use to set the sizes and positions of the buttons.

### Inheritance

GtkButtonBox -> GtkBox -> GtkContainer -> GtkWidget -> GtkObject

### Functions

```c
void gtk_button_box_child_requisition(GtkWidget *widget, int *nvis_children, int *width, int *height)
void gtk_button_box_get_child_padding(GtkButtonBox *widget, gint *ipad_x, gint *ipad_y)
void gtk_button_box_get_child_padding_default(gint *ipad_x, gint *ipad_y)
void gtk_button_box_get_child_size(GtkButtonBox *widget, gint *width, gint *height)
void gtk_button_box_get_child_size_default(gint *width, gint *height)
GtkButtonBoxStyle gtk_button_box_get_layout(GtkButtonBox *widget)
gint gtk_button_box_get_spacing(GtkButtonBox *widget)
GtkType gtk_button_box_get_type(void)
void gtk_button_box_set_child_padding(GtkButtonBox *widget, gint ipad_x, gint ipad_y)
void gtk_button_box_set_child_padding_default(gint ipad_x, gint ipad_y)
void gtk_button_box_set_child_size(GtkButtonBox *widget, gint width, gint height)
void gtk_button_box_set_child_size_default(gint width, gint height)
void gtk_button_box_set_layout(GtkButtonBox *widget, GtkButtonBoxStyle layout_style)
void gtk_button_box_set_spacing(GtkButtonBox *widget, gint spacing)
```

### Enum

```c
typedef enum {
    GTK_BUTTONBOX_DEFAULT_STYLE,
    GTK_BUTTONBOX_SPREAD,
    GTK_BUTTONBOX_EDGE,
    GTK_BUTTONBOX_START,
    GTK_BUTTONBOX_END
} GtkButtonBoxStyle;
```

## GtkCalendar

The GtkCalendar widget displays one month. The user can select the month, year, and then select a specific day of the month.

### Inheritance

GtkCalendar -> GtkWidget -> GtkObject

### Functions

```c
void gtk_calendar_clear_marks(GtkCalendar *calendar)
void gtk_calendar_display_options(GtkCalendar *calendar, GtkCalendarDisplayOptions flags)
```
