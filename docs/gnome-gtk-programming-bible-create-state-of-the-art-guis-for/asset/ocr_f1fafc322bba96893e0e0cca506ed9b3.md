```
```C
toolbar = gtk_toolbar_new(GTK_ORIENTATION_HORIZONTAL, GTK_TOOLBAR_ICONS);
gtk_container_set_border_width(GTK_CONTAINER(toolbar),1);

uibdata.connect_func = uib_signal;
uibdata.data = NULL;
uibdata.is_interp = FALSE;
uibdata.relay_func = NULL;
uibdata.destroy_func = NULL;
gnome_app_fill_toolbar_custom(GTK_TOOLBAR(toolbar), toolbarDef, &uibdata,NULL);

return(toolbar);

static void uib_signal(GnomeUIInfo *uinfo,gchar *signal_name,
    GnomeUIBuilderData *uibdata)
{
}
```
```

![](bbox=[0.17, 0.45, 0.58, 0.7])

**Figure 22-9:** A docking window showing three toolbars

As each toolbar is created, it is inserted into `GnomeDockItem` with a call to `gtk_container_add()`. Then, in turn, the `GnomeDockItem` is added to the `GnomeDockLayout`. Finally, the `GnomeDockLayout` is added to the `GnomeDock` with the call to `gnome_dock_layout_add_to_dock()`.

The `GnomeApp` window provides a simpler way to create toolbars. You can see some examples of this in Chapter 8.