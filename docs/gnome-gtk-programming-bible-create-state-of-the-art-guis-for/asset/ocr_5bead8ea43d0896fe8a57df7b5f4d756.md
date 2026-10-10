```
3 GtkWidget *makeButtonBox();
4 gint eventDelete(GtkWidget *widget,
5 GdkEvent *event,gpointer data);
7 gint eventDestroy(GtkWidget *widget,
8 GdkEvent *event,gpointer data);
9
10 int main(int argc,char *argv[])
11 {
12 GtkWidget *window;
13 GtkWidget *buttonbox;
14
15 gnome_init("hbuttonbox","1.0",argc,argv);
16 window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
17 gtk_signal_connect(GTK_OBJECT(window),
18 "delete_event",
19 GTK_SIGNAL_FUNC(eventDelete),
20 NULL);
21 gtk_signal_connect(GTK_OBJECT(window),
22 "destroy",
23 GTK_SIGNAL_FUNC(eventDestroy),
24 NULL);
25
26 buttonbox = makeButtonBox();
27
28 gtk_container_add(GTK_CONTAINER(window),buttonbox);
29 gtk_widget_show_all(window);
30 gtk_main();
31 exit(0);
32 }
33 GtkWidget *makeButtonBox() {
34 GtkWidget *buttonbox;
35 GtkWidget *button;
36
37 buttonbox = gtk_hbutton_box_new();
38 gtk_container_set_border_width(
39 GTK_CONTAINER(buttonbox),10);
40
41 button = gtk_button_new_with_label("OK");
42 gtk_container_add(GTK_CONTAINER(buttonbox),button);
43
44 button = gtk_button_new_with_label("Refresh");
45 gtk_container_add(GTK_CONTAINER(buttonbox),button);
46
47 button = gtk_button_new_with_label("Clear");
48 gtk_container_add(GTK_CONTAINER(buttonbox),button);
49
50 button = gtk_button_new_with_label("Cancel");
51 gtk_container_add(GTK_CONTAINER(buttonbox),button);
52
53 return(buttonbox);
```