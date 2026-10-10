# ### Functions for float

These are the functions that store float values in the configuration file:

```
```c
void gnome_config_set_float(char *path,gdouble val);
void gnome_config_private_set_float(char *path,gdouble val);
```
```

The value of val is converted to a character string and stored in the configuration file. You can use the following functions to retrieve a float value from the configuration file:

```
```c
gdouble gnome_config_get_float(char *path);
gdouble gnome_config_get_float_with_default(char *path,
    gboolean *def);
gdouble gnome_config_private_get_float(char *path);
gdouble gnome_config_private_get_float_with_default(char *path,
    gboolean *def);
```
```

If the value is not found in the configuration file, the default value of 0.0 is returned. If the def argument is specified, the gboolean value it points to is set to TRUE —if the value is found in the file. It is set to FALSE if the default value is returned.

# ### Functions for int

These are the functions that store int values in the configuration file:

```
```c
void gnome_config_set_int(char *path,gint val);
void gnome_config_private_set_int(char *path,gint val);
```
```

The value of val is converted to a character string and stored in the configuration file. You can use the following functions to retrieve an int value from the configuration file:

```
```c
gint gnome_config_get_int(char *path);
gint gnome_config_get_int_with_default(char *path,
    gboolean *def);
gint gnome_config_private_get_int(char *path);
gint gnome_config_private_get_int_with_default(char *path,
    gboolean *def);
```
```

If the value is not found in the configuration file, the default value of 0 is returned. If the def argument is specified, the gboolean value it points to is set to TRUE —if the value is found in the file. It is set to FALSE if the default value is returned.

# ### Functions for string

These are the functions that store string values in the configuration file:

```
```c
void gnome_config_set_string(char *path,gchar *val);
void gnome_config_private_set_string(char *path,gchar *val);
```
```