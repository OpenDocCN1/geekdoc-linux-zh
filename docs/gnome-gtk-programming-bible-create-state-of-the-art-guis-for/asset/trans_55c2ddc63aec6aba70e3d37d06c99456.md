

# 第 19 章：配置与国际化

## 配置获取

```c
void gnome_config_get_vector(const char *path,
int *argcp, char ***argvp)
void gnome_config_get_vector_with_default(
const char *path, int *argcp, char ***argvp,
gboolean *def)
void gnome_config_private_get_vector(const char *path,
int *argcp, char ***argvp)
void gnome_config_private_get_vector_with_default(
const char *path, int *argcp, char ***argvp,
gboolean *def)
```

如果在配置文件中未找到该值，则返回一个空数组。如果指定了 `def` 参数，当在文件中找到该值时，其指向的 `gboolean` 值会被设置为 `TRUE`。如果返回的是默认值，则将其设置为 `FALSE`。

## 国际化

如果你的应用程序最终可能被翻译成另一种语言（考虑到当今互联网的现状，这种可能性很大），你可以采取一些步骤来促进翻译过程。如果在源代码中正确标记了需要翻译的字符串，翻译过程就可以实现自动化。虽然每个文本字符串翻译成其他语言都需要人类译者的参与，但你的应用程序会检查其环境以确定使用哪种语言。

这个过程非常简单。以下示例展示了如何进行初始设置，以及如何声明字符串以便可供翻译使用。

```c
/* translate.c */
#include <gnome.h>

#define PACKAGE "translate"
#define GNOMELOCALEDIR "/usr/share/locale"

GtkWidget *makeBox();
gint eventDelete(GtkWidget *widget,
GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget,
GdkEvent *event, gpointer data);

static gchar *labelstring = N_("Static string");

int main(int argc, char *argv[])
{
    bindtextdomain(PACKAGE, GNOMELOCALEDIR);
    textdomain(PACKAGE);

    gnome_init("translate","1.0",argc,argv);
    window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
    gtk_container_set_border_width(GTK_CONTAINER(window),
                25);
    gtk_signal_connect(GTK_OBJECT(window),"delete_event",
                GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(window),"destroy",
                GTK_SIGNAL_FUNC(eventDestroy),NULL);

    box = makeBox();
    gtk_container_add(GTK_CONTAINER(window),box);
    gtk_widget_show(window);
    gtk_main();
    exit(0);
}
GtkWidget *makeBox() {
    GtkWidget *box;
    GtkWidget *button;

    box = gtk_vbox_new(FALSE,0);
    gtk_widget_show(box);

    button = gtk_button_new_with_label(_("Inline string"));
    gtk_box_pack_start(GTK_BOX(box),button,FALSE,FALSE,0);
    gtk_widget_show(button);

    button = gtk_button_new_with_label(_(labelstring));
    gtk_box_pack_start(GTK_BOX(box),button,FALSE,FALSE,0);
    gtk_widget_show(button);

    return(box);
}
gint eventDelete(GtkWidget *widget,
                  GdkEvent *event,gpointer data) {
    return(FALSE);
}
gint eventDestroy(GtkWidget *widget,
                   GdkEvent *event,gpointer data) {
    gtk_main_quit();
    return(0);
}
```

第 4 行中 `PACKAGE` 的定义为程序分配了一个包名。一个包中可能包含多个应用程序。任何在应用程序之间共享的字符串只需要翻译一次，因为它们都使用相同的查找表。第 5 行中 `GNOMELOCALEDIR` 的定义指定了存放翻译文件的目录。当软件需要进行翻译时，会在此目录中查找。

### 注意

`PACKAGE` 和 `GNOMELOCALEDIR` 的定义通常在一个专门为此目的的头文件中定义。该文件通常名为 `gnome.h`，并且经常包含这些以及其他配置值。GTK+ 和 GNOME 软件开发系统会自动通过 makefile 生成 `config.h`。此外，还可以通过在编译器命令行上使用 `-D` 选项来创建这些定义。

第 20 行对 `bindtextdomain()` 的调用将包名与要搜索的目录关联起来，以便任何翻译请求都知道去哪里查找。第 21 行对 `textdomain()` 的调用将当前应用程序分配给指定的包。

