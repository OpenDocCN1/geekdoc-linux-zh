
其中 `tags` 是一个标签表。如果你希望创建一个表，可以设置为 `NULL`。你可以通过 `buffer-tag` 属性访问该表。

这些函数操作 `GtkTextBuffer` 的内容：

- `void gtk_text_buffer_set_text(GtkTextBuffer *buffer, const char *text, gint length)`
替换缓冲区的内容为 UTF-8 字符串。`length` 值应该是文本的字节长度，如果文本是 NULL 终止字符串，则为 `-1`。
- `void gtk_text_buffer_insert(GtkTextBuffer *buffer, GtkIter *iter, const char *text, gint length)`
与前面的函数类似，但在 `iter` 处插入而不是替换缓冲区的内容。此函数会导致 `insert-text` 信号发射，默认处理程序执行实际工作

# GNOME 2 开发者官方指南

插入文本。此外，处理程序会将 `iter` 设置为新文本之后的位置。
- `gboolean gtk_text_buffer_insert_interactive(GtkBuffer *buffer, GtkTextIter *iter, const gchar *text, int length, gboolean editable)`

与前面的函数一样，它拒绝在标记为只读的位置插入文本。如果 `editable` 为 `TRUE`，该函数会在未被显式标记为只读的位置插入文本。

注意：在大多数情况下，你可以通过调用 `gtk_text_view_get_editable(GtkView *view)` 查看缓冲区当前的状态来确定是否可编辑。

- `void gtk_text_buffer_insert_at_cursor(GtkTextBuffer *buffer, const gchar *text, int length)`

类似于 `gtk_text_buffer_insert(text)`，但将新文本插入到光标位置。
- `gboolean gtk_text_buffer_insert_interactive_at_cursor(GtkTextBuffer *buffer, const gchar *text, int length, gboolean editable)`

类似于 `gtk_text_buffer_insert_interactive_at_cursor()`，但在光标位置插入。
- `void gtk_text_buffer_range(GtkTextBuffer *buffer, const gchar *text, GtkTextIter *iter, GtkTextIter *end)`

拷贝缓冲区中 `begin` 到 `end` 之间的文本。如果 `begin` 和 `end` 不属于该缓冲区，则该缓冲区必须与缓冲区共享一个 `tag` 缓冲区。`insert-insert` 和 `apply-tag` 信号会完成此函数的工作。
- `gboolean gtk_text_buffer_insert_range_interactive(GtkTextBuffer *buffer, const gchar *text, GtkTextIter *iter, GtkTextIter *begin, GtkTextIter *end, gboolean editable)`

与前面的函数一样，反映了其他 `_interactive` 函数的行为。
- `void gtk_text_buffer_delete(GtkTextBuffer *buffer, GtkTextIter *begin, GtkTextIter *end)`

删除缓冲区中 `begin` 到 `end` 之间的文本。与插入操作一样，有一个信号会完成此函数的工作：`delete-range`。
- `gboolean gtk_text_buffer_delete_interactive(GtkTextBuffer *buffer, GtkTextIter *begin, GtkTextIter *end, gboolean editable)`

与前面的函数一样，但仅遵循其他 `_interactive` 函数的范围限制规则。
- `gboolean gtk_text_buffer_delete_selection(GtkTextBuffer *buffer, gboolean interactive, gboolean editable)`

从缓冲区中移除选择内容；即删除从插入标记到选择边界标记之间的所有文本。如果 `editable` 为 `true`，此函数的行为类似于之前的交互式函数，对于当前标记为只读但现在变为可写的文本会查询 `editable` 状态。
- `void gtk_text_buffer_set_modified(GtkTextBuffer *buffer, gboolean modified)`

更改缓冲区的修改状态。将 `modified` 设置为 `TRUE` 通常意味着缓冲区自上次保存以来发生了变化；`FALSE` 则表示自上次保存以来没有发生任何变化。GTK+ 将在下一次修改时将修改状态设置为 `TRUE`。
- `gboolean gtk_text_buffer_get_modified(GtkTextBuffer *buffer)`

