
![](img/8bcc1ba72831c7d67cfc8b395deab95f_715_0.png)

每个值都分配了一种独特的颜色；颜色和值都定义为数组。传递给 `gnome_proc_bar_new()` 的 `GdkColor` 对象数组不需要在颜色映射中分配，因为 `GnomeProcBar` 部件会处理。

该部件根据计时器生成自己的回调。在此示例中，调用 `gnome_proc_bar_new()` 时指定了 1000 毫秒。这意味着函数 `updateValue()` 每秒被调用一次。由于 `updateValue()` 没有参数，且其工作是更新显示，因此必须将 `GnomeProcBar` 本身声明为全局变量。此示例简单地循环遍历一些值，然后返回到开头。

## GnomePropertyBox

`GnomePropertyBox` 是一个弹出对话框，可以包含多个包含用于设置属性值的部件的页面。这些页面一个接一个地堆叠（使用 `GtkNotebook`），并可以通过顶部的选项卡进行选择。底部的按钮允许用户更新属性值和/或关闭窗口。

## 继承

`GnomePropertyBox` -> `GnomeDialog` -> `GtkWindow` -> `GtkBin` -> `GtkContainer` -> `GtkWidget` -> `GObject`

## 函数

```c
gint gnome_property_box_append_page(
      GnomePropertyBox *property_box, GtkWidget *child,
      GtkWidget *tab_label);

void gnome_property_box_changed(
      GnomePropertyBox *property_box);

guint gnome_property_box_get_type(void);

GtkWidget *gnome_property_box_new(void);

void gnome_property_box_set_modified(
    GnomePropertyBox *property_box, gboolean state);

void gnome_property_box_set_state(
    GnomePropertyBox *property_box, gboolean state);
```

以下示例程序创建了一个具有两页单选按钮的 `GnomePropertyBox`。这些页面可以包含任何能够保留输入值的部件，例如文本部件或切换按钮。当对话框首次出现时，标记为“确定”和“应用”的按钮处于禁用状态。如果进行了任何更改（在此情况下，是切换单选按钮），则“确定”和“应用”按钮将变为可用。此示例生成的窗口如图 22-24 所示。单击“应用”按钮会导致所有页面的值更新属性。单击“关闭”按钮会立即关闭对话框，无论是否进行了更改。单击“确定”相当于先单击“应用”然后单击“关闭”。

```c
/** gnomepropertybox.c **/
#include <gnome.h>

static void propertyboxCallback(GtkWidget *widget,
                                gint page, gpointer data);

static GtkWidget *makeRadioButtonBox();

void radioCallback(GtkWidget *widget,
                   GnomePropertyBox *propertybox);

int main(int argc, char *argv[]) {
    GtkWidget *propertybox;
    GtkWidget *pageWidget;
    GtkWidget *label;
    gnome_init("gnomepropertybox", "1.0", argc, argv);
    propertybox = gnome_property_box_new();
    gtk_window_set_title(GTK_WINDOW(propertybox),
                         "GnomePropertyBox");
    pageWidget = makeRadioButtonBox("Apples",
                                    "Oranges", propertybox);
    label = gtk_label_new("Radio Buttons");
    gnome_property_box_append_page(
        propertybox,
        pageWidget, label);
    pageWidget = makeRadioButtonBox("Light Blue",
                                    "Dark Blue", "Black", propertybox);
    label = gtk_label_new("More Radio Buttons");
    gnome_property_box_append_page(
        propertybox,
        pageWidget, label);
}
```
