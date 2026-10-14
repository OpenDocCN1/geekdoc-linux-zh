
### 3.6.5 滑块组件

滑块可以是水平的（`GtkScale`, `GTK_TYPE_HSCALE`）或垂直的（`GtkVscale`, `GTK_TYPE_VSCALE`）。它们的父类是 `GtkScale`，所有组件都使用这些属性：

- `adjustment` (`GtkAdjustment *`): 滑块的范围和值，如第 3.6.4 节所述。
- `draw–value` (`boolean`): 如果为 `TRUE`，GTK+ 在滑块旁边显示滑块的值。如果你想对显示值的格式进行精细控制，请参见本节后面描述的 `format–value` 信号。
- `digits` (`gint`): 值显示小数点右侧的位数。默认为 1。
- `value-pos` (`GtkPositionType`): 决定滑块显示相对于滑块的位置。可能的值有：
  - `GTK_POS_LEFT`
  - `GTK_POS_RIGHT`
  - `GTK_POS_TOP`
  - `GTK_POS_BOTTOM`

滑块属于父类 `GtkRange`（不要与 `GtkAdjustment` 混淆）；这是调整对象的来源。这里还有两个属性：

- `update-policy` (`enumeration` 枚举): 指定滑块更新其 `GtkAdjustment` 的频率。可能的值有：
  - `GTK_UPDATE_CONTINUOUS`: 只要值变化就立即更新值；这是默认值。
  - `GTK_UPDATE_DISCONTINUOUS`: 当用户松开滑块时更新值。
  - `GTK_UPDATE_DELAYED`: 如果用户仍按住鼠标在滑块上，则在一段时间内没有活动时进行更新。
  后两个对于重绘需要大量计算的滑块效果良好；一个例子是第 33.2 节程序中的调整。
- `inverted` (`boolean`): 如果为 `TRUE`，滑块将反转其下限和上限。

滑块带有 `format–value` 信号，使用此处理函数原型：

```
gchar *handler(GtkScale *slider, double number, gpointer data);
```

GTK+ 发射 `format–value` 以获取字符串，当用户调整滑块时发射该信号，`number` 参数是新值。在你的处理函数中，分配一个新的字符串。GTK+ 在不再需要时会释放它。第 33.2 节程序中的调整是一个例子。注意，如果想对显示值的格式进行精细控制，可以使用该信号。将 `draw–value` 属性设为 `FALSE`。

## 3.6.6 数字调节按钮组件

数字调节按钮（`GtkSpinButton`, `GTK_TYPE_SPIN_BUTTON`）与输入框配合工作，允许用户输入。通常，你会为对话框提供按钮或项目信号处理器。属性：

- `adjustment` (`GtkAdjustment *`): 数字调节按钮的范围和值，如第 3.6.4 节所述。
- `rate` (`gdouble`): 用户按下并按住箭头时数值增加的速率。
- `digits` (`gint`): 值显示小数点右侧的位数。默认为 0。
- `snap-to-ticks` (`boolean`): 如果为 `TRUE`，数字调节按钮将对齐到最近刻度。
- `wrap` (`boolean`): 如果为 `TRUE`，数字调节按钮将循环。
- `update-policy` (`enumeration` 枚举): 指定数字调节按钮更新其 `GtkAdjustment` 的频率。可能的值有：
  - `GTK_UPDATE_ALWAYS`: 只要值变化就立即更新值。
  - `GTK_UPDATE_IF_VALID`: 当用户松开滑块时更新值。
  - `value` (`gdouble`): 数字调节按钮的值。
- `numeric` (`boolean`): 如果为 `TRUE`，数字调节按钮允许数字输入。

## 3.6.7 颜色选择器组件

颜色选择器（`GtkColorSelection`，类类型 `GTK_TYPE_SELECTION`）与组件配合工作，存储组件表示的值，并为组件提供外观提示。