返回缓冲区的修改状态。

注意

### 3.12.1 文本缓冲区

# GNOME 开发者官方指南

上述两个函数可以帮助你在编辑器中实现文件保存功能。每当用户保存文件时，你的应用程序都可以将修改状态设置为 `FALSE`。此外，你可以使用该状态来触发自动保存功能。

- `void gtk_text_buffer_begin_user_action(GtkTextBuffer *buffer)`

发出用户操作开始的信号。

- `gtk_text_buffer_end_user_action(GtkTextBuffer *buffer)`

发出用户操作结束的信号。

用户操作触发 `begin-user-action` 和 `end-user-action` 信号。你可以嵌套这些信号。用户操作帮助你建立撤销 `Undo` 功能的历史记录。

之前的 `_interactive` 函数会调用用户操作函数。因此，如果你坚持使用 `_interactive` 函数，则不需要手动调用用户操作函数。

这些函数从文本缓冲区检索数据：

- `gchar *gtk_text_buffer_get_text(GtkTextBuffer *buffer, const GtkTextIter *begin, const GtkTextIter *end, gboolean hidden)`

返回缓冲区中 `begin` 到 `end` 之间的文本。如果 `hidden` 为 `TRUE`，文本将包含任何标记为隐藏的字符。与后续讨论的 `_get_slice()` 函数不同，此函数不会用特殊字符替换嵌入的图像和锚点。因此，结果文本中的索引和偏移量可能与缓冲区中的不一致。

- `gchar *gtk_text_buffer_get_slice(GtkTextBuffer *buffer, const GtkTextIter *begin, const GtkTextIter *end, gboolean hidden)`

与前面的函数类似，它用特殊的 Unicode 字符 `0xFFFC` 替换嵌入的图像和锚点。切片中的索引和偏移量反映了原始缓冲区。

- `gunchar gtk_text_iter_get_char_count(GtkTextIter *iter)`

返回 `iter` 处的字符；如前面函数所述作为图像和锚点的替代方案。如果 `iter` 位于缓冲区的末尾，此函数返回 `0`，适用于在循环中使用。

- `void gtk_text_buffer_get_line_count(GtkTextBuffer *buffer)`
- `void gtk_text_buffer_get_char_count(GtkTextBuffer *buffer)`

返回缓冲区中的字符数。而非字节数。与前面的函数一样，这是一个高效的函数。

### 迭代器 Iterators

`GtkTextBuffer` 结构指示文本缓冲区中的位置，因此在 `GtkTextBuffer` API 中起着核心作用。注意：处理迭代器的函数会移动迭代器；因此，当你在本章看到 `iter` 时，可能会使用类似 `&iter` 的参数。

### 3.12.1 文本缓冲区

# GNOME 2 开发者官方指南

第 3.12 节的示例展示了这一点。你可以通过多种方式获取迭代器。以下函数：

- `void gtk_text_buffer_iter_at_line(GtkTextBuffer *buffer, GtkTextIter *iter, int line_number)`

将其设置为缓冲区中 `line_number` 行的开始。
- `void gtk_text_buffer_iter_at_offset(GtkTextBuffer *buffer, GtkTextIter *iter, int offset)`

将其设置为缓冲区的 `offset` 处。
- `void gtk_text_buffer_iter_at_line_offset(GtkTextBuffer *buffer, GtkTextIter *iter, int line_number, int offset)`

将其设置为缓冲区中 `line_number` 行的 `offset` 处。
- `void gtk_text_buffer_iter_at_line_index(GtkTextBuffer *buffer, GtkTextIter *iter, int line_number, int index)`

类似于前面的函数，但 `index` 指明 `line_number` 的字节数。
- `void gtk_text_buffer_iter_get_start(GtkTextBuffer *buffer, GtkTextIter *iter)`

将其设置为缓冲区的开始。
- `void gtk_text_buffer_iter_get_end(GtkTextBuffer *buffer, GtkTextIter *iter)`

