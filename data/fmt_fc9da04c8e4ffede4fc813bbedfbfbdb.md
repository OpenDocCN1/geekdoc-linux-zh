
`gtk_set_locale()` 是一个调用 `gtk_init()` 的封装函数（如果你的应用程序决定调用它的话）。`gtk_set_locale()` 由 `gdk_set_locale()` 调用，后者又调用 `locale(LC_ALL)`，导致根据用户环境中由 `LANG` 环境变量定义的区域来读取本地化数据库。关于应用程序国际化的更多详细信息，请参考 `locale(1)` 和 `locale(7)` 手册。如果你不调用 `gtk_set_locale()`，区域将默认为可移植的“C” 区域。

除了 `setlocale()` 之外，还调用了两个 Xlib 库：`XSupports_locale()` 和 `XSetLocaleModifiers()`。如果 `XSupports_locale()` 失败，则 X 不支持 `LANG` 环境变量定义的区域，应用程序将回退到可移植的“C”区域。`XSetLocaleModifiers()` 读取 `XMODIFIERS` 环境变量，它由一系列“category=value”组成。修饰符是 `setlocale()` 处理的 LANG 变量的 X 扩展。截至 R6 定义的唯一标准修饰符是“im”，用于指定用于本地化文本输入的输入方法。更多信息请参阅 `XSetLocaleModifiers()`。

当 `setlocale(locale)` 或 `XSetLocaleModifiers()` 失败时，`gtk_set_locale()` 将生成一个或多个警告。无论成功与否，都会返回当前的区域字符串。为了确保用户的区域选择得到尊重，你应该将返回的字符串与 `LANG` 环境变量进行比较，如果不匹配则退出，如下所示：

```c
gchar *envlang, *lang;

envlang = getenv("LANG");

lang = gtk_set_locale();
```

```c
if ( envlang != (char *) NULL && strcmp(lang, envlang) ) {
    fprintf(stderr, "Unable to set locale to %s\n", envlang);
    exit( 1 );
}
```

我们将查看的下一个可选函数是 `gtk_check_version()`：

```c
gchar *
gtk_check_version(guint major, guint minor, guint micro)
```

`gtk_check_version()` 接受三个参数：主版本、次版本和微版本。调用此可以使你的应用程序确保 Gtk+ 的主、次版本和微版本符合要求。

### 表 2.1 Gtk+ 识别的命令行参数

| 参数名称 | 描述 |
| :--- | :--- |
| `--gtk-module` | 在启动时加载模块。模块将在下一节介绍。 |
| `--g-fatal` | Gtk+ 生成的警告和错误会导致应用程序退出。 |
| `--gtk-debug` | 开启特定的 Gtk+ 跟踪消息。 |
| `--gtk-no-debug` | 关闭特定的 Gtk+ 跟踪消息。 |
| `--gdk-debug` | 开启特定的 GDK 跟踪消息。 |
| `--gdk-no-debug` | 关闭特定的 GDK 跟踪消息。 |
| `--display:s.d` | 连接到指定的服务器，“h”是主机，“s”是服务器号（通常为 0），“d”是显示号。 |
| `--sync` | 在建立 X 服务器连接后调用 XSync(display, True)。 |
| `--no-xshm` | 禁用 X 共享内存。 |
| `--name` | 将程序名称设置为 "name"。未指定则设置为 argv[0]。 |
| `--class` | 按照 X 约定，程序的类是首字母大写的程序名称。 |

## 模块

Gtk+（通过 Glib）允许应用程序在运行时加载共享库代码并执行共享库导出的程序。Glib 提供的机制本质上是 `dlopen(3)` 手册中描述的程序的封装。如果你不熟悉此功能，现在是查看 `dlopen(3)` 手册的好时机。Gtk+ 要求共享库导出一个名为 `gtk_module_init()` 的函数，该函数将在模块加载后由 Gtk+ 调用。`gtk_module_init()` 函数需要确认以下导入原型：

```c
G_MODULE_EXPORT void
gtk_module_init (int *argc, gchar **argv);
```