- `has-palette` (`boolean`): 如果为 `TRUE`，选择器包含调色板。
- `has-opacity` (`boolean`): 如果为 `TRUE`，选择器包含透明度。
- `current-color` (`GdkColor`): 当前颜色。

GTK+ 为调整对象发射两个信号：当对象中的值发生变化或其参数之一发生变化时，发射 `value–changed`。其处理函数的原型为：

```
void handler (GtkAdjustment *adjustment, gpointer data)
```

GTK+ 发射 `format–value` 以获取字符串，当用户调整滑块时发射该信号，`number` 参数是新值。在你的处理函数中，分配一个新的字符串。GTK+ 在不再需要时会释放它。

## 3.6.8 字体选择器组件

字体选择器（`GtkFontSelection`, `GTK_TYPE_FONT_SELECTION`）组件如图 3.10 所示，允许用户预览和选择字体。它有两个属性，均为字符串：

- `font-name`: 当前所选字体的名称。
- `preview-text`: 组件底部用于演示当前所选字体的文本。

### 3.6.9 文件浏览器

文件选择器（`GtkFileSelection`, `GTK_TYPE_FILE_SELECTION`）仅作为独立的对话框可用，如图 3.11 所示。通常，你会为对话框提供按钮或项目信号处理器。你必须提供额外的信号处理器来决定当用户点击“确定”和“取消”按钮时做什么。

# GNOME 开发者官方指南

图 3.11：GTK+ 文件浏览器。

通常情况下，你只能从文件浏览器中选择单个文件；文件的路径名是浏览器 `filename` 中的一个 `garray` 字符串。

然而，你可以通过布尔属性 `select–multiple` 启用多选功能。当然，如果你想要多个文件，就无法再通过简单的 `filename` 属性获取文件了。使用：

```
files = gtk_file_selection_get_selections(file_browser);
```

来获取所有文件。`files` 值的类型应为 `garray*`；`NULL` 值表示字符串数组的最后一个元素。在你处理完文件后，使用 `g_strfree(files)` 释放它们的内存。

注意：所有来自浏览器的文件名都是使用操作系统的字符编码的。如果你想将名称放入 GTK+ 控件中，你应该使用第 1.4.4 节中的任一个函数将名称转换为 UTF–8。

文件浏览器的一个属性是 `show-files`（布尔型）。如果你将其设置为 `TRUE`，文件浏览器框顶部将出现三个用于创建目录、删除文件和重命名文件的按钮。

如果你需要带有文件选择按钮的文件名，请考虑使用第 4.3.5 节中描述 `GnomeFileEntry`。

## 3.6.10 选择器示例

本节展示了颜色选择器、字体选择器和文件浏览器的示例程序；最终产品请见图 3.12。演示从常规的窗口信号处理程序以及文件浏览器框的全局声明开始：

```c
/* coding: utf-8 -*- */
/* selections.c -- 演示选择控件 */
#include <gtk/gtk.h>
GtkFileSelection *file_browser;
/* 标准句处理程序 */
gint gdk_delete_event(GtkWidget *widget, GdkEvent event, gpointer data)
{
    return FALSE;
}
void end_program(GtkWidget *widget, gpointer data)
{
    gtk_main_quit();
}
```

![](img/ae44ff3edd9313fce71c50baa18b0c66_161_0.png)

图 3.12：选择器、颜色和字体选择应用程序。

此处理函数用于选择器的 `color-changed` 信号。请注意，如果用户仍在控件上拖动内容，它将什么都不做。

```c
/* "color-changed" 的处理器，将新颜色打印到控制台 */
void print_color(GtkColorSelection *chooser, gpointer data)
{
    GdkColor color;
    gint red, green, blue;
    gint alpha;
    /* 如果用户仍在调整控件，则什么都不做 */
    if (!gtk_color_selection_is_adjusting(chooser))
        g_object_get(chooser, "current-color", &color, NULL);
    red = color.red;
    green = color.green;
    blue = color.blue;
    g_object_get(chooser, "current-alpha", &alpha, NULL);
```
