```
5
static void helpAbout(GtkWidget *widget, gpointer data)
{
GtkWidget *aboutBox;
const gchar *writtenBy[] = {
"Arthur Griffith",
"Lance Peterson",
NULL
};
aboutBox = gnome_about_new("Gnome Menu Layout.
"0.0",
"(C) 1999 the Free Software Foundation",
writtenBy,
"This source code can be used as a starting "
"point to create a Gnome application.",
NULL);
gtk_widget_show(aboutBox);
}
static void dummyCallback(GtkObject *object,
gpointer data)
{ gnom e_ok_dialog( "Not implemented..." ); }
GnomeUIInfo dummyMenu[] = {
{ GNOME_APP_UI_ITEM,"Dummy",
"A placeholder menu entry",
dummyCallback,NULL,NULL,
GNOME_APP_PIXMAP_NONE,
NULL,0,0,NULL },
GNOMEUIINFO_END
};
GnomeUIInfo fileMenu[] = {
GNOMEUIINFO_MENU_NEW_ITEM("New Window",
"Open a new application window",
dummyCallback,data),
GNOMEUIINFO_MENU_NEW_SUBTREE(dummyMenu),
GNOMEUIINFO_SEPARATOR,
GNOMEUIINFO_MENU_OPEN_ITEM(dummyCallback,data),
GNOMEUIINFO_MENU_SAVE_ITEM(dummyCallback,data),
GNOMEUIINFO_MENU_SAVE_AS_ITEM(dummyCallback,data),
GNOMEUIINFO_MENU_REVERT_ITEM(dummyCallback,data),
GNOMEUIINFO_MENU_PRINT_ITEM(dummyCallback,data),
GNOMEUIINFO_MENU_PRINT_SETUP_ITEM(dummyCallback,data),
GNOMEUIINFO_SEPARATOR,
GNOMEUIINFO_MENU_CLOSE_ITEM(dummyCallback,data),
GNOMEUIINFO_MENU_EXIT_ITEM(dummyCallback,data),
GNOMEUIINFO_END
};
```