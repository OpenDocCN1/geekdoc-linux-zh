
# GnomeFileEntry

The GnomeFileEntry widget (described in Chapter 21) enables the user to select a file.

```c
static GtkWidget *makeWidget()
{
  GtkWidget *fileentry;

  fileentry = gnome_file_entry_new("fseekid","File Seeking");
  return(fileentry);
}
```

**The string** `"fseekid"` **is the ID used to save the list of previously selected file names.** The second string is for the title bar of the `GtkFileSelection` window.

![](img/8bcc1ba72831c7d67cfc8b395deab95f_695_0.png)

Figure 22-11: A GnomeFileEntry widget with four remembered file names

## GnomeFontPicker

The GnomeFontPicker widget is a button that, when selected, presents a window that enables the user to select from among the many available fonts.

### Inheritance

`GnomeFontPicker->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject`

### Functions

```c
GtkWidget *gnome_font_picker_create_inside(
   GnomeFontPicker *gfp)
void gnome_font_picker_dialog_destroy(GtkWidget *widget,
   gpointer data)
void gnome_font_picker_fi_set_show_size(GnomeFontPicker *gfp,
   gboolean show_size)
void gnome_font_picker_fi_set_use_font_in_label(
   GnomeFontPicker *gfp, gboolean use_font_in_label,
   gint size)
void gnome_font_picker_font_extract_attr(gchar *font_name,
   gchar *attr, gint i)
void gnome_font_picker_font_set_attr(gchar **font_name,
   const gchar *attr, gint i)
GdkFont *gnome_font_picker_get_font(GnomeFontPicker *gfp)
gchar *gnome_font_picker_get_font_name(GnomeFontPicker *gfp)
GnomeFontPickerMode gnome_font_picker_get_mode(
  GnomeFontPicker *gfp)
gchar *gnome_font_picker_get_preview_text(
  GnomeFontPicker *gfp)
GtkType gnome_font_picker_get_type(void)
void gnome_font_picker_label_use_font_in_label(
  GnomeFontPicker *gfp)
GtkWidget *gnome_font_picker_new(void)
gboolean gnome_font_picker_set_font_name(
  GnomeFontPicker *gfp, const gchar *fontname)
void gnome_font_picker_set_mode(GnomeFontPicker *gfp,
  GnomeFontPickerMode mode)
void gnome_font_picker_set_preview_text(GnomeFontPicker *gfp,
  const gchar *text)
void gnome_font_picker_set_title(GnomeFontPicker *gfp,
  const gchar *title)
void gnome_font_picker_update_font_info(GnomeFontPicker *gfp)
void gnome_font_picker_ww_set_widget(GnomeFontPicker *gfp,
  GtkWidget *widget)
```

### Enum

```c
typedef enum {
  GNOME_FONT_PICKER_MODE_PIXMAP,
  GNOME_FONT_PICKER_MODE_FONT_INFO,
  GNOME_FONT_PICKER_MODE_USER_WIDGET,
  GNOME_FONT_PICKER_MODE_UNKNOWN
} GnomeFontPickerMode;
```

Chapter 13 provides examples of GnomeFontPicker.

## GnomeFontSelector

The GnomeFontSelector widget is a dialog box that manages all the details of popping up, accepting input, and returning the name of the selected font.

### Inheritance

`GnomeFontSelector->GtkDialog->GtkWindow->GtkBin->GtkContainer->GtkWidget->GObject`

### Functions

```c
gchar *gnome_font_select(void)
gchar *gnome_font_select_with_default(
  const gchar *default_font)
gchar *gnome_font_selector_get_selected(
  GnomeFontSelector *text_tool)
GtkType gnome_font_selector_get_type(void)
GtkWidget *gnome_font_selector_new(void)
```

This example demonstrates how your application can make a single function call that returns the selected font. You can call either `gnome_font_select()` or `gnome_font_select_with_default()` from anywhere in your program, and the dialog shown in Figure 22-12 appears. The function call contains its own event loop, so it does not return until the user selects a font or closes the dialog box.

