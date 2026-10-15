
```c
g_free(path);

/* 销毁对象 */

g_object_unref(client);
```

添加父目录后，你无法向 GConf 客户端添加子目录。例如，添加 `/apps/my_app/this` 是无效的。

## 读写 GConf 值

在创建客户端和目录后，你就可以开始读写键值的实际工作了。这些函数检索：

- `gconf_client_get_int(GConfClient *client, const gchar *key, GError **error)`
- `gdouble gconf_client_get_float(GConfClient *client, const gchar *key, GError **error)`

返回 `GConfClient` 对象中键对应的整数。如果不存在该键或发生错误，此函数返回 0 作为默认值。与之前一样，错误会出现在 `error` 中。

与前一个函数类似，用于浮点值。默认值是 0.0。

- `boolean gconf_client_get_bool(GConfClient *client, const gchar *key, GError **error)`

# 读写 GConf

# GNOME 开发者官方指南

与预测函数类似，用于布尔值。默认值为 FALSE。
- `gchar *gconf_client_get_string(GConfClient *client, const gchar *key, GError **error)`

返回新分配的字符串，如果键不存在或发生某些错误则返回 NULL。
- `GList *gconf_client_get_list(GConfClient *client, const gchar *key, GConfValueType type, GError **error)`

返回元素列表，但仅当列表匹配类型时。类型包括：

```
GCONF_VALUE_INT

GCONF_VALUE_FLOAT

GCONF_VALUE_BOOL

GCONF_VALUE_STRING
```

新列表的元素是无类型指针。对于整数和布尔值，你只需要对元素进行强制转换。
- `gboolean gconf_client_get_pair(GConfClient *client, const gchar *key, GConfValueType type1, GConfValueType type2, gpointer *val1, gpointer *val2, GError **error)`

与预测函数类似，用于键对：`type1` 和 `type2` 指明键对中的类型；`val1_target` 和 `val2_target` 指向键对的一些值（对于字符串，你必须提供指针的地址）。成功后，此函数返回 TRUE。

相似的函数设置键的值并在成功时返回 TRUE。当出现问题时，返回值为 FALSE，错误显示在 `error` 中。

- `gboolean gconf_client_set_int(GConfClient *client, const gchar *key, gint value, GError **error)`

将键的值设置为整数。
- `gboolean gconf_client_set_float(GConfClient *client, const gchar *key, gdouble value, GError **error)`

将键的值设置为浮点数。
- `gboolean gconf_client_set_bool(GConfClient *client, const gchar *key, boolean value, GError **error)`

将键的值设置为布尔值。
- `gboolean gconf_client_set_string(GConfClient *client, const gchar *key, gchar *value, GError **error)`

将键的值设置为字符串。
- `GList gconf_client_set_list(GConfClient *client, const gchar *key, GConfValueType type, GList *list, GError **error)`

将键的值设置为列表：列表中的元素类型为 `type`。
- `gboolean gconf_client_set_pair(GConfClient *client, const gchar *key, GConfValueType type1, GConfValueType type2, gpointer *value1, gpointer *value2, GError **error)`

将键的值设置为键对。

# GNOME 开发者官方指南

设置键的值：第一个元素位于 `value1` 之后，类型为 `type1`；第二个元素位于 `value2` 之后，类型为 `type2`。

所有的 GConf 数据库事务都是异步的。在您调用 `gconf_client_set_*` 函数后，新值可能不会立即对其他进程可用；`gconfd2` 会等到它有时间来设置该值。因此，你不应该将 GConf 值用于关键的进程间通信。

在尝试写入一个值之前，您可以检查其键是否为只读：

```
gconf_client_key_is_writable(client, path, error)
```

如果该键是只读的，则返回 FALSE；如果可以对其值进行写入，则返回 TRUE。

以下是一些读取和写入值的示例代码：

```
GConfClient *client;

GSList *list, *l_ptr;

gchar *name;

int *n;

/* 读取某些值 */

g_print("Your desktop has %d workspace(s).\n",

 gconf_client_get_int(client,

  "/desktop/gnome/applications/window_manager/number_of_workspaces",

  NULL));

g_print("The desktop names are:\n",

 list = gconf_client_get_list(client,

  "/desktop/gnome/applications/window_manager/workspace_names",

  GCONF_VALUE_STRING,

  NULL));

for (l_ptr = list; l_ptr != NULL; l_ptr = glist_next(l_ptr))

{

  g_print("%s\n", (gchar *)l_ptr->data);

  g_free(l_ptr->data);

}

g_list_free(list);

g_print("*s\n");

if (gconf_client_get_bool

  (client, "/desktop/gnome/applications/cursor_blink", NULL))

{

  g_print("Your cursor blinks.\n");

} else {

  g_print("Your cursor does not blank.\n");

}

name = gconf_client_get_string(client,

  "/desktop/gnome/interface/gtk_theme",

  NULL);

g_print("Your GTK+ theme is: %s\n", name);

g_free(name);

/* 写入某些值 */

gconf_client_set_int(client, "/example/number", 42, NULL);
```

## 7.3.2 读取和写入 GConf 值

```
gconf_client_set_float(client, "example/pi", 3.14159, NULL);

gconf_client_set_bool(client, "example/state", FALSE, NULL);

gconf_client_set_string(client, "example/message", "Hello, World.", NULL);
```

```
/* 将一个整数列表放入 conf 值中 */

list = NULL;

list = g_list_append(list, G_TO_POINTER(42));

list = g_list_append(list, G_TO_POINTER(37));

list = g_list_append(list, G_TO_POINTER(1217));

gconf_client_set_list(client, "example/nums", GCONF_VALUE_INT, list);

g_list_free(list);
```

```
/* 设置一对值；一个数字和一个字符串 */
```
