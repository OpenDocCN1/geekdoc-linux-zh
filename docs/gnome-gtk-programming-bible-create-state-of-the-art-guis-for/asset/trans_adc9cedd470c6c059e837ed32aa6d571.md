
# 19
## 配置与国际化工具

### 本章要点

- 读取一组环境变量设置，这些设置可用于配置应用程序
- 编写自定义的环境设置，以便在下次运行应用程序时可用
- 调整程序代码的结构，使其在运行时可以被翻译成其他语言

本章讨论两个相关主题。一个主题是应用程序可以保存和恢复的配置设置，另一个主题是程序在不同区域设置中使用时自动翻译自身的方法。

默认情况下，配置设置存储在用户的主目录中。这意味着每个用户可以有不同的设置。此外，配置值以纯 ASCII 格式存储，因此任何有权访问这些文件的人都可以按需对其进行编辑或处理。

国际化（也称为 i18n，因为 i 和 n 之间有 18 个字母）是相当自动化的。在编写代码时，需要翻译的字符串会被标记出来。利用这些标记的字符串，人工将它们翻译成另一种语言并安装到磁盘上。当用户启动程序，且区域设置指示文本应被翻译时，软件会将程序中的字符串替换为其翻译版本。

## 环境控制

程序可以有用户配置文件来保存设置和值，使这些设置和值能够从一个调用延续到下一次调用。例如，如果在运行应用程序期间，用户更改了字体、窗口大小和一些颜色，那么需要存储这些值，以便下次运行程序时检索和使用它们。

GNOME API 包含一组函数，可用于存储值，以便稍后检索和使用。当程序开始运行时，它可以读取配置设置，并使用找到的值来自定义其操作。程序还可以读取配置值，并可选择性地更改它们并将它们写回。由于配置设置保存在磁盘上的文件中，因此它们可以从程序的一次调用持续到下一次调用。

### 配置文件格式

配置存储在一个 ASCII 文本文件中。文件格式包含类别，每个类别内部包含键。键与值相关联。这是一个包含两个标题和五个键的示例文件：

```
[winsize]
width=120
height=80

[colors/names]
background=white
edges=blue
lettering=gray42
```

名为 *winsize* 的类别包含键 `width` 和 `height`。每个键的值都是整数。类别 *colors/names* 包含键 `background`、`edges` 和 `lettering`。这三个键的值都是字符串。请注意，文件中不包含类型信息——读取和写入值的程序决定实际的数据类型。

### 配置文件位置

默认情况下，文件位于用户主目录下的 `.gnome` 或 `.gnome_private` 子目录中。虽然通常使用 `.gnome` 目录，但您可能会发现将某些配置数据存储到 `.gnome_private` 目录中是有用的。区别在于 `.gnome` 目录对所有人可访问，而 `.gnome_private` 目录通常限制为一个用户可访问。如果您计划存储敏感信息（如密码），请考虑使用 `.gnome_private`。

函数每次处理一个键值，因此必须在每次函数调用中指定键的完整路径。路径名由以下格式的三部分组成：

```
/filename/category/keyname
```

*filename* 是存储配置数据的文件的名称。虽然它以斜杠开头，但它不是绝对路径名。实际的文件路径是这样构建的——包括用户的主目录名：

```
/home/fred/.gnome/filename
```

或者，如果您使用处理私有值的函数调用，文件路径名看起来像这样：

```
/home/fred/.gnome_private/filename
```

地址总是包含三部分：文件、类别和键名。也就是说，每个地址都是键的完整路径名。为了完成上述两个地址，必须像这样包含类别和键名：

```
/home/fred/.gnome/filename/winsize/width
/home/fred/.gnome_private/filename/winsize/width
```

您还有另一个选项。通过在文件名周围加上等号，您可以指定绝对路径，并将配置文件放在任何位置。这可能是处理适用于所有用户的任何配置设置的最好方式。例如：

```
=/var/maxique/config=/colors/background
```

这将文件存储在绝对路径名 /var/maxique/config 中。

### 读写配置文件

当应用程序第一次向其写入数据时，会创建配置文件。从缺失的配置文件中读取，或尝试读取不存在的键，都不是错误——返回值指示该函数具有 NULL 或零值。以下文件是以下示例程序读写的那个文件：

```
[geometry]
width=8
height=3
margin=15

[id]
name=Homer
nickname=
show_menu=true
time=931815930
```

此文件有两个类别：geometry 和 id。geometry 类别为 width、height 和 margin 定义了数值。id 类别指定了一个名称，但没有昵称的设置。布尔键 show_menu 为 true，而 time 是配置文件上次更新的时间。以下程序用于创建此文件。

```c
/* maxique1.c */
#include <gnome.h>

int main(int argc, char *argv[])
{
    gnome_init("maxique", "1.0", argc, argv);
    gnome_config_set_int("/maxique/geometry/width", 8);
    gnome_config_set_int("/maxique/geometry/height", 3);
    gnome_config_set_int("/maxique/geometry/margin", 15);
    gnome_config_set_string("/maxique/id/name", "Homer");
    gnome_config_set_string("/maxique/id/nickname", NULL);
    gnome_config_set_bool("/maxique/id/show_menu", TRUE);
    gnome_config_set_int("/maxique/id/time", time(NULL));
    gnome_config_sync();
    exit(0);
}
```

观察路径名可以看出，该文件名为 maxique，并存储在用户的 .gnome 目录中。“set”例程用于将键及其关联值存储在内存中（而不是磁盘上）。第 8、9 和 10 行分别将 geometry 类别中的键分配给整数值。id 类别通过第 11 到 14 行的函数调用设置。在每种情况下，第一个参数是键的完整路径，第二个参数是分配给它的值。数据保留在内存中，直到调用函数 gnome_config_sync() 将其写入磁盘文件。如果从未调用此函数，文件将永远不会更新。

通过调用 gnome_config_sync() 写入文件时，并不会覆盖已存在的值。如果您指定一个已经包含某些键的文件，并在调用 gnome_config_sync() 将数据写入文件之前只创建了一个新键（且未做其他操作），那么新键会被简单地添加到列表中——所有其他键和值保持不变。

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
