
传递给 `gtk_text_forward_delete()` 的参数与传递给 `gtk_text_backward_delete()` 的参数相同。`gtk_text_forward_delete()` 删除插入点之后的 `n` 个字符。如果插入点之后缓冲区中的字符少于 `n` 个，则操作将失败并返回 FALSE。否则，将删除 `n` 个字符并返回 TRUE 表示成功。该函数不会改变光标的位置。

冻结与解冻组件。通过插入或删除大量文本，或者通过连续进行大量的插入或删除，当 GtkText 更改缓冲区内容时，用户可能会看到闪烁或其他可能的视觉伪影。为了避免这种情况，我建议始终将对 `gtk_text_insert()`、`gtk_text_forward_delete()` 和 `gtk_text_backward_delete()` 的调用封装在 `gtk_text_freeze()` 和 `gtk_text_thaw()` 调用中。`gtk_text_freeze()` 函数：

```
void
gtk_text_freeze(GtkText *text);
```

将阻塞任何对文本 UI 的更新，直到后续调用了 `gtk_text_thaw()`。因此，`gtk_text_thaw()` 会抵消上一次对 `gtk_text_freeze()` 调用的影响。其原型如下：

```
void
gtk_text_thaw(GtkText *text);
```

GtkText 会自动对大于 1,024 个字符的插入或删除操作进行冻结和解冻。以下代码展示了如何使用 `gtk_text_freeze()` 和 `gtk_text_thaw()`：

```
GtkText *text;
char *str;
```

```
gtk_text_freeze( GTK_TEXT(text) );
gtk_text_insert( GTK_TEXT(text), NULL, NULL, str, strlen(str) );
gtk_text_thaw( GTK_TEXT(text) );
```

# 获取文本

GtkText（类似于 GtkEntry）继承自 GtkEditable，此书中未讨论该类。然而，你必须使用 GtkEditable 中的一个函数来获取经用户编辑后文本控件的内容。要检索文本，必须调用 `gtk_editable_get_chars()`。

```
gchar *
gtk_editable_get_chars(GtkEditable *editable, gint start_pos,
    gint end_pos);
```

`editable` 参数是 `GtkEditable` 或其派生类（例如 `GtkText`）的实例。（另一个派生自 `GtkEditable` 的类是 `GtkEntry`，但它提供了一个允许应用程序获取输入字段内容的函数）。将检索的字符由参数 `start_pos` 和 `end_pos` 定义。有效范围为 `[0, text_size-1]`，其中 `text_size` 是本节稍早调用返回的值。你应该确保 `start_pos` 的值小于 `end_pos`。返回的是一个指向所返回缓冲区的指针。你的应用程序可以根据需要自由操作该缓冲区的内容；在不再需要时释放返回缓冲区所指向的内存，你的应用程序可以将其传递给 `g_free()`。

以下代码说明了如何获取 Gtk 组件的内容。在此示例中，我正从一个 GtkButton 的 "clicked" 信号中获取内容（假设在此示例中，该按钮标签为“检查拼写”，且点击信号的任务是从文本控件获取内容并传递给拼写检查器）。

```
static void
SpellCheckCB(GtkWidget *widget, GtkWidget *text)
{
    char *buf;

    // 获取输入缓冲区：start_pos 为 0，end_pos 为
    // 缓冲区中的字符数减去 1。

    buf = gtk_editable_get_chars(GTK_EDITABLE(text), 0,
        gtk_text_get_length(GTK_TEXT( text ) ) - 1 );
    check_spelling(buf);
}
```

```
main(int argc, char *argv[])
{
    GtkWidget *button, *text;

    ...

    text = gtk_text_new(NULL, NULL);

    ...

    button = gtk_button_new_with_label("Check Spelling");
```

```
gtk_signal_connect(GTK_OBJECT(button), "clicked",
GTK_SIGNAL_FUNC(SpellCheckCB), text);
...
gtk_main();
}
```

# GtkSpinButton

## 类名

`GtkSpinButton`

## 父类名

`GtkEntry`

## 宏

- 组件类型宏：`GTK_TYPE_SPIN_BUTTON`
- 对象到组件类的宏：`GTK_SPIN_BUTTON(obj)`
- 组件类型检查宏：`GTK_IS_SPIN_BUTTON(obj)`

## 支持的自旋参数

前缀：`GtkSpinButton::`

### 14.3 GtkSpinButton 参数

| 名称 | 类型 | 权限 |
| --- | --- | --- |
| adjustment | `GTK_TYPE_ADJUSTMENT` | |
| climb_rate | `GTK_TYPE_FLOAT` | |
| digits | `GTK_TYPE_UINT` | |
| snap_to_ticks | `GTK_TYPE_BOOL` | |
| numeric | `GTK_TYPE_BOOL` | |

### 14.3 GtkSpinButton 参数（续）

