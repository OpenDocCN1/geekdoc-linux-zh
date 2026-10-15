
```
001 #include <gtk/gtk.h>
002 #include <stdio.h>
003
004 static GtkWidget *leftButton,*rightButton,*centerButton,*fillButton;
005 static GtkWidget *trueButton,falseButton;
006
007 static void
008 QuitCallback(GtkWidget *widget, GtkWidget *dialog_window)
009   {
010     gtk_quit();
011     exit( 0);
012   }
013 static void
014 ClickedCallback(GtkWidget *widget, GtkWidget *dialog_window)
015 {
016     GtkWidget *window, *labelFrame, *labelTest, vbox;
017 
018     window = gtk_window_new(GTK_WINDOW_TOPLEVEL);
019     gtk_window_position(GTK_WINDOW (window), GTK_WIN_POS_MOUSE);
020     gtk_widget_set_size(window, 320, -1 );
021     vbox = gtk_box_new(FALSE, 0);
022     gtk_container_add(GTK_CONTAINER (window), vbox);
023 
024     labelFrame = gtk_frame_new("Test Label");
025     gtk_box_pack_start(GtkBOX (vbox), labelFrame, TRUE, 10);
026     labelTest = gtk_label_new("Line 1\n"
027     "This is Line 2\n"
028     "And this is Line 3\n"
029     "And finally, this is Line 4\n");
030 
031     gtk_container_add(GTK_CONTAINER (labelFrame), labelTest);
032     if ( GTK_TOGGLE_BUTTON(leftButton)->active == TRUE ) {
033         gtk_label_set_justify(GTK_LABEL(labelTest),
034         GTK_JUSTIFY_LEFT);
035     } else if ( GTK_TOGGLE_BUTTON(rightButton)->active == TRUE ) {
036         gtk_label_set_justify(GTK_LABEL(labelTest),
037         GTK_JUSTIFY_RIGHT);
038     } else if ( GTK_TOGGLE_BUTTON(centerButton)->active == TRUE ) {
039         gtk_label_set_justify(GTK_LABEL(labelTest),
040         GTK_JUSTIFY_CENTER);
041     } else if ( GTK_TOGGLE_BUTTON(fillButton)->active == TRUE ) {
042         gtk_label_set_justify(GTK_LABEL(labelTest),
043         GTK_JUSTIFY_FILL);
044     }
045     if ( GTK_TOGGLE_BUTTON(trueButton)->active == TRUE ) {
046         gtk_label_set_line_wrap(GTK_LABEL(labelTest), TRUE);
047         gtk_label_set_text(GTK_LABEL(labelTest),
048         "This is a huge line that I am hoping will line wrap when I set line wrap to
049         on because, it is big and it ought to line wrap.");
050     } else {
051         gtk_label_set_line_wrap(GTK_LABEL(labelTest), FALSE);
052     }
053     gtk_widget_show_all(window);
054 }
```

## 标签中的下划线（Underscores in the Label）

为了更好地理解这两个标签属性是如何协同工作的，最好看一个它们的用法示例。（此处略）生成上述屏幕的应用程序源代码展示了如何调用 `gtk_label_set_justify()` 和 `gtk_label_set_line_wrap()`：

- **代码列表 5.1** GtkLabel 属性示例代码

（代码块略）

标签中的下划线（Underscores in the Label）

在标签中设置下划线通常可以通过 `gtk_label_set_underline()` 实现。该函数允许你指定标签中的某个字符来显示下划线，这通常作为快捷键（加速键）。

```
void gtk_label_set_underline(GtkLabel *label, gint8);
```

### `gtk_label_set_underline()`

该函数接受两个参数：

- `label`：要设置的标签实例。
- `underline`：下划线的类型。值可以是：
    - `GTK_UNDERLINE_NONE`：无下划线。
    - `GTK_UNDERLINE_SINGLE`：单下划线。
    - `GTK_UNDERLINE_DOUBLE`：双下划线。

### 示例

```c
GtkWidget *label;
label = gtk_label_new("File_Menu");
gtk_label_set_underline(GTK_LABEL(label), GTK_UNDERLINE_SINGLE);
```

在上面的示例中，“File_Menu”中的字母 `M` 将带有一个单下划线，表示 `M` 是加速键。

### 加速键（Accelerators）

在 Gtk 中，加速键可以通过在标签中包含下划线来定义。例如，在菜单项中，如果标签为 `_Edit`，那么 `E` 就会成为该项的加速键。当用户按下 `Alt+E` 键时，会触发该菜单项。

### 注意事项

- 设置下划线仅影响视觉显示，不会改变标签文本本身。
- 如果需要动态更改下划线，可以使用 `gtk_label_set_underline()`。