# 应用启动、终止和主循环函数

模块机制可以用于为应用程序添加插件支持。在我讨论 Glib 时会更多地介绍模块，但目前你只需要知道——`--gtk-module` 是指定应用程序在运行时加载的共享库（插件）的方式之一。

如果出发布的产品需要 `--gtk-module`，最好将其用法封装在脚本中，为用户提供一个简单的接口。例如，如果你的应用程序是一个文字处理器，而你提供在一个名为 `spell.so` 的共享库中提供了一个拼写检查插件模块。与其强制用户执行：

```bash
$ myedit --gtk-module spell myfile
```

不如让用户提供一个名为 `runedit` 的 shell 脚本，该脚本接受一个 `-s` 参数，例如：

```bash
$ runedit -s myfile
```

并让该脚本构建前面的命令行并代表用户执行它。或者，更好的方法是将用户想要的所有选项放在偏好文件中，并让你的脚本读取该文件并创建相应的命令。

在启动时由 Gtk+ 加任何模块的另一种方法是使用 `GTK_MODULES` 环境变量。每个组件由一个模块名称组成，用 `:` 分隔。例如，要加载 `libfoo.so`、`libfee.so` 和 `libbar.so`，你需要设置 `GTK_MODULES=foo:fee:bar`

```bash
$ typeset -x GTK_MODULES=foo:fee:bar
```

## 调试参数

剩余的命令行参数（`--gtk-debug`、`--gtk-no-debug`、`--gdk-debug` 和 `--gdk-no-debug`）控制 Gtk+、GDK 和 Glib 在应用程序运行时显示的调试信息。某些调试输出对应用程序设计人员感兴趣；其他信息对于致力于 Gtk+、GDK 或 Glib 特定部分的人来说非常重要。在本节中，我将尝试在此列出的命令行参数外，涵盖编译时和运行时调试支持的所有方面。

## 编译时

在编译时，有四个定义可以控制应用程序在运行时提供的调试信息量。

- **`G_ENABLE_DEBUG`**: 该编译时标志会被 Gtk+、GDK 和 Glib 代码识别。如果定义，对于 Glib 1.2.0，Glib 中唯一重要的区域是 `gdate` 模块，当发生任何异常情况时，它会在几处生成信息消息。Gtk+ 必须带有 **`G_ENABLE_DEBUG`** 编译，以便在启动时解析 `--gtk-debug`、`--gdk-no-debug` 和 `--gdk-no-debug` 命令行参数，并识别 **`GDK_DEBUG`** 和 **`GTK_DEBUG`** 环境变量。各种 Gtk 和 GDK 模块必须带有 **`G_ENABLE_DEBUG`** 编译，才能启用它们提供的调试支持。例如，编译 `GDK-and-drop`、X 输入法 (XIM)，将启用拖放、视觉和彩色文本模块的调试。一个模块是否实际生成调试输出由调试命令行参数和/或 `GDK_DEBUG` 标志控制。

- **`G_DISABLE_ASSERT`**: 如果启用，Glib 的 `g_assert()` 和 `g_assert_not_reached()` 宏被定义为无所作为。否则，在整个 Gtk+、Glib 和 GDK 中广泛使用的 `g_assert()` 和 `g_assert_not_reached()` 宏将被启用。

- **`G_DISABLE_CHECKS`**: 如果启用，Glib 的 `g_return_if_fail()` 和 `g_return_val_if_fail()` 宏被定义为无所作为。与 `g_assert_not_reached()` 类似，这些宏被用于整个 Gtk、Glib 和 Gtk。

- **`GTK_NO_CHECK_CASTS`**: 如果启用，将在不同对象类型之间进行检查。在第 3 章“信号、事件、对象和类型”中，我将介绍对象和缓存。如 `GTK_OBJECT`、`GTK_WINDOW` 和 `GTK_BUTTON` 等用作强制转换或对象变量以锚定部件或类的宏将执行额外的代码以验证转换是否有效。启用 `GTK_NO_CHECK_CASTS` 将禁用此检查。

