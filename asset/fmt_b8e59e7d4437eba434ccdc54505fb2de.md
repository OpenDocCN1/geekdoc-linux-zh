
# GNOME 官方开发者指南

## 2.6.3 Marshallers

```
_my_marshal__INT__VOID
_my_marshal__VOID__INT
_my_marshal__UINT__BOOLEAN
```

其中 `my_marshal` 是你的前缀。幸运的是，你不需要实际上编写封化器代码；有一个名为 `glib-genmarshall` 的工具可以完成这些工作。例如，为了创建上述封化器，请在名为 `my_marshaller.list` 的文件中放入：

```
INT:VOID
VOID:OBJECT, INT
```

文件格式非常直观；每行定义一个新的封化器，以返回类型开头。冒号之后列出参数类型。你可以根据本节之前的表格确定有效的类型。

要生成实际代码，请运行以下命令：

```
glib-genmarshall --prefix my_marshal --header my_marshaller.list > my_marshaller.h
glib-genmarshall --prefix my_marshal --body my_marshaller.list > my_marshaller.c
```

你现在有了源文件 `my_marshaller.c` 和头文件 `my_marshaller.h`。

你不需要提供前缀。默认是 `g_signal`，但如果你选择了其他的，请注意在调用处理程序的地方必须链接这些符号。`my_marshaller.h` 文件如下：

```c
#ifndef MY_SHALLER_H__

#include <glib-object.h>

G_BEGIN_DECLS

/* INT:VOID */
extern void _my_marshal__INT__VOID(GClosure *closure,
GValue *return_val,
gint n_params,
const GValue *params,
gpointer data,
Gpointer *error);

/* VOID:OBJECT, INT */
extern void _my_marshal__VOID__OBJECT_INT(GClosure *closure,
GValue *return_val,
gint n_params,
const GValue *params,
gpointer data,
Gpointer *error);

/* UINT:BOOLEAN_BOOLEAN */
extern void _my_marshal__UINT__BOOLEAN_BOOLEAN(GClosure *closure,
GValue *return_val,
gint n_params,
const GValue *params,
gpointer data,
Gpointer *error);

G_END_DECLS

#endif /* MY_SHALLER_H__ */
```

如果你正在构建 `Makefile`，创建封化器的规则如下：

```make
my_marshaller.h: my_marshaller.list
	glib-genmarshall --prefix my_marshal --header my_marshaller.list

my_marshaller.c: my_marshaller.list
	glib-genmarshall --prefix my_marshal --body my_marshaller.list
```

此书中没有提供累加器（accumulator）的示例（空间有限），但很容易找到一个：解压 GTK+ 源码，进入发行版的顶层目录，并运行此命令：

```bash
grep GSignalInvocationHint /*
```

此命令会打印源文件中所有包含累加器的行。

## 2.6.5 为信号附加处理器

正如你将在第 3 章的小部件中看到的那样，你希望为同类型的对象附加不同的信号处理器（例如，如果你有两个按钮对象，你不希望这两个按钮执行完全相同的操作）。

这段代码使用 `g_signal_connect()` 在 `media` 对象的解包信号上附加了一个新的处理器 `meep_meep`：

```c
static void meep_meep(Media *media)
{
    int nr;
    g_object_get(media, "inventory-id", &nr, NULL);

    g_print("Meep-meep! (Inventory number: %d)\n", nr);
}
// <-- ...
```

```c
gulong handler_id;
```

```c
/* 连接新处理器 */
handler_id = g_signal_connect(media,
    "unpacked",
    (GCallback) meep_meep,
    NULL);
```

```c
/* 测试新处理器 */
g_signal_emit_by_name(media, "unpacked");
/* 期望输出 "meep-meep" 信息，以及其他处理器的输出 / */
```

在例例中，`GSignal` 在默认信号处理器之前调用了 `meep_meep()`，因为默认处理器在安装时使用了 `G_SIGNAL_RUN_FIRST`。

附加处理器的最常用方法是使用：

```c
gulong handler_id;
```

```c
handler_id = g_signal_connect(object, name, function, data);
```

- `object` (指针)：目标对象。
- `name` (const char*)：信号名称。
- `function` (GCallback*)：新的信号处理器。此回调函数函数的原型必须与实例结构体中的一致，但你可能需要对参数进行类型转换。
- `data` (指针)：用于信号处理器的可选数据。

你将在本书中看到许多可选数据指针处理器的用法，例如第 3.3 节描述的那种。通常情况下，`GSignal` 尝试将数据作为最后一个参数传递给信号。然而，如果你想使用一个接受数据指针作为第一个参数的处理器，请使用：

```c
g_signal_connect_swapped(object, name, function, data)
```

如果你的处理器是一个只接受一个参数的库函数，你可能想这样做。示例见第 3.6.10 节。

```c
g_signal_connect_after(object, name, function, data)
```

这与 `g_signal_connect()` 几乎相同，不同之处函数在第 2.6.2 节列出的第 5 阶段运行，而不是第 3 阶段。其理念是让你可以在默认处理器之后运行处理器，但正如你在该节看到的，你在安装默认处理器时也可以覆盖它。

所有 `g_signal_connect*()` 都返回一个处理器绑定的标识符。如果你将标识符存储为 `handler_id`，就可以检查绑定状态：

```c
g_signal_handler_is_connected(object, handler_id)
```

要移除绑定，请调用：

```c
g_signal_handler_disconnect(object, handler_id)
```

以下是一些示例：

```c
/* 测试并断开处理器 */
if (g_signal_handler_is_connected(media, handler_id))
{
    g_print("meep_meep is connected to media. Detaching...\n");
}
g_signal_handler_disconnect(media, handler_id);

if (!g_signal_handler_is_connected(media, handler_id))
{
    g_print("meep_meep no longer connected:\n");
    g_signal_emit_by_name(media, "unpacked");
}
```

**注意** 请记住，连接到任何对象的任何处理器都是基于单个对象的，不适用于该类的其他部分。你还可以在信号发射期间连接、断开和阻塞信号。

## 2.6.6 细节

信号细节（details）是信号的进一步细分。要在信号名称中指定细节，请附加两个冒号和细节名称（例如 `unpacked:ding`）。

当你连接处理器或发射信号时，可以添加细节信息。当你发射带细节的信号时，`GSignal` 会调用带该细节的处理器以及完全不带细节的处理器。`GSignal` 不会调用与给定发射不匹配的细节的处理器。此外，如果你发射不带细节的信号，`GSignal` 将不会调用任何连接了细节的处理器。你可以从下面的示例中理解这一点：
