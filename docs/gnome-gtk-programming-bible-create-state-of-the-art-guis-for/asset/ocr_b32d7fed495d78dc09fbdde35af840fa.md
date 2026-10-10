# ### Popping Down by Hiding

In the previous example, a new dialog was constructed every time it was to be displayed; when it was closed, it was destroyed. This is a valid and especially useful approach if the dialog is to be a little different each time it is displayed. However, if a dialog is going to be used a lot, you may want to build it once and then pop it up and down whenever you want to. This example hides and redisplay a dialog:

```
```c
1 /** hiding.c **/
2 #include <gnome.h>
3 
4 void closeDialog(GtkWidget *widget,gpointer data);
5 void showDialog(GtkWidget *widget,gpointer data);
6 gint eventShutdown(GtkWidget *widget,gpointer data);
7
8 typedef struct {
9   GtkWidget *dialog;
10 } hidingContext;
11
12 int main(int argc,char *argv[])
13 {
14   GtkWidget *topLevelWindow;
15   GtkWidget *dialogButton;
16   hidingContext context;
17
18   context.dialog = NULL;
19
20   gnome_init("hiding", "1.0",argc,argv);
21   topLevelWindow = gtk_window_new(GTK_WINDOW_TOPLEVEL);
22   gtk_signal_connect(GTK_OBJECT(topLevelWindow),
23                     "destroy",
24                     GTK_SIGNAL_FUNC(eventShutdown),
25                     &context);
26   gtk_container_set_border_width(
27                     GTK_CONTAINER(topLevelWindow),20);
28
29   dialogButton = gtk_button_new_with_label("Dialog");
30   gtk_signal_connect(GTK_OBJECT(dialogButton),
31                     "clicked",
32                     GTK_SIGNAL_FUNC(showDialog),
33                     &context);
34   gtk_container_add(GTK_CONTAINER(topLevelWindow),
35                     dialogButton);
36
37   gtk_widget_show(dialogButton);
38   gtk_widget_show(topLevelWindow);
39
40   gtk_main();
41   exit(0);
```
```