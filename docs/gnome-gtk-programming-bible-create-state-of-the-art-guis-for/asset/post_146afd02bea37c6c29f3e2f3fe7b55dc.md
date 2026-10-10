
```c
16 #define WIDTH 400
17 #define HEIGHT 300
18
19 int main(int argc,char *argv[])
20 {
21     GtkWidget *window;
22     GtkWidget *fixed;
23
24     gnome_init("fixed", "1.0",argc, argv);
25     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
26     gtk_window_set_default_size(GTK_WINDOW(window),
27         WIDTH,HEIGHT);
28
29     gtk_signal_connect(GTK_OBJECT(window),
30         "delete_event",
31         GTK_SIGNAL_FUNC(eventDelete),
32         NULL);
33     gtk_signal_connect(GTK_OBJECT(window),
34         "destroy",
35         GTK_SIGNAL_FUNC(eventDestroy),
36         NULL);
37
38     fixed = makeFixedContainer();
39
40     gtk_container_add(GTK_CONTAINER(window),fixed);
41     gtk_widget_show(window);
42     gtk_main();
43     exit(0);
44 }
45
46 GtkWidget *makeFixedContainer() {
47     int i;
48     static ButtonMover bm[3];
49     fixed = gtk_fixed_new();
50     gtk_widget_show(fixed);
51
52     for(i=0; i<3; i++) {
53         bm[i].fixed = fixed;
54         bm[i].button = gtk_button_new_with_label(
55             "(100,100)");
56         gtk_signal_connect(GTK_OBJECT(bm[i].button),
57             "clicked",
58             GTK_SIGNAL_FUNC(buttonClick),
59             &bm[i]);
60         gtk_widget_show(bm[i].button);
61         gtk_fixed_put(GTK_FIXED(fixed),bm[i].button,
62             100,100);
63     }
64     return(fixed);
65 }
66 void buttonClick(GtkWidget *widget,ButtonMover *bm)
67 {
68     gchar labelString[80];
69     GtkWidget *label;
70
71     gint x = (int)(random() % WIDTH);
72     gint y = (int)(random() % HEIGHT);
73     sprintf(labelString, "(%d,%d)", x, y);
74     label = GTK_WIDGET(GTK_BUTTON(bm->button)->child);
75     gtk_label_set_text(GTK_LABEL(label), labelString);
76     gtk_fixed_move(GTK_FIXED(bm->fixed), bm->button, x, y);
77 }
78 gint eventDelete(GtkWidget *widget,
79                 GdkEvent *event, gpointer data) {
80     return(FALSE);
81 }
82 gint eventDestroy(GtkWidget *widget,
83                 GdkEvent *event, gpointer data) {
84     gtk_main_quit();
85     return(0);
86 }
```

The function `makeFixedContainer()` starting on line 44 creates a fixed container and adds the three buttons to it. The container itself is created by the call to `gtk_fixed_new()` on line 49.

The fixed container has no predefined size. Instead, it automatically resizes itself to hold all of the widget positions that are added to it. In the previous example, the window holding the container was set to a fixed size by the call to `gtk_window_set_default_size()` on line 26. This forces the window to stay the same size no matter what. If this function call is taken out of the code, the displayed window starts off small. As the buttons are moved from one place to another, the container expands forcing the window to expand to hold it.

The loop beginning on line 52 creates the three buttons and adds them to the container. The call to `gtk_fixed_put()` attaches each button to the container at location (100,100). There is a `ButtonMover` struct defined on line 4 and declared as an array—one for each button—on line 47. Pointers to the button and to the fixed container are stored in the struct so they can be passed to the callback function. The callback function `buttonClick()` is used for all three buttons.

The callback function `buttonClick()` beginning on line 66 moves the selected button from one place to another. Lines 71 and 72 use a random number generator to establish a new set of x and y coordinates. Lines 73 and 74 set up the ASCII representation of the values as the label for the button. A button contains a label widget for the purpose of displaying text, so line 75 calls `gtk_label_set_text()` to change the string displayed by the button. On line 76, a call is made to `gtk_fixed_move()` with the new coordinates to reposition the button. After a few clicks on the buttons, the display looks something like the one in Figure 5-1.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_139_0.png)

The minimum size of a fixed widget is fairly easy to calculate. The width is the maximum distance from the left side of the container to the right side of each widget. Likewise, the height is the maximum distance from the top of the container to the bottom of each widget.

