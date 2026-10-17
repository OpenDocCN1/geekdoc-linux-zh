
现在，你迫不及待想要开始编码，渴望探索只有 GNOME 才能提供的力量。很好，你来对地方了。在本节中，我们将一起学习创建一个简单的应用程序，在屏幕上显示一个窗口，并配备工具栏以及菜单（包括带有图标的菜单项）。

我本以为这只是很小的应用程序，但在 GTK+ 中实现类似的功能需要一些代码。正如你将看到的，在 GNOME 中，这种应用程序在代码规模方面的现实是非常微不足道的。我还会向你展示如何编译，如果你不想经历创建源码树的麻烦，或者你目前没有可用 Glade 来创建源码树的话。

## 初始化

就像 GTK+ 一样，在开始调用创建窗口和其他内容的函数之前，有必要初始化 GNOME 库。这仅涉及调用 `gnome_init`，其形式如下：

```c
int gnome_init (const char * app_id,
                const gchar *app_version,
                gint argc,
                gchar ** argv);
```

你可以看到，它与 `gtk_init` 有些不同，但执行的是相同的功能。调用时，`gnome_init` 会设置所有 GNOME 内部变量和结构，并初始化 GNOME 应用程序可能使用的所有其他库——包括 GTK+。这是一个非常重要的点。如果你在应用程序中调用了 `gnome_init`，就不需要再调用 `gtk_init` 了。

调用的前两个参数 `app_id` 和 `app_version` 允许你向 GNOME 传递有关应用程序的一些标识信息。这被 GNOME 内部用于跟踪哪些 GNOME 资源属于哪些 GNOME 应用程序，并用于提供的任何标准 GNOME 反馈（例如运行应用程序的命令行上的警告和错误消息）。

## 引入 GNOME

后两个参数基本上与调用 `gtk_init` 时的参数相同。我之所以这么说，是因为 GNOME 处理命令行参数的方式与 GTK+ 的方式有重要区别。像 GTK+ 一样，GNOME 会查看你传递给 `gnome_init` 的命令行参数，但它不会改变它们。如果你记得的话，`gtk_init` 会剥离任何传递给应用程序且被 GTK+ 识别为需要它处理的参数。由于由于原因，注意你不是作为指针传递它们，而是通过值进行传递。

让我们使用 `gnome_init` 开始启动应用程序。在你最喜欢的代码编辑器中启动一个新的源文件 `GnomeTest.c` 并输入以下内容：

```c
#include <gnome.h>

static gchar app_id[] = { "GnomeTest" };

gint main (int argc, gchar * argv[]) {
    gnome_init ( app_id, "1.0", argc, argv);
    return 0;
}
```

这里已经有一些重要的点需要注意。首先，我们注意到我们为包含 `app_id` 的字符串设置了一个字符数组。这的理由是，有惊数量的 GNOME 函数调用要求你传递应用程序 ID。这可以在不同函数之间变化，因此将其放入静态变量中供以后重用是有意义的。

在理想的应用程序中，我们还将应用程序版本放在字符数组中，由某些源码控制系统（如 RCS）更新。然而，它不像应用程序 ID 那么必须，而且这是一个非常简单的示例应用程序。

此外，你有没有注意到应用程序顶部的 `#include` 行非常简单，而且完全没有提到 GTK+？正如你将在本书的后续部分认真学习 GNOME 编程时将看到的，你仍然需要对 GTK+ 库进行大量调用。单独包含 `gnome.h` 就会为你处理包含 `gtk/gtk.h`。

## 编译 GNOME 应用程序

你可能已经发现，这个应用程序目前几乎没有做任何有价值的事情。尽管如此，它现在是一个 GNOME 应用程序了，调用了 GNOME 用户界面库并使用了 GNOME 头文件。现在是向你展示如何编译 GNOME 应用程序的好时机，而无需经历为这个微小应用程序构建源码树的所有麻烦。

记得 `gtk-config` 吗？你当然记得。那么，发现有一个 GNOME 的等效工具可能不会太意外。然而，它使用起来稍微复杂一点。

```
$ gnome-config [OPTION]
用法: gnome-config [OPTION]
```

通用选项

- `--version`   显示版本

- `--help`      显示帮助

编译选项

- `--flags`     编译器标志

- `--libs`      链接信息

| arginfo | 说明 |

| :--- | :--- |

| `POPT_ARG_INTL_DOMAIN` | 此参数在指定时，指示使用哪种语言进行应用程序中文本的翻译。 |

