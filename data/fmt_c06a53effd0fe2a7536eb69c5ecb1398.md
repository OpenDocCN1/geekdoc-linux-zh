
在 19 行，我注册了 `clicked` 信号，使其调用之前讨论过的 GtkTipsQuery 函数 `tips_query_start()`：

```
049 gtk_signal_connect_object(GTK_OBJECT(button), "clicked",
050     GTK_SIGNAL_FUNC(tips_query_start),
051     GTK_OBJECT(tips));
053 gtk_widget_show(dialog_window)
054 gtk_main();
055 }
```

### 退出查询模式

正如本节开头提到的，一旦用户点击任何小部件，无论该小部件是否关联了提示，Gtk+ 自动退出查询模式。如果需要，可以通过调用 `gtk_tips_stop_query()` 并将其传递给小部件来让应用程序退出查询模式：

```
void
gtk_tips_stop_query(GtkTipsQuery *tips_query);
```

正如我们看到的，导致小部件进入查询模式的按钮、菜单项或其他控件在点击时会导致小部件退出查询模式并恢复正常操作。如果你愿意，可以更改点击时带应用程序退出查询模式的小部件。可以在进入查询模式之前的任何时候将小部件传递给 `gtk_tips_set_caller()` 实现：

```
void
gtk_tips_set_caller(GtkTipsQuery *tips_query,
GtkWidget *caller);
```

### 设置无提示小部件的文本

最后一个函数每当用户在查询模式下悬停在一个没有注册提示的小部件上时，就会设置 tips_query 接口显示的文本，就像应用程序不在查询模式时提示查询显示的那样。如果提示查询小部件在 UI 中可见（即它已实现但未映射），则该函数无效。要更改这些字符串，请调用 `gtk_tips_set_labels()`：

```
void
gtk_tips_set_labels(GtkTipsQuery *tips_query,
const gchar *label_inactive, const gchar *label_no_tip);
```

# GtkCombo

类名

`GtkCombo`

父类名

`GtkHBox`

## 宏

小部件类型宏：`GTK_TYPE_COMBO`

对象到小部件转换宏：`GTK_COMBO(obj)`

小部件类型检查宏：`GTK_IS_COMBO(obj)`

# 应用程序级摘要

运行时获取常量 `GTK_TYPE_COMBO`：

```
guint
gtk_combo_get_type(void);
```

创建一个 `GtkCombo` 实例：

+ * `GtkWidget`

* `gtk_combo_new(void);`

强制字段字段匹配弹出列表项：

```
void
gtk_combo_set_value_in_list(GtkCombo *combo, int val,
int ok_if_empty);
```

启用/禁用使用方向键导航弹出列表：

```
void
gtk_combo_set_arrows(GtkCombo *combo, int val);
```

# 应用程序级 API 摘要继续

用于导航弹出列表的方向键换行控制：

```
void
gtk_combo_set_arrows_always(GtkCombo *combo, gint val);
```

设置弹出列表项的大小敏感性：

```
void
gtk_combo_set_case_sensitive(GtkCombo *combo, gint val);
```

设置非标签弹出列表项的字段文本：

```
void
gtk_combo_set_item_string(GtkCombo *combo, GtkItem *item,
    const gchar * item_value);
```

设置弹出列表项：

```
void
gtk_combo_set_popdown_strings(GtkCombo *combo, GList * strings);
```

禁用字段触发的激活 信号：

```
void
gtk_combo_disable_activate(GtkCombo *combo);
```

## 类描述

`GtkCombo` 实现了图 15.6 和 15.7 所示的组合小部件。组合小部件是弹出列表小部件和字段小部件的组合。组合小部件的目标是从字段获取文本字符串。字段的值是用户输入到字段中的文本，或者是用户从弹出列表中选择的字符串。应用程序可以强制用户从列表中选择一个项，但默认配置允许用户在字段中输入任意文本。

![](img/1441ee0eb9a357efc9aff107f92bf0c0_806_0.png)

图 15.6 组合小部件

# GtkCombo

![](img/1441ee0eb9a357efc9aff107f92bf0c0_807_0.png)

**图 15.7** 组合框下拉菜单

对于大多数应用程序，创建和使用组合框（combo widget）是一件简单的事情，包含以下步骤：

- 1. 使用 `gtk_combo_new()` 创建一个组合框。
- 2. 使用 `gtk_combo_set_popdown_strings()` 向组合框下拉列表添加字符串。
- 3. 通过调用 `gtk_entry_set_text()` 设置组合框输入字段的默认值。
- 4. 完成编辑后，获取输入字段的值。

# 创建组合框控件

让我们来看之前提到的两个 `GtkCombo` 函数以及一个示例应用程序，该程序使用了上述步骤在窗口中创建一个简单的组合框，并在用户按下 OK 按钮时获取其值。代码还说明了如何通过用户输入向下拉列表添加字符串。

要创建组合框，调用 `gtk_combo_new()`：

```
GtkWidget *
gtk_combo_new(void);
```

与所有 `*new()` 函数一样，该函数返回一个 `GtkWidget` 实例。对于需要 `GtkCombo` 实例的 `GtkCombo` 函数，只需使用 `GTK_COMBO` 宏将返回值强制转换为组合框实例即可。

# 设置组合框内容

要向组合框下拉列表添加字符串，调用 `gtk_combo_set_popdown_strings()`：

```
void
gtk_combo_set_popdown_strings(GtkCombo *combo, GList *strings);
```

第一个参数 `combo` 是 `GtkCombo` 实例，第二个参数是将在组合框下拉列表中显示的字符串列表。要创建字符串列表，请使用 `Glib_list` 函数（参见 `glib.h`）。在这些函数中，最易用的是 `g_list_append()`；示例请参见随后的代码。你可以随时调用 `gtk_combo_set_popdown_strings()` 来更改组合框下拉列表显示的字符串列表。

## 示例

此示例程序（见下文列表和图 15.6、图 15.7）说明了以下内容：

- 如何创建一个 `GtkCombo` 控件实例
- 如何设置组合框下拉列表显示的字符串列表
- 如何获取用户选择或输入的值
- 如何更改（添加）组合框下拉列表显示的字符串列表。

# 列表 15.4 GtkCombo 示例