Widgets can be moved from one place to another. You can do this whether or not the window is actively displayed. The call to `gtk_fixed_move()` to reposition a widget has the same arguments as `gtk_fixed_put()` but does not add a widget. For example, if the widget button is already added to the fixed container, this call moves it to a new location:

```c
gtk_fixed_move(GTK_FIXED(fixed),button,25,25);
```

## The Alignment Container

This container can be used to hold a single widget and to impose some control over the widget's size and position. The contained widget changes and positions to fit inside the current size and shape of the alignment container. The widget is positioned in the container a certain percentage of the distance from the top, and a certain percentage of the distance from the left side. Also, the widget is sized as a certain percentage of the width and height of the container.

This example program centers a GtkButton widget in an alignment container:

```c
1 / ** alignment.c ** /
2 #include <gname.h>
3
4 GtkWidget *makeAlignment();
5 gint eventDelete(GtkWidget *widget,
6            GdkEvent *event, gpointer data);
7 gint eventDestroy(GtkWidget *widget,
8            GdkEvent *event,gpointer data);
9 
10 int main(int argc,char *argv[])
11 {
12     GtkWidget *window;
13     GtkWidget *alignment;
14 
15     gnome_init("alignment","1.0",argc,argv);
16     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
17     gtk_window_set_default_size(GTK_WINDOW(window),
18                 200,200);
19     gtk_signal_connect(GTK_OBJECT(window),
20                "delete_event",
21                GTK_SIGNAL_FUNC(eventDelete),
22                NULL);
23     gtk_signal_connect(GTK_OBJECT(window),
24                "destroy",
25                GTK_SIGNAL_FUNC(eventDestroy),
26                NULL);
27 
28     alignment = makeAlignment();
29 
30     gtk_container_add(GTK_CONTAINER(window),alignment);
31     gtk_widget_show(window);
32     gtk_main();
33     exit(0);
34 }
35 GtkWidget *makeAlignment()
36 {
37     GtkWidget *alignment;
38     GtkWidget *button;
39     gfloat xalign = 0.5;
40     gfloat yalign = 0.5;
41     gfloat xscale = 0.8;
42     gfloat yscale = 0.8;
43 
44     alignment = gtk_alignment_new(xalign,yalign,
45                 xscale,yscale);
46     button = gtk_button_new_with_label("Button");
47     gtk_widget_show(button);
48     gtk_container_add(GTK_CONTAINER(alignment),button);
49 
50     return(alignment);
51 }
52 gint eventDelete(GtkWidget *widget,
53                 GdkEvent *event,gpointer data)
54 {
55     return(FALSE);
56 }
57 gint eventDestroy(GtkWidget *widget,
58                 GdkEvent *event,gpointer data)
59 {
60     gtk_main_quit();
61     return(0);
62 }
```

The function `makeAlignment()` beginning on line 35 creates an alignment container holding a `GtkButton` widget. The alignment widget is created with the call to `gtk_alignment_new()` on line 43. The alignment container can contain only one widget, and the values that control its size and positioning are set when the container is constructed. The values `xalign` and `yalign` specify the position of the widget relative to the size and shape of the container. The values `xscale` and `yscale` specify the size of the widget relative to the size of the container.

The values shown on lines 38 through 41, along with the initial window size specification on line 17, cause the window in Figure 5-2 to appear. The button resizes itself to fit its container. Figure 5-3 shows the same window after the mouse was used to change its size.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_141_0.png)

**Figure 5-2**: A button being centered by a `GtkAlignment` container

![](img/8bcc1ba72831c7d67cfc8b395deab95f_141_1.png)

**Figure 5-3**: Resizing a `GtkAlignment` container resizes its widget

The two sizing numbers `xscale` and `yscale` are floating point values from 0.0 to 1.0. They size the widget to a percentage of the total height and width of the container. In the example, both values are set to 0.8, so the button covers 80 percent of the height and the width of the container. Using 1.0 for these numbers expands the button to completely fill the alignment container.

The two alignment numbers, `xalign` and `yalign`, are floating point values from 0.0 to 1.0 that represent a percentage of the distance across the container. In Figure 5-2, the button is centered because the value of both `xalign` and `yalign` is 0.5. Setting both `xalign` and `yalign` to 0.0 causes the window to look like the one in Figure 5-4. Setting both `xalign` and `yalign` to 1.0 causes the window to look like the one in Figure 5-5.
