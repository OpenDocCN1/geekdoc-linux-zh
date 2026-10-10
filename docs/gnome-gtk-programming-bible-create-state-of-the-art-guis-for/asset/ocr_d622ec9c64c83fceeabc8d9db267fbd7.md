**Table 19-1**
**Data Types Stored and Retrieved in the Configuration Files**

| Type | Description |
| :--- | :--- |
| `bool` | An integer value with zero representing FALSE and non-zero representing TRUE. It is stored in the file as "true" or "false." |
| `float` | A 64-bit floating point number (double). It is stored in the file with a decimal point and, if necessary, an exponent. |
| `int` | A 32-bit integer (gint). It is stored in the file as base-10 digits. |
| `string` | An ASCII string of characters. It can be empty (the zero-length string). It also can contain spaces. |
| `translated string` | A character string that may vary depending on the current language setting. |
| `vector` | A list of ASCII string values. The vector can be empty; each value may contain spaces. |

The following is a descriptive list of the functions available for communicating with the configuration files. All of these functions include the data type as part of its name.

# **Functions for bool**

These are the functions that store `bool` values in the configuration file:

```
```c
void gnome_config_set_bool(char *path,gboolean val);
void gnome_config_private_set_bool(char *path,gboolean val);
```
```

The value of `val` determines whether the string to be stored in the configuration file is "true" or "false." You can use the following functions to retrieve a `bool` value from the configuration file:

```
```c
gboolean gnome_config_get_bool(char *path);
gboolean gnome_config_get_bool_with_default(char *path,
gboolean *def);
gboolean gnome_config_private_get_bool(char *path);
gboolean gnome_config_private_get_bool_with_default(char *path,
gboolean *def);
```
```

If the value is not found in the configuration file, the default value of FALSE is returned. If the *def* argument is specified, the `gboolean` value it points to is set to TRUE—if the value is found in the file. It is set to FALSE if the default value is returned.