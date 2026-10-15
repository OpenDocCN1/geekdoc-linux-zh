
`gchar * gnome_config_get_string_with_default (const gchar * path, gboolean * was_default);`

`gchar * gnome_config_get_translated_string_with_default (const gchar * path, gboolean, was_default);`

`int gnome_config_get_int_with_default (const gchar * path, gboolean * was_default);`

`double gnome_config_get_float_with_default (const gchar * path, gboolean * was_default);`

`gboolean gnome_config_get_bool_with_default (const gchar * path, gboolean * was_default);`

`void gnome_config_get_vector_with_default (const gchar * path, int argpc, gchar ** argvp, gboolean * was_default);`

`was_default` 参数需要指向一个布尔变量，如果返回的值是从配置文件加载的默认值，则该变量被设置为 `true`。默认值作为路径的一部分指定：

```
application_name/section_name/key_name=default_value
```

你只需要在 `=` 后面将路径末尾添加默认值。在 vector 的情况下，这是一个逗号分隔的列表。

将值存储到配置文件中和读取一样简单。巨大的区别是函数名称都以 `gnome_config_set` 或 `gnome_config_private_set` 开始，并且通常接受两个参数：路径和要设置其中的值。

```
void gnome_config_set_string (const gchar * path, const gchar * value);
void gnome_config_set_translated_string (const gchar * path, const gchar * value);
void gnome_config_set_int (const gchar * path, gint value);
void gnome_config_set_float (const gchar * path, double value);
void gnome_config_set_bool (const gchar * path, gboolean value);
void gnome_config_set_vector (const gchar * path, int argc, const gchar * const array[]);
```

```
void gnome_config_private_set_float ( const gchar * path, gdouble value );
void gnome_config_private_set_bool ( const gchar * path, gdouble value );
void gnome_config_private_set_vector ( const gchar * path, int argc,
      const gchar * argv[] );
```

在编写设置程序时，无法保证你设置的数据已经实际写入。当你的代码完成配置文件的设置后，调用 `gnome_config_sync` 是至关重要的。

```
void gnome_config_sync ();
```

该函数使 `gnome_config` 写入你通过 `set` 调用所的所有更改。仔细查看应用程序 `config1.c`。它展示了向配置文件设置并写入值的简单示例。

```
/*
* config1.c
*
* 一个显示从配置文件中设置和读取值的
* 简单应用程序
*/
#include <gnome.h>
/* 将键和值作为参数传递给程序 */
gint main ( gint argc, gchar * argv[] )
{
gchar * path;
gchar * value;

if ( argc < 3 )
{
  g_print ( "Usage : config1 <key> <value>\n" );
  return -1;
}

gnome_init ( "config", "1.0", argc, argv );

/* 构建路径以获取和设置 */
path = g_strncat ( "config/demotionsection/", argv[1] , NULL );

value = gnome_config_get_string ( path );

g_print ( "Current : %s\n", path, value );
g_free ( value );

gnome_config_set_string ( path, argv[2] );
gnome_config_sync ( );
g_print ( "The new value has now been set.\n" );

g_free ( path );
return 0;
}
```

# 第 14 章

在编译后使用该应用程序，只需输入以下内容。

```
$ ./config <key> <value>
```

你需要将 `<key>` 和 `<value>` 替换为你想要赋值的键和值。这些值将被写入到你 `.gnome` 目录下的配置文件中。多次使用可以向你的配置文件添加越来越多的键值对。

该应用程序非常易理解。在初始化 GNOME 之后，会调用 `gnome_config_get_string` 来加载请求。如果此时该键尚不存在，此函数将返回 `NULL`。注意返回的字符串在应用程序使用完毕后是如何通过 `g_free` 释放的。

在加载的值打印到屏幕上之后，通过调用 `gnome_config_set_string` 将命令行指定的值设置到配置文件中。注意随后的对 `gnome_config_sync` 的调用。如果没有此，新值将永远不会写入文件，因此在完成新值的设置后，记得调用 `gnome_config_sync` 是至关重要的。

`gnome_config` 工具还提供了一系列函数，如果你需要，它们允许你遍历配置文件中的节以及节中的键。这被称为迭代，它允许你通过代码通过非常直观的循环找到配置文件中所有节的名称以及所有的键及其值。

要开始此过程，你需要调用以下函数之一：

