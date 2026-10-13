
| `TARGETS` | `ATOM`, `TARGETS` | 当前有效的目标列表。 |

| `TEXT` | | 所有者选择的编码的选择文本。 |

| `TIMESTAMP` | `INTEGER` | 获取选择所有权的时间。 |

| `USER` | `TEXT` | 运行所有者的用户名称。 |

> `text` 目标仅存在于转换请求。其目的是让所有者能够最方便的编码提供文本数据。生成的目标名称和类型永远不会是 `TEXT`。表 20.1 类型列中的 `TEXT` 一词仅表示将返回文本类型的指示。例如，这可以是 `STRING` 或所有者选择的任何其他编码。

第二类目标使用标准的 MIME 类型作为目标名称。这种方法比以前的方法好得多，因为所有名称之间都有逻辑关系，并随着新 MIME 类型的通用而保持更新。唯一的缺点是这种方法最近才被采用，许多旧的 X11 应用程序可能不支持它们。表 20.2 是一些已知 MIME 类型的列表。

# 实现选择

## 表 20.2 可作为目标名称的示例 MIME 类型

| 目标 (Target) | 类型 | 接收到的数据 |
| --- | --- | --- |
| text/plain | TEXT | 选择的标准文本表示。 |
| text/html | TEXT | 选择的 HTML 表示法。 |
| text/tab-separated-values | TEXT | 使用制表符作为分隔符的选择的选择，主要用于表示数据库数据。 |
| text/uri-list | TEXT | 任意数量的空终止字符串，代表 URI（统一资源标识符）。 |
| text/xml | TEXT | 选择的 XML 表示法。 |

你可以使用 `Gclipper` 分析由其他应用程序注册但未在此列表中的目标。然后你可以使用 `Gclipper` 报告的相同名称。

> MIME（多用途互联网邮件扩展）最初是为了扩展电子邮件的功能而开发的。互联网电子邮件的原始格式仅限于 ASCII 文本。为了支持更丰富的字符、外语言和多媒体数据，必须提供一个新的标准。

关于 MIME 技术的概览可以在 `http://www.mindspring.com/~mgrand/mime.html` 找到。

注册的 MIME 媒体类型的官方列表可以查询 `http://www.isi.edu/in-notes/assignments/media-types/media-types`。

要获取更多关于 MIME 后层技术细节的信息，请阅读以下 RFC（征求意见）：`RFC 2045`, `RFC 2046`, `RFC 2047`, `RFC 2048`, `RFC 2049`。这些可以在 `http://www.rfc-editor.org/rfc.html` 找到。

## 强制目标

X11 架构规范定义了几个目标为强制性。这些是 `TARGETS`、`MULTIPLE` 和 `TIMESTAMP`。你不需要自己负责为这些目标提供数据；它们由 `GTK+` 自动且透明地支持。

`TARGETS` 和 `TIMESTAMP` 的含义在之前讨论过。`MULTIPLE` 提供了一种通过一次转换请求恢复多个目标数据的方法。然而，无法通过标准的 `GTK+` 函数调用恢复此类请求的数据。

目标的声明通过填充 `GtkTargetEntry` 结构体完成。该结构体的定义如下：

```
struct GtkTargetEntry {
  gchar *target;
  guint flags;
  guint info;
}
```

结构体成员的含义如下：

| 成员 | 含义 |
| --- | --- |
| target | 包含目标名称的字符串。 |
| flags | 这些仅在拖放上下文中使用。在下一节中会有更多介绍。 |
| info | 应用程序特定的整数，稍后将通过信号传回。这允许为目标附加附加信息。 |

必须支持多个目标，并且 `info` 字段必须对多个不同的函数可用。因此，最好在一个包含 `GtkTargetEntry` 结构体的数组中全局定义目标。列表 20.2 就是一个示例。

## 列表 20.2 使用 GtkTargetEntry 结构体数组

