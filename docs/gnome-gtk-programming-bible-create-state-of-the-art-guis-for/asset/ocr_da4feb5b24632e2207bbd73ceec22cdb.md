```
9    GtkWidget *dialog;
10   GtkWidget *button;
11
12   gnome_init("cammppialog", "1.0", argc, argv);
13   app = gnome_app_new("cammppialog", "Question Dialog");
14   button = gtk_button_new_with_label("Button");
15   gtk_container_set_border_width(GTK_CONTAINER(app), 30);
16   gnome_app_set_contents(GNOME_APP(app), button);
17   gtk_widget_show(button);
18   gtk_widget_show(app);
19
20   dialog = gnome_ok_cancel_dialog_modal_parented(
21       "Do you really want to do this?",
22       (GnomeReplyCallback)cancel_or_ok,
23       NULL,
24       GTK_WINDOW(app));
25
26   gtk_main();
27   exit(0);
28 )
29 void cancel_or_ok(gint reply, gpointer data) {
30     if(reply == GNOME_CANCEL)
31         g_print("Action cancelled\n");
32     else
33         g_print("Action okayed\n");
34 }
```

The main window has a button that is disabled while the dialog is being displayed because the function call on line 20 that creates the dialog specifies a modal dialog. Also, the main window cannot hide the dialog because the dialog created is parented. However, there are other function calls that can be used to create non-modal and/or non-parented dialogs. It is a simple matter of replacing lines 20 through 24 with one of the following. To create a dialog that is parented but not modal, use this form:

```
dialog = gnome_ok_cancel_dialog_parented(
        "Do you really want to do this?",
        (GnomeReplyCallback)cancel_or_ok,
        NULL,
        GTK_WINDOW(app));
```

To create a dialog that is modal but not parented, use this form:

```
dialog = gnome_ok_cancel_dialog_modal(
        "Do you really want to do this?",
        (GnomeReplyCallback)cancel_or_ok,
        NULL,
        GTK_WINDOW(app));
```