```
void * gnome_config_init_iterator ( const gchar * path );
void * gnome_config_private_init_iterator ( const gchar * path );
void * gnome_config_init_iterator_sections ( const gchar * path );
void * gnome_config_private_init_iterator_sections ( const gchar * path );
```

如你所示，这里的函数与 `.gnome_private` 配置文件一起，而其他函数处理 `.config` 文件。如果你需要遍历配置文件中的节，你需要传递一个仅指定要使用的配置文件文件名的路径。要遍历节中的键，路径需要由通常格式下的文件名和节名称组成。

这些函数返回的指针是一个 `iterator_handle`，并用于以下函数调用：

```
void * gnome_config_iterator_next ( void * iterator_handle, gchar ** key, gchar ** value );
```

该函数返回一个新的迭代器句柄，供下次调用 `gnome_config_iterator_next` 时使用；如果文件中没有更多数据可供迭代，则返回 `NULL`。除了当前的迭代器句柄外，函数还需要传入两个字符串指针的指针。一个指针用于键或节的名称字符串，另一个用于键值（如果你正在遍历键）。这些指针将填充为指向刚刚加载的数据的新指针，并且像既往一样，在使用完毕后需要通过 `g_free` 释放。

我们可以在一个简单的应用程序中看到这些函数的作用，该程序遍历我们在 `config1.c` 中构建的 `config1` 配置文件。

```
/** * config2.c
 * 一个显示遍历配置文件的简单应用程序
 */
```

```c
#include <gnome.h>

/* 将值的键和值作为参数传递给程序 */
int main (int argc, gchar * argv[]) {

gchar * key;
gchar * value;
void * iterator;

gnome_init ( "config", "1.0", argc, argv );

iterator = gnome_config_init_iterator ( "config" );

while ( iterator = gnome_config_iterator_next ( iterator, &key, &value ) )
{
  g_print ( "Key: %s, Value: %s\n", key, value );
  g_free ( key );
  g_free ( value );
}

g_free ( iterator );
return 0;
}
```

默认情况下，GNOME 将大多数应用程序帮助文件存储在如 `/usr/share/gnome/help` 等目录中。你的应用程序也应该将帮助文件存储在相同的位置。在该目录（或你的系统使用的任何目录）中，你会找到每个随附的 GNOME 应用程序的子目录，而在这些目录内部，你还会找到不同语言版本的帮助文件的子目录。默认语言通常位于名为 `C` 的目录中。因此，你会在 `/usr/share/gnome/help/gnorpm/` 找到 gnorpm 应用程序的默认语言帮助文件。

简单来说，使用 `gnome_help` 涉及填充一个 `GnomeHelpMenuEntry` 结构体，然后调用 `gnome_help_display` 来调用系统的默认浏览器显示所需的帮助文件。

```c
typedef struct
{
  const gchar * application;
  const gchar * helpfile;
} GnomeHelpMenuEntry;
void gnome_help_display ( void * ignore, GnomeHelpMenuEntry * ref ) ;
```

因此，为了显示 `gnorpm` 的 `index.html` 文件，你可以像下面的代码一样使用。

```c
static GnomeHelpMenuEntry helpref = { "gnorpm", "index.html" };
gnome_help_display ( NULL, &helpref ) ;
```

`gnome_help_display` 的第一个参数始终为 `NULL`，它是为了未来 `gnome_help` 系统的开发而留的。下面的代码 `help.c` 展示了用法。

```c
/*
* help.c
*
* 显示如何通过利用 gnorpm 帮助文件
* 来使用 gnome-help。
 */

#include <gnome.h>

void CloseTheApp ( GtkWidget * window, gpointer data )
{
  gtk_main_quit ( );
}

void HelpButtonClicked ( GtkButton * button, gpointer data )
{
  /* 调用帮助系统，假装此应用程序是
  * gnorpm */
  static GnomeHelpMenuEntry helpref = { "gnorpm", "index.html" };

  gnome_help_display ( NULL, &helpref );
}

gint main ( int argc, gchar * argv[]) {
{
GtkWidget * window;
GtkWidget * helpbutton;

gnome_init ( "Helpdemo", "1.0", argc, argv );

window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );
gtk_container_set_border_width ( GTK_CONTAINER ( window ), 10 );

helpbutton = gtk_button_new_with_label ( "Help" );
gtk_container_add ( GTK_CONTAINER ( window ), helpbutton );

gtk_signal_connect ( GTK_OBJECT ( window ),
    "destroy",
    GTK_SIGNAL_FUNC ( CloseTheApp ),
    NULL );

gtk_signal_connect ( GTK_OBJECT ( helpbutton ),
    "clicked",
    GTK_SIGNAL_FUNC ( HelpButtonClicked ),
    NULL );

gtk_widget_show_all ( window );

gtk_main ( );
return 0;
}
```

