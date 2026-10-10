# # A Popup Menu

A popup menu is one that normally is not visible but, by using the right mouse button anywhere in the window, the menu appears. The menu from the following example is shown in Figure 8-8.

```
```
1 /** gnomepopup.c **/
2 #include <gnome.h>
3
4 static void dummyCallback(GtkObject *gpointer);
5
6 gint eventDelete(GtkWidget *widget,
          GdkEvent *event,gpointer data);
7
8 gint eventDestroy(GtkWidget *widget,
          GdkEvent *event,gpointer data);
9
10
11 GnomeUIInfo showMenu[] = {
12      GNOMEUIINFO_ITEM("Next",NULL,dummyCallback,NULL),
13      GNOMEUIINFO_ITEM("Previous",NULL,dummyCallback,NULL),
14      GNOMEUIINFO_ITEM("Zoom in",NULL,dummyCallback,NULL),
15      GNOMEUIINFO_ITEM("Zoom Out",NULL,dummyCallback,NULL),
16      GNOMEUIINFO_END
17 };
18
19 GnomeUIInfo editMenu[] = {
20      GNOMEUIINFO_MENU_CUT_ITEM(dummyCallback,NULL),
21      GNOMEUIINFO_MENU_COPY_ITEM(dummyCallback,NULL),
22      GNOMEUIINFO_MENU_PASTE_ITEM(dummyCallback,NULL),
23      GNOMEUIINFO_ITEM("Delete",NULL,dummyCallback,NULL),
24      GNOMEUIINFO_END
25 };
26
27 GnomeUIInfo mainMenu[] = {
28      GNOMEUIINFO_SUBTREE("Show",showMenu),
29      GNOMEUIINFO_ITEM("Reduce",NULL,
             dummyCallback,NULL),
30      GNOMEUIINFO_ITEM("Expand",NULL,
             dummyCallback,NULL),
31      GNOMEUIINFO_SUBTREE("Edit",editMenu),
32      GNOMEUIINFO_END
33 };
34
35 int main(int argc,char *argv[])
36 {
37     GtkWidget *window;
38     GtkWidget *menu;
39
40     gnome_init("gnomepopup","1.0",argc,argv);
41     window = gnome_app_new("gnomepopup","Popup");
```
```