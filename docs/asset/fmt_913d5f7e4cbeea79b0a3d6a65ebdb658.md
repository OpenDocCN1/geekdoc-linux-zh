
8. 使用`gnome_app_create_menu`将菜单栏及其菜单（menubar）放置在应用程序（app）上。

9. 使用`gnome_app_create_toolbar`将工具栏（toolbar）放置在应用程序（app）上。

10. 使用`gtk_widget_show_all(app)`显示带有菜单和工具栏的应用程序窗口。

`mymenu.c`程序的内容所示：

```c
#include <gnome.h>
static void copy_func(GtkWidget *button, gpointer data)
{
    g_print("Copy operation\n");
}
static void open_func(GtkWidget *button, gpointer data)
{
    g_print("Open operation\n");
}
```

```c
GnomeUIInfo file_menu[] = {
GNOMEUIINFO_MENU_OPEN_ITEM(open_func, NULL),
GNOMEUIINFO_MENU_EXIT_ITEM(gtk_main_quit, NULL),
GNOMEUIINFO_END
};
```

```c
GnomeUIInfo edit_menu[] = {
GNOMEUIINFO_MENU_COPY_ITEM(copy_func, NULL),
GNOMEUIINFO_END
};
```

```c
GnomeUIInfo menubar[] = {
GNOMEUIINFO_MENU_FILE_TREE(file_menu),
GNOMEUIINFO_MENU_EDIT_TREE(edit_menu),
GNOMEUIINFO_END
};
```

```c
GnomeUIInfo toolbar[] = {
GNOMEUIINFO_ITEM_STOCK("Exit","Exit the application",
gtk_main_quit, GNOME_STOCK_PIXMAP_EXIT),
GNOMEUIINFO_END
};
```

```c
int
main(int argc, char *argv[]) {
GtkWidget *app;
GtkWidget *button;
GtkWidget *label;

gnome_init("menu-sample", "0.1", argc, argv);
/* 创建一个 Gnome 应用组件 */
app = gnome_app_new("Menu-App", "My Gnome Menu");
gtk_signal_connect(app, GTK_OBJECT (app), "delete_event",
GTK_SIGNAL_FUNC (gtk_main_quit), NULL);

label = gtk_label_new("Menu Example");
gnome_app_set_contents(GNOME_APP (app), label);

/* 创建菜单和工具栏 */
gnome_app_create_menu(GNOME_APP (app), menubar);
gnome_app_create_toolbar(GNOME_APP (app), toolbar);

gtk_widget_show_all(app);
gtk_main();
return 0;
}
```

# 第 9 模块：GNOME 337

## GNOME 图标

`libgnomeui`提供了一套丰富的库存图标（stock icons），用于菜单项和工具栏。表 9-9 列出了一些常用图标。它还为 OK 等标准项目提供了库存按钮。

### 工具栏图标

| 说明 | 图标 |
| --- | --- |
| `#define GNOME_STOCK_PIMAP_NEW "New"` | 新建图标 |
| `#define GNOME_STOCK_PIMAP_OPEN "Open"` | 打开文件图标 |
| `#define GNOME_STOCK_PIMAP_CLOSE "Close"` | 关闭文件图标 |
| `#define GNOME_STOCK_PIMAP_SAVE "Save"` | 保存文件图标 |
| `#define GNOME_STOCK_PIMAP_CUT "Cut"` | 剪切编辑操作图标 |
| `#define GNOME_STOCK_PIMAP_COPY "Copy"` | 复制编辑操作图标 |
| `#define GNOME_STOCK_PIMAP_PASTE "Paste"` | 粘贴编辑操作图标 |
| `#define GNOME_STOCK_PIMAP_UNDO "Undo"` | 撤销编辑操作图标 |
| `#define GNOME_STOCK_PIMAP_REDO "Redo"` | 重做编辑操作图标 |
| `#define GNOME_STOCK_PIMAP_PROPERTIES "Properties"` | 属性图标 |
| `#define GNOME_STOCK_PIMAP_PREFERENCES "Preferences"` | 选项图标 |
| `#define GNOME_STOCK_PIMAP_HELP "Help"` | 帮助图标 |
| `#define GNOME_STOCK_PIMAP_PRINT "Print"` | 打印图标 |
| `#define GNOME_STOCK_PIMAP_SEARCH "Search"` | 搜索图标 |
| `#define GNOME_STOCK_PIMAP_BACK "Back"` | 浏览器后退图标 |
| `#define GNOME_STOCK_PIMAP_FORWARD "Forward"` | 浏览器前进图标 |
| `#define GNOME_STOCK_PIMAP_FIRST "First"` | 浏览器首页图标 |
| `#define GNOME_STOCK_PIMAP_LAST "Last"` | 浏览器末页图标 |
| `#define GNOME_STOCK_PIMAP_HOME "Home"` | 浏览器首页图标 |
| `#define GNOME_STOCK_PIMAP_STOP "Stop"` | 浏览器停止图标 |
| `#define GNOME_STOCK_PIMAP_MAIL "Mail"` | 邮件图标 |
| `#define GNOME_STOCK_PIMAP_TRASH "Trash"` | 垃圾箱图标 |
| `#define GNOME_STOCK_PIMAP_TRASH_FULL "Trash Full"` | 垃圾箱满图标 |
| `#define GNOME_STOCK_PIMAP_MIC "Microphone"` | 麦克风图标 |
| `#define GNOME_STOCK_PIMAP_CDROM "Cdrom"` | CD 驱动器图标 |
| `#define GNOME_STOCK_PIMAP_ABOUT "About"` | 关于图标 |
| `#define GNOME_STOCK_PIMAP_QUIT "Quit"` | 退出图标 |

# 表 9-9 库存工具栏图标、菜单和按钮

338 Linux 编程：入门指南

## 库存菜单图标

说明

```
#define GNOME_STOCK_MENU_SAVE "Menu-Save"
#define GNOME_STOCK_MENU_REVERT "Menu-Revert"
#define GNOME_STOCK_MENU_OPEN "Menu-Open"
#define GNOME_STOCK_MENU_CLOSE "Menu-Close"
#define GNOME_STOCK_MENU_QUIT "Menu-Quit"
#define GNOME_STOCK_MENU_CUT "Menu-Cut"
#define GNOME_STOCK_MENU_COPY "Menu-Copy"
#define GNOME_STOCK_MENU_PASTE "Menu-Paste"
#define GNOME_STOCK_MENU_ABOUT "Menu-About"
#define GNOME_STOCK_MENU_PRINT "Menu-Print"
#define GNOME_STOCK_MENU_HELP "Menu-Help"
#define GNOME_STOCK_MENU_UP "Menu-Up"
#define GNOME_STOCK_MENU_DOWN "Menu-Down"
```

表 9-9 库存工具栏图标、菜单和按钮（续）

- 菜单-保存
- 菜单-恢复
- 菜单-打开
- 菜单-关闭
- 菜单-退出
- 菜单-剪切
- 菜单-复制
- 菜单-粘贴
- 菜单-关于
- 菜单-打印
- 菜单-帮助
- 菜单-向上
- 菜单-向下
- 菜单-保存
- 菜单-恢复
- 菜单-打开
- 菜单-关闭
- 菜单-退出
- 菜单-剪切
- 菜单-复制
- 菜单-粘贴
- 菜单-关于
- 菜单-打印