## 更多 GNOME 功能

`gnome_help`（库、函数等）也让提供页面帮助变得更加简单。

```c
void gnome_help_pbox_display ( void * ignore,
  gint page_num, GnomeMenuHelpEntry * ref );
```

你需要将页面的属性作为第二个参数传递，如果是这样，`gnome_help_pbox_display` 将将其附加到所需的帮助文件名上。因此，如果你在寻找 `info.html` 并请求第 2 页，该函数将尝试加载 `info-2.html`。

## 互联网访问

GNOME 主要用于 GNU/Linux 平台，这是一种以其网络能力而闻名的操作系统和内核。事实上，该操作系统的网络能力也非常强大，以至于应用程序开发者需要为自己的使用而编写自己版本的网络应用程序的情况实际上是非常罕见的。

如果你正在开发一个某个时刻需要从远程服务器下载文件的 GNOME 应用程序，那么直接调用操作系统提供的 FTP 应用程序将更快、更简单且更可靠。更好的是，你实际上可以将 FTP 应用程序的大部分代码直接复制到自己的程序中，因为每一个都是开源操作系统。但记住，如果 FTP 程序的源码在未来某个点发生了变化，你的应用程序将无法从这些更改中受益。

然而，某些时候，可用函数来执行常用任务仍然非常方便，例如对远程主机进行 DNS 查询，或者通过用户输入的 URL 调用默认的操作系统查看器。这两项任务在 GNOME 中都得到了很好的照顾。GNOME 相比标准系统 API 具有优势。例如，调用 `gethostbyname` 会让你的应用程序等待主机名被解析。而 GNOME 版本只需在完成后回调你即可。

## DNS 查询

GNOME 为 DNS 查询提供了非常方便的支持，将主机名解析为可用的 IP 地址。这不仅从获取有效地址到原生网络调用的过程中非常方便，而且检查用户输入的地址是否有效也同样方便。

整个过程围绕着三个函数调用。

```c
void gnome_dns_init ( int server_count );
gint gnome_dns_lookup ( const char * hostname, gpointer data );
void gnome_dns_free ( gpointer * data );
```

`gnome_dns_init` 初始化 DNS 系统。`gnome_dns_lookup` 函数接收主机名和一个指向存储结果结构体的指针。`gnome_dns_free` 函数释放查询使用的内存。

# 第 14 章

```c
gtk_signal_connect ( GTK_OBJECT ( widget ),
    "clicked",
    GTK_SIGNAL_FUNC ( LookupClicked ),
    NULL );

gtk_widget_show_all ( window );

gtk_main ();
return 0;
```

代码相当多，但那是因为这是一个带有用户界面的完整应用程序。

![](img/aa3546013f120531cd191b770d85869c_389_0.png)

当用户输入主机名并点击窗口中的按钮时，按钮处理程序实际上会调用查找函数，并将 `LookupHandler` 指定为回调函数。该函数检查是否找到了有效地址，如果是，则将 `guint32` 拆分为一个包含四个字节的数组。这四个字节将显示在窗口的标签上，作为“已找到的 Internet 地址”。

将域名解析为有效的 Internet 地址，依赖于你的机器是否正确配置了本地网络，以及 Internet——如果它真的进入了这些领域的话。

当应用程序请求操作系统解析主机名时，首先会检查一个名为 `/etc/hosts` 的文件。这是一个带有主机名的 IP 地址简单列表，通常应该列出你的机器经常通信的本地网络上的计算机列表。如果在该文件中没有找到所需的主机名，大多数 Unix 和 Linux 机器会检查 `/etc/resol.conf` 文件。它的格式与 `/etc/hosts` 文件相同，即列出了名为“域名服务器”（DNS）的特殊机器的 IP 地址。你的计算机将尝试连接到这些机器之一，并询问它们是否知道你请求的主机名。它可以询问 DNS 已知的其他机器，并沿着链链一直向下查询，直到你最终获得有效的 IP 地址，或者查找失败。