将其设置为缓冲区的结束。
- `void gtk_text_buffer_iter_get_bounds(GtkTextBuffer *buffer, GtkTextIter *begin, GtkTextIter *end)`

分别将 `begin` 和 `end` 设置为缓冲区的开始和结束。
- `gboolean gtk_text_buffer_iter_get_selection_bounds(GtkTextBuffer *buffer, GtkTextIter *begin, GtkTextIter *end)`

如果缓冲区中有当前选择，将 `begin` 和 `end` 设置为选择范围；否则返回 `FALSE` 并两个迭代器设置为光标位置。如果你只关心是否有选择，可以将两个迭代器设置为 `NULL`。这些函数返回关于迭代器的信息：

- `GtkBuffer *gtk_text_iter_get_buffer(GtkTextIter *iter)`

返回 `iter` 所描述的缓冲区。
- `gint gtk_text_iter_get_offset(GtkTextIter *iter)`

返回 `iter` 与缓冲区开始位置之间的字符数。
- `gint gtk_text_iter_get_line(GtkTextIter *iter)`

返回 `iter` 的行号。缓冲区的第一行是 `0`。
- `gint gtk_text_iter_get_line_offset(GtkTextIter *iter)`

返回 `iter` 与其行开始位置之间的字符数。
- `gint gtk_text_iter_get_visible_line_offset(GtkTextIter *iter)`

返回 `iter` 与行可见起始位置之间的字符数。

# 3.1.2 文本缓冲区

与前面的函数一样，仅计算标记为隐藏的字符。
- `gint gtk_text_iter_get_line_index(GtkTextIter *iter)`

返回 `iter` 与行开始位置之间的字节数。
- `gint gtk_text_iter_get_visible_index(GtkTextIter *iter)`

与前面的函数一样，仅计算标记为隐藏的字符的字节数。
- `gint gtk_text_iter_get_chars_in_line(GtkTextIter *iter)`

返回 `iter` 所在行的字符数。
- `gint gtk_text_iter_get_bytes_in_line(GtkTextIter *iter)`

返回 `iter` 所在行的字节数。
- `gboolean gtk_text_iter_get_starts_word(GtkTextIter *iter)`

如果 `iter` 位于单词开头，则返回 `TRUE`。Pango 根据特定语言算法确定单词开头。
- `gboolean gtk_text_iter_ends_word(GtkTextIter *iter)`

如果 `iter` 位于单词结尾，则返回 `TRUE`。
- `gboolean gtk_text_iter_inside_word(GtkTextIter *iter)`

如果 `iter` 位于单词内部，则返回 `TRUE`。
- `gboolean gtk_text_iter_starts_line(GtkTextIter *iter)`

如果 `iter` 位于行首，则返回 `TRUE`。
- `gboolean gtk_text_iter_ends_line(GtkTextIter *iter)`

如果 `iter` 位于行末，则返回 `TRUE`。
- `gboolean gtk_text_iter_starts_sentence(GtkTextIter *iter)`

如果 `iter` 位于句首，则返回 `TRUE`。
- `gboolean gtk_text_iter_inside_sentence(GtkTextIter *iter)`

如果 `iter` 位于句末，则返回 `TRUE`。
- `gboolean gtk_text_iter_is_start(GtkTextIter *iter)`

如果 `iter` 位于缓冲区起始，则返回 `TRUE`。
- `gboolean gtk_text_iter_is_end(GtkTextIter *iter)`

如果 `iter` 位于缓冲区结束，则返回 `TRUE`。
- `gboolean gtk_text_iter_is_cursor_position(GtkTextIter *iter)`

如果 `iter` 位于缓冲区当前的光标位置，则返回 `TRUE`。
- `gboolean gtk_text_iter_can_insert(const GtkTextIter *iter, gboolean default_editable)`

# GNOME 2 开发者官方指南

如果 `iter` 的位置被标记为可读写，则返回 `TRUE`。如果没有此类标记，此函数将返回 `default_editable`。前几页中的所有 *交互式函数* 都会调用此函数来决定它们是否可以向缓冲区中插入内容或从缓冲区中删除内容。

