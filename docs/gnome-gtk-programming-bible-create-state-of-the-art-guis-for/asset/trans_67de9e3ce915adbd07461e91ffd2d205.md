
变量 `helloauto_SOURCES` 指定了用于构建名为 `helloauto` 的二进制输出文件的源文件。利用这些信息，生成 make 文件以检查所有这些文件的依赖关系。

变量 `helloauto_LDADD` 指定了一个库列表，用于搜索以解析构成 `helloauto` 的文件中的外部引用。

你可以将其名称添加到 `bin_PROGRAMS` 的列表中，并为它添加新的 `SOURCES` 和 `LDADD` 条目，从而将其他程序添加到同一文件中。此外，如果你希望使用源文件的子目录，可以使用 `SUBDIRS` 定义来指向正确的目录。这意味着，要向你的源代码树中添加一个新目录，你只需在新源目录中创建一个 `Makefile.am` 文件，并在父目录的 `Makefile.am` 中添加一个 `SUBDIRS` 条目。

## 运行 `autogen.sh` 脚本

编译所有内容需要两个步骤。首先，从你的根开发目录运行该脚本，如下所示：

```
autogen.sh
```

这会向你的根开发目录添加许多文件。具体添加哪些文件在很大程度上取决于你之前所做的设置和选择。例如，如果你使用 `ALL_LINGUAS` 设置一些翻译，则会创建子目录 `po` 和 `intl` 来容纳翻译字符串。

脚本运行后，只需输入：

```
make
```

此命令编译并链接整个目录树中的所有内容。如果你在任何源子目录中，输入 `make` 只编译该当前目录及其下方的目录。

make 文件比较源文件和对象文件的日期，因此如果你再次编译，只有更改的文件会被包含。但是，你可以通过删除对象文件来强制完整重新编译。要删除所有对象文件以及编译期间创建的其他文件，请输入：

```
make clean
```

当你开发应用程序并添加新的源文件时，你需要更新相应的 `Makefile.am` 文件，然后执行 `autogen.sh` 以包含新的源文件。

成功编译后，你可以使用以下命令安装可执行文件：

```
make install
```

## 摘要

使自动编译工作起来的设置有点复杂，但随着你开发软件，回报会在后来到来。你的源文件之间的所有依赖关系都会自动跟踪，并且使用一组正确且完整的命令来编译和链接你的程序。正如本章中详细解释的那样，以下是需要采取的步骤列表：

-   创建一个开发目录，其中包含适当的文件和目录集合。它还应该包含一个随 GNOME 开发软件分发的宏的副本。
-   创建 `configure.in` 文件，该文件通过使用宏包含项目的基本描述。另外，创建 `acconfig.h` 文件，作为创建 `config.h` 的模板使用。
-   创建一个简单的 `autogen.sh` 脚本，你可以用它来查找依赖关系并生成 make 文件。
-   创建一个 `Makefile.am` 文件，列出将用作输入的文件名，以及要生成的对象文件名。开发树中的每个目录都包含其中一个。

接下来的两章是参考资料。第 21 章包含 GTK+ 控件的列表，第 22 章包含 GNOME 控件的列表。书中前面许多程序中已经使用了这些控件，但对于未使用的控件，有一些小例子。

![](img/8bcc1ba72831c7d67cfc8b395deab95f_560_0.png)

# GTK+ 的控件

## 本章内容

本章提供了 GTK+ 对象的按字母顺序排列的列表。大多数对象是控件，但有几个对象直接继承自基类 `GtkObject`。每个条目包括继承关系以及可供你的应用程序使用的所有功能。

-   列出并解释 GTK+ 的控件和其他对象
-   确定定义给对象的所有信号和功能
-   通过检查其继承关系，确定对象中可用的所有继承功能
-   确定为向功能传递配置设置而定义的枚举常量
-   通过包含每个对象的简单示例来帮助你入门

你可以将任何控件作为基础来创建另一个控件，但并非所有控件都可以显示——有些仅用作基类。如果一个类没有以 `_new` 结尾（或名称中某处包含 `_new_`）的功能，并且返回指向新创建控件的指针，那么只能将其用作基类。

