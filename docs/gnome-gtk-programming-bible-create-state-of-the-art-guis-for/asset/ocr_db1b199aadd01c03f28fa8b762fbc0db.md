```
argv[1] = "MyRestartValue";

gnome_client_set_clone_command(client, argc, argv);
gnome_client_set_restart_command(client, argc, argv);

return(TRUE);
```

This example uses a vertical box to hold a column of labels with each label showing one of the arguments on the command line. When the program is first run, its window looks like the one in Figure 22-4. If the user shuts down the program (with the Close option from a menu, or the button in the upper-right corner), no configuration information is saved. If, on the other hand, the user logs off and chooses to save the configuration, then the `save_yourself` signal is sent to the program. The next time the user logs in, the program starts automatically and is passed the saved information. The information on the command line causes the window to look like the one in Figure 22-5.

![](bbox=[0.12, 0.44, 0.42, 0.49])

Figure 22-4: The command line with no client arguments

![](bbox=[0.12, 0.54, 0.42, 0.63])

Figure 22-5: The command line with previously saved arguments

# ## GnomeColorPicker

The `GnomeColorPicker` button pops up a `GtkColorSelectionDialog` and allows a color to be selected. The button changes color to match the currently selected color.

# ### Inheritance

```
GnomeColorPicker->GtkButton->GtkBin->GtkContainer->GtkWidget->GtkObject
```

# ### Functions

```
void gnome_color_picker_get_d(GnomeColorPicker *cp, gdouble *r, gdouble *g, gdouble *b, gdouble *a)
```