## GtkButton

### 类名

`GtkButton`

### 父类名

`GtkBin`

## 宏

- 小部件类型宏：`GTK_TYPE_BUTTON`
- 对象到小部件转换：`GTK_BUTTON(obj)`
- 小部件类型检查宏：`GTK_IS_BUTTON(obj)`

### 表 5.4 信号

| 信号名称 | 触发信号的条件 |
|---|---|
| pressed | 按钮小部件在逻辑上被“按下”。 |
| released | “按下”的按钮在逻辑上被释放。 |
| clicked | 按钮小部件在逻辑上被点击。 |
| enter | 鼠标指针进入了按钮占据的区域。 |
| leave | 鼠标指针离开了按钮占据的区域。 |

## 信号原型

```c
void pressed(GtkButton *button, gpointer user_data);
void released(GtkButton *button, gpointer user_data);
void clicked(GtkButton *button, gpointer user_data);
void enter(GtkButton *button, gpointer user_data);
void leave(GtkButton *button, gpointer user_data);
```

### 表 5.5 GtkButton 参数

| 名称 | 类型 | 权限 |
|---|---|---|
| label | GTK_TYPE_STRING | GTK_ARG_READWRITE |
| relief | GTK_TYPE_RELIEF_STYLE | GTK_ARG_READWRITE |

### 应用层级摘要

- 在运行时获取 `GTK_TYPE_BUTTON` 的值：`GtkType gtk_button_get_type(void);`
- 创建一个没有标签的 `GtkButton` 实例：`GtkWidget *gtk_button_new(void);`
- 创建一个指定标签的 `GtkButton` 实例：`GtkWidget *gtk_button_new_with_label(const gchar *label);`
- 为指定的 `GtkButton` 实例触发 `pressed` 信号：`void gtk_button_pressed(GtkButton *button);`
- 为指定的 `GtkButton` 实例触发 `released` 信号：`void gtk_button_released(GtkButton *button);`
- 为指定的 `GtkButton` 实例触发 `clicked` 信号：`void gtk_button_clicked(GtkButton *button);`
- 为 `GtkButton` 实例触发 `enter` 信号：`void gtk_button_enter(GtkButton *button);`
- 为指定的 `GtkButton` 实例触发 `leave` 信号：`void gtk_button_leave(GtkButton *button);`
- 为指定的 `GtkButton` 实例设置浮雕样式：`void gtk_button_set_relief(GtkButton *button, GtkReliefStyle newstyle);`
- 获取指定的 `GtkButton` 实例的当前浮雕样式：`GtkReliefStyle gtk_button_get_relief(GtkButton *button);`

### 类描述

`GtkButton` 可能是 Gtk+ 小部件集（或任何其他小部件集）提供的最基础的控件部件之一。想象中，简单且可能最常用的对话框是消息对话框，图 5.11 显示了这样一个示例。实现此类对话框所需的唯一控件部件是 `GtkButton`，在这种情况下，它提供了一个推按钮，用户在阅读完消息后点击该按钮来关闭对话框。

`GtkButton` 非常简单，无论是在其布局和外观上（参见图 5.11），还是在与应用程序的交互上。关于外观，推按钮无非是一个显示标签的矩形区域。在 `GtkButton` 的情况下，该标签是 `GtkLabel` 的一个实例。`GtkButton` 的父类是 `GtkBin`，这反映了按钮是一个管理 `GtkLabel` 实例的容器。我将在本章后面讨论创建 `GtkButton` 实例的函数时，再讨论此的影响。

## 信号

在交互方面，大多数应用程序主要感兴趣的是按钮何时被点击，点击是按钮被按下并释放的逻辑术语。这里再次详细说明 `GtkButton` 小部件支持的信号：

- **clicked**: 该信号表示用户在 `GtkButton` 实例管理的区域内物理地按下并释放了按钮，结果按钮在逻辑上被按下或点击。
- **enter**: 该信号表示鼠标指针进入了按钮占据的区域。
- **pressed**: 该信号在用户物理按下按钮时触发。
- **released**: 该信号在用户物理释放按钮时发送。
- **leave**: 该信号表示鼠标指针离开了按钮占据的区域。

图 5.8、5.9 和 5.10 展示了三个对话框，每个对话框都包含标记为苹果、橙子和梨的按钮。

**图 5.8** 单选按钮

**图 5.9** 切换按钮

**图 5.10** 复选框按钮

