
每个 GnomeUIInfo 结构体被定义为特定类型。表 8-2 列出了 type 字段的可能值。

## 表 8-2：GnomeUIInfo 条目的类型

| 类型 | 描述 |
| :--- | :--- |
| Gnome_APP_UI_ENDOFINFO | 一种特殊条目，用作每个数组末尾的终止符。 |
| Gnome_APP_UI_ITEM | 普通菜单项——如果位于单选按钮组内，则为单选按钮。 |
| Gnome_APP_UI_TOGGLEITEM | 复选框。 |
| Gnome_APP_UI_RADIOITEMS | 一组单选按钮。 |
| Gnome_APP_UI_SUBTREE | 子树。包含指向另一个 GnomeInfo 结构体数组的指针。 |
| Gnome_APP_UI_SEPARATOR | 对于菜单，这是一条分隔线。对于工具栏，这是一个空白空间。 |
| Gnome_APP_UI_HELP | 帮助菜单中的帮助主题列表。 |
| Gnome_APP_UI_BUILDER_DATA | 在创建菜单时，创建函数从此数组成员读取信息，以配置后续的项。 |
| Gnome_APP_UI_ITEM_CONFIGURABLE | 可配置的菜单项。此类型完全忽略先前由 Gnome_APP_UI_BUILDER_DATA 条目所做的任何值设置。 |
| Gnome_APP_UI_SUBTREE_STOCK | 与 Gnome_APP_UI_SUBTREE 相同，只是标签和提示字符串需要在 gnome-libs 目录中查找。 |

表 8-3 列出了在 gnome-app-helper.h 中定义的宏，这些宏可用于创建菜单。这些宏并没有什么特别神奇之处——它们只是扩展为一组格式正确的值，用于初始化 GnomeUIInfo 结构体——但使用它们可以使程序更容易编写和阅读。鉴于结构体中字段数量众多，可能存在成千上万种宏组合；如果你的应用程序需要这里没有的宏，你完全可以自己编写一个。

## 表 8-3：用于构建菜单和工具栏的宏

| 宏名称 | 描述 |
| :--- | :--- |
| GNOMEUIINFO_END | 类型为 GNOME_APP_UI_ENDOFINFO。终止 GnomeUIInfo 结构体数组。它必须出现在每个数组中。 |
| GNOMEUIINFO_HELP (app_name) | 类型为 GNOME_APP_UI_HELP。这会根据应用程序名称插入相应的帮助主题。 |
| GNOMEUIINFO_ITEM (label, tooltip, callback, xpm_data) | 类型为 GNOME_APP_UI_ITEM。该条目使用 xpm_data 作为图标进行绘制。必须指定标签、提示和回调函数。 |
| GNOMEUIINFO_ITEM_DATA (label, tooltip, callback, user_data, xpm_data) | 类型为 GNOME_APP_UI_ITEM。该条目使用 xpm_data 作为其图标。必须指定标签、提示、回调和 user_data 函数。 |
| GNOMEUIINFO_ITEM_STOCK (label, tooltip, callback) | 类型为 GNOME_APP_UI_ITEM。该条目绘制时无图标。必须指定标签、提示和回调函数。 |
| GNOMEUIINFO_ITEM_STOCK (label, tooltip, callback, stock_id) | 类型为 GNOME_APP_UI_ITEM。该条目使用 stock_id 指定的标准图标进行绘制。必须指定标签、提示和回调函数。 |
| GNOMEUIINFO_RADIOITEM (label, tooltip, callback, xpm_data) | 类型为 GNOME_APP_UI_ITEM。插入一个使用 xpm_data 作为图标的单选按钮。必须指定标签、提示和回调函数。 |
| GNOMEUIINFO_RADIOITEM_DATA (label, tooltip, callback, user_data, xpm_data) | 类型为 GNOME_APP_UI_ITEM。插入一个使用 xpm_data 作为图标的单选按钮。必须指定标签、提示、回调和 user_data 函数。 |
| GNOMEUIINFO_SEPARATOR | 类型为 GNOME_APP_UI_SEPARATOR。对于菜单，这插入一条空白线。对于工具栏，它插入一个空白空间。 |
| GNOMEUIINFO_SUBTREE (label, tree) | 类型为 GNOME_APP_UI_SUBTREE。tree 是 GnomeUIInfo 结构体数组第一个成员的地址。必须指定标签函数。 |
| GNOMEUIINFO_SUBTREE_HINT (label, tooltip, tree) | 类型为 GNOME_APP_UI_SUBTREE。tree 是 GnomeUIInfo 结构体数组第一个成员的地址。必须指定标签和提示函数。 |
| GNOMEUIINFO_SUBTREE_STOCK (label, tree, stock_id) | 类型为 GNOME_APP_UI_SUBTREE。tree 是 GnomeUIInfo 结构体数组第一个成员的地址。label 用于该条目，而 hint 是用于状态栏的文本。stock_id 是用于绘制该条目的标准图标。 |
| GNOMEUIINFO_TOGGLEITEM (label, tooltip, callback, xpm_data) | 类型为 GNOME_APP_UI_TOGGLEITEM。这是一个使用 xpm_data 作为图标的复选框。必须指定标签、提示和回调函数。 |
| GNOMEUIINFO_TOGGLEITEM_DATA (label, tooltip, callback, user_data, xpm_data) | 类型为 GNOME_APP_UI_TOGGLEITEM。这是一个使用 xpm_data 作为图标的复选框。必须指定标签、提示、user_data 和回调函数。 |