包含在每个控件中的示例代码是一个创建可显示控件并返回其指针的功能。显示控件的所有程序的主流程都非常相似。以下示例是用于 `GtkEntry` 控件的：

```c
/** xgtkentry.c **/
#include <gnome.h>

gint eventDelete (GtkWidget *widget,
                  GdkEvent *event, gpointer data);
gint eventDestroy (GtkWidget *widget,
                   GdkEvent *event, gpointer data);
static GtkWidget *makeWidget();

int main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *widget;

    gnome_init ("xgtkentry", "1.0", argc, argv);
    app = gnome_app_new("xgtkentry", "GtkEntry");
    gtk_container_set_border_width(GTK_CONTAINER(app), 20);
    gtk_signal_connect(GTK_OBJECT(app), "delete_event",
                       GTK_SIGNAL_FUNC(eventDelete), NULL);
    gtk_signal_connect(GTK_OBJECT(app), "destroy",
                       GTK_SIGNAL_FUNC(eventDestroy), NULL);

    widget = makeWidget();
    gnome_app_set_contents(GNOME_APP(app), widget);
    gtk_widget_show_all(app);
    gtk_main();
    exit(0);
}

gint eventDelete(GtkWidget *widget,
                 GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget,
                  GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}

static GtkWidget *makeWidget()
{
    GtkWidget *widget;

    widget = gtk_entry_new_with_max_length(40);
    gtk_entry_set_text(GTK_ENTRY(widget), "Edit me!");
    return(widget);
}
```

这里可能有一些细微的差别。例如，那些将自己包装在自己的顶级窗口中，并因此控制自己操作的控件，并不返回指针。如果你查看 CD 上的源代码，或从网站下载的源代码，你会看到每个示例的完整程序——而不仅仅是本章中显示的代码片段。

## GtkAccelLabel

这个标签控件从另一个控件读取并显示加速键。它显示用于创建它的文本（如果有的话），直到它被分配了一个具有加速键的控件。

### 继承

`GtkAccelLabel` -> `GtkLabel` -> `GtkWMisc` -> `GtkWidget` -> `GtkObject`

### 功能

```c
guint gtk_accel_label_get_accel_width(
              GtkAccelLabel *accel_label);
GtkType gtk_accel_label_get_type(void);
GtkWidget *gtk_accel_label_new(const gchar *string);
boolean gtk_accel_label_refetch(GtkAccelLabel *accel_label);
void gtk_accel_label_set_accel_widget
     (GtkAccelLabel *accel_label, GtkWidget *accel_widget);
```

### 信号

- `"changed"` `void cb(GtkWidget *, gpointer)`
- `"value_changed"` `void cb(GtkWidget *, gpointer)`

以下示例显示了图 21-1 中所示的窗口。

```c
static GtkWidget *makeWidget()
{
    GtkWidget *widget;

    widget = gtk_accel_label_new("Label String");
    return(widget);
}
```

![](img/8bcc1ba72831c7d67cfc8b395deab95f_562_0.png)

## GtkAdjustment

此对象存储几何信息，例如上下界、步长和页面增量以及页面大小。其他对象使用 GtkAdjustment 对象来存储它们的内部尺寸设置。它还被作为参数传递以指定几何信息。

调用 `gtk_adjustment_changed()` 会发出 `"changed"` 信号；如果自上次发出信号以来值发生了变化，调用 `gtk_adjustment_value_changed()` 会发出 `"value changed"` 信号。

### 继承

`GtkAdjustment` -> `GtkData` -> `GtkObject`

### 功能

- `void gtk_adjustment_changed(GtkAdjustment *adjustment)`
- `void gtk_adjustment_clamp_page(GtkAdjustment *adjustment, gfloat lower, gfloat upper)`
- `GtkType gtk_adjustment_get_type(void)`
- `GtkObject *gtk_adjustment_new(gfloat value, gfloat lower, gfloat upper, gfloat step_increment, gfloat page_increment, gfloat page_size)`
- `void gtk_adjustment_set_value(GtkAdjustment *adjustment, gfloat value)`
- `void gtk_adjustment_value_changed(GtkAdjustment *adjustment)`

