```
16 int main(int argc,char *argv[])
17 { 18 GtkWidget *app;
19 GtkWidget *area;
20
21 gnome_init("rectangles","1.0",argc,argv);
22 app = gnome_app_new("rectangles","Drawing Rectangles");
23 gtk_signal_connect(GTK_OBJECT(app),"delete_event",
24 GTK_SIGNAL_FUNC(eventDelete),NULL);
25 gtk_signal_connect(GTK_OBJECT(app),"destroy",
26 GTK_SIGNAL_FUNC(eventDestroy),NULL);
27
28 area = gtk_drawing_area_new();
29 gtk_widget_set_usize(area,WIDTH,HEIGHT);
30 gnome_app_set_contents(GNOME_APP(app),area);
31
32 gtk_signal_connect(GTK_OBJECT(area),"event",
33 GTK_SIGNAL_FUNC(eventDraw),NULL);
34
35 gtk_widget_show_all(app);
36 gtk_main();
37 exit(0);
38 }
39 gbool eventDraw(GtkWidget *widget,
40 GdkEvent *event,gpointer data) { 41 gint x;
42 gint y;
43 gint width = HORIZ * 2;
44 gint height = VERT;
45
46 x = HORIZ;
47 y = VERT;
48 gdk_draw_rectangle(widget->window,
49 widget->style->black_gc,
50 FALSE,
51 x,y,
52 width,height);
53
54 x = HORIZ * 4;
55 gdk_draw_rectangle(widget->window,
56 widget->style->white_gc,
57 TRUE,
58 x,y,
59 width,height);
60
61 x = HORIZ * 7;
62 gdk_draw_rectangle(widget->window,
63 widget->style->white_gc,
64 TRUE,
65 x,y,
66 width,height);
67 gdk_draw_rectangle(widget->window,
```