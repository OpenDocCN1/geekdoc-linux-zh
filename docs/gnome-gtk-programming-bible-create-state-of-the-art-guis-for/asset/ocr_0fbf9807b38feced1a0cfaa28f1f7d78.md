GnomeMDIGenericChild \*child, GnomeMDIChildViewCreator func,  
GtkCallbackMarshal marshal, gpointer data,  
GtkDestroyNotify notify)

See Chapter 17 for examples of GnomeMDIGenericChild.

# # GnomeMessageBox

A GnomeMessageBox is a dialog box you can use to display a simple message and  
get a response. The dialog box is created as its own top-level window. It displays a  
standard icon, a text message, and a row of buttons.

**Inheritance**  
GnomeMessageBox->GnomeDialog->GtkWindow->GtkBin->GtkContainer->  
GtkWidget->GtkObject

**Functions**  
```
 guint gnome_message_box_get_type()
 GtkWidget *gnome_message_box_new(const gchar *message,
 const gchar *message_box_type, ...)
 GtkWidget *gnome_message_box_new(const gchar *message,
 const gchar *message_box_type, const gchar *buttons)
 void gnome_message_box_set_default(
 GnomeMessageBox *message_box, gint button)
 void gnome_message_box_set_modal(
 GnomeMessageBox *message_box)
```

A GnomeMessageBox is a wrapper around GnomeDialog for the purpose of  
simplifying the interface. It automatically includes the text message and an  
appropriate icon. Also, after responding to the mouse and the callback, it shuts  
itself down. Chapter 3 has examples and information on a set of predefined dialog  
boxes.

The following example asks a question and provides three buttons for the user to  
choose (as shown in Figure 22-18).

```
```c
/** gnomebox.c **/
#include <gnome.h>

static void messageboxCallback(GtkWidget *widget,
 gint button, gpointer data);

int main(int argc, char *argv[])
{
 GtkWidget *messagebox;
 gnome_init("gnomebox", "1.0", argc, argv);
```
```