图 5.8 中的按钮是 `GtkRadioButton` 的实例，而图 5.9 和 5.10 中的按钮分别是 `GtkToggleButton` 和 `GtkCheckButton` 的实例。单选按钮（见图 5.8）允许用户进行“多选一”的选择。单选按钮，这些标记为苹果、橙子和梨的按钮通过将它们放入一个“单选组”来相互关联。一个单选组一次只能选择一个单选按钮。给定图 5.8 所示的单选组状态，点击标记为橙子的按钮会导致它被选中，并使标记为苹果的按钮取消选中。另一方面，`GtkToggleButton` 和 `GtkCheckButton` 允许用户进行“多选多”的选择。例如，用户可以如图 5.10 所示同时选择苹果和梨。`GtkToggleButton` 和 `GtkCheckButton` 类在功能上相似，这两个类唯一的区别在于小部件的外观，可以通过比较图 5.9 和 5.10 看出。

```
void
gtk_button_leave(GtkButton *button);
```

生成合成事件的能力主要为小部件编写者提供，应用程序设计师通常不需要。

# 凸起样式 (Relief Styles)

`GtkButton` 允许你设置 `GtkButton` 实例的凸样式。支持以下凸起样式：`GTK_RELIEF_NORMAL`、`GTK_RELIEF_HALF` 和 `GTK_RELIEF_NONE`。`GtkButton` 的默认凸起样式为 `GTK_RELIEF_NORMAL`。在 Gtk 1.2 中，`GTK_RELIEF_HALF` 和 `GTK_RELIEF_NORMAL` 是同义的，因为 `GtkButton` 只区分 `GTK_RELIEF_NORMAL`、`GTK_RELIEF_NONE` 和其他样式。指定 `GTK_RELIEF_NONE` 告诉 `GtkButton` 不要在按钮周围绘制边框；当小部件没有焦点时，只会显示按钮的文本。指定 `GTK_RELIEF_NORMAL` 或 `GTK_RELIEF_HALF` 则会在按钮周围绘制一个边框，如图所示。

![](img/b9af04aaed46302cb075052312fcd667_212_0.png)

### 5.12 GTK_RELIEF_HALF 和 GTK_RELIEF_NORMAL

![](img/b9af04aaed46302cb075052312fcd667_212_1.png)

### 5.13 GTK_RELIEF_NONE

要为指定的 `GtkButton` 实例设置凸起样式，可以调用 `gtk_button_set_relief()`：

```
void
gtk_button_set_relief(GtkButton *button, GtkReliefStyle newstyle);
```

要获取指定的 `GtkButton` 实例的当前凸起样式，可以调用 `gtk_button_get_relief()`：

```
GtkReliefStyle
gtk_button_get_relief(GtkButton *button);
```

## GtkToggleButton

### 类名

`GtkToggleButton`

### 父类名

`GtkButton`

## 宏

- 类型类型宏：`GTK_TYPE_TOGGLE_BUTTON`
- 对象到小部件的转换宏：`GTK_TOGGLE_BUTTON(obj)`
- 类型类型检查宏：`GTK_IS_TOGGLE_BUTTON(obj)`

### 表 5.6 信号

| 信号名称 | 触发信号的条件 |
|--- |--- |
| toggled | 切换按钮小部件的状态发生了变化（例如从开启到关闭）。 |

# 信号函数原型

```
void toggled(GtkToggleButton *togglebutton, gpointer user_data);
```

### 支持的参数

前缀：`GtkToggleButton::`

### 表 5.7 GtkToggleButton 参数

| 名称 | 类型 | 权限 |
|--- |--- |--- |
| active | GTK_TYPE_BOOL | GTK_ARG_READWRITE |
| draw_indicator | GTK_TYPE_BOOL | GTK_ARG_READWRITE |

## 应用程序级 API 摘要

在运行时获取常量 `GTK_TYPE_TOGGLE_BUTTON`：

```
GtkType
gtk_toggle_button_get_type(void);
```

创建一个不带标签的 `GtkToggleButton` 新实例：

```
GtkWidget *
gtk_toggle_button_new(void);
```

创建一个带有指定标签的 `GtkToggleButton` 新实例：

```
GtkWidget *
gtk_toggle_button_new_with_label(const gchar *label);
```

切换切换按钮指示器的显示或隐藏：

```
void
gtk_toggle_button_toggle(GtkToggleButton *toggle_button,
gboolean draw_indicator);
```

将 `GtkToggleButton` 实例设置为激活状态（选中）：

```
void
gtk_toggle_button_set_active(GtkToggleButton *toggle_button,
gboolean is_active);
```

获取 `GtkToggleButton` 实例的激活状态：

```
gboolean
gtk_toggle_button_get_active(GtkToggleButton *toggle_button);
```
