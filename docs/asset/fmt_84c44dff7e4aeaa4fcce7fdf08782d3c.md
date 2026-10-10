
```c
modalCallback,modalxXPX),

GNOMEUIINFO_RADIOITEM("Notebook",
    "Change to the Notebook display mode",
    notebookCallback,notebookxXPX),

GNOMEUIINFO_RADIOITEM("Toplevel",
    "Change to the Toplevel display mode",
    toplevelCallback,toplevelxXPX),

GNOMEUIINFO_END
};

static GnomeUIInfo modeToolbar[] = {
    { GNOME_APP_UI_ITEM,"New",
        "Create a new file",dummyCallback,NULL,NULL,
        GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_NEW,
        0,0,NULL },
    GNOMEUIINFO_SEPARATOR,
    GNOMEUIINFO_RADIOLIST(modelist),
    GNOMEUIINFO_SEPARATOR,
    { GNOME_APP_UI_ITEM,"Save as",
        "Save to a new file",dummyCallback,NULL,NULL,
        GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_SAVE_AS,
        0,0,NULL ),
    GNOMEUIINFO_END
};

int main(int argc,char *argv[])
{
  gnome_init("toolbarmdi","1.0",argc,argv);
  mdi = gnome_mdi_new("toolbarmdi","ToolbarMDI");
  gtk_signal_connect(mdi,"destroy",
    GTK_SIGNAL_FUNC(eventDestroy),NULL);
  gtk_signal_connect(mdi,"app_created",
    GTK_SIGNAL_FUNC(appCreated),NULL);
  addChild(mdi, "First");
  addChild(mdi, "Second");
  addChild(mdi, "Third");
  addChild(mdi, "Last");
  gnome_mdi_open_toplevel(GNOME_MDI(mdi));
  gtk_main();
  exit(0);
}

static void addChild(Gtk Object *mdi,gchar *name)
{
  GnomeMDIGenericChild *child;
  child = gnome_mdi_generic_child_new(name);
  gnome_mdi_add_child(GNOME_MDI(mdi),
    GNOME_MDI_CHILD(child));
  gnome_mdi_generic_child_set_view_creator(child,
    createView,name);
  gnome_mdi_generic_child_set_label_func(child,setLabel,
    NULL);
  gnome_mdi_add_view(GNOME_MDI(mdi),
    GNOME_MDI_CHILD(child));
}

static GtkWidget *createView(GnomeMDIChild *child,
  gpointer data)
{
  char str[80];
  GtkWidget *label;
  sprintf(str,"View of the\n%s widget",(gchar *)data);
  label = gtk_label_new(str);
  gtk_widget_set_usize(label,200,200);
  return(label);
}

static GtkWidget *setLabel(GnomeMDIChild *child,
  GtkWidget *currentLabel,gpointer data)
{
  if(currentLabel == NULL)
    return(gtk_label_new(child->name));
  gtk_label_set_text(GTK_LABEL(currentLabel),
    child->name);
  return(currentLabel);
}

static void appCreated(GnomeMDI *mdi, GnomeApp *app,
  gpointer data)
{
  gnome_app_create_toolbar(app, modeToolbar);
}

static void topLevelCallback(GtkObject *object,
  gpointer data)
{
  GtkToggleButton *button = GTK_TOGGLE_BUTTON(object);
  if(gtk_toggle_button_get_active(button))
    gnome_mdi_set_mode(GNOME_MDI(mdi),
      GNOME_MDI_TOPLEVEL);
}

static void modalCallback(GtkObject *object,
  gpointer data)
{
  GtkToggleButton *button = GTK_TOGGLE_BUTTON(object);
  if(gtk_toggle_button_get_active(button))
    gnome_mdi_set_mode(GNOME_MDI(mdi),
      GNOME_MDI_MODAL);
}

static void notebookCallback(GtkObject *object,
  gpointer data)
{
  GtkToggleButton *button = GTK_TOGGLE_BUTTON(object);
  if(gtk_toggle_button_get_active(button))
    gnome_mdi_set_mode(GNOME_MDI(mdi),
      GNOME_MDI_NOTEBOOK);
}

static void dummyCallback(GtkObject *object, gpointer data)
{
  gnome_ok_dialog("The dummy callback.");
}

gint eventDestroy(GtkWidget *widget,
  GdkEvent *event, gpointer data) {
  gtk_main_quit();
  return(0);
}
```
