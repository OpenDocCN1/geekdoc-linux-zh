```
46 GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_OPEN,
47 0,0,NULL },
48 { GNOME_APP_UI_ITEM,"Modulate",
49 "Create a new file",NULL,NULL,NULL,
50 GNOME_APP_PIXMAP_DATA,&modulate,
51 0,0,NULL },
52 { GNOME_APP_UI_ITEM,"Save",
53 "Save the current file",NULL,NULL,NULL,
54 GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_SAVE,
55 0,0,NULL },
56 GNOMEUIINFO_END
57 };
58
59 int main(int argc,char *argv[])
60 {
61 GtkWidget *app;
62
63 gnome_init("toolbarcustom","1.0",argc,argv);
64 app = gnome_app_new("toolbarcustom",
65 "Custom Toolbar Icons");
66 gtk_window_set_default_size(GTK_WINDOW(app),300,200);
67 gtk_signal_connect(GTK_OBJECT(app),"delete_event",
68 GTK_SIGNAL_FUNC(eventDelete),NULL);
69 gtk_signal_connect(GTK_OBJECT(app),"destroy",
70 GTK_SIGNAL_FUNC(eventDestroy),NULL);
71
72 gnome_app_create_toolbar(GNOME_APP(app),toolbarfile);
73 gtk_widget_show_all(app);
74 gtk_main();
75 exit(0);
76 }
77 gint eventDelete(GtkWidget *widget,
78 GdkEvent *event,gpointer data) {
79 return(FALSE);
80 }
81 gint eventDestroy(GtkWidget *widget,
82 GdKEVENT *event,gpointer data) {
83 gtk_main_quit();
84 return(0);
85 }
```

The toolbar definition beginning on line 39 is made up of two custom icons and two GNOME stock icons. The Open and Save icons defined on lines 44 and 52 are the two stock icons. The window displayed is shown in Figure 8-15.

![](bbox=[0.19, 0.86, 0.48, 0.98])

**Figure 8-15:** Toolbars mix custom and stock icons