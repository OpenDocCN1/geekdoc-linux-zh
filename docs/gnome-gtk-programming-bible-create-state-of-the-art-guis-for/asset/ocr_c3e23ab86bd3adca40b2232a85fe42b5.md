```
void gtk_entry_set_max_length(GtkEntry *entry, guint16 max)
void gtk_entry_set_position(GtkEntry *entry, gint position)
void gtk_entry_set_text(GtkEntry *entry, const gchar *text)
void gtk_entry_set_visibility(GtkEntry *entry,
    gboolean visible)
```

This example creates the text-entry window shown in Figure 21-16. It is 40 characters wide and initialized with text.

```
static GtkWidget *makeWidget()
{
   GtkWidget *widget;

    widget = gtk_entry_new_with_max_length(40);
    gtk_entry_set_text(GTK_ENTRY(widget), "Edit me!");
    return(widget);
}
```

![](bbox=[0.13, 0.47, 0.61, 0.54])

# GtkEventBox

The GtkEventBox widget is a container with a see-through window that can receive events for the contained widget—normally one that cannot receive its own. Events are sent to windows, so a widget without windows cannot receive events.

**Inheritance**
GtkEventBox->GtkBin->GtkContainer->GtkWidget->GtkObject

**Functions**
GtkType gtk_event_box_get_type(void)
GtkWidget *gtk_event_box_new(void)

This example wraps a GtkEventBox around a GtkLabel to make the label sensitive to mouse movements. The callbacks are used to change the text of the label, as shown in Figure 21-17, to indicate whether or not the mouse pointer is inside the label.

```
static GtkWidget *makeWidget()
{
   GtkWidget *eventbox;
   GtkWidget *label;
```