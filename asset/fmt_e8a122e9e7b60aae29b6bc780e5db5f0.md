
```c
GNOMEUIINFO_END
};

GnomeUIInfo editMenu[] = {
    { GNOME_APP_UI_ITEM, "Cut",
      "Delete and copy selection to clipboard",
      editCut, NULL, NULL,
      GNOME_APP_PIXMAP_NONE,
      NULL, 0, 0, NULL },
    { GNOME_APP_UI_ITEM, "Cop_y",
      "Copy selection to clipboard",
      editCopy, NULL, NULL,
      GNOME_APP_PIXMAP_NONE,
      NULL, 0, 0, NULL },
    { GNOME_APP_UI_ITEM, "Paste",
      "Paste selection from clipboard",
      editPaste, NULL, NULL,
      GNOME_APP_PIXMAP_NONE,
      NULL, 0, 0, NULL }
};
```

```c
GNOMEUIINFO_END
});

GnomeUIInfo mainMenu[] = {
    GNOMEUIINFO_SUBTREE("_File",fileMenu),
    GNOMEUIINFO_SUBTREE("_Edit",editMenu),
    GNOMEUIINFO_END
};

int main(int argc,char * argv[])
{
	GtkWidget *app;
    gnome_init("cutpaste","1.0",argc,argv);
    app = gnome_app_new("cutpaste",
		"Cut, Copy, and Paste");
    gtk_signal_connect(GTK_OBJECT(app),"delete_event",
		GTK_SIGNAL_FUNC(eventDelete),NULL);
    gtk_signal_connect(GTK_OBJECT(app),"destroy",
		GTK_SIGNAL_FUNC(eventDestroy),NULL);
    gnome_app_create_menus(GNOME_APP(app),mainMenu);
    text = gtk_text_new(NULL,NULL);
    gtk_widget_set_usize(text,300,200);
    gtk_text_set_editable(GTK_TEXT(text),TRUE);
    gnome_app_set_contents(GNOME_APP(app),text);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

static void fileExit(GtkObject *object,gpointer data) {
    gtk_main_quit();
}

static void editCut(GtkObject *object,gpointer data) {
    gtk_editable_cut_clipboard(GTK_EDITABLE(text));
}

static void editCopy(GtkObject *object,gpointer data) {
    gtk_editable_copy_clipboard(GTK_EDITABLE(text));
}

static void editPaste(GtkObject *object,gpointer data) {
    gtk_editable_paste_clipboard(GTK_EDITABLE(text));
}

gint eventDelete(GtkWidget *widget,
    GdkEvent *event,gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
    GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```
