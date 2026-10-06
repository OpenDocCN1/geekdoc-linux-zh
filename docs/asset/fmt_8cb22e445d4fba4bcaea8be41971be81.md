
为指定的 `GtkToggleButton` 实例生成一个 `toggled` 信号：

```
void
gtk_toggle_button_toggled(GtkToggleButton *toggle_button);
```

![](img/b9af04aaed46302cb075052312fcd667_214_0.png)

### 类描述

`GtkToggleButton` 与 `GtkButton` 密切相关，因此它是 `GtkButton` 的子类也并不令人意外。作为一个子类，`GtkToggleButton` 的实例可以使用 `GtkToggleButton` 支持的所有功能。这包括 `GtkButton` 的 API、信号以及其参数。

例如，先前的 `SetButtonLabel()` 也可以用于更改切换按钮小部件的标签文本。这是因为由 `GtkButton` 定义的 `GtkButton::label` 参数适用于任何派生自 `GtkButton` 的类，包括 `GtkToggleButton`。

`GtkButton` 和 `GtkToggleButton` 的主要区别在于应用程序如何使用这些类的实例。你使用 `GtkButton` 实例来提供一个在点击时执行操作的控制控件，而你使用 `GtkToggleButton` 实例来表示一种状态，例如，开启或关闭影响激活或非激活。切换按钮在被点击时也可能执行操作；这取决于应用程序的逻辑。

以下来自流行的 `Gtk+` IRC `X-Chat` 的截图说明了两种按钮的使用。`GtkButton` 实例包括右下角的按钮，标记为 `Op`、`Ban` 等。当按下时，这些按钮会执行操作。注：此处原文描述较乱，已逻辑翻译

![](img/b9af04aaed46302cb075052312fcd667_215_0.png)

图 14 `X-Chat`

`GtkToggleButton` 在按钮点击时会改变外观，并在释放时再次改变，以表示正在激活。用户释放按钮后，恢复到视觉状态。图 14 右角标记为 `"T"`、`"S"`、`"L"` 的按钮是 `GtkToggleButton` 的实例。这些按钮显示状态。标记为 `"N"` 的激活或非激活。`GtkToggleButton` 实例的默认状态是非激活，在用户第一次点击时激活，在第二次点击时变为非激活。

`GtkToggleButton` 允许随时更改按钮的状态。`X-Chat` 如下使用此功能：用户可以点击切换按钮以触发关联的操作。如果操作成功，按钮将保持在激活状态，以表示按钮的模式当前激活。如果无法执行操作，按钮将恢复非激活状态。这种逻辑由应用程序控制，而不是切换按钮。

## 信号

当用户点击切换按钮时，小部件会生成 `toggled` 信号，通知应用程序小部件的状态发生了变化。切换信号可以如下所示注册：

```
gtk_signal_connect (GTK_OBJECT(my_toggle_button), "toggled",
GTK_SIGNAL_FUNC(toggled), NULL);
```

`toggled` 信号函数的原型如下：

```
void
toggled_signal_function(GtkWidget *toggle_button, gpointer arg)
```

本章稍后会有关于此函数的更多内容。

## 创建切换按钮

现在我们理解了如何使用 `GtkToggleButton` 实例，让我们看看 `GtkToggleButton` 类提供的 API。创建一个不带标签的 `GtkToggleButton` 实例，应用程序可以调用 `gtk_toggle_button_new()`：

```
GtkWidget *
gtk_toggle_button_new(void);
```

这类似于 `GtkButton` 类中的 `gtk_toggle_button_new()`。你可以通过设置小部件标签参数在创建后添加或更改切换按钮的标签。创建一个带有标签的 `GtkToggleButton` 实例，应用程序可以调用 `gtk_toggle_button_new_with_label()`：

```
GtkWidget *
gtk_toggle_button_new_with_label(const gchar *label);
```

### 获取和设置切换按钮的状态

用户应该控制切换按钮的状态。由于切换按钮的外观和作用类似于推送按钮，用户倾向于点击它，这应该是视觉状态变化的催化剂。然而，有时应用程序可能控制按钮的状态。例如将按钮的初始状态反转为激活状态。之前说明了用户由于无法处理关联的操作引起的变化。要更改切换按钮的状态，应用程序可以调用 `gtk_toggle_button_set_active()`：

```
void
gtk_toggle_button_set_active(GtkToggleButton *toggle_button,
gboolean is_active);
```

如果 `is_active` 为 `TRUE`，小部件的状态将改变，使按钮采用激活状态相关的外观。如果 `is_active` 为 `FALSE`，按钮被设置为非激活状态的外观。如果状态由于此调用而变化，`Gtk+` 会模拟对切换按钮的点击，这意味着为切换按钮注册的任何信号函数将被调用。同样，还会注册切换信号，因此如果应用程序为此小部件实例注册了切换信号，那么它将被调用。

```
gboolean
gtk_toggle_button_get_active(GtkToggleButton *toggle_button);
```

