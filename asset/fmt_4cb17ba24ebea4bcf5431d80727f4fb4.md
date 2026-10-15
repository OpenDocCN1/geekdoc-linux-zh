
```c
app = gnome_app_new("stipple","Stipple and Tile");

g_signal_connect(GTK_OBJECT(app),"delete_event",
                GTK_SIGNAL_FUNC(eventDelete),NULL);
g_signal_connect(GTK_OBJECT(app),"destroy",
                GTK_SIGNAL_FUNC(eventDestroy),NULL);

area = gtk_drawing_area_new();
gtk_widget_set_usize(area,WIDTH,HEIGHT);
gnome_app_set_contents(GNOME_APP(app),area);
g_signal_connect(GTK_OBJECT(area),"event",
                GTK_SIGNAL_FUNC(eventDraw),NULL);

gtk_widget_show_all(app);
```

```c
gtk_main();
exit(0);
}

gboolean eventDraw(GtkWidget *widget,
GdkEvent *event,gpointer data) {
GdkGC *gc;
GdbBitmap *mask;
GdkStyle *style;
GdkPixmap *stipple;
GdkPixmap *terminal;
GdkColormap *colormap;
GdkColor foreground;
GdkColor background;

colormap = gdk_colormap_get_system();
gc = gdk_gc_new(widget->window);
if(gdk_color_parse("blue",&foreground)) {
gdk_color_alloc(colormap,&foreground);
gdk_gc_set_foreground(gc,&foreground);
}
if(gdk_color_parse("yellow",&background)) {
gdk_color_alloc(colormap,&background);
gdk_gc_set_background(gc,&background);
}

stipple = gdk_bitmap_create_from_data(widget->window,
stipple_bits,
stipple_width,
stipple_height);
gdk_gc_set_stipple(gc,stipple);
style = gtk_widget_get_style(widget);
terminal = gdk_pixmap_create_from_xpm_d(widget->window,
&mask,
&style->bg,GTK_STATE_NORMAL,
(gchar **)terminal_sun.xpm);
gdk_gc_set_tile(gc,terminal);

gdk_gc_set_ts_origin(gc,30,30);
gdk_gc_set_tfill(gc,GDK_STIPPLED);
gdk_draw_rectangle(widget->window,
gc,
TRUE,
30,30,
200,100);

gdk_gc_set_ts_origin(gc,30,160);
gdk_gc_set_tfill(gc,GDK_OPAQUE_STIPPLED);
gdk_draw_rectangle(widget->window,
gc,
TRUE,
30,160,
200,100);

gdk_gc_set_ts_origin(gc,30,280);
gdk_gc_set_fill(gc,GDK_TILED);
gdk_draw_rectangle(widget->window,
gc,
TRUE,
30,280,
200,100);

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
