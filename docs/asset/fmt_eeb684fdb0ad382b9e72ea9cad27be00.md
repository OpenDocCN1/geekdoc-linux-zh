
```c
list = g_list_append(list, conf_value);

conf_value = gconf_value_new(GCONF_VALUE_STRING);

gconf_value_set_string(conf_value, "tomorrow");

list = g_list_append(list, conf_value);

/* 将列表放入 ConfValue（conf_list） */

conf_value = gconf_value_new(GCONF_VALUE_LIST);

gconf_value_set_list_type(conf_value, GCONF_VALUE_STRING);

gconf_value_set_list_nocopy(conf_value, list);

/* 使用诊断函数打印字符串 */

string = gconf_value_to_string(conf_value);
```

# GNOME 2 开发者官方指南

```c
g_print("conf_value = %s\n", string);

g_free(string);

conf_value_free(conf_value);
```

## `GConfEntry`

你可以通过 `GConfEntry` 进一步使用 `GConfValue`，它是一个包含键（key）及其值的数据结构。要创建一个 `GConfEntry` 数据结构，请调用此函数：

```c
GConfEntry *entry;

entry = gconf_client_get_entry(client, NULL, use_default, error);
```

在这里，`client` 和 `error` 分别是你在之前看到的访问函数中的 `GConfClient` 对象、键（key）结构体和错误指针。如果你想获取 schema 的默认值，请将布尔参数 `use_default` 设置为 TRUE。第三个参数本应该是本地语言（locale），但目前尚不支持。请使用 `NULL` 作为默认本地语言。

你可以使用以下两个函数从 `GConfEntry` 结构中获取键或 `GConfValue`：

```c
const char *gconf_entry_get_key(const GConfEntry *entry)

GConfValue *gconf_entry_get_value(const GConfEntry *entry)
```

注意，`gconf_entry_get_value()` 函数如果其键没有值，可能会返回 `NULL`。你应该始终通过这种方式进行检查。要释放 `GConfEntry` 结构体，请调用

```c
gconf_entry_free(entry)
```

如果你在释放 `entry` 之前想保留内部的 `GConfValue`，请先调用此函数：

```c
conf_value = gconf_entry_steal_value(entry);
```

记住，你有责任释放 `conf_value`。

这里是其他几个可以帮助你复制 `gconftool–2` 导航功能的 GConf API 函数：

- `boolean gconf_client_dir_exists(GConfClient *client, const char *dir, GError **error)`
  如果 `dir` 存在于 GConf 数据库中，返回 TRUE。
- `GList *gconf_client_all_entries(GConfClient *client, const char *dir, GError **error)`
  返回 `dir` 中所有键值的 `GConfEntry` 结构体列表。
- `GList *gconf_client_all_dirs(GConfClient *client, const char *dir, GError **error)`
  返回 `dir` 中所有目录的列表。列表元素是新分配的字符串，包含每个子目录的绝对路径。在完成列表后，请确保在释放列表之前释放字符串。

## 7.3.2 读取和写入 `GConfValue`

- `boolean gconf_client_unset(GConfClient *client, const gchar *path, GError **error)`
移除路径处的目录或键并返回 TRUE。如果不存在此类项或为只读，此函数将返回 FALSE 并设置错误。

现在是来看一个示例了：一个在每个目录及其子目录中搜索并打印内容的程序，类似于 `gconf2 -R`。你不需要包含整个 GNOME 包含路径：

```c
/* -coding: utf-8; - */

/* gconfilister.c - 列出 GConf 数据库中的内容 */

#include <gnome.h>

#include <gconf/gconf-client.h>

/* 要列出的路径 */

#define PATH ""

接下来的 `list_contents` 过程处理了所有工作。参数是一个 GConf 客户端、一个路径和当前深度。该函数通过带有 `depth+1` 调用自身来更新深度。

/* 递归列出 GConf 数据库中路径下的项 */

void list_contents(GConfClient *client, gchar *path, int depth)

{

    GList *subdirs = NULL, *entries = NULL, *p;

    int i;

    gchar *path=value_str;
```

准备工作包括错误检查、提取目录内容以及打印目录名：

```c
/* 确保这是一个目录 */

if (!gconf_client_dir_exists(client, path, NULL))

{

    g_printer("%s: 数据库中没有此类 GConf 目录\n", path);

    return;

}

/* 提取路径下的所有子目录 */

subdirs = gconf_client_all_dirs(client, path, NULL);

/* 提取路径下的所有项 */

entries = gconf_client_all_entries(client, path, NULL);

/* depth 是当前目录深度；在输出前打印空格 */

if (depth)

{

    for (i=0; i < depth; i++)

    {

        g_print(" ");

    }

}

/* 打印目录名 */

g_print("%s\n", path);
```

为了打印每个子目录的内容，此函数遍历子目录列表并在每个子目录上再次调用自身。

```c
/* 打印子目录内容 */

if (subdirs)

{

    for (p = subdirs; p != NULL; p = g_slist_next(p))

    {

        list_contents(client, p->data, depth+1);

        g_free(p->data);

    }

    g_slist_free(subdirs);

}
```

最后一项是打印当前目录中可能存在的任何键的值：

```c
/* 打印目录中的所有项 */

if (entries)

    for (p = entries; p != NULL; p = g_slist_next(p))

    {

        /* 如果目录中存在 */
```

`main` 函数创建了 `client`：

```c
int main(int argc, char **argv)

{

    GnomeProgram *program;

    GConfClient *client;

    program = gnome_init(&argc, &argv, NULL);

    client = gconf_client_open(NULL, FALSE, NULL);

    list_contents(client, PATH, 0);

    gconf_client_close(client);

    gnome_main_quit();

    return 0;

}
```

## 7.3.3 GConf 通知

为了检测 GConf 中的变化，你的应用程序应该做出反应。`GConfNotify` 的原型如下：

```c
typedef void (*GConfNotify)(GConfClient *client, guint id, GConfEntry *entry, gpointer user_data);
```

在这里，`client` 和 `entry` 分别是 `GConfClient` 和 `entry`；`user_data` 是传递的数据。你可以使用此函数向 GConf 附加回调：

```c
```