参数 `toggle_button` 是 `GtkToggleButton` 的实例或我们稍后看到的 `GtkToggleButton` 的子类。如果返回 `TRUE`，按钮处于激活状态；否则返回 `FALSE`。

我预见到应用程序使用上述调用的两种情况。第一种是在 `toggled` 信号函数内部。在这里，你想知道小部件的当前状态。因此，典型的信号函数结构如下：

```
void
toggled_signal_function(GtkWidget *w, gpointer arg)
{
  gboolean state;

  state = gtk_toggle_button_get_active(
    GTK_TOGGLE_BUTTON( w ));
  if ( state == TRUE )
    // 在处执行某些操作
  else
    // 在处执行其他操作
}
```

调用 `gtk_toggle_button_get_active()` 的另一个重要时刻是在与关闭对话框相关的信号函数中，或者在保存处理器中。在这里，你的代码将检查切换按钮的状态作为保存操作的一部分。让我们来看一个具体的例子。假设有一个弹框，包含三个标记为苹果、橙子和梨的按钮。在这些切换按钮下方是标记为打印 `Print` 和退出 `Quit` 的按钮。用户点击一个或多个切换按钮来指定，例如用户经常吃的水果。如果用户点击退出按钮，对话框将关闭，什么都不留下。如果用户点击打印按钮，与打印按钮关联的点击函数将查询切换按钮的状态并打印出

输出到标准输出。为了简单起见，这里假设切换按钮控件存储在全局变量中。

```
void
print_clicked_function (GtkWidget *w
```

```
gboolean apples, oranges, pears;
  apples = gtk_toggle_button_get_active(
  GTK_TOGGLE_BUTTON(apples_toggle_button_widget) );
  oranges = gtk_toggle_button_get_active(
  GTK_TOGGLE_BUTTON(oranges_toggle_button_widget) );
  pears = gtk_toggle_button_get_active(
  GTK_TOGGLE_BUTTON(pears_toggle_button_widget) );
```

```
printf("%s apples, %s oranges, and %s pears regularly\n",
  apples == TRUE ? "eat" : "do not eat" ),
  oranges == TRUE ? "eat" : "do not eat" ),
  pears == TRUE ? "eat" : "do not eat" );
}
```

### 其他函数

您的应用程序可以使用为 `GtkToggleButton` 实例注册的切换信号，通过调用 `gtk_toggle_button_toggled()` 随时进行调用。

```
void
gtk_toggle_button_toggled (GtkToggleButton *button);
```

此调用不会改变切换按钮控件的视觉状态。

我将描述的 `GtkToggleButton` 暴露的最后一个函数是 `gtk_toggle_button_set_mode()`。

```
void
gtk_toggle_button_set_mode (GtkToggleButton *button,
 gboolean draw_indicator);
```

该函数接受两个参数：一个 `GtkToggleButton` 控件实例和一个布尔参数。该布尔参数控制切换按钮控件的可见性。如果设置为 `FALSE`，则切换按钮将从视图中隐藏。如果设置为 `TRUE`，则切换按钮将变为可见。实际上，传递 `TRUE` 相当于对切换按钮调用了 `gtk_widget_show_all()`，而传递 `FALSE` 则产生相反的效果，导致切换按钮被隐藏。

## GtkCheckButton

### 类名

`GtkCheckButton`

### 父类名

`GtkToggleButton`

## 宏

- 控件类型宏：`GTK_TYPE_CHECK_BUTTON`
- 对象到控件的转换宏：`GTK_CHECK_BUTTON(obj)`
- 控件类型检查宏：`GTK_IS_CHECK_BUTTON(obj)`

## 应用级 API 摘要

在运行时获取常量 `GTK_TYPE_CHECK_BUTTON`：

```
GtkType
gtk_check_button_get_type(void);
```

创建一个不带标签的 `GtkCheckButton` 新实例：

```
GtkWidget *
gtk_check_button_new(void);
```

创建一个带有指定标签的 `GtkCheckButton` 新实例：

```
GtkWidget *
gtk_check_button_new_with_label(const gchar *label);
```

### 类描述

`GtkButton` 层次结构中的下一个控件是 `GtkCheckButton`。该类继承自 `GtkToggleButton`，这意味着它有完全权限访问 `GtkToggleButton` 提供的函数和属性，以及我们之前看到的 `GtkButton` 提供的属性 `GtkButton` 是 `GtkToggleButton` 的父类。之前对 `GtkToggleButton` 的的所有描述都适用于此类；；当调用函数或宏时，只需传递一个 `GtkCheckButton` 实例而非 `GtkToggleButton` 实例即可。

# 第 5 章 • 标签与按钮

`GtkCheckButton` 和 `GtkToggleButton` 唯一的真实区别在于控件的渲染方式 见图 5.10。控件的敏感部分 即接收鼠标事件的区域由包含按钮及其标签的矩形区域组成。

`GtkCheckButton` 的 API 仅包含实例创建函数。再次，实际功能由 `GtkToggleButton` 及其父类 `GtkButton` 提供，这些类结合了供 `GtkCheckButton` 可用的功能。

