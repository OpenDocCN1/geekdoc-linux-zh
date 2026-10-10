![](bbox=[0.15, 0.11, 0.66, 0.22])

There really are two widgets involved here. The first one is the button that pops up the selection dialog box. The other is the selection dialog box that is constructed as a *GnomeDialog* widget. Whenever the button is selected, the dialog window appears for the user to select an icon. The following **example** connects a “changed” signal to the *GnomeEntry* widget inside the *GnomeIconEntry* widget; this executes the callback *eventIconChanged*() every time the user selects an icon with the mouse or types an icon name.

You can retrieve the name of the icon inside the callback *eventIconChanged*(), but it really doesn’t matter until the OK button is selected. To wait until a button is clicked, it is necessary to add the “clicked” callback to the *GnomeDialog* widget. This signal is set to execute the *eventIconSelected*() callback whenever the user selects either the OK or Cancel button. If the user selects the OK button, the name of the selected icon can be retrieved. All signals are removed from the button before the new one is attached because the *eventIconChanged*() callback can be called a number of times before the “clicked” signal arrives.

> Note 
> This double callback sequence is necessary only because the callback function *eventIconChanged*() is called every time the user clicks an icon in the browse window. While the new icon file name is available at that point, you need the other callback to determine whether the user has clicked the OK or Cancel button.

# GnomeIconSelection

This widget loads and displays a set of icons and enables the user to select one. The application must specify the directory, or directories, containing the icons to be displayed. This widget is used as the selection window in the *GnomeIconEntry* widget.

# Inheritance

```
```
GnomeIconSelection->GtkVBox->GtkBox->GtkContainer->GtkWidget->
    GtkObject
```
```

# Functions

```
```c
void gnome_icon_selection_add_defaults(
    GnomeIconSelection *gis)
void gnome_icon_selection_add_directory(
    GnomeIconSelection *gis, const gchar *dir)
```
```