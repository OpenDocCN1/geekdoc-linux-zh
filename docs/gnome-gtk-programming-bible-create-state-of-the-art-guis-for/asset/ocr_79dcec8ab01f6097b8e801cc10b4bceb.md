```
```
26                GTK_WINDOW(app));
27                gtk_window_set_modal(GTK_WINDOW(dialog),TRUE);
28
29                gtk_main();
30                exit(0);
31    }
32 void requestCallback(gchar *string,gpointer data)
33 {
34     if(string == NULL)
35         g_print("Called back with a NULL string\n");
36     else if(strlen(string) == 0)
37         g_print("Called back with a zero-length string\n");
38     else
39         g_print("GOT: %s\n",string);
40    } ```
```

The call to `gnome_request_dialog()` on line 20 creates the dialog box shown in Figure 3-10.

![](bbox=[0.19, 0.45, 0.44, 0.57])

The first argument is either TRUE or FALSE to indicate whether or not the input string is to be obscured, as with a password. If the value is TRUE, both the initial value and any characters typed by the user are displayed as a string of asterisks. The second argument is the display prompt and the third is the default string value that is inserted into the text field as the dialog first appears. If no initial value is needed, you either can pass the function a NULL or a zero-length string.

The next parameter, on line 23 in this example, is the maximum number of characters that are allowed in the input field. Use 0 for the maximum if you don't want to limit the number of characters. The number of characters can be more than will fit in the data entry window because the window can be scrolled back and forth as necessary to allow data entry.

The last two arguments are the same as in the previous examples. Line 25 is the data pointer that is passed to the callback routine and, the last parameter, is the window that will be the parent of this one. If you don't want the dialog parented, pass a NULL pointer as the parent's window.