## 创建复选按钮

要创建一个不带标签的 `GtkCheckButton` 实例，请调用 `gtk_check_button_new()`：

```
GtkWidget *
gtk_check_button_new(void);
```

要创建一个带有标签的 `GtkCheckButton` 实例，请调用 `gtk_check_button_new_label()`：

```
GtkWidget *
gtk_check_button_new_label(const gchar *label);
```

关于 `gtk_check_button_new()` 和 `gtk_check_button_new_label()` 的详细信息，请分别参考之前提供的 `gtk_toggle_button_new()` 和 `gtk_toggle_button_new_label()` 的信息。

现在让我们关注 `GtkRadioButton`，它是 `GtkButton` 层次结构中剩余的控件类。

## GtkRadioButton

### 类名

`GtkRadioButton`

### 父类名

`GtkCheckButton`

## 宏

- 控件类型宏：`GTK_TYPE_RADIO_BUTTON`
- 对象到控件的转换宏：`GTK_RADIO_BUTTON(obj)`
- 控件类型检查宏：`GTK_IS_RADIO_BUTTON(obj)`

## 支持参数

前缀：`GtkRadioButton::`

表 5.8 `GtkRadioButton` 参数

| 名称 | 类型 | 权限 |
| --- | --- | --- |
| group | `GTK_TYPE_RADIO_BUTTON` | `GTK_ARG_WRITABLE` |

## 应用级 API 摘要

在运行时获取 `GTK_TYPE_RADIO_BUTTON` 常量：

```
GtkType
gtk_radio_button_get_type(void);
```

创建一个不带标签的 `GtkRadioButton` 实例，可选地添加到组中：

```
GtkWidget *
gtk_radio_button_new(GtkList *group);
```

创建一个带有指定标签的 `GtkRadioButton` 实例，并可选地添加到组中：

```
GtkWidget *
gtk_radio_button_new_with_label(GtkList *group, const gchar *label);
```

与 `gtk_radio_button_new` 相同，传递一个控件以确定单选组：

```
GtkWidget *
gtk_radio_button_new_from_widget(GtkList *group);
```

与 `gtk_radio_button_new_with_label` 相同，传递一个控件以确定单选组：

```
GtkWidget *
gtk_radio_button_new_with_label_from_widget(GtkList *group, const gchar *label);
```

获取指定的 `GtkRadioButton` 实例所属的单选组：

```
GtkList
gtk_radio_button_group(GtkRadioButton *radio_button);
```

将 `GtkRadioButton` 实例与指定的按钮组关联：

```
void
gtk_radio_button_set_group(GtkRadioButton *radio_button, GtkList *group);
```

### 类描述

`GtkRadioButton` 是继承自 `GtkButton` 的控件类中最功能强大且专门的类。`GtkButton` 实例与 `GtkToggleButton` 实例在外观和功能上有所不同。`GtkCheckButton` 的方形按钮是菱形的。而且，虽然 `GtkButton` 允许多选，你将使用一组 `GtkRadioButton` 来实现多选一。然后你会使用 `GtkButton` 来实现一个允许用户 例如回答他们出生地的用户界面。

为了实现多选一，`GtkRadioButton` 要求将相关的 `GtkRadioButton` 实例分组。这样做使 `GtkRadioButton` 能够确保在任何时刻组内只有一个按钮被选中。当组中的任何单选按钮被用户选中 或通过应用程序调用 `gtk_toggle_button_set_active()` 时，`GtkRadioButton` 将确保其他按钮取消选中。

# 创建单选按钮控件

创建 `GtkRadioButton` 实例与创建 `GtkButton` 实例略有不同。`gtk_radio_button_new()` 和 `gtk_radio_button_new_with_label()` 分别创建带标签和不带标签的单选按钮。

这两个函数都有额外的参数 `group`。在创建单选按钮组的第一个单选按钮时，`group` 参数应为 `(GtkList *) NULL`。在创建同一组的后续单选按钮时，使用属于该组的任何控件的控件 ID 来指定要将新单选按钮添加到哪个组。以下代码和讨论应该说明这一点：

```
GtkWidget *apples, *oranges, *pears;
apples = gtk_radio_button_new_with_label (NULL, "Apples");
oranges = gtk_radio_button_new_with_label (
gtk_radio_button_group (GTK_RADIO_BUTTON (apples)),
"Oranges");
pears = gtk_radio_button_new_with_label (
gtk_radio_button_group (GTK_RADIO_BUTTON (oranges)),
"Pears");
```

在这里，标记为 `"Apples"` 的第一个按钮的 `group` 参数设置为 `NULL`，因为正在定义该组。标记为 `"Oranges"` 的按钮的 `group` 参数设置为 `Apples` 所属的单选组，而标记为 `"Pears"` 的按钮的 `group` 参数设置为 `Oranges` 按钮所属的组。或者，你也可以如下设置 `Pears` 按钮组：

```
pears = gtk_radio_button_new_with_label (
    gtk_radio_button_group (GTK_RADIO_BUTTON (apples)),
    "Pears");
```