虽然有很多选项，但坦率地说，你大多数时候可能只会使用前四个。

如上方的结构定义所示，`arg` 的值很大程度上取决于你分配给 `arginfo` 的值。通常情况下，你需要将其设置为一个变量。如果 `argInfo` 设置为 `POPT_ARG_NONE`，你将 `arg` 设置为一个布尔变量。如果找到了表条目中指定的参数，则该变量被设置为 `TRUE`。如果 `argInfo` 设置为 `POPT_ARG_CALLBACK`，你将 `arg` 设置为调用回调函数，这一点我们将在书的稍后部分再进行详细介绍。

调用末尾的两个描述 `desc` 和 `argDesc` 用于向用户提供如何使用你定义的选项的信息。看，一旦你设置应用程序自动解析命令行，你就会自动启用 GNOME 的帮助功能来打印 `--help`。你使用最后两个参数来帮助用户了解你自己的选项。第一个描述选项本身，而第二个用于在你将选项设置为变量时，例如今天许多应用程序支持的 `DISPLAY` 或 `GEOMETRY` 变量。只需将变量名放在那里即可。

在展示代码中如何实现它之前，值得仔细观察一下命令行：

```
$ someprogram --value value2 value3
```

大多数命令行可以分为三个不同的部分。第一部分显然是你想要运行的应用程序名称。第二部分包含应用程序选项列表，即你为 `popOptions` 填充的那种类型。第三部分也是最后一部分是应用程序参数列表，在本例中为 `value1`、`value2` 和 `value3`。现在，你对这些参数的操作通常取决于命令行上设置的选项。当你调用 `popGetArgs` 获取参数时：

```
char **popGetArgs ( popContext const );
```

它返回一个指向字符串数组的指针，即传入的参数列表（示例中的 `value1`、`value2` 和 `value3`）。`context` 是一个允许你在应用程序之间共享一组选项和参数的东西——只要两个或多个应用程序使用相同的上下文值，它们就能获取相同的参数列表。

当你使用 pop 表初始化 GNOME 时，上下文会返回给你。

```
int
gnome_init_with_pop_table ( const char* app_id,
const char * app_version,
int argc,
char ** argv,
const struct popOption * options,
int flags,
poptContext* return_ctx );
```

## 介绍 GNOME

上下文的指针作为调用的最后一个参数传入。别担心那个 `flags`——它在 GNOME 中还没有什么实用的作用。

是时候付诸行动了。加载你的 `GnomeTest.c` 代码并将其修改如下所示（我为你高亮了更改）：

```c
#include <gnome.h>

static gchar app_id[] = { "GnomeTest" };

/* popOptions table */
static gboolean SayHi = FALSE;

struct popOption options[] = {
  { "hello", 'h', POPT_ARG_NONE, &SayHi, 0, "Just says Hi", NULL,
  { NULL, '\0', 0, NULL, 0, NULL, NULL }
};

gint
 main (int argc, gchar * argv[]) {
  poptContext context;

  gnome_init_with_pop_table ( app_id, "1.0", argc, argv,
  options, 0, &context );

  poptFreeContent ( context );

  if ( SayHi ) {
    g_print ("You asked for it...Hi!\n");
  }

  return 0;
}
```

你的应用程序执行了一些操作。编译后，在命令行上带有 `--help` 参数运行，你会得到这些：

```
$ ./GnomeTest --help
Usage: GnomeTest [OPTION...]

GNOME Options
  --disable-sound             禁用声音服务器使用
  --enable-sound              启用声音服务器使用
  --speaker-HOSTNAME:PORT      运行使用的声音服务器的主机:端口
  --version

Help options
  -?, --help                  显示此帮助消息
  --usage                     显示简要的用法消息
```

