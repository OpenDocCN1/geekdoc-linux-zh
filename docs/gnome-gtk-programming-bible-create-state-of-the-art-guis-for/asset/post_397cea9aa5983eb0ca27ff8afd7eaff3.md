
```cpp
65    gint eventDestroy(GtkWidget *widget,
66                    GdkEvent *event, gpointer data) {
67       gtk_main_quit();
68       return(0);
69    }
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_153_0.png)

![](img/8bcc1ba72831c7d67cfc8b395deab95f_153_1.png)

The function `makeHorizontalPane()` beginning on line 35 creates the paned container and inserts the two text widgets into it. The text widgets are created and filled with text on lines 41 through 52.

The call to `gtk_hpaned_new()` on line 54 creates a horizontal paned widget like the one shown in Figures 5-13 and 5-14.

The call to the function `gtk_hpaned_new()` on line 52 creates a new horizontal pane widget. On lines 56 and 57, the function `gtk_paned_add1()` adds the text widget on the left and `gtk_paned_add2()` adds the text widget to the right.

That's all there is to it. The paned widget and its two contained widgets communicate with one another about positioning and resizing. The overall window can be resized and the gutter can be shifted back and forth to make all the widgets resize together. The minimum widget size does not limit gutter movement, and it is possible to move the gutter all the way to one side or the other completely obscuring one widget and allocating the whole window to the other.

A vertical paned container is shown in Figures 5-15 and 5-16. You can achieve this configuration by changing one line of code in the example. Line 54 should look like this:

```cpp
paned = gtk_vpaned_new();
```

Everything else can stay the same. The same functions are used to add widgets to a vertical *paned* container. The `gtk_paned_add1()` function adds a widget at the top and `gtk_paned_add2()` adds a widget at the bottom.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_154_0.png)

## **Figure 5-15:** A vertical pane with two text widgets

![](img/8bcc1ba72831c7d67cfc8b395deab95f_154_1.png)

## **Figure 5-16:** A vertical pane with two text widgets

It is possible to adjust the thickness of the gutter and size of the button. For example, to produce the configuration shown in Figure 5-17, insert the following two function calls after line 54 in the above example:

```cpp
gtk_paned_set_handle_size(GTK_PANED(paned), 30);
gtk_paned_set_gutter_size(GTK_PANED(paned), 20);
```

This makes the handle into a square that is 30 pixels on a side, and sets the gutter width to 20 pixels. However, the width of the handle is limited to the width of the gutter, so the handle ends up being a rectangle of 20x30 pixels. The default handle size is 10 and the default gutter size is 6.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_155_0.png)

## The Layout Container

The layout container can hold any number of widgets. The widgets are positioned by x and y pixel offsets. There is no limit to the size of this container. It can be as tall and as wide as you like. There is also a pair of special adjustment objects, one for each axis, that can be used to specify which portions of the container are available. In effect, you are looking at a section of the container window through a porthole; the window can be moved around making different portions of it visible.

This example program creates a layout container covered with buttons and uses the positional values from a pair of scrollbars to determine which buttons are visible.

```cpp
 1 /** layout.c **/
 2 #include <gnome.h>
 3
 4 GtkWidget *makeLayout();
 5 void addButtons (GtkWidget *layout);
 6 gint eventDelete (GtkWidget *widget,
 7      GdkEvent *event, gpointer data);
 8 gint eventDestroy (GtkWidget *widget,
 9      GdkEvent *event, gpointer data);
