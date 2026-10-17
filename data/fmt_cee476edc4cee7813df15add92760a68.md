
`g_print ( "Open/Save got clicked\n" );`

}

/** 菜单工具函数 **/

`GtkWidget *BuildMenuItem ( gchar * menutest, gchar acceleratorkey, GtkSignalFunc signal_handler, GtkWidget * menu, GtkAccelGroup * accelgroup )`

{

    `GtkWidget * menuitem;`

    /* 第一，构建菜单项 */

    if ( `menuitem` != NULL )

        `menuitem = gtk_menu_item_new_label ( menuitem );`

    else

        `menuitem = gtk_menu_item_new ( );`

    /* 接下来，连接信号处理器 */

    if ( `signal_handler` != NULL )

        `gtk_signal_connect ( GTK_OBJECT ( menuitem ),"activate", signal_handler, NULL );`

    /* 现在我们可以将项添加到菜单本身了 */

    if ( `menu` != NULL )

        `gtk_menu_append ( GTK_MENU ( menu ), menuitem );`

    /* 最后，构建加速器 */

    if ( `accelgroup` != NULL && ( int ) `acceleratorkey` == 0 )

        `gtk_accel_group_add ( accelgroup, GTK_CONTROL_MASK, GTK_ACCEL_VISIBLE, GTK_OBJECT ( menuitem ), "activate" );`

    /* 全部完成，返回菜单项 */

    return `menuitem;`

}

/** 主代码 **/

`int main ( gint argc, gchar * argv[])`

{

    `GtkWidget * window;`

    `GtkWidget * menubar;`

    `GtkWidget * menu;`

    `GtkWidget * menuitem;`

    `GtkAccelGroup * accelgroup;`

    `gtk_init ( &argc, &argv );`

    /* 创建一个窗口来存放菜单，不再包含其他 */

    `window = gtk_window_new ( GTK_WINDOW_TOPLEVEL );`

    `gtk_window_set_default_size ( GTK_WINDOW ( window ), 320, 25 );`

    `gtk_signal_connect ( GTK_OBJECT ( window ), "destroy", (GtkFunc)CloseTheApp, NULL );`

    /* 创建菜单栏并将其添加到窗口 */

    `menubar = gtk_menu_new ();`

    `gtk_container_add ( GTK_CONTAINER ( window ), menubar );`

    /* 创建加速器组并绑定到它 */

    `accelgroup = gtk_accel_group_new ();`

    `gtk_accel_group_attach ( GTK_ACCEL_GROUP ( accelgroup ), GTK_OBJECT ( window ) );`

    /* 创建菜单并添加它 */

    `menu = gtk_menu_new ();`

    `gtk_container_add ( GTK_CONTAINER ( menubar ), menu );`

    /* 创建菜单项 */

    `menuitem = BuildMenuItem ( "Open", 'O', MenuHandler, menu, accelgroup );`

    `menuitem = BuildMenuItem ( "Save", 'S', MenuHandler, menu, accelgroup );`

    `menuitem = BuildMenuItem ( "Quit", 'Q', CloseTheApp, menu, accelgroup );`

    /* 显示窗口 */

    `gtk_widget_show_all ( window );`

    `gtk_main ();`

    return 0;

}

## 使用项目工厂创建菜单

GTK+ 提供了一种名为“项目工厂”（Item Factory）的机制，它可以在极短的时间和代码量内创建出整个菜单树。然而，这是一种权衡。使用项目工厂时，你无法对菜单项本身的创建拥有完全的控制权，如果你想要在菜单内部嵌入图形或其他小部件等功能，这可能会让工作变得复杂。不过，如果你愿意，也可以将那种冗长、繁琐的实现方法与我们在这里将要探索的更快速的方法结合。

对于大多数人来说，这种权衡并不比大幅减少需要编写的代码量更令人不可接受。使用项目工厂非常简单。你只需要提供一个 `GtkItemEntry` 对象的数组来描述你的菜单的外观。这就像创建一个字符串数组一样简单。当然，缺点是由于这些只是字符串，因此在编译时没有帮助你检查错误。如果你在字符串中写了错误，你将在实际运行应用程序时才会发现。

一个 `GtkItemEntry` 由五个不同的部分组成；一个描述菜单路径的字符串（`"/File"`）

```
struct GtkItemFactoryEntry {
  gchar * path;
  gchar * accelerator;
  GtkItemFactoryCallback callback;
  guint callback_action;
  gchar * item_type;
}
```

