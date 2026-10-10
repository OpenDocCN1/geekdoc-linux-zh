```
20
21
22
23
24
25
26
27
28
29
30
31
32
33
34
35
36
37
38
39
40
41
42
43
44
45
46
47
48
49
50
51
52
53
54
55
56
57
58
59
60
61
62
63
64
65
66
67
68
69
70

gnome_init("pixmap", "1.0", argc, argv);
app = gnome_app_new("pixmap", "Pimaxps Etcetera");
gtk_signal_connect(GTK_OBJECT(app), "delete_event",
			GTK_SIGNAL_FUNC(eventDelete), NULL);
gtk_signal_connect(GTK_OBJECT(app), "destroy",
			GTK_SIGNAL_FUNC(eventDestroy), NULL);

area = gtk_drawing_area_new();
gtk_widget_set_usize(area, WIDTH, HEIGHT);
gnome_app_set_contents(GNOME_APP(app), area);
gtk_signal_connect(GTK_OBJECT(area), "event",
			GTK_SIGNAL_FUNC(eventDraw), NULL);

gtk_widget_show_all(app);
gtk_main();
exit(0);
}
gboolean eventDraw(GtkWidget *widget,
		GdkEvent *event, gpointer data) {
GdkBitmap *mask;
GdkPixmap *pixmap;
GtkStyle *style;
GdkFont *font = gdk_font_load("10x20");
static GdkPoint points[] = {
	{ 210, 253 },
	{ 220, 245 },
	{ 220, 252 },
	{ 295, 252 },
	{ 295, 254 },
	{ 220, 254 },
	{ 220, 260 },
};

style = gtk_widget_get_style(widget);
pixmap = gdk_pixmap_create_from_xpm_d(widget->window,
		&mask, &style->bg[GTK_STATE_NORMAL],
		(gchar **)logo);

gdk_draw_pixmap(widget->window,
		widget->style->black_gc,
		pixmap,
		0,0,
		257,303);

gdk_draw_pixmap(widget->window,
		widget->style->black_gc,
		pixmap,
		70,60,
```