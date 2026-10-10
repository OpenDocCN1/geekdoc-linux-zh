![](bbox=[0.19, 0.13, 0.34, 0.2])

**Figure 22-13: A GnomeHRef widget** is a link to a Web site

# ## GnomeIconEntry

A GnomeIconEntry is a button that pops up a window displaying a collection of icons. The user can select one of the icons found in /usr/share/pixmaps or browse the file system to find icons in other directories. The pull-down list of directory names maintains a history of previously opened directories.

# ### Inheritance

GnomeIConEntry->GtkVBox->GtkBox->GtkContainer->GtkWidget->GtKObject

# ### Functions

```
char *gnome_icon_entry_get_filename(GnomeIConEntry *ientry)
quint gnome_icon_entry_get_type(void)
GtkWidget *gnome_icon_entry_gnome_entry(GnomeIConEntry *ientry)
GtkWidget *gnome_icon_entry_gnome_file_entry(GnomeIConEntry *ientry)
GtkWidget *gnome_icon_entry_gtk_entry(GnomeIConEntry *ientry)
GtkWidget *gnome_icon_entry_new(char *history_id,
            char *browse_dialog_title)
void gnome_icon_entry_set_icon(GnomeIConEntry *ientry,
            const char *filename)
void gnome_icon_entry_set_pixmap_subdir(GnomeIConEntry *ientry, const char *subdir)
```

The following example creates a button that, when clicked, displays the dialog box shown in Figure 22-14. If the user selects an icon, the button changes to display the icon—as shown in Figure 22-15.

```
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
```