```
```C
32		gtk_object_set(GTK_OBJECT(clist),
33			"GtkContainer::border_width",(gulong)12,
34			"GtkCList::reorderable",(gboolean)TRUE,
35			"GtkWidget::name", "fred",
36			NULL);
37		gtk_signal_connect(GTK_OBJECT(clist),"show",
38			GTK_SIGNAL_FUNC(eventShow),NULL);
39		gnome_app_set_contents(GNOME_APP(app),clist);
40	
41		gtk_widget_show_all(app);
42		gtk_main();
43		exit(0);
44	}
45	void eventShow(GtkWidget *widget,gpointer data)
46	{
47		int i;
48		GtkArg arg[5];
49	
50		arg[0].name = "GtkCList::reorderable";
51		arg[1].name = "border_width";
52		arg[2].name = "GtkWidget::name";
53		arg[3].name = "GtkCList::n_columns";
54		arg[4].name = "row_height";
55		gtk_object_getv(GTK_OBJECT(widget),5,arg);
56		for(i=0; i<5; i++)
57		{
58			switch(arg[i].type) {
59			case GTK_TYPE_UINT:
60				g_print("%s=%u\n",arg[i].name,
61					GTK_VALUE_UINT(arg[i]));
62				break;
63			case GTK_TYPE_ULONG:
64				g_print("%s=%lu\n",arg[i].name,
65					GTK_VALUE_ULONG(arg[i]));
66				break;
67			case GTK_TYPE_FLOAT:
68				g_print("%s=%g\n",arg[i].name,
69					GTK_VALUE_FLOAT(arg[i]));
70				break;
71			case GTK_TYPE_STRING:
72				g_print("%s="%s"\n",arg[i].name,
73					GTK_VALUE_STRING(arg[i]));
74				break;
75			case GTK_TYPE_BOOL:
76				g_print("%s=%s\n",arg[i].name,
77					GTK_VALUE_UINT(arg[i]) ? "TRUE" : "FALSE");
78				break;
79			default:
80				g_print("%s is type %d\n",
81					arg[i].name,arg[i].type);
82				break;
83		}
84	}
85	}```
```