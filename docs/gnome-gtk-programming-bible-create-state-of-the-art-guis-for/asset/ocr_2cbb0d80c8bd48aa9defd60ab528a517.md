```
```
43    gnome_mdi_generic_child_set_view_creator(child,
44        createView,name);
45    gnome_mdi_generic_child_set_label_func(child,setLabel,
46        NULL);
47    gnome_mdi_add_view(GNOME_MDI(mdi),
48        GNOME_MDI_CHILD(child));
49 }
50 static GtkWidget *createView(GnomeMDIChild *child,
51    gpointer data)
52 {
53    char str[80];
54
55    sprintf(str,"View of the\n%s widge",(gchar *)data);
56    return (gtk_label_new(str));
57 }
58 static GtkWidget *setLabel(GnomeMDIChild *child,
59    GtkWidget *currentLabel,gpointer data)
60 {
61    if(currentLabel == NULL)
62        return (gtk_label_new(child->name));
63
64    gtk_label_set_text(GTK_LABEL(currentLabel),
65        child->name);
66    return (currentLabel);
67 }
68 gint eventDestroy(GtkWidget *widget,
69    GdkEvent *event,gpointer data) {
70    gtk_main_quit();
71    return (0);
72 }
```
```

![](bbox=[0.12, 0.61, 0.28, 0.76])

# **Figure 17-1: An MDI window displayed in notebook mode**

GNOME and GTK+ are initialized by the call to `gnome_init()` on line 19. Then, instead of an application window, the call to `gnome_mdi_new()` on line 20 creates a GnomeMDI object. The GnomeMDI object is not a widget—it is a special type of container that has the ability to hold a number of child widgets (or documents, or views) and allows them to be displayed one at a time. When the GnomeMDI object is created, it has nothing to display because it is empty. The application program must call functions to define the displayable contents and make modifications to the option settings.