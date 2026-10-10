
The button in the dialog window, defined on line 61, uses the callback function `closeDialog()` defined on line 77. The data argument passed to the callback is the pointer to the dialog. In the callback, a call is made to `gtk_widget_hide()`, causing the dialog box — along with everything it contains — to disappear from the display.

Line 70 sets the dialog to be modal. In this small, single-dialog example, this really doesn’t matter because the only button on the main window is the one that displays the dialog, and there is only one copy of the dialog. This is unlike some of the previous examples where a new dialog was created each time, allowing the creation of any number of displayed dialogs. Multiple calls to `gtk_widget_show()` don’t have any effect and the dialog continues to display and operate normally.

The callback function `eventShutdown()` closes the application, and there is a special situation because of the persistence of the dialog. If the dialog is on the display at the time the application is shut down, and it is not specifically destroyed, the dialog continues to display itself. This can be particularly bothersome. For example, if after the application has been halted the user makes a selection in the dialog (pressing the button), then there is no program there to receive the call to the callback function and an error is issued. The dialog continues to remain on the display because it has not been told to do otherwise. To prevent this, the `eventShutdown()` function, on lines 47 and 48, checks whether the dialog exists and calls `gtk_widget_destroy()` if it does.

## Data Out and Data In

From the point of view of the program, dialogs and popups only exist to display data to the user, get data from the user, or both. There can be a number of widgets in a window that enable the user to enter data. The program must be able to insert data values into the widgets and, later, to retrieve data entered by the user.

The following is a simple program that sets up a dialog and retrieves the user input:

```c
/** dataoutin.c **/
#include <gnome.h>

void closeDialog(GtkWidget *widget, gpointer data);
void showDialog(GtkWidget *widget, gpointer data);
gint eventShutdown(GtkWidget *widget, gpointer data);

typedef struct {
    GtkWidget *dialog;
    GtkEntry *nameEntry;
} dataoutinContext;

int main(int argc, char *argv[]) {
    GtkWidget *topLevelWindow;
    GtkWidget *dialogButton;
    dataoutinContext context;

    context.dialog = NULL;
    context.nameEntry = NULL;

    gnome_init("dataoutin", "1.0", argc, argv);
    topLevelWindow = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_signal_connect(GTK_OBJECT(topLevelWindow),
        "destroy", GTK_SIGNAL_FUNC(eventShutdown),
        &context);

    gtk_container_set_border_width(
        GTK_CONTAINER(topLevelWindow), 20);

    dialogButton = gtk_button_new_with_label("Dialog");
    gtk_signal_connect(GTK_OBJECT(dialogButton),
        "clicked", GTK_SIGNAL_FUNC(showDialog),
        &context);

    gtk_container_add(GTK_CONTAINER(topLevelWindow),
        dialogButton);

    gtk_widget_show(dialogButton);
    gtk_widget_show(topLevelWindow);

    gtk_main();
    exit(0);
}

int eventShutdown(GtkWidget *widget, gpointer data) {
    dataoutinContext *context;

    context = (dataoutinContext *)data;
    if (context->dialog != NULL)
        gtk_widget_destroy(GTK_WIDGET(context->dialog));
    gtk_main_quit();
    return(0);
}

void showDialog(GtkWidget *widget, gpointer data) {
    GtkWidget *box;
    GtkWidget *okButton;
    dataoutinContext *context;

    context = (dataoutinContext *)data;

    if (context->dialog == NULL) {
        context->dialog =
            gtk_window_new(GTK_WINDOW_DIALOG);
        gtk_container_set_border_width(
            GTK_CONTAINER(context->dialog), 20);
        box = gtk_vbox_new(FALSE, 0);
        gtk_container_add(
            GTK_CONTAINER(context->dialog), box);
        gtk_widget_show(GTK_WIDGET(box));

        context->nameEntry = (GtkEntry *)gtk_entry_new();
        gtk_entry_set_text(context->nameEntry,
            "Initial String");
        gtk_box_pack_start(GTK_BOX(box),
            GTK_WIDGET(context->nameEntry),
            FALSE, FALSE, 0);
        gtk_widget_show(GTK_WIDGET(context->nameEntry));

        okButton = gtk_button_new_with_label("OK");
        gtk_signal_connect(GTK_OBJECT(okButton),
            "clicked",
            GTK_SIGNAL_FUNC(closeDialog),
            context);
        gtk_box_pack_start(GTK_BOX(box),
            okButton, FALSE, FALSE, 0);
        gtk_widget_show(okButton);

        gtk_window_set_modal(
            GTK_WINDOW(context->dialog), TRUE);
    }
    gtk_widget_show(context->dialog);
}

void closeDialog(GtkWidget *widget, gpointer data)
{
    dataoutinContext *context;
    gchar *gotName;

    context = (dataoutinContext *)data;

    gotName = gtk_entry_get_text(context->nameEntry);
    g_print("GOT: %s\n", gotName);

    gtk_widget_hide(GTK_WIDGET(context->dialog));
}
```