```
GTK options-debug=FLAGS
--gdk-debug=FLAGS
--gdk-no-debug=FLAGS
--display=DISPLAY
--sync
--no-xsm
--name=NAME
--class=CLASS
--xgid_host=HOST
--xgid_port=PORT
--xim-preedit=STYLE
--xim-status=STYLE
--gtk-debug=FLAGS
--gtk-no-debug=FLAGS
--fatal-warnings
--gtk-module=MODULE

要设置的 Gdk 调试标志
要取消的 Gdk 调试标志
使用的 X 调试
使 X 调用同步
不使用共享内存扩展
窗口管理器使用的程序名
要设置的 Gtk+ 调试标志
要取消的 Gtk+ 调试标志
将所有警告视为致命
加载额外的 Gtk 模块

GNOME GUI options
--disable-crash-dialog
会话管理选项
--sm-client-id=ID
--sm-config-prefix=PREFIX
--sm-disable
指定管理 ID
指定保存配置的前缀
与会话管理器断开

GnomeTests
-h, --hello
Just says Hi GNOME 会自动列出它通过 pop table 定义的自己的参数。在我们的例子中，这些是 `-h` 或 `--hello`。查看代码，特别是定义 options 的部分。注意的是，你需要在数组末尾创建一个空的 `popOption` 结构，就像我在这里这样做的，这样 pop 解析就知道选项已经结束了。

几乎每个图形应用程序都围绕一个核心的 GNOME 对象展开。这个对象并不是神秘的，它只是继承自书中第一部分过的 `GtkWindow`。它相比标准的 `GtkWindow` 提供了一组函数，可以非常方便地获取带有标准状态栏、工具栏的窗口。创建一个相对容易，只需调用 `gnome_app_new` 即可。

```
GtkWidget * gnome_app_new ( const gchar * appname, const gchar * title );
```

返回一个指向 `GtkWidget` 的指针。由于 `GNOMEAPP` 是 `GtkWindow` 的子类，可以使用指针对任何窗口执行常规操作，如连接信号处理器、更改特性（大小和位置）等。函数本身非常简单，只需要两个参数。第一个是调用 `gnome_init` 时使用的 `appname`。一旦创建并显示（感谢调用了 `gtk_widget_show`），就可以调用 `gtk_main` 运行应用程序。尝试一下：继续修改 `GnomeTest.c` 来创建一个 `GNOMEAPP` 对象并显示它。我们还将编写一个信号处理器来处理窗口销毁。

```c
#include <gnome.h>

static gchar app_id[] = {"GnomeTest"};

/* popOptions table */

static gboolean SayHi = FALSE;

struct popOption options[] = {

    "hello", 'h', POPT_ARG_NONE, &SayHi, 0, "Just says Hi", NULL,

    NULL, '\0', 0, NULL, NULL

};

void

CloseTheApp (GtkWidget * window, gpointer data)

{

    gtk_main_quit();

}

gint

main (int argc, char * argv[])

{

    GtkWidget * mainappwindow;

    popContext context;

    gnome_init_with_pop_table ( app_id, "1.0", argc, argv,

    options, 0, &context);

    poptFreeContext ( context );

    if ( SayHi)

    g_print ("You asked for it..Hi!");

    mainappwindow = gnome_app_new ( app_id, "This is my first GNOME app" );

    gtk_window_set_default_size ( GTK_WINDOW (mainappwindow), 320, 200 );

    gtk_signal_connect ( GTK_OBJECT (mainappwindow), "destroy",

    GTK_SIGNAL_FUNC (CloseTheApp), NULL );

    gtk_widget_show (mainappwindow);

    gtk_main ();

    return 0;

}
```

编译并运行此应用程序，你就能第一次看到 `GNOMEAPP` 窗口。

![](img/aa3546013f120531cd191b770d8586c_307_0.png)

还没有什么，但你拥有的是非常强大的功能基础。例如，从现在开始向你的应用程序添加菜单和工具栏确实非常容易。

## 菜单和工具栏

由于 `GNOMEAPP` 对象真的是 `GtkWindow` 的派生类，没有什么能阻止你使用 GTK+ 创建菜单和工具栏并将它们挂载到 `GNOMEAPP` 窗口。事实上，GNOME 提供了几个函数让挂载标准的 GTK+ 菜单和工具栏变得更简单。

```
void gnome_app_set_menus ( GNOMEAPP * app, GtkMenuBar * menubar );

void gnome_app_set_toolbar ( GNOMEAPP * app, GtkToolbar * toolbar );
```

但不要完全忽略 GNOME 提供的易用性。GNOME 处理事务的方式（包括菜单和工具栏）围绕着一个名为 `GNOMEUIInfo` 的结构。

```c
typedef struct {

  GNOMEInfoType type;

  gchar * label;

  gchar * hint;

  gpointer moreinfo;

  gpointer user_data;

  gpointer unused_data;

  GNOMEUIPixmapType pixmap_type;

  gpointer pixmap_info;

  guint accelerator_key;

  GdkModifierType ac_mods;

  GtkWidget * widget;

} GNOMEUIInfo;
```
