```
```
71 
72 GnomeCanvasPoints *makeOriginArrow(gint h,gint v)
73 {
74     int i;
75     GnomeCanvasPoints *points;
76     static const gint xy[16] = {
77         0,-2,-2.0,-1.0,-1.2, 1.2, 1.0, 2.0, 0,-2
78     };
79 
80     points = gnome_canvas_points_new(8);
81     for(i=0; i<16; i += 2) {
82         points->coords[i] = (xy[i] * h);
83         points->coords[i+1] = (xy[i+1] * v);
84     }
85     return(points);
86 }
87 gint eventDelete(GtkWidget *widget,
88          GdkEvent *event,gpointer data) {
89     return(FALSE);
90 }
91 gint eventDestroy(GtkWidget *widget,
92          GdkEvent *event,gpointer data) {
93     gtk_main_quit();
94     return(0);
95 }
```
```

This example creates three arrow items and applies an affine transformation to each one. The resulting display is shown in Figure 9.12.

![](bbox=[0.12, 0.51, 0.55, 0.69])

An affine transform is an array of 6 numbers, as defined on line 22. When an affine is applied to a graphic object, this array of numbers is applied to each point in the object—thus transferring all of its points to another location. There are some GNOME functions that can be used to initialize the array for certain standard affine operations.

The arrows are all created by a call to the function makeOriginArrow() on line 72. This arrow is slightly different from the one in the previous example because this one places the origin—the (0,0) point—at the center of the arrow. To have the