项目标志（item flag）是项目工厂威力所在，可以设置为以下任何一个值：

- `<Item>` - 创建一个简单的菜单项（默认值，你不需要使用这个）
- `<CheckItem>` - 表示该项是复选框
- `<RadioItem>` - 表示该项是单选框
- `<Separator>` - 表示该项不显示，而是被一个分隔条代替
- `<Branch>` - 表示这会导致另一个菜单的出现
- `<LastBranch>` - 一个右对齐的菜单项，例如帮助菜单
- `<Tearoff>` - 表示拖动鼠标可以从菜单下方分离出菜单项

你可以使用如下代码创建一个结构体：

```
GtkItemFactoryEntry items[] = {
  {"/File", NULL, NULL, NULL, "<Branch>" },
  {"/File/New", NULL, NULL, NULL,},
  {"/File/dash", NULL, NULL, NULL, "<Separator>" },
  {"/File/Quit", NULL, NULL, NULL, "<control>Q"}
};
```

注意路径中的每个分支都是以 `/` 开头的——这只是在指定文件路径，即使是根目录也以 `/` 开始。还要注意路径中某些单词前的下划线。在运行时，这些将变成热键，因此当菜单栏被选中时，用户只需按下带有下划线的键即可激活菜单。

创建了你的 `GtkFactoryEntry` 数组后，实际获取菜单栏变得轻而易举。首先，你需要创建一个加速器组（accelerator group）——项目工厂将用填充指定的加速器。

```
GtkAccelGroup * accel_group = gtk_accel_group_new();
```

然后，你需要将其传递给 `gtk_item_factory_new`，如下所示：

```
GtkItemFactory * item_factory = gtk_item_factory_new ( GTK_TYPE_MENU_BAR, "<SOMENAME>", accel_group );
```

该函数接受三个参数。第一个指定了你想创建的内容，在本例中是菜单栏。第二个给出菜单栏名称，你稍后会需要它（必须要求项目工厂给你它用于创建菜单项的“已命名”小部件）。最后一个参数是你想要填充加速器键的加速器组。

接下来，你需要使用工厂来构建菜单。

```
gtk_item_factory_create_items ( item_factory, numberofitems, menuitems, NULL );
```

你只需要传递项目工厂的指针、你正在创建的项目数量以及项目本身即可。确定你创建了多少个项目不需要手动查阅代码。一个简单的 `sizeof` 就可以为你完成任务：

```
numberofitems = sizeof ( menuitems ) / sizeof ( menuitems );
```

只需将结构体的大小除以列表中第一个项目的大小，这就是你创建的菜单项数量。到此，你就完成了。你需要做的就是向项目工厂请求你的新菜单。这就是 `"<SOMENAME>"` 发挥作用的地方。

```
GtkWidget * menubar = gtk_item_factory_get_widget ( item_factory, "<SOMENAME>" );
```

从那以后，工作就几乎结束了。将加速器组附加到窗口并将菜单栏放入容器中，你就可以运行了。项目工厂甚至会负责为你让菜单栏和菜单项可见，所以你甚至不需要自己做。

不过，项目工厂有一个可能的问题。`GtkItemFactoryEntry` 项目中使用的回调函数格式如下：

```
void ItemFactoryCallback ( gpointer callback_data, GtkWidget * widget );
```

## 第8章

自己试玩一下。让我们看看我们原始的 `menutest.c` 程序在使用项目工厂后是什么样子的。输入代码、编译并运行 `itemfactory.c`：

```c
/**
* itemfactory.c
* 使用项目工厂生成菜单的演示
*/
```

