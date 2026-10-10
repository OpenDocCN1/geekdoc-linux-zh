```
NULL);
27	box = makeBox();
28	gtk_container_add(GTK_CONTAINER(window),box);
29	gtk_widget_show(window);
30	gtk_main();
31	exit(0);
32	}
33	
34	GtkWidget *makeBox() {
35		GtkWidget *box;
36		GtkWidget *button;
37		
38		box = gtk_vbox_new(FALSE,0);
39		gtk_widget_show(box);
40		
41		button = gtk_button_new_with_label("Start 1");
42		gtk_box_pack_start(GTK_BOX(box),button,FALSE,FALSE,0);
43		gtk_widget_show(button);
44		
45		button = gtk_button_new_with_label("End 1");
46		gtk_box_pack_end(GTK_BOX(box),button,FALSE,FALSE,0);
47		gtk_widget_show(button);
48		
49		button = gtk_button_new_with_label("Start 2 button");
50		gtk_box_pack_start(GTK_BOX(box),button,FALSE,FALSE,0);
51		gtk_widget_show(button);
52		
53		button = gtk_button_new_with_label("End 2 button");
54		gtk_box_pack_end(GTK_BOX(box),button,FALSE,FALSE,0);
55		gtk_widget_show(button);
56		
57		return(box);
58	}
59	gint eventDelete(GtkWidget *widget,
60			GdkEvent *event,gpointer data) {
61		return(FALSE);
62	}
63	gint eventDestroy(GtkWidget *widget,
64			GdkEvent *event,gpointer data) {
65		gtk_main_quit();
66		return(0);
67	}
```

The mainline of the program creates a top-level window on line 16 and places a 25-pixel border around its edges on lines 17 and 18. After the shutdown callbacks are initialized, the box of widgets is created on line 28 with a call to makeBox(). The function gtk_container_add() on line 29 places the box widget in the main window, and the call to gtk_widget_show() on line 30 makes the main window visible.