你可以在 Gtk 配置时启用或禁用 `G_ENABLE_DEBUG`、`G_DISABLE_ASSERT`、`G_DISABLE_CHECKS` 和 `GTK_NO_CHECK_CASTS` 吗？配置脚本接受 `--enable-debug`。如果设置为“minimum”（默认值），将执行廉价的完整性检查，并设置 `GTK_NO_CHECK_CASTS` 以禁用对象转换检查。如果设置为“yes”，则设置 `G_ENABLE_DEBUG`。设置为“no”或指定配置脚本选项 `--disable-debug`，则通过设置 `G_DISABLE_ASSERT`、`G_DISABLE_CHECKS` 和 `GTK_NO_CHECK_CASTS` 来禁用调试端口。

运行时。如果 Gtk+ 是开启调试的情况下编译的（即定义了 `G_ENABLE_DEBUG`），则运行的各种调试信息基于模块进行控制，使用 `GTK_DEBUG` 和 `GDK_DEBUG` 环境变量以及 Gtk+ 支持的 `--gtk-debug`、`--gtk-no-debug` 和 `--gtk-no-debug` 命令行参数。如果存在，则先应用环境变量，然后是命令行参数。

# 第 2 章 · Hello Gtk+

## 应用启动、终止与主循环函数

### Gtk+ 主循环函数

在本章的开头，我介绍了函数 `gtk_main()`：

```c
void
gtk_main (void)
```

我们已经看到，一旦 Gtk+ 应用调用了 `gtk_main()`，Gtk+ 就会接管控制权。`gtk_main()` 本质上是一个循环，不断等待用户输入（如按键和鼠标移动），并根据接收到的任何输入调用由你的应用程序为控件注册的信号函数。你的大部分代码逻辑都位于这些信号函数中；除了 `main` 函数中调用 `gtk_main()` 之前的代码外，大部分代码都位于信号函数的上下文中。当然，这条规则也有例外，我们将在本书的后半部分进行介绍：UNIX 信号函数、X 错误处理器等均属于这些例外。

### 终止主循环

要退出 `gtk_main()`，你的应用程序必须调用 `gtk_main_quit()`：

```c
void
gtk_main_quit (void)
```

`gtk_main_quit()` 基本上导致 `gtk_main()` 跳出循环并返回。大多数应用程序会在与“退出”（Quit or Exit）按钮菜单相关的信号函数内部调用 `gtk_main_quit()`。

Gtk+ 允许 `gtk_main()` 嵌套，这很有帮助，因为有时你可能需要在信号函数内部调用 `gtk_main()`。我将在以后讨论对话框时涵盖 `gtk_main()` 嵌套调用的用法。注意，每次对 `gtk_main()` 的调用都对应一次对 `gtk_main_quit()` 的调用。

应用程序可以通过 `gtk_main_level()` 获取 `gtk_main()` 的当前嵌套深度：

```c
guint
gtk_main_level (void)
```

返回 0 表示你的应用程序当前没有执行 `gtk_main()` 的上下文。返回 1 表示正在生效的是一次 `gtk_main()` 调用，依此类推。

### 控制主循环

在类似于需要嵌套 `gtk_main()` 的情况下，应用程序可能会调用 `gtk_main_iteration()`。`gtk_main_iteration()` 会导致 Gtk+ 对主循环进行单次通过，处理下一个可用事件并允许控件调用信号函数等。然而，在本章稍后描述的初始化和退出函数不会被调用；这些函数仅通过调用 `gtk_main()` 来被触发。以下是 `gtk_main_iteration()` 的函数原型：

```c
gint
gtk_main_iteration (void)
```

# 第 2 章 · Hello Gtk!

使用 `gtk_main()` 的优点是 `gtk_main()` 会执行一个无限运行的循环，直到应用程序从信号内部调用 `gtk_main_quit()` 为止。如果你的程序注册了初始化和退出函数，它们将在每次进入循环时被调用。如果这些初始化或退出函数对你的应用程序至关重要，请使用 `gtk_main()`。如果它们不需要被调用，或者在执行下一个主循环的上下文中调用它们对应用程序有害，请改用 `gtk_main_iteration()`，因为 `gtk_main_iteration()` 内部不会触发初始化或退出函数。