```c
/** gnomefontpicker.c **/
#include <gnome.h>

int main(int argc, char *argv[])
{
    gchar *font;

    gnome_init("gnomefontpicker","1.0",argc,argv);

    font = gnome_font_select();
    if(font == NULL)
        g_print("No font selected\n");
    else
        g_print("Selected: %s\n",font);

    exit(0);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_697_0.png)

Figure 22-12: A GnomeFontSelector dialog box

## GnomeGuru

This is an unfinished widget. When finished, it will be a tool for constructing a wizard (a list of steps that changes according to which branch you take).

### Inheritance

`GnomeGuru->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtkObject`

### Functions

```c
void gnome_guru_append_page(GnomeGuru *guru, const gchar *name, GtkWidget *graphic, GnomeDialog *dialog)
void gnome_guru_back_set_sensitive(GnomeGuru *guru, gboolean sensitivity)
void gnome_guru_construct(GnomeGuru *guru, const gchar *name, GtkWidget *graphic, GnomeDialog *dialog)
GtkWidget *gnome_guru_current_page(GnomeGuru *guru)
GtkType gnome_guru_get_type()
GtkWidget *gnome_guru_new(const gchar *name, GtkWidget *graphic, GnomeDialog *dialog)
void gnome_guru_next_set_sensitive(GnomeGuru *guru, gboolean sensitivity)
```

## GnomeHRef

The GnomeHRef widget displays a frameless button that, when selected, issues a command for the web browser to connect to a Web site. The actual command to the browser is defined globally as the default member of URL Handler list in the GNOME Control Center.

### Inheritance

`GnomeHRef->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject`

### Functions

```c
gchar *gnome_href_get_label(GnomeHRef *self)
GtkType gnome_href_get_type(void)
gchar *gnome_href_get_url(GnomeHRef *self)
GtkWidget *gnome_href_new(const gchar *url, const gchar *label)
void gnome_href_set_label(GnomeHRef *self, const gchar *label)
void gnome_href_set_url(GnomeHRef *self, const gchar *url)
```

This example creates a widget with the label *Gnome’s start page* and attaches a URL to it. The widget appears as normal text, as shown in Figure 22-13, which is blue and underlined. This way, you can include it in the body of text among other widgets and it should be recognized as a link. Also, a frame appears around it when the mouse passes over it.

```c
static GtkWidget *makeWidget()
{
    GtkWidget *href;

    href = gnome_href_new("http://www.gnome.org/start",
        "Gnome's start page");

    return(href);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_699_0.png)

Figure 22-13: A GnomeHRef widget is a link to a Web site

## GnomeIconEntry

A GnomeIconEntry is a button that pops up a window displaying a collection of icons. The user can select one of the icons found in /usr/share/pixmaps or browse the file system to find icons in other directories. The pull-down list of directory names maintains a history of previously opened directories.

### Inheritance

`GnomeIconEntry->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtkObject`

### Functions

```c
char *gnome_icon_entry_get_filename(GnomeIconEntry *ientry)
GtkType gnome_icon_entry_get_type(void)
GtkWidget *gnome_icon_entry_gnome_entry(GnomeIconEntry *ientry)
GtkWidget *gnome_icon_entry_gnome_file_entry(GnomeIconEntry *ientry)
GtkWidget *gnome_icon_entry_gtk_entry(GnomeIconEntry *ientry)
GtkWidget *gnome_icon_entry_new(char *history_id,
            char *browse_dialog_title)
void gnome_icon_entry_set_icon(GnomeIconEntry *ientry,
            const char *filename)
void gnome_icon_entry_set_pixmap_subdir(GnomeIconEntry *ientry, const char *subdir)
```

The following example creates a button that, when clicked, displays the dialog box shown in Figure 22-14. If the user selects an icon, the button changes to display the icon—as shown in Figure 22-15.

```c
static GtkWidget *makeWidget()
{
    GtkWidget *iconentry;
    GtkWidget *entry;

    iconentry = gnome_icon_entry_new("historyID",
                "Select an Icon");
    entry = gnome_icon_entry_gtk_entry(
                GNOME_ICON_ENTRY(iconentry));
    gtk_signal_connect(GTK_OBJECT(entry),"changed",
                GTK_SIGNAL_FUNC(eventIconChanged),iconentry);
    return(iconentry);
}

void eventIconChanged(GtkWidget *widget,
    GnomeIconEntry *iconentry)
{
    GtkWidget *dialog;

    dialog = GNOME_ICON_ENTRY(iconentry)->pick_dialog;
    if(dialog != NULL) {
        gtk_signal_handlers_destroy(GTK_OBJECT(dialog));
        gtk_signal_connect(GTK_OBJECT(dialog),"clicked",
            eventIconSelected,iconentry);
    }
}

void eventIconSelected(GtkWidget *widget, gint button,
    GnomeIconEntry *iconentry)
{
    gchar *iconfile;

    switch(button) {
    case 0:
        iconfile = gnome_icon_entry_get_filename(iconentry);
        g_print("Icon file name: %s\n",iconfile);
        break;
    case 1:
        g_print("No icon selection was made\n");
    }
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_700_0.png)

Figure 22-14: The Icon Selection dialog box of the GnomeIconEntry widget
