```
```
19  GtkWidget *area;
20
21  gnome_init("configure","1.0",argc,argv);
22  app = gnome_app_new("configure","Resizing Rectangles");
23  gtk_signal_connect(GTK_OBJECT(app),"delete-event",
24    GTK_SIGNAL_FUNC(eventDraw),NULL);
25  gtk_signal_connect(GTK_OBJECT(app),"destroy",
26    GTK_SIGNAL_FUNC(eventDestroy),NULL);
27
28  area = gtk_drawing_area_new();
29  gtk_widget_set_usize(area,width,height);
30  gnome_app_set_contents(GNOME_APP(app),area);
31
32  gtk_signal_connect(GTK_OBJECT(area),"expose-event",
33    GTK_SIGNAL_FUNC(eventDraw),NULL);
34  gtk_signal_connect(GTK_OBJECT(area),"configure-event",
35    GTK_SIGNAL_FUNC(eventConfigure),NULL);
36
37  gtk_widget_show_all(app);
38  gtk_main();
39  exit(0);
40  }
41  gboolean eventDraw(GtkWidget *widget,
42    GdkEvent *event,gpointer data) {
43    gint xDelta = width / 5;
44    gint yDelta = height / 5;
45
46    gdk_draw_rectangle(widget->window,
47      widget->style->white_gc,
48      TRUE,
49      0,0,
50      width,height);
51
52    gdk_draw_rectangle(widget->window,
53      widget->style->black_gc,
54      TRUE,
55      xDelta,yDelta,
56      width - (2 * xDelta),height - (2 * yDelta));
57
58    xDelta *= 2;
59    yDelta *= 2;
60    gdk_draw_rectangle(widget->window,
61      widget->style->white_gc,
62      TRUE,
63      xDelta,yDelta,
64      width - (2 * xDelta),height - (2 * yDelta));
65
66    return(TRUE);
67  }
68  gboolean eventConfigure(GtkWidget *widget,
69    GdkEventConfigure *event,gpointer data) {
```
```