| 名称 | 类型 | 权限 |
| --- | --- | --- |
| wrap | `GTK_TYPE_BOOL` | `GTK_READ_WRITE` |
| update_policy | `GTK_TYPE_SPIN_BUTTON_UPDATE` | `GTK_READ_WRITE` |
| shadow_type | `GTK_TYPE_SHADOW` | `GTK_READ` |

# 应用级概述

运行时获取 `GTK_TYPE_SPIN_BUTTON`：

```
GtkType
gtk_spin_button_get_type();
```

创建一个 `GtkSpinButton` 实例：

```
GtkWidget *
gtk_spin_button_new(GtkAdjustment *adjustment, gfloat climb_rate, guint digits)
```

设置自旋按钮的调整和其他属性：

```
void
gtk_spin_button_configure(GtkSpinButton *spin_button, GtkAdjustment *adjustment, gfloat climb_rate, guint digits)
```

设置自旋按钮的调整对象：

```
void
gtk_spin_button_set_adjustment(GtkSpinButton *spin_button, GtkAdjustment *adjustment);
```

获取自旋按钮的调整对象：

```
GtkAdjustment *
gtk_spin_button_get_adjustment(GtkSpinButton *spin_button);
```

作为浮点数获取自旋按钮的值：

```
gfloat
gtk_spin_button_get_value_as_float(GtkSpinButton *spin_button);
```

作为整数获取自旋按钮的值：

```
gint
gtk_spin_button_get_value_as_int(GtkSpinButton *spin_button);
```

## 应用级概述（续）

设置自旋按钮的当前值：

```
void
gtk_spin_button_set_value(GtkSpinButton *spin_button, gfloat value);
```

设置自旋按钮的更新策略（`GTK_UPDATE_ALWAYS` 或 `GTK_UPDATE_IF_VALID`；见文本）：

```
void
gtk_spin_button_set_update_policy(GtkSpinButton *spin_button, GtkSpinButtonUpdatePolicy policy);
```

设置自旋按钮的数字模式（默认为 FALSE）：

```
void
gtk_spin_button_set_numeric(GtkSpinButton *spin_button, gboolean numeric);
```

通过指定的增量和方向设置自旋按钮（见 `GtkSpinType` 定义）：

```
void
gtk_spin_button_set_spin(GtkSpinButton *spin_button, GtkSpinType direction, gfloat increment);
```

设置自旋按钮的换行属性：

```
void
gtk_spin_button_set_wrap(GtkSpinButton *spin_button, gboolean wrap);
```

设置自旋按钮的阴影类型（`GTK_SHADOW_NONE`、`GTK_SHADOW_IN`、`GTK_SHADOW_OUT`、`GTK_SHADOW_ETCHED_IN` 或 `GTK_SHADOW_ETCHED_OUT`）：

```
void
gtk_spin_button_set_shadow_type(GtkSpinButton *spin_button, GtkShadowType shadow_type);
```

设置自旋按钮的对齐刻度属性：

```
void
gtk_spin_button_set_snap_to_ticks(GtkSpinButton *spin_button, gboolean snap_to_ticks);
```

更新自旋按钮的显示：

```
void
gtk_spin_button_update(GtkSpinButton *spin_button);
```

### 类描述

自旋按钮是一种专门设计的输入控件，用于支持在定义的整数或浮点范围内的数值输入。自旋按钮接受任意精度的正负整数和浮点数值。图 14.1 展示了一个

包含多个调节按钮（spin button）小部件的对话框（参见标记为小时、分钟、秒和距离的字段）。如图 14.1 所示，一个调节按钮由两个区域组成。第一个区域类似于 `GtkEntry` 实例，提供了一个供部件显示调节按钮当前值的区域，并提供了一个用户可以直接在控件中输入新值的位置。第二个区域紧邻输入字段右侧，由一对箭头按钮组成。点击上箭头按钮会增加输入字段中的值，而点击下箭头按钮会减少该值。

![](img/b9af04aaed46302cb075052312fcd667_740_0.png)

**图 14.1** 对话框中的调节按钮

`GtkSpinButton` 接受的数值范围由使用 Gtk+ 调整对象（adjustment object）的应用程序指定（参见第 13 章，“范围部件和调整对象”）。例如，一个下限设置为 1、上限设置为 12 且 `step_increment` 设置为 1 的调整对象，适用于指定一个接受用户输入的日期月份部分的调节按钮范围。

## 键盘和鼠标事件

调节按钮对鼠标点击和按键按下事件敏感；`GtkSpinButton` 专门监听表 14.4 列出的按键事件。

### GtkSpinButton

| 表 14.4 GtkSpinButton 按键事件 | |
| 键 | 动作 |
|---|---|
| 上 (Up) | 值增加 `timer_step`（最小为 `step_increment`）。 |
| 下 (Down) | 值减少 `timer_step`（最小为 `step_increment`）。 |
| 翻向上 (Page Up) | 值增加 `page_increment`。 |
| 翻页向下 (Page Down) | 值减少 `page_increment`。 |