你可以使用这些函数设置迭代器的绝对位置。这些函数假设迭代器已经设置在适当缓冲区内的某个位置：

- `void gtk_text_iter_set_offset(GtkTextIter *iter, int offset)`

将 `iter` 移动到其缓冲区起始处之后的 `_offset_` 个字符处。如果 `offset` 过大，`iter` 将移动到缓冲区的最后一个位置。

- `void gtk_text_iter_set_line(GtkTextIter *iter, int line_number)`

将 `iter` 放置在第 `_number_` 行的行首。缓冲区从第 `0` 行开始。如果该行内容过长，此函数将 `iter` 设置为缓冲区最后行的行首。

- `void gtk_text_iter_set_line_offset(GtkTextIter *iter, int offset)`

将 `iter` 移动到其行起始处之后的 `_offset_` 个字符处。`_offset` 值必须在 `0` 和该行的字符数之间。

- `void gtk_text_iter_set_visible_line_offset(GtkTextIter *iter, int offset)`

与前一个函数类似，但忽略被标记为隐藏的字符。

- `void gtk_text_iter_set_line_index(GtkTextIter *iter, int index)`

- `void gtk_text_iter_set_visible_line_index(GtkTextIter *iter, int index)`

与前一个函数类似，但忽略被标记为隐藏的字符。

此列表中是将迭代器移动到缓冲区内部相对位置的函数。如果按照请求移动迭代器，则它们都返回布尔 `TRUE`。如果你要求其中一个函数将迭代器移动到缓冲区开头或结束之后，迭代器将移动到尽可能到达的位置，且函数返回 `FALSE`。

注意：光标位置是缓冲区中光标可以停留的任何点。这并不一定位于每对相邻字符之间，特别是在那些不使用拉丁字母或希腊字母的语言中。你可以按光标位置或字符移动迭代器；请确保你选择了所需的那一个。

- `gtk_text_iter_forward_cursor_position(GtkTextIter *iter)`

向前移动一个光标位置。

- `gtk_text_iter_backward_cursor_position(GtkTextIter *iter)`

向后移动一个光标位置。

- `gtk_text_iter_forward_cursor_positions(GtkTextIter *iter, int count)`

向前移动 `count` 个光标位置。

- `gtk_text_iter_backward_cursor_positions(GtkTextIter *iter, int count)`

向后移动 `count` 个光标位置。

# 3.1.2 文本缓冲区

- `gboolean gtk_text_iter_forward_char(GtkTextIter *iter)`

将 `iter` 向前移动一个字符。

- `gboolean gtk_text_iter_backward_char(GtkTextIter *iter)`

将 `iter` 向后移动一个字符。

- `gboolean gtk_text_iter_forward_chars(GtkTextIter *iter, gint count)`

将 `iter` 向前移动 `count` 个字符。

- `gboolean gtk_text_iter_backward_chars(GtkTextIter *iter, gint count)`

将 `iter` 向后移动 `count` 个字符。

- `gboolean gtk_text_iter_forward_line(GtkTextIter *iter)`

将 `iter` 移动到下一行的行首。

- `gboolean gtk_text_iter_backward_line(GtkTextIter *iter)`

将 `iter` 移动到上一行的行首。

- `gboolean gtk_text_iter_forward_lines(GtkTextIter *iter, gint count)`

将 `iter` 向前移动 `count` 行，到达目标行的行首。

- `gboolean gtk_text_iter_backward_lines(GtkTextIter *iter, gint count)`

将 `iter` 向后移动 `count` 行，到达目标行的行首。

- `gboolean gtk_text_iter_forward_word_end(GtkTextIter *iter)`

将 `iter` 移动到下一个单词结束处。

- `gboolean gtk_text_iter_backward_word_start(GtkTextIter *iter)`

将 `iter` 移动到上一个单词起始处。

- `gboolean gtk_text_iter_forward_word_ends(GtkTextIter *iter, gint count)`

