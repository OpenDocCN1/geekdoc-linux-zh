optional column heading buttons also are included, and you can resize the columns by dragging the mouse pointer between the two buttons.

```
```
static GtkWidget *makeWidget()
{
    GtkWidget *widget;
    static gchar *titles[] = {"Column 1", "Column 2"};
    static char *row1[] = {"Apple", "Orange"};
    static char *row2[] = {"Car", "Truck"};
    static char *row3[] = {"Airplane", "Bird"};

    widget = gtk_clist_new_with_titles(2,titles);
    gtk_clist_append(GTK_CLIST(widget),row1);
    gtk_clist_append(GTK_CLIST(widget),row2);
    gtk_clist_append(GTK_CLIST(widget),row3);
    return(widget);
}
```
```

![](bbox=[0.19, 0.55, 0.61, 0.65])

# GtkClock

This widget is an elapsed timer that either counts up or down. You also can set it to display the current time.

**Inheritance**

GtkClock->GtkLabel->GtkMisc->GtkWidget->GtkObject

**Functions**

```
quint gtk_clock_get_type(void)
GtkWidget *gtk_clock_new(GtkClockType type)
void gtk_clock_set_format(GtkClock *clock, gchar *fmt)
void gtk_clock_set_seconds(GtkClock *clock, time_t seconds)
```