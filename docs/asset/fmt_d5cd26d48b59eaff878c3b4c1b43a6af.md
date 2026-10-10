
在此处，`argDesc` 是 `"DISPLAY"`，`desc` 是 `"X to use."`。记住为这两个字符串标记为需要翻译。

`desc` 对于 `POPT_ARG_INCLUDE_TABLE` 的含义略有不同，以防它在帮助输出中是一个“组”选项。以下输出中的“Help options”：

- Help options
  -?
  -usage Show this help message  Display brief usage message

如果你在表的开头放置类型为 `POPT_ARG_CALLBACK` 的条目，将调用用户定义的回调，并带有命令行上每个选项的信息。以下是你的回调所需的类型：

```c
typedef void (*poptCallbackType)(poptContext con,
  enum poptCallbackReason,
  const struct poptOption *opt,
  const char *arg,
  void *data);
```

不透明的 `poptContext` 包含了 popt 状态的所有对象。这使得在同一个程序中使用多次或同时使用多个选项成为可能。你还可以使用 popt 的函数从 `poptContext` 中提取有关当前解析状态的信息。

可能的 `popCallbackReason` 值为：

- `POPT_CALLBACK_REASON_PRE`
- `POPT_CALLBACK_REASON_POST`
- `POPT_CALLBACK_REASON_OPTION`

你的回调会在命令行上的每个选项处被调用，并以 `POPT_CALLBACK_REASON` 作为参数。如果你请求，它也可以在解析之前和之后调用。在这些情况下，返回 `POPT_CALLBACK_REASON_PRE` 或 `POPT_CALLBACK_REASON_POST`。要指定你想让回调在解析之前或之后被调用，你必须将一个标志与 `POPT_ARG_CALLBACK` 结合。例如，以下 `struct poptOption` 初始化器指定了在参数解析之前和之后都调用的回调：

```c
NULL, '\0', POPT_ARG_CALLBACK|POPT_CBFLAG_PRE|POPT_CBFLAG_POST,
    &parse_an_arg_callback, 0, NULL
```

传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。传递回调的 `opt` 参数是对应于最近看到的选项的 `struct popOption`。 (此处省略了原文中重复的文本内容)

```c
struct pptOption options[] = {
  "greet",
```

# 第 5 章 Gnome 应用基础

```
'g',
POPT_ARG_NONE,
&greet_mode,
0,
N_("向命令行中列出的特定人物打问候"),
NULL,
{
  "message",
  'm',
  POPT_ARG_STRING,
  &message,
  0,
  N_("指定一个除\"Hello, World!\"以外的消息的消息"),
  N_("MESSAGE")
},
{
  "geometry",
  'g',
  POPT_ARG_STRING,
  &geometry,
  0,
  N_("指定主窗口的几何形状"),
  N_("GEOMETRY")
},
NULL,
'0',
0,
NULL,
0,
NULL,
NULL
};
```

这是 `main()` 的第一部分，其中 Gnome 检查参数是否正确编译，并组装了一个需要问候的人员列表：

```c
GtkWidget* app;
poptContext pctx;
char** args;
int i;
GList* greet = NULL;
GnomeClient* client;
bindtextdomain(PACKAGE, GNOMELOCALEDIR);
textdomain(PACKAGE);
gnome_init_with_popt_table(PACKAGE, VERSION, argc, argv,
options, 0, &pctx);
```

```c
/* 解析参数 */
args = poptGetArgs(pctx);
if (greet_mode && args)
```

```c
i = 0;
while (args[i] != NULL)
{
    greet = g_slist_prepend(greet, args[i]);
    ++i;
}
/* 为它们排序 */
greet = g_slist_reverse(greet);
} else if (greet_mode && args == NULL)
{
    g_error("你必须指定一个问候的对象。");
}
else if (args != NULL)
{
    g_error("命令行参数仅允许配合 -greet 使用。");
}
else
{
    g_assert(!(greet_mode && args == NULL));
}
poptFreeContext(pctx);
```