单次调用 `gtk_main_iteration()` 可能无法完成应用程序所需的任务。通常，你的应用程序进入一个循环，不断调用 `gtk_main_iteration()`，直到在信号函数中设置了某个标志。例如：

```c
flag = 0;
while (!flag)
    gtk_main_iteration();
```

在这种情况下，标志最终会在从 `gtk_main_iteration()` 触发的信号函数中被设置。

### 检查等待事件

应用程序可以通过调用 `gtk_events_pending()` 判断事件队列中是否有任何待处理事件：

```c
gint
gtk_events_pending(void)
```

如果在调用时没有待处理的事件，`gtk_events_pending()` 将返回 `FALSE`；否则返回 `TRUE`。`gtk_events_pending()` 不阻塞，也不会处理事件队列中的等待事件。我们可以修改前面的循环，在没有等待处理的事件时执行应用程序特定的任务，如下：

```c
flag = 0;
while ( gtk_events_pending() == TRUE )
    gtk_main_iteration();
else
    do_something();
```

在这里，如果 `gtk_events_pending()` 返回 `TRUE`，则通过调用 `gtk_main_iteration()` 分发事件。否则，调用 `do_something()` 执行其相应功能。在本章稍后描述的超时或空闲函数是组织此类循环的另一种且可能更好的方法，由 Gtk+ 定期调用你的代码，而不是你的代码调用 Gtk+。

### 初始化与退出函数

你可以向 Gtk+ 注册初始化函数，这些函数将在应用程序下次调用 `gtk_main()` 时被调用。可以注册任意数量的函数，但每个函数必须具有以下原型：

```c
void
function( gpointer data );
```

要添加函数，请调用 `gtk_init_add()`：

```c
void
gtk_init_add(GtkFunction function, gpointer data)
```

第一个参数是你想要的函数指针；第二个参数可以是任何强制转换为指针的值。如果你需要向初始化函数传递多个值，请将这些值存储在一个结构体中，并传递一个指向该结构体的指针。你必须确保在 Gtk+ 调用初始化函数时数据是有效的。

每调用一次 `gtk_init_add()`，函数和数据就会被添加到 Gtk+ 维护的列表中。下次调用 `gtk_main()` 时，所有注册的初始化函数将按照添加的顺序执行。

退出函数与初始化函数类似，但它们在主循环终止时被调用。要注册退出函数，请使用 `gtk_quit_add()`：

```c
void
gtk_quit_add(GtkFunction function, gpointer data)
```

第一个参数是你想要的函数指针；第二个参数可以是任何强制转换为指针的值。如果你需要向退出函数传递多个值，请将这些值存储在一个结构体中，并传递一个指向该结构体的指针。你必须确保在 Gtk+ 调用退出函数时数据是有效的。

每调用一次 `gtk_quit_add()`，函数和数据就会被添加到 Gtk+ 维护的列表中。当调用 `gtk_main_quit()` 时，所有注册的退出函数将按照添加的反顺序执行。

## 应用启动、终止与主循环函数

当邮件用户代理需要检查邮件服务器时，邮件用户代理将向邮件服务器发送命令，请求用以判断是否有新邮件送达的信息，并等待服务器的响应。简而言之，在轮询新邮件时启用了以下步骤：

1. 等待整个轮询间隔（例如 2 分钟）结束
2. 向邮件服务器发送命令，请求邮箱信息（例如，信箱中有多少条消息），并等待邮件服务器的响应

正如我将说明的那样，这两个任务都可以通过使用像 Gtk+ 提供的超时机制来实现。Gtk+ 中有两个提供超时支持的程序：`gtk_timeout_add()` 和 `gtk_timeout_remove()`。它们的函数原型如下：

```c
guint
gtk_timeout_add (guint32 interval, GtkFunction function, gpointer data)
```

以及

```c
void
gtk_timeout_remove (guint tag)
```
