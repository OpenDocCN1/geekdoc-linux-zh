```
86	GDK_DEST_DEFAULT_DROP,
87	&canvas, 1,
88	GDK_ACTION_COPY);
89
90	gtk_box_pack_start(GTK_BOX(box), canvas, TRUE, FALSE, 0);
91	addImage(tdcontext, miniLogo, WIDTH / 2, HEIGHT / 2);
92
93	button = gtk_button_new_with_label("Text Target");
94	g_signal_connect(GTK_OBJECT(button),
95	"drag-data-received", 
96	GTK_SIGNAL_FUNC(receiveCallback), tdcontext);
97
98	gtk_drag_dest_set(button,
99	GDK_DEST_DEFAULT_MOTION |
100	GDK_DEST_DEFAULT_HIGHLIGHT |
101	GDK_DEST_DEFAULT_DROP,
102	&GButton, 1,
103	GDK_ACTION_COPY);
104	gtk_box_pack_start(GTK_BOX(box), button, TRUE, FALSE, 0);
105	return(box);
106}
107
108 void addImage(GtkWidget *box, char **xpm,
109				 gint x, gint y)
110{
111	int width;
112	int height;
113	GtkStyle *style;
114	GdkBitmap *mask;
115	GdkPixmap *pixmap;
116	GtkWidget *button;
117	GtkWidget *pixmapWidget;
118	GnomeCanvasItem *item;
119
120	style = gtk_widget_get_style(
121	GDK_WIDGET(tdcontext->app));
122	pixmap = gdk_pixmap_create_from_xpm_d(
123	GDK_WIDGET(tdcontext->app)->window,
124	&mask, &style->bg[GTK_STATE_NORMAL], xpm);
125	pixmapWidget = gtk_pixmap_new(pixmap, mask);
126	button = gtk_button_new();
127	gtk_container_add(GTK_CONTAINER(button), pixmapWidget);
128
129	sscanf(xpm[0], "#d %d", &width, &height);
130	item = gnome_canvas_item_new(tdcontext->rootGroup,
131	gnome_canvas_widget_get_type(),
132	"widget", button,
133	"x", (double) x,
134	"y", (double) y,
135	"width", (double) width + 10,
136	"height", (double) height + 10,
137	"anchor", GTK_ANCHOR_CENTER,
138	NULL);
139	g_signal_connect(GTK_OBJECT(button), "drag-data-get",
```