10
11 int main (int argc, char *argv[])
12 {
13    GtkWidget *window;
14    GtkWidget *layout;
15
16    gnome_init ("layout", "1.0", argc, argv);
17    window = gtk_window_new (GTK_WINDOW_TOPLEVEL);
```

```cpp
18  gtk_window_set_default_size(GTK_WINDOW(window),
                  200,200);
19
20  gtk_signal_connect(GTK_OBJECT(window),
                 "delete_event",
                 GTK_SIGNAL_FUNC(eventDelete),
                 NULL);
21
22  gtk_signal_connect(GTK_OBJECT(window),
                 "destroy",
                 GTK_SIGNAL_FUNC(eventDestroy),
                 NULL);
23
24
25  layout = makeLayout();
26
27  gtk_container_add(GTK_CONTAINER(window),layout);
28
29  gtk_widget_show_all(window);
30
31  gtk_main();
32
33  exit(0);
34}
35
36 GtkWidget *makeLayout()
37{
38   GtkWidget *layout;
39   GtkWidget *vscroll;
40   GtkWidget *hscroll;
41   GtkWidget *table;
42   GtkAdjustment *horizAdj;
43   GtkAdjustment *vertAdj;
44
45   vertAdj = (GtkAdjustment *)gtk_adjustment_new(
                      0.0,
                      0.0,
                      1000.0,
                      1.0,
                      10.0,
                      20.0);
46
47   horizAdj = (GtkAdjustment *)gtk_adjustment_new(
                      0.0,
                      0.0,
                      1000.0,
                      1.0,
                      10.0,
                      20.0);
48
49   layout = gtk_layout_new(horizAdj,vertAdj);
50   gtk_layout_set_size(GTK_LAYOUT(layout),1000,1000);
51   addButtons(layout);
52
53   vscroll = gtk_vscrollbar_new(vertAdj);
54   hscroll = gtk_hscrollbar_new(horizAdj);
55
56   table = gtk_table_new(2,2,FALSE);
57}
```

```cpp
69 gtk_table_attach_defaults(GTK_TABLE(table),layout,
70 0,1,0,1);
71 gtk_table_attach(GTK_TABLE(table),vscroll,
72 1,2,0,1,
73 GTK_FILL,GTK_FILL,0,0);
74 gtk_table_attach(GTK_TABLE(table),hscroll,
75 0,1,1,2,
76 GTK_FILL,GTK_FILL,0,0);
77
78 return(table);
79 }
80 void addButtons(GtkWidget *layout)
81 {
82 gint i;
83 gint j;
84 GtkWidget *button;
85 gchar label[20];
86
87 for(i=100; i<1000; i += 100) {
88 for(j=100; j<1000; j+= 50) {
89 sprintf(label,"(%d,%d)",i,j);
90 button = gtk_button_new_with_label(label);
91 gtk_layout_put(GTK_LAYOUT(layout),button,i,j);
92 }
93 }
94 }
95 gint eventDelete(GtkWidget *widget,
96 GdkEvent *event,gpointer data) {
97 return(FALSE);
98 }
99 gint eventDestroy(GtkWidget *widget,
100 GdkEvent *event,gpointer data) {
101 gtk_main_quit();
102 return(0);
103 }
```

This example creates a 2x2 table that holds a layout widget in the upper-left corner, and holds scrollbars on the right and on the bottom—as shown in Figure 5-18. The layout has buttons placed at regular intervals across it. The label of each button is the values of its x and y coordinates within the layout container. So you are able to move the layout around and see all the buttons, the `GtkAdjustment` objects used by the layout are the same ones used by the scrollbar.

The `makeLayout()` function beginning on line 36 creates a table and inserts the various widgets into it. The table is a 2x2 grid with the layout in the upper left, a vertical scrollbar in the upper right, and a horizontal scrollbar in the lower left. There is nothing in the cell at the lower right.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_158_0.png)

### Figure 5-18: A layout container makes part of its window visible

Lines 45 through 58 create a pair of `GtkAdjustment` objects that are used to control the position of the layout container. There is one adjustment object for horizontal positioning and one for vertical. The function `gtk_adjustment_new()` requires six floating-point values. The first argument is the initial value, and it must be some value between the values of the second and third arguments. The second and third ones are the beginning and ending values of the position of the layout container. In this example, both the vertical and horizontal sizes are set so the values can range from 0 to 1000.

The last three arguments to `gtk_adjustment_new()` are instructions to any software elements (such as scrollbars) that will update the current `GtkAdjustment` value. The argument 1.0 is the step increment. It is the minimum amount the window can be shifted. (In this example, the value 1.0 just happens to correspond with 1 pixel.) The argument 10.0 is the number of units the layout is to move when it jumps (that is, when you select the trough of the scrollbar with the mouse). The last value is the size of a page in case you want the software to be capable of shifting up or down by a whole page.

The layout container is created on line 60. It is passed the two adjustment objects. To change the position of the layout container in the displayable porthole, you only need to adjust the current value of the adjustment object. Line 62 sets the size of the layout object, and line 62 calls `add_button()` to fill it with buttons. The `add_buttons()` function beginning on line 80 is a simple loop creating buttons and placing them on the layout container in a large rectangle. The buttons are hung onto the face of the layout by `gtk_layout_put()` on line 91.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_158_1.png)

Notice the call to `gtk_widget_show_all()` on line 32. This causes the named widget (in this case, the main window) and all of its child widgets to be displayed. This has the same effect as calling `gtk_widget_show()` for each individual widget.