将 `iter` 向前移动 `count` 个单词结束处。

- `gboolean gtk_text_iter_backward_word_starts(GtkTextIter *iter, gint count)`

将 `iter` 向后移动 `count` 个单词起始处。

- `gboolean gtk_text_iter_forward_sentence_end(GtkTextIter *iter)`

将 `iter` 移动到下一个句子结束处。

- `gboolean gtk_text_iter_backward_sentence_start(GtkTextIter *iter)`

将 `iter` 移动到上一个句子起始处。

- `gboolean gtk_text_iter_forward_sentence_ends(GtkTextIter *iter, gint count)`

将 `iter` 向前移动 `count` 个句子结束处。

- `gboolean gtk_text_iter_backward_sentence_starts(GtkTextIter *iter, gint count)`

将 `iter` 向后移动 `count` 个句子起始处。

- `gboolean gtk_text_iter_forward_to_end(GtkTextIter *iter)`

将迭代器移动到其缓冲区中最后一个字符之后的位置。

- `gboolean gtk_text_iter_forward_to_line(GtkTextIter *iter)`

将 `iter` 移动到当前行的行尾。

- `gboolean gtk_text_iter_forward_to_toggle(GtkTextIter *iter, GtkTag *tag)`

将迭代器移动到文本中下一个标签变化的地方。如果 `tag` 为 `NULL`，此函数将迭代器移动到下一个 `tag`。

- `gboolean gtk_text_iter_backward_to_toggle(GtkTextIter *iter, GtkTag *tag)`

与前一个函数类似，但向后搜索。

- `gboolean gtk_text_iter_find_char(GtkTextIter *iter)`

该函数用于在缓冲区中查找指定字符。

# GNOME 开发者指南官方指南

- `void gtk_text_buffer_move_mark(GtkTextBuffer *buffer, GtkTextMark *mark, GtkTextIter *iter)`

将标记移动到缓冲区中的 `iter` 位置。

- `void gtk_text_buffer_move_by_name(GtkTextBuffer *buffer, const gchar *name, const GtkTextIter *iter)`

与前一个函数类似，但使用名称字符串而不是对象句柄。

- `void gtk_text_buffer_delete_mark(GtkTextBuffer *buffer, GtkTextMark *mark)`

从缓冲区中移除标记。如果该标记没有现有的引用，GTK+ 将释放该标记的内存。

- `void gtk_text_buffer_delete_mark_by_name(GtkTextBuffer *buffer, const gchar *name)`

与前一个函数类似，但使用名称字符串而不是对象句柄。

- `boolean gtk_text_mark_get_deleted(GtkTextMark *mark)`

如果标记由于未处理的引用仍然存在，则返回 `TRUE`。你可能在调用上述任一个函数后调用此函数。

- `void gtk_text_mark_get_visible(GtkTextMark *mark, boolean visible)`

如果 `visible` 为 `TRUE` 则设为可见，否则不可见。GTK+ 将标记绘制为两个字符之间的线。在正常情况下，这是缓冲区中唯一的标记，但此功能对于调试目的非常有用。

- `boolean gtk_text_mark_get_visible(GtkTextMark *mark)`

如果标记当前可见，则返回 `TRUE`。

- `const gchar *gtk_text_mark_get_name(GtkTextMark *mark)`

返回标记的字符串标识符，如果没有则返回 `NULL`。

- `GtkTextBuffer *gtk_text_mark_get_buffer(GtkTextMark *mark)`

返回标记；如果你从缓冲区中删该标记，此函数将返回 `NULL`。

- `boolean gtk_text_mark_get_left_gravity(GtkTextMark *mark)`

如果标记具有左引力则返回 `TRUE`，具有右引力则返回 `FALSE`。

### 标签 Tags

标记对象表示缓冲区中的位置，而 `GtkTextTag` 对象表示每个缓冲区内文本的部分。每个缓冲区都有一个包含所有标签的标签表。

要为缓冲区创建标签，

```
```