The top-level window shown in Figure 3-19 has a single button that is used to pop up the dialog box shown in Figure 3-20. The dialog box here contains two widgets: a window allowing text entry and an OK button. When the OK button is pressed, the dialog disappears and the program displays the entered string on the command line. The structure of this program is not all that it should be, but it was kept simple to demonstrate the basic method of retrieving user-input data from the screen.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_95_0.png)

**Figure 3-19:** The main window contains a button to pop up the dialog.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_95_1.png)

**Figure 3-20:** A dialog box capable of accepting keyboard input

The structure defined on line 8 is the data passed to the callbacks. It contains a pointer to the dialog widget and a pointer to the text-entry widget that is inside the dialog. With both of them in the structure, the display of the dialog can be controlled and the text can be extracted from the data-entry widget.

The context structure is initialized on lines 19 and 20. On line 35, its address is used as the data pointer passed to the button’s callback function `showDialog()`. The `showDialog()` function starting on line 54 creates a new dialog if there is not one already installed in the context structure. When the data entry widget is created, on lines 72 and 73, the initial value in the window is set to the string "Initial String". The OK push button is built on lines 79 through 86, and has a callback assigned to it. On line 83, the address of the context struct is used as the data pointer to the callback function. There is no callback function defined for the data entry widget because it accepts and retains the user’s input, and there is no need to retrieve the text until the OK button is pressed.

Starting on line 94 is the callback function for the OK button. The context pointer is passed to it, so it has the address of the data-entry widget and the dialog. Line 101 retrieves the character string from the data-entry widget. The return value from `gtk_entry_get_text()` is a pointer to the string. If you need to save the string, your program should make a copy of it before using it. (In this example, the string is simply printed and then ignored.) Memory for the string is allocated inside the widget, and then deallocated again by the widget.

The data-entry widget keeps track of the current string and displays its internal string whenever the dialog pops up. As the user edits the string, the internal string is modified. This way, the changes are in effect even after the window is popped down and back up again. This may or may not be what you want and there is more about data control in Chapter 4.

## Summary

Dialog and popup windows are just like any other window. Once they are put on display, they have a life of their own with the only connection to the main program being one or more callback functions. For example, in this chapter you learned:

-   ✦ There is a collection of built-in dialogs designed for the standard operations of displaying a message to the user or asking the user a yes or no question.
-   ✦ A dialog can grab the mouse, preventing the rest of the application from being accessible.
-   ✦ There are two basic kinds of temporary windows. A dialog pops up with a full frame around it, just as if it were the main window of an application. A popup pops up with no frame and no window manager controls.
-   ✦ Widgets can be assigned a callback function and, when some specific action takes place, the function is called. The first parameter of the call is always the widget itself. The last parameter is the address that your program specified should be passed to the callback. There may or may not be other parameters in between these two.
-   ✦ When a dialog disappears, it can be destroyed or it can be saved for display again.
-   ✦ A dialog is a widget that contains another widget. The other widget it contains can be displayed as the dialog is being displayed. The widget contained in a dialog, or popup, window can be a special container widget. A container widget can organize and display several other widgets.

In the next chapter, you’ll learn how to place widgets on windows using boxes and tables.
