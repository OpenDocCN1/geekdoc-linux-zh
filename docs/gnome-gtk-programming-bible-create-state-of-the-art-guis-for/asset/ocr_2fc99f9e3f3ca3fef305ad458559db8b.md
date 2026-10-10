# # GtkDialog

A **GtkDialog** widget is a window with some preinstalled and configured containers that you can use to create your own popup dialog boxes.

# Inheritance

GtkDialog - >GtkWindow- >GtkBin- >GtkContainer- >GtkWidget- >
GtkObject

# Functions

```
GtkType gtk_dialog_get_type(void)
GtkWidget *gtk_dialog_new(void)
```

The following example, shown in Figure 21-15, places three buttons in each of the two available containers. The vertical box, named vbox, is configured at the top and is designed for use by toolbars and menus. Also, you can use the vertical box as a container for pixmap windows and text labels. The horizontal box, named action_area, spaces widgets out in the center and is designed for response buttons.

```
static void makeWidget()
{
  GtkWidget *dialog;
  GtkWidget *button;
  GtkWidget *vbox;
  GtkWidget *hbox;

  dialog = gtk_dialog_new();

  vbox = GTK_DIALOG(dialog)->vbox;
  button = gtk_button_new_with_label("VBOX First");
  gtk_box_pack_start(GTK_BOX(vbox),button,TRUE,TRUE,0);
  button = gtk_button_new_with_label("VBOX Second");
  gtk_box_pack_start(GTK_BOX(vbox),button,TRUE,TRUE,0);
  button = gtk_button_new_with_label("VBOX Third");
  gtk_box_pack_start(GTK_BOX(vbox),button,TRUE,TRUE,0);

  hbox = GTK_DIALOG(dialog)->action_area;
  button = gtk_button_new_with_label("HBOX First");
  gtk_box_pack_start(GTK_BOX(hbox),button,TRUE,TRUE,0);
  button = gtk_button_new_with_label("HBOX Second");
  gtk_box_pack_start(GTK_BOX(hbox),button,TRUE,TRUE,0);
  button = gtk_button_new_with_label("HBOX Third");
  gtk_box_pack_start(GTK_BOX(hbox),button,TRUE,TRUE,0);

  gtk_widget_show_all(dialog);
}
```