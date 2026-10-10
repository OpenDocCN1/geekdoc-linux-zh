```
24 "destroy",
25 GTK_SIGNAL_FUNC(eventDestroy),
26 NULL);
27
28 aspect = makeAspectFrame();
29
30 gtk_container_add(GTK_CONTAINER(window),aspect);
31 gtk_widget_show(window);
32 gtk_main();
33 exit(0);
34 }
35 GtkWidget *makeAspectFrame() {
36 GtkWidget *aspect;
37 GtkWidget *button;
38 gfloat xalign = 0.5;
39 gfloat yalign = 0.5;
40 gfloat ratio = 2;
41
42 aspect = gtk_aspect_frame_new("AspectFrame",
43 xalign,yalign,
44 ratio,
45 FALSE);
46
47 gtk_widget_show(aspect);
48 gtk_container_set_border_width(GTK_CONTAINER(aspect),
49 10);
50 button = gtk_button_new_with_label("Button");
51 gtk_widget_show(button);
52 gtk_container_set_border_width(GTK_CONTAINER(button),
53 10);
54 gtk_container_add(GTK_CONTAINER(aspect),button);
55
56 return(aspect);
57 gint eventDelete(GtkWidget *widget,
58 GdkEvent *event,gpointer data) {
59 return(FALSE);
60 }
61 gint eventDestroy(GtkWidget *widget,
62 GdkEvent *event,gpointer data) {
63 gtk_main_quit();
64 return(0);
65 }
```

![](bbox=[0.17, 0.79, 0.37, 0.95])

Figure 5-10: A button in an aspect
frame at a 2:1 ratio