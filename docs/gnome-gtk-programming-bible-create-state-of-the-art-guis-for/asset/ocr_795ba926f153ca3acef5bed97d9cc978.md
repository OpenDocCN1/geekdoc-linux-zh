```
58
gdk_color_alloc(colormap,&foreground);
59
gdk_gc_set_foreground(gc,&foreground);
60	}
61	if(gdk_color_parse("yellow",&background)) {
62	gdk_color_alloc(colormap,&background);
63	gdk_gc_set_background(gc,&background);
64	}
65
66	/* The MITER join */
67	gdk_gc_set_line_attributes(gc,
68	10,
69	GDK_LINE_SOLID,
70	GDK_CAP_BUTT,
71	GDK_JOIN_MITER);
72	gdk_draw_polygon(widget->window,
73	gc,
74	FALSE,
75	points,
76	(int)(sizeof(points)/sizeof(GdkPoint)));
77	gdk_draw_string(widget->window,
78	font,
79	gc,
80	points[1].x,points[1].y + 20,
81	"Miter");
82
83	/* The ROUND join */
84	for(i=0; i<3; i++)
85	points[i].x += 80;
86	gdk_gc_set_line_attributes(gc,
87	10,
88	GDK_LINE_SOLID,
89	GDK_CAP_BUTT,
90	GDK_JOIN_ROUND);
91	gdk_draw_polygon(widget->window,
92	gc,
93	FALSE,
94	points,
95	(int)(sizeof(points)/sizeof(GdkPoint)));
96	gdk_draw_string(widget->window,
97	font,
98	gc,
99	points[1].x,points[1].y + 20,
100	"Round");
101
102	/* The BEVEL join */
103	for(i=0; i<3; i++)
104	points[i].x += 80;
105	gdk_gc_set_line_attributes(gc,
106	10,
107	GDK_LINE_SOLID,
108	GDK_CAP_BUTT,
```