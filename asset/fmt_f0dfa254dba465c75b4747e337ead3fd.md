
你还可以使用 `gtk_tooltips_set_delay` 函数设置工具提示的延迟。可以使用 `gtk_tooltips_disable` 函数禁用工具提示，并使用 `gtk_tooltips_enable` 函数重新启用。

## 加速键

许多人并不使用鼠标选择菜单，而是习惯使用键盘快捷键执行命令。良好的开发者会考虑到这些人，并为常用命令创建键盘快捷键。在使用加速键之前，需要先创建它们，并将它们与窗口关联。`gtk_AccelGroup_new` 函数创建加速组，`gtk_window_add_accelerator_table` 函数将加速表与窗口关联。

```c
/* 创建加速表 ... */

accel_group = gtk_accel_group_new ();
```

```c
/* 将加速表添加到应用程序窗口 ... */

gtk_accel_group_attach (accel_group, GTK_OBJECT (win_name));
```

虽然已经创建了加速表，但此示例将 Control-C (`GTK_CONTROL_MASK`, 'C') 组合键序列映射到 `GtkMenuItem`，并使加速键在菜单上可见 (`GTK_ACCEL_VISIBLE`)。当按下 Control-C 键序列时，会发送 "activate" 信号。

```c
/* ... Control-C 键激活此菜单 ... */

gtk_widget_install_accelerator (menuitem,
    "activate",
    accel_group,
    'C',
    GTK_CONTROL_MASK,
    GTK_ACCEL_VISIBLE);
```

## 代码合并

你可以将所有这些步骤合并到一个函数中，创建一个 `GtkMenuItem`（包含菜单、加速键和工具提示）。该函数每个项目可以替换 10 到 15 行代码，并使代码更容易编写。

该函数带有工具提示和加速键的参数，但如果没有提供它们，则不会进行设置。如果没有为菜单标签提供名称，则创建一个分隔符。整个函数看起来如下：

```c
/*
* CreateMenuItem
* 创建 GtkMenuItem（包含菜单、加速键和工具提示）
此函数替换了每个项目 10 到 15 行代码，并使代码更容易编写。

函数带有工具提示和加速键的参数，但如果没有提供它们，则不会进行设置。如果没有为菜单标签提供名称，则创建一个分隔符。整个函数看起来如下：
*/
```

```c
/*
* CreateMenuItem
* 创建菜单项
* menu - 菜单
* szName - 菜单标签
* szAccel - 加速键
* szTip - 工具提示
* func - 回调函数
*/
GtkWidget *CreateMenuItem(GtkMenu *menu,
    char *szName,
    char *szAccel,
    char *szTip,
    GCallback func,
    gpointer data) {

    GtkWidget *menuitem;
    /* 如果没有提供名称，则创建一个分隔符 */
    if (!szName) {
        // 此处省略了创建分隔符的逻辑
    } else {
        // 创建菜单项
        // 此处省略了创建项的逻辑
    }

    /* 设置加速键 */
    if (szAccel) {
        gtk_widget_install_accelerator (menuitem,
            "activate",
            accel_group,
            szAccel[0],
            GTK_CONTROL_MASK,
            GTK_ACCEL_VISIBLE);
    }

    /* 设置工具提示 */
    if (szTip) {
        gtk_tooltips_set_tip(tooltips, menuitem, szTip, NULL);
    }

    return menuitem;
}
```

*(注：由于原文中代码块部分存在截断或不完整，翻译时保持了其逻辑结构并对注释进行了翻译)*
