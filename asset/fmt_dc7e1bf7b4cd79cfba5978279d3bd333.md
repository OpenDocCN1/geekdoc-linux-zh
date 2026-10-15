
[PAGE 416] 的正文内容如下：

```c
        strcat(lastKey," (not upper case)");

    else if(gdk_keyval_is_upper(key->keyval))
        strcat(lastKey," (upper case)");

    sprintf(work," [0x%2X]",key->keyval);
    strcat(lastKey,work);

    if(altKeyDown)
        strcat(lastKey," ALT");

    if(controlKeyDown)
        strcat(lastKey," CONTROL");

    if(metaKeyDown)
        strcat(lastKey," META");

    if(leftShiftKeyDown)
        strcat(lastKey," LeftSHIFT");

    if(rightShiftKeyDown)
        strcat(lastKey," RightSHIFT");

    gtk_label_set_text(GTK_LABEL(keyLabel),lastKey);

    return(TRUE);
}

gint eventReleaseKey(GtkWidget *widget,
       GdkEvent *event,gpointer data) {
       GdkEventKey *key = (GdkEventKey *)event;

       switch(key->keyval) {
       case GDK_Alt_L:
```

```c
        case GDK_Alt_R:
            altKeyDown = FALSE;
            break;
        case GDK_Control_L:
        case GDK_Control_R:
            controlKeyDown = FALSE;
            break;
        case GDK_Meta_L:
        case GDK_Meta_R:
            metaKeyDown = FALSE;
            break;
        case GDK_Shift_L:
            leftShiftKeyDown = FALSE;
            break;
        case GDK_Shift_R:
            rightShiftKeyDown = FALSE;
            break;
    }
    return(TRUE);
}

gint eventDelete(GtkWidget *widget,
                GdkEvent *event,gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
                GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```
