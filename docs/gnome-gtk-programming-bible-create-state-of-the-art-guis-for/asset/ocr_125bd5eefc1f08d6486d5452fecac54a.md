```
57    if(counter++ < 5)
58       return(TRUE);
59    return(FALSE);
60  }
61 gint eventDelete(GtkWidget *widget,
62                  GdkEvent *event,gpointer data) {
63    return(FALSE);
64  }
65 gint eventDestroy(GtkWidget *widget,
66                  GdkEvent *event,gpointer data) {
67    gtk_main_quit();
68    return(0);
69  }
```

The displayed window contains a single button. On line 28, the call to `gtk_signal_connect()` assigns the function `eventButton()` on line 42 as the one to be called each time the button is clicked. All this callback function does is send a message string to standard output.

An idle function is added with the call to `gtk_idle_add()` on line 37. The first argument is the name of the idle function, and the second argument is a data pointer that will be passed to the idle function when it is called.

The idle function is named `idleFunction()` and it begins on line 47. To simulate extensive processing, the idle function repeatedly calls `sleep()` for one-second intervals. This achieves the same effect as it would for the program to process database records, perform a large sort-merge operation, or any number of other things that take a lot of time. There is the static invocation `counter` variable that keeps track of the number of times the function is called, and there is a loop `counter i` that prints out a line just before each one-second wait.

The idle function is called over and over again as long as it returns `TRUE`. Once the function returns `FALSE`, it is never called again. This way, the function can be designed to perform its task in incremental steps because, after returning to the system, it is called again.

Running this program shows that no events are processed while the idle function is being executed. The function `gtk_main()` looks at the event queue and, finding nothing there, calls the idle function and waits for its return. If the return is `FALSE`, the function is removed from the list of idle functions and is never called again. If the function return is `TRUE`, it is called again as soon as the event queue is empty. If you click the button several times while the idle function is running, nothing seems to happen. The fact is that the mouse events are queued and are all processed when the idle function releases control back to the event loop. This blockage not only affects the button, but it also affects mouse access to the control buttons and menu at the top of the window.