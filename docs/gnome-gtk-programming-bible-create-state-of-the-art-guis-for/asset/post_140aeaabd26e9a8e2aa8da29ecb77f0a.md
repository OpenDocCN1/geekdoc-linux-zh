
There are better ways to create a make file. As a software project grows and contains more and more files, the make file becomes more and more cumbersome. It is best to automate certain aspects of make-file creation. I explain automatic make-file generation in Chapter 20.

In this make file, two variable names (CFLAGS and LDFLAGS) are defined to hold some information needed for the compiling and linking process. The CFLAGS contains a list of gcc arguments that are required for compilation, and LDFLAGS contains a list of gcc arguments that are required for linking. Usually, this is a very confusing task, but GTK+ has made it very simple by supplying a program (a script, actually) that generates the arguments automatically. This reduces the possibility of error and, as a bonus, automatically updates our make file to fit with any new releases of GTK+. You can see the generated arguments by entering these commands:

```
gtk-config --cflags
gtk-config --libs
```

Notice how `gtk-config` is used in the make file. A pair of backward tic marks - not the single quote mark - surrounds the command. This instructs make to execute the command and read the output from it as the string to store in the variable. The generated settings are all that is needed for the LDFLAGS variable. However, from the way CFLAGS is defined in the make file, you can see that it is possible to add other arguments on the line. The option `-Wall` turns on the highest level of warning messages and `-g` causes debugging information to be included.

## A Window That Closes

Most programs have a built-in “Close” option on a menu or toolbar. Also, the user can use the mouse to select the cross at the upper-right corner of a window to instruct the window to close. Selecting Close from the menu that pops down from the upper-left corner of the window is the same as selecting the cross at the upper right. Either way, an event is sent to the program informing it that the window is to be closed. To work properly, the program should intercept the event and make some decisions about what to do. The program can even refuse to allow the window to close. Mainly, the event mechanism provides the program an opportunity to flush buffers, close files, drop communication links, and whatever else nice programs do when they clean up behind themselves.

This program displays the default window and sets up a pair of functions to bring the program to a clean halt:

```c
/* closWin.c **/
#include <gtk/gtk.h>

gint downCount = 0;

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);

int main(int argc, char *argv[])
{
    GtkWidget *topLevelWindow;

    gtk_init(&argc, &argv);
    topLevelWindow = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_signal_connect(GTK_OBJECT(topLevelWindow),
        "delete_event",
        GTK_SIGNAL_FUNC(eventDelete),
        NULL);
    gtk_signal_connect(GTK_OBJECT(topLevelWindow),
        "destroy",
        GTK_SIGNAL_FUNC(eventDestroy),
        NULL);

    gtk_widget_show(topLevelWindow);
    gtk_main();
    g_print("Done!\n");
    exit(0);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
    g_print("Attempt number %d\n", ++downCount);
    if (downCount > 2)
        return(FALSE);
    return(TRUE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
    g_print("Shutting down\n");
    gtk_main_quit();
    return(0);
}
```

This program displays the same default window as the programs in the previous example, but this one has code that allows for a controlled and tidy shutdown. The program begins with calls to `gtk_init()` and `gtk_window_new()` as in the previous example. This is followed by two calls to the function `gtk_signal_connect()`.

The function `gtk_signal_connect()` relates an event to a specific function. There are four arguments passed to it. Every event is associated with a specific window, so the first argument is the window from which the event is expected. The second argument is the name of the event. The third argument is the name of the function to be called every time the event occurs. The macro `GTK_SIGNAL_FUNC()` simply casts the function to the type `GtkSignalFunc()`. The last argument is an optional pointer that you can use to pass data to your event-handler function.

When this program runs, the function `gtk_widget_show()` displays a window and `gtk_main()` goes to sleep waiting for some input from the window. The only window input that can have any meaning is either a "delete_event" or a "destroy" event because those are the only event handlers that are registered with the system. When you use the mouse to try to close the window, a "delete_event" is received by `gtk_main()` and the event is used as an argument in the call to `eventDelete()`. The value of `downCount` is incremented and, if it is less than 2, the `eventDelete()` function returns `FALSE` to prevent any further action. The window does not close and the program continues to run. On the other hand, if `downCount` is 3 or more, `eventDelete()` returns `TRUE`. This `TRUE` return causes the window to be closed immediately as closing and a "destroy" event is issued that causes a call to the function `eventDestroy()`. There is a call to `gtk_main_quit()` that causes the blocking call to `gtk_main()` to release and return. The program makes a clean exit. Running the program produces the following output:

```
Attempt number 1
Attempt number 2
Attempt number 3
Shutting down
Done!
```

As you can see from the order in which things occur, there are three places that your program can take control and clean up things before shutting down. It may not be a good idea to rely on the "delete_event" function for clean up because it is possible to have a "destroy" event arrive from some other source. It is probably best to rely on the "delete_event" only if you want to have the option of refusing to close the window. Otherwise, just put in a simple dummy that always returns `TRUE`. If you have work to do at shutdown, do it either in the "destroy" callback function, or in the mainline following the call to `gtk_main()`.

The call to `gtk_main_quit()` is necessary. Without it, the call to `gtk_main()` continues to wait for an event on a nonexistent window. This is what happened in the previous example, and is the reason you had to kill the program after you closed the window.

## Callbacks and Events

All `GNOME` and `GTK` programs are based on events being received and acted upon. As we just saw in the previous example, the mainline of the program sits and waits on an input queue for the arrival of an event and, when an event arrives, a function is called. A function called because of the arrival of an event is called a *callback function* because it is the `GTK` system that calls these functions in your program.

The events are handled in order, one at a time. Whenever `gtk_main()` reads an event from the queue, it checks to see if there are any callback functions that are assigned to it (there can be more than one) and, if so, these functions are called. When the last of these functions has returned, `gtk_main()` reads the queue looking for the next event.

There are events issued from locations other than a window. Your program can place events in the queue. For example, it is possible to set a period of time for an event to be hidden in the queue and this mechanism can set timers that will cause functions to be called. The queue also can be used for interprocess communications because other programs, by knowing the ID of your window, can place events in your queue.

## A Window with a Button

The graphical elements are all widgets. There are menu widgets, label widgets, scroll bar widgets, and in this example, button widgets. This example displays a simple window with a push button and, when the mouse selects the button, reports that the button has been pushed:

```c
/** buttonwin.c **/
#include <gtk/gtk.h>

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);
void eventButton(GtkWidget *widget, GdkEvent *event, gpointer data);

int main(int argc, char *argv[])
{
    GtkWidget *topLevelWindow;
    GtkWidget *pushMeButton;

    gtk_init(&argc, &argv);
    topLevelWindow = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_signal_connect(GTK_OBJECT(topLevelWindow),
        "delete_event",
        GTK_SIGNAL_FUNC(eventDelete),
        NULL);
    gtk_signal_connect(GTK_OBJECT(topLevelWindow),
        "destroy",
        GTK_SIGNAL_FUNC(eventDestroy),
        NULL);
    pushMeButton = gtk_button_new_with_label("Push me!");
    gtk_signal_connect(GTK_OBJECT(pushMeButton),
        "clicked",
```
