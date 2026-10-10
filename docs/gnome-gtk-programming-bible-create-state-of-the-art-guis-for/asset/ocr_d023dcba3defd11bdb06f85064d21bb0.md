```
```text
98	gnome_init("menumdi","1.0",argc,argv);
99	mdi = gnome_mdi_new("menumdi","Menu MDI");
100	gnome_mdi_set_menubar_template(GNOME_MDI(mdi),
101			mainMenu);
102	g_signal_connect(mdi,"destroy",
103			G_TYPE_FUNC(eventDestroy),NULL);
104
105	addChild("First");
106	addChild("Second");
107	addChild("Third");
108	addChild("Last");
109
110	gnome_mdi_open_toplevel(GNOME_MDI(mdi));
111
112	gtk_main();
113	exit(0);
114	}
115	static void addChild(gchar *name)
116	{
117		GnomeMDIGenericChild *child;
118		child = gnome_mdi_generic_child_new(name);
119		gnome_mdi_add_child(GNOME_MDI(mdi),
120			GNOME_MDI_CHILD(child));
121
122		gnome_mdi_generic_child_set_view_creator(child,
123			createView,name);
124		gnome_mdi_generic_child_set_label_func(child,setLabel,
125			NULL);
126		gnome_mdi_add_view(GNOME_MDI(mdi),
127			GNOME_MDI_CHILD(child));
128	}
129	static GtkWidget *createView(GnomeMDIChild *child,
130		gpointer data)
131	{
132		gchar *name;
133		char str[80];
134		GtkWidget *view;
135
136		name = (gchar *)data;
137		sprintf(str,"View of the %s widget",name);
138		view = gtk_label_new(str);
139		gtk_widget_set_usize(view,250,100);
140		if(!strcmp(name,"First"))
141			firstView = view;
142		else if(!strcmp(name,"Second"))
143			secondView = view;
144		else if(!strcmp(name,"Third"))
145			thirdView = view;
146		else
147			lastView = view;
148		return(view);
149	}
150	static GtkWidget *setLabel(GnomeMDIChild *child,
151```
```