```c
#include <gtk/gtk.h>

void ItemFactoryCallback ( gpointer callback_data, GtkWidget * widget );

/* 构建菜单的项 */
static GtkItemFactoryEntry items[] = {
    {"/File", NULL, NULL, NULL, "<Branch>"},
    {"/File/tearoff", NULL, NULL, NULL, "<tearoff>"},
    {"/File/Open", NULL, NULL, NULL, "<control>"},
    {"/File/Save", NULL, NULL, NULL, "<control>"},
    {"/File/dash", NULL, NULL, NULL, "<Separator>"},
    {"/File/Quit", NULL, NULL, NULL, "<control>"}
};

/** 项的通用回调 */
void GenericCallback ( gpointer callback_data, guint callback_action)
{
    g_print("菜单被点击!");
}

/** 窗口销毁处理器 **/
void CloseTheApp ( GtkWidget * window, gpointer data)
{
    gtk_main_quit();
}

int main (int argc, char * argv[])
{
    GtkAccelGroup * accel;
    GtkItemFactory * itemFactory;
    GtkWidget * window;

    /* 以通常的方式创建窗口 */
    window = gtk_new (GTK_TOPLEVEL, NULL);
    gtk_window_set_title (GTK_WINDOW (window), "Item factories");
    gtk_window_set_default_size (GTK_WINDOW (window), 100, 20);
    gtk_signal_connect (GTK_OBJECT (window), "destroy", G_CALLBACK(CloseTheApp), NULL);

    /* 创建准备填充的空加速器组 */
    accel = gtk_accel_group_new ();

    /* 创建准备构建菜单栏的项目工厂 */
    itemFactory = gtk_item_factory_new (GTK_TYPE_MENU_BAR, "<menu>", accel);

    /* 为菜单创建实际项 - 它们进入工厂并就绪 */
    gtk_item_factory_create_items (itemFactory, sizeof (items) / sizeof(items[0]), items, NULL);

    /* 附加加速器组 */
    gtk_accel_group_attach (accel, GTK_OBJECT (window));

    /* 最后从工厂获取菜单栏并将其放入窗口中 */
    gtk_container_add (GTK_CONTAINER (window),
        gtk_item_factory_get_widget (itemFactory, "<menu>"));

    gtk_widget_show_all (window);
    gtk_main();
    return 0;
}
```

![](img/aa3546013f120531cd191b770d85869c_220_0.png)

当你运行时，你应该能看到类似的内容：

与硬编码菜单的方法不同，你会立即发现这些菜单可以被分离并单独拖动。代码有良好的文档说明，所以浏览并尝试理解其中发生的一切。

## 弹出菜单

上下文菜单是许多应用程序中另一种常见的图形元素。它通常设置成：如果你在应用程序窗口内右键点击，会在该位置出现一个菜单，显示与鼠标悬停处的数据或小部件相关的项。

我们可以使用 GTK+ 自身在点击项时弹出菜单的相同函数，只是在鼠标位置弹出一个浮动菜单。这是通过恰当的 `gtk_menu_popup` 函数实现的：

```
void gtk_menu_popup ( GtkMenu * menu, GtkWidget * parent_menu_shell
    GtkWidget * parent_menu_item
    GtkMenuPositionFunc func
    gpointer data
    guint button
    guint32 activate_time );
```

## 第 8 章

它看起来很复杂，但其实并非如此。调用时的大部分参数只有在你处理从菜单项下拉菜单时才会真正生效，而这并不是我们追求的。事实上，这里唯一真正需要提供的参数是第一个，即指向菜单本身的指针。其余部分用于向信号处理程序（signal handlers）和内置菜单代码提供更多信息。老实说，它们已经超出了这类书籍的范畴，更多属于高级代码，即你希望完全控制菜单如何出现、何时出现，以及它应该是什么样子的。

让我们用一个很不错的示例来结束本章，这个示例展示了如何处理弹出窗口，同时也向你介绍了一些更高级的事件处理，而不是信号处理。

```c
/**
 * popupmenu.c
 * 一个简单的代码模板块，用于以灵活
 * 的构建菜单。
 */

#include <gtk/gtk.gpointer.h>

void CloseTheApp ( GtkWidget * window, gpointer data )
{
    gtk_main_quit (
}

gboolean MousePressed ( GtkWidget * widget, GdkEvent * event, gpointer data )
{
    /* 检查事件是否为菜单按钮按下 */
    if (event->type == GDK_BUTTON_PRESS)
    {
        /* 将事件强制转换为 GdkEventButton 结构 */
        GdkEventButton * buttonevent = ( GdkEventButton *) event;

        /* 检查 button 成员以查看按下了哪个按钮 */
        if (buttonevent->button == 3)
        {
            /* 如果按了右键，弹出菜单 */
            gtk_menu_popup ( GTK_MENU ( menu ), NULL, NULL, NULL
                            NULL, buttonevent->button, 0);

            /* 返回 TRUE 因为我们处理了该事件 */
            return TRUE;
        }

        /* 在这里返回 FALSE，因为我们没有对事件进行任何操作 */
        return FALSE;
}

/** 菜单工具函数 **
GtkWidget * BuildMenuItem ( gchar * menutext, gchar * accelerator,
```