调节按钮小部件的 `timer_step` 属性将在本章稍后进行描述。我将描述 `gtk_spin_button_new()` 的 `climb_rate` 参数。表 14.5 描述了鼠标按下和释放事件如何影响调节按钮小部件的值：

| 表 14.5 GtkSpinButton 鼠标事件 | |
| 按钮事件 | 动作 |
|---|---|
| 按钮 1 按下 | 与 Up 和 Down 键相同 |
| 按钮 2 按下 | 与 Page Up 和 Down 键相同 |
| 按钮 3 释放，上箭头 | 将调整值赋给调整上限字段 |
| 按钮 3 释放，下箭头 | 将调整值赋给调整下限字段 |

例如，如果调节按钮调整对象的下限设置为 30，且用户在下箭头上释放了按钮 3，那么调节按钮的值（以及调整对象的值）将被设置为 30（调整对象下限字段的值）。

## 创建调节按钮小部件

要创建一个 `GtkSpinButton` 实例，请调用 `gtk_spin_button_new()`：

```
GtkWidget *
gtk_spin_button_new(GtkAdjustment *adjustment, gfloat climb_rate,
guint digits);
```

`gtk_spin_button_new()` 函数接受三个参数。第一个参数 `adjustment` 是一个 `GtkAdjustment` 对象。它可以是你创建的调整对象、从其他部件中获取的调整对象（例如，从滑块或滚动条部件获取），也可以是 `NULL`。如果如果设置为 `NULL`，系统将为你创建一个调整对象，在这种情况下，所有调整对象的字段都将初始化为 0.0。

第二个参数 `climb_rate` 用于控制当用户触发表 14.4 和表 14.5 列出的事件（鼠标按钮释放事件外）时，调节按钮值的变化率。

## 理解变化率 (Climb Rate)

为了理解 `climb_rate` 如何使用，我将描述用户在其中一个调节按钮上按住鼠标按钮1 时发生的情况。首先，调节按钮的值向适当的方向移动；移动量由调整对象的 `step_increment` 定义，方向（正或负）取决于按了哪个箭头（上或下）。接下来，调节按钮会注册一个定时器，该器将在大约 200 ms 后触发。调节按钮将 `step_increment` 的值保存在名为 `timer_step` 的内部字段中；此（`timer_step`）将被超时函数用于决定改变调节按钮值多少，正如我将描述的那样。

超时函数第一次被调用时，每隔 20 ms 重置一次计时器，加快调节按钮值的更新速度。接下来，调节按钮的值将根据 `timer_step` 中保存的值进行增加（或减少）。在函数被调用的前五次中，`timer_step` 值保持不变（在箭头上第一次按下按钮约 300 ms 后）。然而，每次调用时，`timer_step` 值都会增加 `climb_rate` 值。其效果是，当用户持续按下鼠标1时，调节按钮值的变化量随时间不断增加；按住鼠标的时间越长，每次调用函数时对调节按钮值产生的变化就越大。

`gtk_spin_button_new()` 的第三个参数 `digits` 定义了调节按钮值在小数点右侧显示的位数。该参数的接受值范围为 `[0, 5]`。

## 配置调节按钮小部件

当您使用 `gtk_spin_button_new()` 创建一个新的调节按钮时，它将调用 `gtk_spin_button_configure()` 来通过 `adjustment`、`climb_rate` 配置调节按钮。您也可以调用 `gtk_spin_button_configure()` 来更改调节按钮的属性。函数原型如下：

```
void
gtk_spin_button_configure(GtkSpinButton *spin_button,
GtkAdjustment *adjustment, gfloat climb_rate, guint digits)
```

第一个参数 `spin_button` 是要配置的 `GtkSpinButton` 实例。`adjustment`、`climb_rate` 和 `digits` 参数如 `gtk_spin_button_new()` 所述。

## 设置和获取调整对象

接下来两个函数允许应用程序设置或获取调节按钮的调整对象。要设置调整对象，调用 `gtk_spin_button_set_adjustment()`：

```
void
gtk_spin_button_set_adjustment(GtkSpinButton *spin_button,
GtkAdjustment *adjustment);
```

参数 `spin_button` 是调节按钮部件，而调整是一个对象。要获取调整对象，调用 `gtk_spin_button_get_adjustment()`：

```
GtkAdjustment *
gtk_spin_button_get_adjustment(GtkSpinButton *spin_button);
```

返回值为 `GtkAdjustment` 对象。如果您在创建 `gtk_spin_button_new()` 时为调整对象指定了 `NULL`，并且需要设置由代创建的调整对象的属性，可以使用 `GtkAdjustment` 提供的 API（见第 13 章）。

## 设置调节按钮显示的位数

您也可以通过调用 `gtk_spin_button_set_digits()` 来设置（无法获取）调节按钮显示的有效位数：

```
void
gtk_spin_button_set_digits(GtkSpinButton *spin_button, guint digits);
```
