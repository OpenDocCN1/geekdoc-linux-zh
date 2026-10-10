
观察路径名可以看出，该文件名为 `maxique`，并存储在用户的 `.gnome` 目录中。`set` 例程用于将键及其关联值存储在内存中（而不是磁盘上）。第 8、9 和 10 行分别将 `geometry` 类别中的键分配给整数值。`id` 类别通过第 11 到 14 行的函数调用设置。在每种情况下，第一个参数是键的完整路径，第二个参数是分配给它的值。数据保留在内存中，直到调用函数 `gnome_config_sync()` 将其写入磁盘文件。如果从未调用此函数，文件将永远不会更新。

通过调用 `gnome_config_sync()` 写入文件时，并不会覆盖已存在的值。如果您指定一个已经包含某些键的文件，并在调用 `gnome_config_sync()` 将数据写入文件之前只创建了一个新键（且未做其他操作），那么新键会被简单地添加到列表中——所有其他键和值保持不变。

以下程序读取并显示存储在此配置文件中的所有值：

```c
/* maxique2.c */

#include <gnome.h>

int main(int argc, char * argv[])

{

    time_t timeval;

    gnome_init("maxique2", "1.0", argc, argv);

    g_printf("geometry width=%d\n",

        gnome_config_get_int("/maxique/geometry/width"));

    g_printf("geometry height=%d\n",

        gnome_config_get_int("/maxique/geometry/height"));

    g_printf("geometry margin=%d\n",

        gnome_config_get_int("/maxique/geometry/margin"));

    g_printf("id name=%s\n",

        gnome_config_get_string("/maxique/id/name"));

    g_printf("id nickname=%s\n",

        gnome_config_get_string("/maxique/id/nickname"));

    g_print("id_show_menu=%s\n",

        gnome_config_get_bool("/maxique/id/show_menu")

        ? "true" : "false");

    timeval = gnome_config_get_int("/maxique/id/time");

    g_print("id_time=%s", ctime(&timeval));

    exit(0);

}
```

以 `gnome_config_get_*` 开头的函数用于从配置文件中检索数据。文件中的所有数据都以字符串形式存储，因此您的程序需要知道类型并进行相应的转换（这是通过调用相应函数完成的）。该程序的输出看起来像这样：

```
geometry width=8
geometry height=3
geometry margin=15
id name=Homer
id nickname=
id show_menu=true
id time=Mon Jul 12 14:20:44 1999
```

## 存储和检索向量

您可以将一个键分配多个值。这些值的集合可以称为列表、数组或向量。GNOME 软件通常使用术语 *vector*（向量）。要将一组值分配给一个键，您需要创建一个字符串指针数组。字符串指针数组以及它们指向的字符串是在从配置文件中读取数组时分配的。

以下示例包含两个函数。一个创建数组并将其写入配置文件；另一个从配置文件中读取并显示其找到的内容。

```c
/* configvec.c */

#include <gnome.h>

static void retrieveVector();

static void storeVector();

int main(int argc, char *argv[])

{

    gnome_init("configvec", "1.0", argc, argv);

    storeVector();

    retrieveVector();

    exit(0);

}

static void storeVector()
```

```c
15 {
16     gint user_count = 5;
17     const gchar *user_name[] = {
18         "fred",
19         "wilford",
20         "ship worth",
21         "norton",
22         "maglin"
23     };
24     gnome_config_set_vector("convec/user/names",
25             user_count,user_name);
26     gnome_config_sync();
27 }
28 static void retrieveVector()
29 {
30     gint i;
31     gint user_count;
32     gchar **user_name;
33     gnome_config_get_vector("convec/user/list",
34             &user_count,&user_name);
35     for(i=0; i<user_count; i++)
36         printf("%d: %s\n",i,user_name[i]);
37     g_strfreev(user_name);
38 }
```

第 14 行的 `storeVector()` 函数在一个名为 `convec` 的配置文件中的 `user` 类别下、以 `list` 为键存储了一个姓名列表。数组中的五个姓名中有一个包含空格。该文件的内容如下所示：

```
[user]
  names=fred\ wilford\ ship\ worth\ norton\ maglin
```

双斜杠用作转义序列，指示下一个字符不是空格，而是姓名的一部分。第 29 行的 `retrieveVector()` 函数读取姓名列表并逐一列出。返回的数组及其字符串是动态分配的，因此需要将内存归还给系统——这正是第 39 行调用 `g_strfreev()` 所做的。这是一个方便函数，用于删除数组中的每个字符串，然后删除数组本身。

## 配置文件的数据类型

表 19-1 列出了在配置文件中可用的各种数据类型。由于有如此多种操作配置设置的方法，因此设计了许多针对每种类型的函数。

**表 19-1 配置文件中存储和检索的数据类型**

| 类型 | 描述 |
| :--- | :--- |
| `bool` | 一个整数值，零表示 FALSE，非零表示 TRUE。它在文件中存储为 "true" 或 "false。" |
| `float` | 64 位浮点数（double）。它在文件中存储时带有小数点，必要时还带有指数。 |
| `int` | 32 位整数（gint）。它在文件中存储为十进制数字。 |
| `string` | 一个 ASCII 字符字符串。它可以是空的（零长度字符串）。它也可以包含空格。 |
| `translated string` | 根据当前语言设置可能不同的字符字符串。 |
| `vector` | 一个 ASCII 字符串值列表。向量可以为空；每个值可以包含空格。 |

以下是可用于与配置文件通信的函数描述列表。所有这些函数的名称都包含数据类型作为其一部分。

### 用于 bool 的函数

这些是将 `bool` 值存储在配置文件中的函数：

```c
void gnome_config_set_bool(char *path,gboolean val);
void gnome_config_private_set_bool(char *path,gboolean val);
```

`val` 的值决定了存储在配置文件中的字符串是 "true" 还是 "false"。你可以使用以下函数从配置文件中检索 `bool` 值：

```c
gboolean gnome_config_get_bool(char *path);
gboolean gnome_config_get_bool_with_default(char *path,
gboolean *def);
gboolean gnome_config_private_get_bool(char *path);
gboolean gnome_config_private_get_bool_with_default(char *path,
gboolean *def);
```
