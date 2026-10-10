```
62 item = gnome_canvas_item_new(rootGroup,
63 gnome_canvas_rect_get_type()),
64 "x1",(double)(HORIZ * 3),
65 "y1",(double)(VERT * 3),
66 "x2",(double)(HORIZ * 5),
67 "y2",(double)(VERT * 5),
68 "fill_color","black",
69 "outline_color","white",
70 NULL);
71 gtk_signal_connect(GTK_OBJECT(item),"event",
72 (GtkSignalFunc)itemEvent,NULL);
73 
74 gtk_widget_show_all(app);
75 gtk_main();
76 exit(0);
77 }
78 static gint itemEvent(GnomeCanvasItem *item,
79 GdkEvent *event,gpointer data) {
80 if(event->type == GDK_ENTER_NOTIFY)
81 gnome_canvas_item_raise_to_top(item);
82 return(0);
83 }
84 gint eventDelete(GtkWidget *widget,
85 GdkEvent *event,gpointer data) {
86 return(FALSE);
87 }
88 gint eventDestroy(GtkWidget *widget,
89 GdkEvent *event,gpointer data) {
90 gtk_main_quit();
91 return(0);
92 }
```

![](bbox=[0.11, 0.64, 0.82, 0.89])

**Figure 9-2:** Three overlapped canvas items showing their stacking order