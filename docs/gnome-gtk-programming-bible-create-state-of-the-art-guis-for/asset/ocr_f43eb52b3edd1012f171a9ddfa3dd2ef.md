# GtkFlagsValue *

```
gtk_type_flags_find_value(GtkType flag_type,
		const gchar *value_name)

gtk_type_flags_get_values(GtkType flags_type)
```

# GtkItemFactory *

```
gtk_item_factory_from_path(const gchar *path)

gtk_item_factory_from_widget(GtkWidget *widget)

gtk_item_factory_new(GtkType container_type, const gchar *path,
	GtkAccelGroup *accel_group)
```

# GtkMenuFactory *

```
gtk_menu_factory_new(GtkMenuFactoryType type)
```

# GtkMenuPath *

```
gtk_menu_factory_find(GtkMenuFactory *factory,
		const char *path)
```

# GtkObject *

```
gnome_gentry_edit_new(void)

gnome_gentry_edit_new_notebook(GtkNotebook *notebook)

gnome_mdi_new(gchar *appname, gchar *title)

gtk_adjustment_new(gfloat value, gfloat lower, gfloat upper,
	gfloat step_increment, gfloat page_increment,
	gfloat page_size)

gtk_object_new(GtkType object_type,
	const gchar *first_arg_name, ...)

gtk_object_newv(GtkType object_type, guint n_args,
	GtkArg *args)

gtk_xmhtml_parser_new()
```