该程序创建了两个按钮，每个按钮都有一个文本标签。第一个标签在第 45 行声明为一个带引号的字符串。标签的声明方式与普通情况相同，只是它位于名为 `_()` 的宏的大括号内。该宏的名称是下划线字符；下划线宏标记字符串以供翻译。在第 49 行创建的第二个按钮也具有可翻译的标签，但这次使用的是变量名。仍然需要下划线宏，但由于字符串在其他地方定义，因此还多了一步。字符串在第 13 行声明，并且因为需要标记为可翻译，所以被包含在另一个短名称的宏中——即 `N_()` 宏。

事情就是这样。确保你标记了所有需要翻译的字符串（跳过那些不需要的，如第 23 行和第 27 行）。如果你的所有字符串都已标记，并且你的应用程序被翻译成另一种语言，它们都会被翻译并插入到表中。

编写可翻译代码有一个缺点。你的程序在动态创建字符串方面受到很大限制。如果在编译时不知道字符串的内容，它就不能被翻译。没有办法从文件或用户输入中读取字符串并将其翻译用于显示。不过，你可以使用 `printf()` 或 `sprintf()` 将未翻译的字符串与已翻译的字符串组合起来。例如，假设译者发现此字符串需要翻译：

```c
"The last device in the list is %s\n"
```

只要将 `%s` 保留在字符串的某个位置，这个字符串就可以被翻译，并且会按你预期的那样工作。如果字符串中有两个变量，事情会变得更加复杂。例如：

```c
"Device number %d has been set to %s mode\n"
```

它可以被翻译，但译者必须注意保持 `%d` 和 `%s` 的顺序不变，因为这是函数调用中参数出现的顺序。

## 摘要

大量的环境设置和控制可以存储在磁盘文件中，用于配置你的程序。这可以包括颜色设置、菜单项、工具栏，甚至语言。本章涵盖的主要内容包括：

- 可以为每个单独的用户创建配置设置，也可以设置为适用于所有用户。配置数据的安全也有特别的规定。
- 保存和恢复配置数据有标准 API。数据以 ASCII 形式存储，但在应用程序内部会转换为 C 数据类型并从 C 数据类型转换回来。
- 你可以使用两个预定义的宏来标记应用程序中包含的文本，以便根据程序运行的环境自动翻译成另一种语言。

本章完成了本书的第二部分，即分步教程部分。本书的第三部分包含更具通用性质的信息，例如完整的控件参考。第三部分的第一章，第 20 章，解释了使用 `automake` 和 `autoconf` 来自动化编译和链接的过程。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_544_0.png)

# 参考文献与机制

- **本章内容**
  - **第 20 章：** 配置与编译
  - **第 21 章：** GTK+ 的控件
  - **第 22 章：** GNOME 的控件
  - **第 23 章：** 一些 Linux 机制
  - **第 24 章：** 比较解剖学：Win32 和 GNOME

# 第 20 章：配置与编译

![](img/8bcc1ba72831c7d67cfc8b395deab95f_548_0.png)

本章提供了一份步骤列表，用于设置基于 GNOME 和 GTK+ 的应用程序开发环境。

设置软件开发环境有数百种方法。本书中使用的 make 文件简单且易于使用。然而，由于其简单性，在大型项目中会变得笨拙。手动更新 make 文件可能变得困难，并且容易出错。

有许多方法可以自动化编译和链接过程，但 GNOME 使用一种半标准形式，因此复制这些方法并将其用于你的 GNOME 应用程序是有意义的。

使用这种配置，你仍然需要手动维护一些文件。但是，一旦设置好，要做出更改和添加却 surprisingly 简单。例如，要更改正在编译系统的版本号，你只需在一个地方输入新的版本号，它就会自动插入到头文件中。如果你添加一个新的源模块，你只需在一个文件中的一个地方输入其名称。因此，其所有依赖关系都会确定，并与其他代码一起编译。

## 安装 GNOME 源代码

对于 GNOME 开发，你需要访问 GNOME 源代码。它作为 GNOME 的一部分提供，因此如果你已安装 GNOME，你可能已经安装了源代码。

## 本章内容

- 安装你的 GNOME 系统源代码副本
- 创建可用于生成 make 文件的 autoconf 和 autogen 脚本
- 理解脚本、你的源代码和 make 文件之间的关系

