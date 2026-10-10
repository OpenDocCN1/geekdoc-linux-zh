```
34         &pc);
35     gnome_app_set_contents (GNOME_APP(pc.app),button);
36 
37     gtk_container_set_border_width
38             (GTK_CONTAINER(pc.app),30);
39     gtk_widget_show(button);
40     gtk_widget_show(pc.app);
41     gtk_main();
42     exit(0);
43 }
44 void saveAsButton(GtkWidget *widget,pgmContext *pc) {
45     GtkWidget *dialog;
46 
47     dialog = gnome_request_dialog(FALSE,
48                                     "File name",
49                                     pc->defaultFilename,
50                                     40,
51                                     (GnomeStringCallback)fileSaveCallback,
52                                     pc,
53                                     GTK_WINDOW(pc->app)));
54     gtk_window_set_modal(GTK_WINDOW(dialog),TRUE);
55 }
56 void fileSaveCallback(gchar * filename,pgmContext *pc) {
57     if((filename == NULL) || (strlen(filename) == 0)
58         return;
59     strcpy(pc->currentFilename, filename);
60     g_print("Save file as %s\n",pc->currentFilename);
61 }
62 
63 void setTermination(GtkWidget *app) {
64     gtk_signal_connect(GTK_OBJECT(app),
65                         "delete_event",
66                         GTK_SIGNAL_FUNC(eventDelete),
67                         NULL);
68     gtk_signal_connect(GTK_OBJECT(app),
69                         "destroy",
70                         GTK_SIGNAL_FUNC(eventDestroy),
71                         NULL);
72 }
73 gint eventDelete(GtkWidget *widget,
74                 GdkEvent *event,gpointer data) {
75     return(FALSE);
76 }
77 gint eventDestroy(GtkWidget *widget,
78                   GdkEvent *event,gpointer data) {
79     gtk_main_quit();
80     return(0);
81 }
```

This program displays a window with a single push button, as shown in Figure 3-11.