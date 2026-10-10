```
```
gtk_signal_connect(GTK_OBJECT(radiobutton), "toggled",
    radioCallback,propertyBox);
gtk_box_pack_start(GTK_BOX(box),radiobutton,
    FALSE,TRUE,0);

    return(box);
}

void radioCallback(GtkWidget *widget,
    GnomePropertyBox *propertyBox)
{
    gnome_property_box_changed(propertyBox);
}
```
```

![](bbox=[0.12, 0.35, 0.55, 0.48])

**Figure 22-24: A GnomePropertyBox with two pages of radio buttons**

The property box is created by the call to `gnome_property_box_new()`. The call to `property_box_append_page()` adds a new page along with the label that appears as its tab. The "apply" callback signal is connected to the GnomePropertyBox, and the function `propertyboxCallback()` is called whenever one or more values are changed and they need to be stored as the new property values.

The `propertyboxCallback()` is called whenever the OK or Apply button is clicked. In fact, it gets called more than once. It is called once with the number of each page that changes, and then it is called again with a page number of -1. For example, if there are changes on pages 0 and 3, but pages 1, 2, and 4 stay the same, the callback is called with the page number 0, then again with the number 3, and finally with -1. In most cases, all you need to concern yourself with is the -1 call. However, there may be circumstances that require special processing for some pages, and it would be inefficient to do it every time the callback executes.

The buttons OK and Apply remain inactive until something changes on one of the pages. It is up to your application to let the GnomePropertyBox know when a change occurs. In this example, all of the radio buttons cause the callback function `radioCallback()` to execute, which, in turn, calls `gnome_property_box_changed()` to register the fact that something has changed. And, because the GnomePropertyBox knows which is the current page, it records that information so it can be passed to the "apply" signal callback.