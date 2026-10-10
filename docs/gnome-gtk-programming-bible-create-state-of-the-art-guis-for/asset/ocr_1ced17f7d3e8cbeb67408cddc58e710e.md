```
40 ( 
41 GtkWidget *app; 
42 gnome_init("tbtoggle","1.0",argc,argv); 
43 app = gnome_app_new("tbtoggle", "Toolbar Toggles"); 
44 gtk_signal_connect(GTK_OBJECT(app),"delete_event", 
45 GTK_SIGNAL_FUNC(eventDelete),NULL); 
46 gtk_signal_connect(GTK_OBJECT(app),"destroy", 
47 GTK_SIGNAL_FUNC(eventDestroy),NULL); 
48 gnom_app_create_toolbar(GNOME_APP(app),toggleToolBar); 
49 gtk_widget_show_all(app); 
50 gtk_main(); 
51 exit(0); 
52 static void dummyCallback(GtkObject *object,gpointer data) 
53 { 
54 gnome_ok_dialog("The dummy callback executed."); 
55 } 
56 static void toggleOne(GtkObject *object, 
57 gpoint data) 
58 if{gtk_toggle_button_get_active( 
59 GTK_TOGGLE_BUTTON(object)) 
60 gnome_ok_dialog("The toggle one button is on."); 
61 else 
62 gnome_ok_dialog("The toggle one button is off."); 
63 static void toggleTwo(GtkObject *object, 
64 gpoint data) 
65 if{gtk_toggle_button_get_active( 
66 GTK_TOGGLE_BUTTON(object)) 
67 gnome_ok_dialog("The toggle two button is on."); 
68 else 
69 gnome_ok_dialog("The toggle two button is off."); 
70 static void toggleThree(GtkObject *object, 
71 gpoint data) 
72 if{gtk_toggle_button_get_active( 
73 GTK_TOGGLE_BUTTON(object)) 
74 gnome_ok_dialog("The toggle three button is on."); 
75 else 
76 gnome_ok_dialog("The toggle three button is off."); 
77 gint eventDelete(GtkWidget *widget, 
78 GdkEvent *event,gpointer data) { 
79 return(FALSE); 
80 } 
81 gint eventDestroy(GtkWidget *widget, 
82 GdkEvent *event,gpointer data) { 
83 gtk_main_quit();
```