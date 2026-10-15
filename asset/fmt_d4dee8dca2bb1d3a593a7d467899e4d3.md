
`window = gtk_window_new(GTK_WINDOW_TOPLEVEL);`

`gtk_window_set_size(GTK_WINDOW(window), 200, 100);`

`gtk_window_set_title(GTK_WINDOW(window), "Menu");`

`g_signal_connect(GTK_OBJECT(window), "delete-event", (GtkSignalFunc) gtk_quit, NULL);`

```c
/* 初始化菜单项 */
menu = gtk_menu_new();/* 这是持有菜单项的菜单，当你点击 "Root Menu" 时弹出的那个 */
gtk_widget_show(menu);

/* 创建根菜单，这是在菜单栏上显示的标签 */
root_menu = gtk_menu_item_new_with_label("Root Menu");

gtk_widget_show(root_menu);/* 现在指定我们新创建的 "menu" 为 "root menu" */
gtk_menu_item_set_submenu(GTK_MENU_ITEM (root_menu), menu);
```

/* 创建 vbox： */

`vbox = gtk_box_new(FALSE, 0);`

`gtk_container_add(GTK_CONTAINER (window), vbox);`

`gtk_widget_show(vbox);`

```c
/* 创建菜单栏以持有菜单并将其添加到主窗口 */
menu_bar = gtk_menu_bar_new();
gtk_box_pack_start(GTK_BOX (vbox), menu_bar, FALSE, 2);
gtk_widget_show (menu_bar);
```

/* 创建一个按钮将每个菜单作为弹出窗口附加 */

`button = gtk_button_new_label("press me");`

`gtk_signal_connect_object(GTK_OBJECT (button), "event",`

`GTK_FUNC (button_press), GTK_OBJECT (menu));`

`gtk_box_pack_end(GTK_BOX (vbox), button, TRUE, 2);`

`gtk_widget_show (button);`

```c
/* 最后将菜单项添加到菜单栏 —— 我们一直在讨论的 "root" 菜单项 */
gtk_menu_bar_append(GTK_MENU_BAR (menu_bar), root_menu);
```

/* 最后一步显示窗口以便显示 */

`gtk_widget_show (window);`

`gtk_main ();`

`return(0);`

`}`

```c
/* 通过传递消息作为 widget 来响应按钮按下。
注意 "widget" 参数是正在发布的菜单，而不是
被按下的按钮。 */
```

```c
static gint button_press (GtkWidget *widget, GdkEvent *event) {
    if (event->type == GDK_BUTTON_PRESS) {
        GdkButton *bevent = (GdkButton *)event;
        gtk_menu_popup(GTK_MENU (widget), NULL, NULL, NULL,
        bevent->button, button, event->time);
        /* 告诉调用代码我们已处理该事件，回调在此停止。 */
        return TRUE;
    }
    /* 告诉调用代码我们没有处理此事件；将其传递下去。 */
    return FALSE;
}
```

```c
/* 选择菜单项时打印字符串 */
```

```c
static void menuitem_response(gchar *string)
{
    printf("%s\n", string);
}
```

/* example-end */

你还可以设置菜单项为不可用，并使用加速器表将键绑定到菜单函数。

## 13.3 使用 GtkItemFactory

现在我们已经向你展示了困难的方法，这里是使用 `gtk.item_factory` 调用的方法。

## 13.4 项目工厂示例

这里是一个使用 GTK 项目工厂的示例。

```c
/* example-start menu itemfactory.c */
#include <gtk/gtk.h>
#include <strings.h>
```

/* 强制的基础回调 */

```c
static void print_hello(GtkWidget *w, gpointer data)
{
    g_message("Hello, World!\n");
}
```

```c
/*/* 这是用于生成新菜单的 GtkItemFactory 结构。
项 1: 菜单路径。下划线下的字母表示菜单打开后的加速键。
项 2: 对应条目的的加速键。
项 3: 回调函数。
项 4: 回调动作。这更改了调用函数时的参数。默认值是 0。
项 5: 项类型，用于定义它是哪种项。
以下是可能的值：
NULL                -> "Item"
"<Title>"           -> 创建标题项
"<Item>"            -> 创建简单项
"<CheckItem>"      -> 创建复选项
"<ToggleItem>"     -> 创建切换项
"<RadioItem>"      -> 创建单选项
"<path>"             -> 用于链接的单选项路径
"<Separator>"       -> 创建分隔符
"<Branch>"          -> 创建持有子项的项（可选）
"<LastBranch>"     -> 创建右对齐分支
*/
```

```c
static GtkItemFactory menu_items[] = {
    {"/File", NULL, NULL, 0, "Branch" },
    {"/File/New", "<control>N", print_hello, 0,NULL},
    {"/File/Open", "<control>O", print_hello, 0,NULL},
}
```

```c
/* (其余代码省略) */
```

# 13. 菜单 Widget

```c
{ "/File/.Save", "<Control-S>", print_hello, 0, NULL },
{ "/File/Save_As", NULL, NULL, 0, NULL },
{ "/File/sep", NULL, NULL, 0, "<Separator>" },
{ "/File/Quit", "<Control-Q", gtk_main_quit, 0, NULL },
{ "/Options", NULL, NULL, 0, "<Branch>" },
{ "/Options/Test", NULL, NULL, 0, NULL },
{ "/Help", NULL, NULL, 0, "<LastBranch>" },
{ "/Help/About", NULL, NULL, 0, NULL };
void get_main_menu(Gtkwidget *window, GtkMenubar *menubar)
{
  GtkItemFactory *item_factory;
  GtkAccelGroup *accel_group;
  gint menu_items = sizeof(menu_items) / sizeof (menu_items[0]);
  accel_group = gtk_accel_group_new (NULL);
  /* 此函数初始化了项目工厂。
     参数 1：菜单类型 - 可以是 GTK_TYPE_MENU_BAR, GTK_TYPE_MENU,
     或 GTK_TYPE_OPTION_MENU。
     参数 2：菜单的路径。
     参数 3：指向 gtk_accel_group 的指针。项目工厂在生成菜单时
     会设置加速键。 */
  item_factory = gtk_item_factory_new (GTK_TYPE_MENU_BAR, "<main>", accel_group);
  /* 此函数生成菜单项。传递项目工厂、
     数组中的项数量、数组本身以及
     用于菜单项的回调数据。 */
  gtk_item_factory_create_items (item_factory, menu_items, menu_items, NULL);
  /* 将新的加速组附加到窗口上。 */
```
