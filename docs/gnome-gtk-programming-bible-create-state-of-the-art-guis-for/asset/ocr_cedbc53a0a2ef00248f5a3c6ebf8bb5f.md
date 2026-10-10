```
11 gint eventDelete(GtkWidget *widget,
12 GdkEvent *event,gpointer data);
13 gint eventDestroy(GtkWidget *widget,
14 GdKEvent *event, gpointer data);
15 
16 GnomeUIInfo radioList[] = {
17 GNOMEUIINFO_RADIOITEM("Radio One",
18 "The first radio button",
19 radioOneToolbar,downXPM),
20 GNOMEUIINFO_RADIOITEM("Radio Two",
21 "The second radio button",
22 radioTwoToolbar,attachXPM),
23 GNOMEUIINFO_RADIOITEM("Radio Three",
24 "The third radio button",
25 radioThreeToolbar,propertiesXPM),
26 GNOMEUIINFO_END
27};
28 
29 static GnomeUIInfo radioToolbar[] = {
30 { GNOME_APP_UI_ITEM,"New",
31 "Create a new file",dummyCallback,NULL,NULL,
32 GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_NEW,
33 0,0,NULL },
34 GNOMEUIINFO_SEPARATOR,
35 GNOMEUIINFO_RADIOLIST(radioList),
36 GNOMEUIINFO_SEPARATOR,
37 { GNOME_APP_UI_ITEM,"Save as",
38 "Save to a new file",dummyCallback,NULL,NULL,
39 GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_SAVE_AS,
40 0,0,NULL },
41 GNOMEUIINFO_END
42};
43 
44 int main(int argc,char *argv[])
45 (
46 GtkWidget *app;
47 
48 gnome_init("tbradio","1.0",argc,argv);
49 app = gnome_app_new("tbradio","Toolbar Radio Buttons");
50 g_signal_connect(GTK_OBJECT(app),"delete_event",
51 GKT_SIGNAL_FUNC(eventDelete),NULL);
52 gtk_signal_connect(GTK_OBJECT(app),"destroy",
53 GTK_SIGNAL_FUNC(eventDestroy),NULL);
54 
55 gnome_app_create_toolbar(GNOME_APP(app),radioToolbar);
56 gtk_widget_show_all(app);
57 
58 gtk_main();
59 exit(0);
60}
61 static void dummyCallback(GtkObject *object,gpointer data)
```