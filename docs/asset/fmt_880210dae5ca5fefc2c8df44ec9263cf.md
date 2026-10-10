
创建一个新的 `GtkText` 实例，可选地设置垂直和/或水平调整对象：

```c
GtkWidget *
gtk_text_new(GtkAdjustment *hadj, GtkAdjustment *vadj);
```

切换文本部件的可编辑属性：

```c
void
gtk_text_set_editable(GtkText *text, gboolean editable);
```

切换文本部件的自动换行属性：

```c
void
gtk_text_set_word_wrap(GtkText *text, int word_wrap);
```

切换文本部件的换换行属性：

```c
void
gtk_text_set_line_wrap(GtkText *text, int line_wrap);
```

## 应用级 API 摘要（续）

设置文本部件的水平和垂直调整对象：

```c
void
gtk_text_set_adjustments (GtkText *text, GtkAdjustment *hadj,
GtkAdjustment *vadj);
```

设置文本插入/删除点：

```c
void
gtk_text_set_point (GtkText *text, guint index);
```

查询文本插入/删除点：

```c
guint
gtk_text_get_point (GtkText *text);
```

获取当前由文本部件管理的文本长度：

```c
guint
gtk_text_get_length (GtkText *text);
```

冻结小部件（在修改文本前调用）：

```c
void
gtk_text_freeze (GtkText *text);
```

解冻小部件（撤销之前的对 `gtk_text_freeze()` 调用）：

```c
void
gtk_text_thaw (GtkText *text);
```

相对于插入/删除点插入文本：

```c
void
gtk_text_insert (GtkText *text, GdkFont *font, GdkColor *fore,
GdkColor *back, const char *chars, guint nchars);
```

在插入/删除点之前向前删除 n 个字符：

```c
guint
gtk_text_backward_delete (GtkText *text, guint nchars);
```

在插入/删除点之后删除 n 个字符：

```c
guint
gtk_text_forward_delete (GtkText *text, guint nchars);
```

## 类描述

与 `GtkLabel`（见第 5 章“标签与按钮”）一样，`GtkText` 主要设计用于显示文本。然而，`GtkLabel` 和 `GtkText` 小部件类之间存在显著差异。具体而言，你使用 `GtkLabel` 实例在对话框、警告以及消息对话框中显示小型对象。相比之下，`GtkText` 设计用于显示大得多的文本（例如文件内容或编译器的文本输出）。

`GtkText` 允许应用程序控制其管理的文本的以下方面：

- 它的样式（例如字体、背景色等）
- 用户是否可以编辑文本
- 是否启用了行换行或单词换行（两者均可）

最后两项是全局的，这意味着它们适用于整个文本部件及其管理的所有文本。然而，文本样式可以在添加文本时应用于由文本部件管理的文本部分。

## 滚动文本

在某些情况下，`GtkText` 管理的文本量足够小，可以在 `GtkText` 创建的窗口中完全显示。然而，如果文本大于窗口，则必须使用滚动条。`GtkText` 提供了一种处理此问题的机制，但它并不提供滚动条本身。相反，应用程序需要使用 `GrolledWindow`。

在某些情况下，`GtkText` 管理的文本量足够小，可以在 `GtkText` 创建的窗口中完全显示。然而，如果文本大于窗口，则必须使用滚动条。`GtkText` 提供了一种处理此问题的机制，但它并不提供滚动条本身。相反，应用程序需要使用 `GtkrolledWindow`。

## 创建文本部件

要创建 `GtkText` 实例，调用 `gtk_text_new`：

```c
GtkWidget *
gtk_text_new(GtkAdjustment *hadj, GtkAdjustment *vadj);
```

`gtk_text_new` 两个两个参数：`hadj` 是水平调整，`vadj` 是可选垂直调整。如果你不使用滚动，对 `hadj` 和 `vadj` 传递 `NULL`。

## 修改调整对象

通常在创建文本部件时指定调整对象。你也可以在文本部件创建后设置它们。例如，要设置水平垂直调整对象，可以调用 `gtk_text_set_adjustments`：

