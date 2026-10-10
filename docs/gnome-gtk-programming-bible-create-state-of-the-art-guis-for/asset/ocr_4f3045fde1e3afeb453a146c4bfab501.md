```
65    gint eventDestroy(GtkWidget *widget,
66                    GdkEvent *event,gpointer data) {
67       gtk_main_quit();
68       return(0);
69    }
```

![](bbox=[0.17, 0.235, 0.49, 0.39])

![](bbox=[0.17, 0.425, 0.49, 0.57])

The function `makeHorizontalPane()` beginning on line 35 creates the paned container and inserts the two text widgets into it. The text widgets are created and filled with text on lines 41 through 52.

The call to `gtk_hpaned_new()` on line 54 creates a horizontal paned widget like the one shown in Figures 5-13 and 5-14.

The call to the function `gtk_hpaned_new()` on line 52 creates a new horizontal pane widget. On lines 56 and 57, the function `gtk_paned_add()` adds the text widget on the left and `gtk_paned_add2()` adds the text widget to the right.

That's all there is to it. The paned widget and its two contained widgets communicate with one another about positioning and resizing. The overall window can be resized and the gutter can be shifted back and forth to make all the widgets resize together. The minimum widget size does not limit gutter movement, and it is possible to move the gutter all the way to one side or the other completely obscuring one widget and allocating the whole window to the other.