```
1: typedef enum
2: {
3: STRING,
4: TEXT,
5: TIMESTAMP
6:) targetInfo;
7:
8: static GtkTargetEntry target_entries[] =
9: {
10: { 'STRING', 0, STRING },
11: { 'TEXT', 0, TEXT },
12: { 'TIMESTAMP', 0, TIMESTAMP }
13: };
```

目标目标信息常量定义在枚举中（第 1–6 行）。在创建（第 8 行）并初始化（第 10–12 行）包含三个 `GtkTargetEntry` 结构体的数组后，支持的目标有 'STRING'、'TEXT' 和 'TIMESTAMP'。每个目标名称与其对应的信息常量关联。

## 注册目标

下一步是为特定的选择和小部件注册支持的目标。可以使用 `gtk_selection_add_target()` 函数来注册单个目标。完整的原型如下：

```
void gtk_selection_add_target(GtkWidget *widget, GdkAtom selection,
            GdkAtom target, guint info);
```

`gtk_selection_add_target()` 的参数为：

| 参数 | 说明 |
| --- | --- |
| widget | 指向要注册目标的小部件的指针。 |
| selection | 与要注册的目标的选择对应的原子（atom）。 |
| target | 与你想要注册的目标名称对应的原子。 |
| info | 应用程序特定的整数，稍后将通过信号传递（参见“定义目标”中 `GtkTargetEntry` 结构体的定义）。 |

通常，你可能通过调用 `gtk_selection_add_targets()` 一次注册所有目标。完整的原型如下：

```
void gtk_selection_add_targets(GtkWidget *widget, GdkAtom selection,
            const GtkTargetEntry *targets, guint ntargets);
```

`gtk_selection_add_targets()` 的参数为：

| 参数 | 说明 |
| --- | --- |
| widget | 指向要注册目标的小部件的指针。 |
| selection | 与要注册的目标的选择对应的原子。 |
| targets | 指向已填充的 `GtkTargetEntry` 结构体数组的指针。 |
| ntargets | 数组中的条目数量。 |

为了允许灵活修改目标条目，最好计算目标数量而不是使用常量。这种计算可以这样完成：

```
static guint ntargets = sizeof(target_entries) / sizeof(target_entries[0]);
```

*(注：此处原文代码块不完整，但根据上下文推断为计算数组长度)*

*(注：原文中存在多处格式错误导致的乱码或重复，翻译时已根据逻辑进行了修正优化)*

[注：由于原文在后半部分存在大量无意义的重复和格式乱码（可能是由于复制粘贴错误），上述翻译已在保持原意的基础上对逻辑可读性进行了清理。]

表 20.3 列出了最常用目标类型的格式。

## 表 20.3 最常用目标类型的格式

| 目标类型 | 格式 |
| --- | --- |
| ATOM | 32 |
| COMPOUND_TEXT | 8 |
| INTEGER | 32 |
| STRING | 8 |

如果你需要知道上述未列出的目标的类型或格式，可以使用 `GClipper` 来分析目标以及其他应用程序注册的相应信息。然后你只需要简单地使用相同的值即可。

> 如你在第 13 天“GLib 基础函数”中所学到的，存储包含多个字节的变量有两种不同的技术：大端序（big-endian）和小端序（little-endian）。大端序系统首先存储最高位字节（持有数值高位部分的字节）。小端系统首先存储最低位字节。

这些术语源于乔纳森·斯威斯的《格列列夫游记》。在书中，对于小人国来说，从哪一端打开水煮蛋是一项重大的政治问题。大端人从大端打开，而小端人则从小端打开。

为 `STRING` 和 `INTEGER` 类型提供数据相对容易。如果产生任何疑问，你可以查看本节末尾提供的简单示例。然而，`COMPOUND_TEXT` 类型的数据必须符合预定义的标准。因此，最好使用 `gdk_string_to_compound_text()` 函数来格式化文本。其原型如下：

```
gint gdk_string_to_compound_text(gchar *string, GdkAtom *encoding, gist *format, guchar *text, gist *length);
```