```c
void
gtk_text_set_adjustments (GtkText *text, GtkAdjustment *hadj,
GtkAdjustment *vadj);
```

设置 `hadj` 和 `vadj` 的指南与 `gtk_text_new` 相同。

## 使文本部件可编辑

一旦创建了文本部件，就可以可选地更改某些默认属性。例如，要切换文本部件的可编辑属性，可以调用 `gtk_text_set_editable`：

```c
void
gtk_text_set_editable(GtkText *text, gboolean editable);
```

参数是你想设置可编辑属性的文本部件，`editable` 是控制用户更改文本的布尔值。如果 `editable` 设置为 `FALSE`，用户无法设置插入/删除点，也无法使用文本内容。然而，应用程序根据需要调用 `GtkText` API 进行插入/删除点、插入文本和删除文本。默认情况下，文本部件是不可编辑的，因此如果你想让用户编辑文本部件的内容，必须调用 `gtk_text_set_editable` 并 `editable` 参数设置为 `TRUE`。

## 单词换行

你还可以切换文本部件的单词换行和换行属性。默认情况下，单词换行是禁用的，而换行是启用的。如果启用了换行，文本将根据字符边界自动换行，而不考虑行的内容。换行后的文档可能包含被断开在不同行的单词。如果这是一个问题，你可以启用单词换行。启用单词换行后，需要换行的行将在空白边界处换行。这是一个相当简单的单词换行算法；`GtkText` 有可能在未来版本实现更复杂的单词换行算法（例如在连字符或音节边界处断开）。但在 `Gtk` 1.2 中，空格是用于区分单词的定符。

要切换文本部件的单词换行属性（默认为 `FALSE`），可以调用 `gtk_text_set_word_wrap`：

```c
void
gtk_text_set_word_wrap(GtkText *text, int word_wrap);
```

参数是 `GtkText` 的实例，`word_wrap` 是一个整数。要启用单词换行，将 `word_wrap` 设置为 `TRUE`；否则，将其设置为 `FALSE`。

同样，为了启用或禁用换行属性（默认为 `TRUE`），你可以调用 `gtk_text_set_line_wrap()`。

```
void
gtk_text_set_line_wrap(GtkText *text, gint line_wrap);
```

参数 `text` 是 `GtkText` 的一个实例，像常一样，`line_wrap` 是一个整数，应设置为 `TRUE` 以启用换行，或设置为 `FALSE` 以禁用。

## 文本控件缓冲区操作

`GtkText` 提供了几个函数，所有应用程序都使用它们向控件管理的文本中添加或删除内容。这本质上是一个字符字符串，结构类似于 C 语言字符串（例如 `char` 类型的变量）。字符串中的第一个字符位于偏移量 0，最后一个字符位于偏移量 n-1，其中字符串的字符数等于 n。在本节的剩余部分中，我将此称为“缓冲区”（buffer）。

**插入点。** 在从缓冲区中添加或删除字符之前，你必须首先确定要在缓冲区的哪个位置执行插入或删除操作。该位置称为“点”（point），是 [0, n] 范围内的一个索引，其中 n 是缓冲区中当前的字符数。当创建文本时，点被设置为 0。随着文本被添加到缓冲区，点会根据添加的字符数而增加。正因如此，只要你向缓冲区反向追加文本，就不需要在每次插入前都设置点：如，当文本从缓冲区中移除时，点会根据删除的字符数而递减，使其指向缓冲区的当前末尾。我将在“插入和删除文本”章节中详细讨论从缓冲区中插入和删除文本。

**设置和获取插入点。** 如果你想从缓冲区末尾的其他点插入或删除文本，或者你想将点重置为缓冲区末尾，你必须调用 `gtk_text_set_point()` 函数在执行插入或删除之前指定点。`gtk_text_set_point()` 的原型如下：

```
void
gtk_text_set_point(GtkText *text, guint index);
```

参数 `text` 是 `GtkText` 的一个实例，`index` 指定 [0, n] 范围内的点，其中 n 是缓冲区中的字符数。

**获取文本缓冲区的长度。** 通过调用 `gtk_text_get_length()` 获取缓冲区的长度。
