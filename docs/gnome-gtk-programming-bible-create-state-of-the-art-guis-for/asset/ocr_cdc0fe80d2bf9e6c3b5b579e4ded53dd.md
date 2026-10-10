program has a couple of standard toolbar buttons and a set of radio buttons, but an MDI toolbar can contain any of the toolbar items described in Chapter 8.

```
1 /** toolbarmdi.c **/
2 #include <gnome.h>
3
4 #include "toolbarxp.m"
5
6 static GObject *mdi;
7
8 gint eventDestroy(GtkWidget *widget,
9                 GdkEvent *event,gpointer data);
10
11 static void addChild(GtkObject *mdi,gchar *name);
12 static GtkWidget *setLabel(GnomeMDIChild *child,
13                 GtkWidget *currentLabel,gpointer data);
14 static GtkWidget *createView(GnomeMDIChild *child,
15                 gpointer data);
16
17 static void notebookCallback(GtkObject *object,
18                 gpointer data);
19 static void modalCallback(GtkObject *object,
20                 gpointer data);
21 static void toplevelCallback(GtkObject *object,
22                 gpointer data);
23 static void dummyCallback(GtkObject *object,
24                 gpointer data);
25 static void appCreated(GnomeMDI *mdi,GnomeApp *app,
26                 gpointer data);
27
28 GnomeUIInfo modelist[] = {
29     GNOMEUIINFO_RADIOITEM("Modal",
30        "Change to the Modal display mode",
31        modalCallback,modalxXPX),
32     GNOMEUIINFO_RADIOITEM("Notebook",
33        "Change to the Notebook display mode",
34        notebookCallback,notebookxXPX),
35     GNOMEUIINFO_RADIOITEM("Toplevel",
36        "Change to the Toplevel display mode",
37        toplevelCallback,toplevelxXPX),
38     GNOMEUIINFO_END
39 };
40
41 static GnomeUIInfo modeToolbar[] = {
42     { GNOME_APP_UI_ITEM,"New",
43        "Create a new file",dummyCallback,NULL,NULL,
44        GNOME_APP_PIXMAP_STOCK,GNOME_STOCK_PIXMAP_NEW,
45        0,0,NULL },
46     GNOMEUIINFO_SEPARATOR,
47     GNOMEUIINFO_RADIOLIST(modelist),
48     GNOMEUIINFO_SEPARATOR,
49     { GNOME_APP_UI_ITEM,"Save as",
50        "Save to a new file",dummyCallback,NULL,NULL,
```