### 标准 GNOME 菜单布局

使用标准的菜单组织有一些优势。由于布局是熟悉的，对于你的应用程序的新用户来说，他们可以快速找到所需的内容——而经验丰富的用户也不必回忆多种菜单布局。标准布局的很大一部分是随时间演变得来的。我们都习惯了在左侧找到“文件”菜单，并在其旁边找到“编辑”菜单。此外，我们还期望“保存”和“退出”位于“文件”菜单中。另外，我们期望在右侧找到“帮助”菜单，并在“帮助”菜单中看到一个关于弹出窗口。

很少有需要所有标准菜单选项的应用程序，正如很少有不需要添加自己菜单选项的应用程序一样。然而，从标准布局开始应该可以简化整体菜单组织的任务。

以下程序是一个更复杂程序的主线，它所做的只是在标准位置定义一组带有选项的菜单。

```c
/** stdmin.c **/
#include <gnome.h>

GtkWidget *createMenus(GtkWidget *app);
gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data);
gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data);

int main(int argc, char *argv[]) {
    GtkWidget *app;
    GtkWidget *statusbar;

    gnome_init("stdmain","1.0",argc,argv);
    app = gnome_app_new("stdmain", "Gnome Menu Layout");
    gtk_window_set_default_size(GTK_WINDOW(app),200,300);
    gtk_signal_connect(GTK_OBJECT(app),"delete_event", GTK_SIGNAL_FUNC(eventDelete),NULL);
    gtk_signal_connect(GTK_OBJECT(app),"destroy", GTK_SIGNAL_FUNC(eventDestroy),NULL);

    statusbar = createMenus(app);

    gtk_widget_show_all(app);

    gtk_main();
    exit(0);
}

gint eventDelete(GtkWidget *widget, GdkEvent *event, gpointer data) {
    return(FALSE);
}

gint eventDestroy(GtkWidget *widget, GdkEvent *event, gpointer data) {
    gtk_main_quit();
    return(0);
}
```

第 25 行对 createMenus() 的调用创建了所有菜单，并在窗口底部安装了一个状态栏。每当鼠标位于某个菜单项内时，状态栏都会显示提示（或工具提示）文本。状态栏小部件会被返回，以便应用程序的其他部分希望使用它时可以使用。

以下代码定义了菜单布局，并提供了一个可用于创建菜单并将其附加到 GnomeApp 窗口的函数。为创建这些菜单项设计了一些特殊的宏，因此它们不仅位于与其他应用程序相同的位置，还具有相同的装饰图标。

```c
/* stdmenu.c **/
#include <gnome.h>
const gchar data[] = "Dummy callback data";

static void helpAbout(GtkWidget *widget, gpointer data) {
    GtkWidget *aboutBox;
    const gchar *writtenBy[] = {
        "Arthur Griffith",
        "Lance Peterson",
        NULL
    };
    aboutBox = gnome_about_new("Gnome Menu Layout. 0.0",
        "(C) 1999 the Free Software Foundation",
        writtenBy,
        "This source code can be used as a starting point to create a Gnome application.",
        NULL);
    gtk_widget_show(aboutBox);
}

static void dummyCallback(GtkObject *object, gpointer data) {
    gnome_ok_dialog("Not implemented...");
}

GnomeUIInfo dummyMenu[] = {
    { GNOME_APP_UI_ITEM,"Dummy",
        "A placeholder menu entry",
        dummyCallback,NULL,NULL,
        GNOME_APP_PIXMAP_NONE,
        NULL,0,0,NULL },
    GNOMEUIINFO_END
};

GnomeUIInfo fileMenu[] = {
    GNOMEUIINFO_MENU_NEW_ITEM("New Window",
        "Open a new application window",
        dummyCallback,data),
    GNOMEUIINFO_MENU_NEW_SUBTREE(dummyMenu),
    GNOMEUIINFO_SEPARATOR,
    GNOMEUIINFO_MENU_OPEN_ITEM(dummyCallback,data),
    GNOMEUIINFO_MENU_SAVE_ITEM(dummyCallback,data),
    GNOMEUIINFO_MENU_SAVE_AS_ITEM(dummyCallback,data),
    GNOMEUIINFO_MENU_REVERT_ITEM(dummyCallback,data),
    GNOMEUIINFO_MENU_PRINT_ITEM(dummyCallback,data),
    GNOMEUIINFO_MENU_PRINT_SETUP_ITEM(dummyCallback,data),
    GNOMEUIINFO_SEPARATOR,
    GNOMEUIINFO_MENU_CLOSE_ITEM(dummyCallback,data),
    GNOMEUIINFO_MENU_EXIT_ITEM(dummyCallback,data),
    GNOMEUIINFO_END
};
```

