```
18     gint vertical;   
19 ) Context;
20
21 gint eventDelete(GtkWidget *widget,
22         GdkEvent *event,gpointer data);
23 gint eventDestroy(GtkWidget *widget,
24         GdkEvent *event,gpointer data);
25 void eventFontSet(GtkWidget *widget,
26         gchar *string,Context *context);
27 gboolean eventDraw(GtkWidget *widget,
28         GdkEvent *event,Context *context);
29.void topButton(GtkWidget *widget,Context *context);
30 void middleButton(GtkWidget *widget,Context *context);
31 void bottomButton(GtkWidget *widget,Context *context);
32 void leftButton(GtkWidget *widget,Context *context);
33 void centerButton(GtkWidget *widget,Context *context);
34 void rightButton(GtkWidget *widget,Context *context);
35 static GtkWidget *createPositionWidget(Context *context);
36
37 int main(int argc,char *argv[])
38 {
39         GtkWidget *app;
40         GtkWidget *position;
41         Context context =
42                 ( NULL, NULL, STRING_RIGHT, STRING_MIDDLE );
43
44         gnome_init("fontposition","1.0",argc,argv);
45         app = gnome_app_new("fontposition","Font Position");
46         gtk_container_set_border_width(GTK_CONTAINER(app),30);
47         gtk_signal_connect(GTK_OBJECT(app),"delete_event",
48                 GTK_SIGNAL_FUNC(eventDelete),NULL);
49         gtk_signal_connect(GTK_OBJECT(app),"destroy",
50                 GTK_SIGNAL_FUNC(eventDestroy),NULL);
51
52         position = createPositionWidget(&context);
53
54         gnome_app_set_contents(GNOME_APP(app),position);
55         gtk_widget_show_all(app);
56         gtk_main();
57         exit(0);
58 }
59 static GtkWidget *createPositionWidget(Context *context)
60 {
61         GtkWidget *position;
62         GtkWidget *box;
63         GtkWidget *button;
64         GtkWidget *frame;
65         GtkWidget *fontpicker;
66
67         position = gtk_vbox_new(FALSE,0);
68
69         box = gtk_hbox_new(TRUE,10);
70         button = gtk_button_new_with_label("Top");
71         gtk_signal_connect(GTK_OBJECT(button),"clicked",
```