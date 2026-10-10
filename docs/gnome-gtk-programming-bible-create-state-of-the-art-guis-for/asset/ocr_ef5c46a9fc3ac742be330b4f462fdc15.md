GtkFileSelection widget (described in Chapter 21) that enables the user to select a file.

```
```c
static GtkWidget *makeWidget()
{
  GtkWidget *fileentry;

  fileentry = gnome_file_entry_new("fseekid","File Seeking");
  return(fileentry);
}
```
```

**The string** `"fseekid"` **is the ID used to save the list of previously selected file names.** The second string is for the title bar of the `GtkFileSelection` window.

![](bbox=[0.17, 0.38, 0.44, 0.48])

Figure 22-11: A GnomeFileEntry widget with four remembered file names

# ## GnomeFontPicker

The GnomeFontPicker widget is a button that, when selected, presents a window that enables the user to select from among the many available fonts.

# **Inheritance**

```
`GnomeFontPicker->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject`
```

# **Functions**

```
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
```
```