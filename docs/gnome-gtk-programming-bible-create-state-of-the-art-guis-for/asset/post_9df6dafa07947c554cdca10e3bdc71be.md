
# ## Dialogs Are on Their Own

A popup or a dialog is made up of one or more widgets. A *widget* is a single-purpose software object that usually displays a window. The window is used for input, output, or both. A widget can be quite simple (such as a push button) or quite complicated (such as a dynamically sized, pull-down selection list). There is an exception here and there, but most widgets are intended for inclusion in a window, along with other widgets, to define the interface for a popup or dialog window.

There are all kinds of popup windows. The simple ones have a single statement and an Ok button, and others have multiple labels and other widgets for data input. Normally a program has one main window and everything else is done by dialogs that appear and disappear under the control of the user's mouse.

When your program creates and displays a dialog, the dialog immediately goes off on its own. This architecture is part of the basics of the X Window System. Once a dialog is running, the function that created it returns so your program can continue to run. The only way your program can hear from a dialog is if it calls the **optional callback function** you specified. Of course, it can grab the mouse to prevent access to any other windows in your application, but your program won't know about that. It just waits patiently for input from the mouse or keyboard.

Every program uses the same function for its main loop:

```
gtk_main()
```

This function call waits for events to come from the mouse or the keyboard. Whenever an event arrives, the information is dispatched to the correct window, which, in turn, may invoke a callback function. If you write a callback function that uses a lot of time (for instance, sorting a huge file) the entire time your function is running, the mouse has no effect whatsoever because there are no events being read. There are ways to run time-consuming tasks while leaving the mouse active, as discussed in Chapter 5, but the point I want to make here is that a dialog box disassociates itself from your program so the event-grabbing loop in `gtk_main()` can continue to function.

# ## The GNOME Defined Dialogs

There is a collection of dialog boxes that are predefined and ready to be displayed. They are the traditional information and question boxes that inform the user of things such as, "File not found!" and ask things such as, "Are you sure?"

# ## Make a Simple Statement

This program demonstrates that a dialog box can be displayed using very little code:

```c
/** okdialog.c **/
#include <gnome.h>

int main(int argc, char *argv[])
{
    gnome_init("okdialog", "1.0", argc, argv);
    gnome_ok_dialog("A simple information window");
    gtk_main();
    exit(0);
}
```

Before the dialog can be displayed, it is only necessary to call gnome_init(). The function call to gnome_ok_dialog() creates and displays the dialog box as shown in Figure 3-1. The call to gtk_main() waits for you to click the OK button; when that happens, the dialog is closed.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_68_0.png)

There is no information fed back to the program from this dialog. In fact, the program continues on just as if the dialog had not been displayed—it remains on the screen until the OK button is clicked and then it silently disappears.

The dialog box automatically adjusts its size to accommodate the size of the text. If the text is too long to fit on a single line, it can continue on the next line with the insertion of a newline character, like the ones in this example:

```c
/** okmultiple.c **/
#include <gnome.h>

gchar message[] =
    "To display a message on\nmore than one line\n"
    "it is only necessary to insert\na newline character\n"
    "\nWherever you would like the line to break.";

int main(int argc, char *argv[])
{
    gnome_init("okmultiple", "1.0", argc, argv);
    gnome_ok_dialog(message);
    gtk_main();
    exit(0);
}
```

The multiline dialog produced by this example is shown in Figure 3-2.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_69_0.png)

**Figure 3-2:** A simple message popup with multiple lines

A dialog box also can be made *modal*, which means that no other window in the application will accept mouse or keyboard input. This program demonstrates how that works:

```c
/** okmddialog.c **/
#include <gnome.h>

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *dialog;
    GtkWidget *button;

    gnome_init("okmdialog", "1.0", argc, argv);
    app = gnome_app_new("okmdialog", "Okay Dialog");
    button = gtk_button_new_with_label("Button");
    gtk_container_set_border_width(GTK_CONTAINER(app), 30);
    gnome_app_set_contents(GNOME_APP(app), button);
    gtk_widget_show(button);
    gtk_widget_show(app);

    dialog = gnome_ok_dialog(
            "A simple information window");
    gtk_window_set_modal(GTK_WINDOW(dialog), TRUE);

    gtk_main();
    exit(0);
}
```

This program displays the dialog box previously shown in Figure 3-1, and also displays the window shown in Figure 3-3. Lines 10 through 20 create and display the main window and its button. While both the main window and the dialog are being displayed, only the button in the dialog box responds to the mouse because of the call to gtk_window_set_modal() on line 20. The button in the main window ignores the mouse until the OK button of the dialog box is clicked and the dialog closes. After that, the main window button works normally.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_70_0.png)

**Figure 3-3:** The button of the main window

Lines 15 and 16 display the button and app widgets. In this example, the button widget is displayed before its parent, the app widget. If the order of the calls to gtk_widget_show() is reversed, the end result is the same—but the process of painting the widgets on the screen is different. I discuss more about this later in the chapter.

The code on lines 18 through 20 that creates and displays the dialog does not require the app window as an argument. This means that a dialog easily can be created from any point in your program and can halt all window activity within the application until the dialog is acknowledged.

The calls to gtk_widget_show() on lines 15 and 16 can be in any order. The fact is that the button widget does not display at all if the app widget is not being displayed also, because the call to gnome_app_set_contents() on line 14 places the button inside the app widget. Generally speaking, it is better to display the widgets from the inside out this way because the entire window and all its widgets will appear at once. In a large window—one that contains lots of widgets—if the outer window is displayed first, the widgets can all appear one at a time after the containing window first appears.

Up until now, the dialog window has been a free agent and the mouse could place it either in front or behind any of the other windows on the display. This example shows that if the dialog has a parent window, it always remains in front of the parent. This seems to make especially good sense when using modal dialogs, because the parent window is inactive anyway and hiding the dialog could cause confusion. You can alter the program by changing lines 18 and 19 to this:

```
dialog = gnome_ok_dialog_parented( 
  "A simple information window", 
  GTK_WINDOW(app));
```

This causes the app window to be the parent of the dialog. Any window can be the parent of one or more child windows, so you can use this same technique for popping up dialogs for any window in an application.

There are two other dialog windows that work the same way as the OK dialog window. The warning and error dialog windows both have parented and non-parented modes, and they both can be modal or non-modal. To display the error window shown in Figure 3-4, change lines 18 and 19 to this:

```
dialog = gnome_error_dialog_parented(
    "A simple error window",
    GTK_WINDOW(app));
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_71_0.png)

The third form of the simple OK popups is the warning, as shown in Figure 3-5. The display code follows the same form as the others:

```
dialog = gnome_warning_dialog_parented(
    "A simple warning window",
    GTK_WINDOW(app));
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_71_1.png)

### Ask a Simple Question

To get a yes or no answer from a dialog box, it is necessary to find out which of the two choices the user made. The response is captured with a callback function. Here is an example of a program that displays a question dialog box and captures the response:
