
参数 `node` 和 `column` 的描述与之前的 `gtk_ctree_node_get_text()` 相同。参数 `pixmap` 是一个指向 `GdkPixmap *` 的指针，`mask` 是一个指向 `GdkBitmap *` 的指针。返回的是树实际使用的 pixmap 和 mask，而不是副本。因此，请不要释放这些值中任一的所指向的内存，并在修改图像数据时要小心，因为修改将影响获取该数据的树。

要为指定的节点和列设置 pixmap 和 mask，你可以调用 `gtk_ctree_node_set_pixmap()`：

```c
void
gtk_ctree_node_set_pixmap(GtkCTree *ctree, GtkCTreeNode *node,
gint column, GdkPixmap *pixmap, GdkBitmap *mask);
```

请记住 `GtkCTree` 不会为 pixmap 或 mask 创建副本，但它会将两者的引用计数减为 0。此外，GDK 会意识到此处设置的 pixmap 和 mask 数据是临时的，因为引用计数变为了 0。同时，`GtkCTree` 会继续维护节点被添加到树时指定的打开和关闭状态的 pixmap 和 mask 数据。当用户（或你的应用程序）更改状态节点的展开/折叠状态时，响应对 `gtk_ctree_node_set_pixmap()` 调用而显示的 pixmap 和 mask 数据将被丢弃，显示的 pixmap 和 mask 将恢复到节点添加到树时设置的。接下来的两个函数结合了文本获取器和设置器的功能。要从树中同时检索 pixmap 和文本数据，请调用 `gtk_ctree_node_get_pixmap()`：

```c
gint
gtk_ctree_node_get_pixmap(GtkCTree *ctree, GtkCTreeNode *node,
gint column, GdkPixmap **pixmap, GdkBitmap **mask);
```

`gtk_ctree_node_get_pixmap()` 的参数见表 12。

| 参数 | 类型 | 值 |
| :--- | :--- | :--- |
| ctree | GtkCTree * | 输入树 |
| node | GtkCTreeNode * | 输入节点 |
| column | gint | 输入要获取的列 |
| text | gchar ** | 返回节点显示的文本 |
| spacing | uint8 | 图像数据之间的间距 |
| pixmap | GdkPixmap ** | 返回 pixmap 指针 |
| mask | GdkBitmap ** | 返回 mask 指针 |

`gtk_ctree_node_set_pixmap()` 的参数见表 12。

| 参数 | 类型 | 值 |
| :--- | :--- | :--- |
| ctree | GtkCTree * | 输入树 |
| node | GtkCTreeNode * | 输入节点 |
| column | gint | 输入要设置的列 |
| text | gchar * | 输入节点要显示的文本 |
| spacing | uint8 | 图像数据之间的间距 |
| pixmap | GdkPixmap * | 输入节点显示的 pixmap 指针 |
| mask | GdkBitmap * | 输入关联的 mask 指针 |

# 设置列偏移

要将指定节点中指定列对应的数据按指定的像素数进行偏移，请调用 `gtk_ctree_node_set_shift()`。

```c
void
gtkk_ctree_node_set_shift (GtkCTree *ctree, GtkCTreeNode *node,
gint column, gint vertical, gint horizontal);
```

垂直和水平的默认值均为 0。没有函数可以查询树中节点/列的偏移值。

# 获取和设置节点的可选属性

应用程序可以通过调用 `gtk_ctree_node_set_selectable()` 来控制树中行的选择性：

```c
void
gtk_ctree_node_set_selectable (GtkCTree *ctree, GtkCTreeNode *node,
gboolean selectable);
```

节点的选择性可以通过 `gtk_ctree_node_get_selectable()` 查询：

```c
gboolean
gtk_ctree_node_get_selectable (GtkCTree *ctree, GtkCTreeNode *node);
```

如果节点可以被用户或应用程序通过程序方式选择，将返回 TRUE。

# 确定单元格类型

应用程序可以通过调用 `gtk_ctree_node_get_cell_type()` 来确定树中特定节点列存储的数据类型：

```c
GtkType
gtk_ctree_node_get_cell_type (GtkCTree *ctree, GtkCTreeNode *node,
gint column);
```

参数 `ctree`、`node` 和 `column` 指定要查询的列。返回值见表 12.12。

| 值 | 含义 |
|---|---|
| GTK_CELL_EMPTY | 列不包含任何数据。 |
| GTK_CELL_TEXT | 列包含文本。 |
| GTK_CELL_PIXMAP | 列包含位映射图（pixmap）和掩码。 |
| GTK_CELL_PITEXT | 列同时是 GTK_CELL_TEXT 和 GTK_CELL_PIXMAP。 |
| GTK_CELL_WIDGET | 列包含一个部件（在 Gtk+1.2 中未实现）。 |

# 设置和获取样式对象

接几个函数允许您查询或更改树中节点或行内特定列的 Gtk+ 样式对象。有两对 setter 和 getter 函数。一对用于设置和获取树中行或节点的样式对象，而另一对用于设置和获取特定行中列的样式对象。让我们先看看行定向的函数。要获取行（或节点）样式，可以调用 `gtk_ctree_node_get_row_style()`。

```c
GtkStyle *
gtk_ctree_node_get_row_style(GtkCTree *ctree, GtkCTreeNode *node);
```

参数标识树和行；返回值为 Gtk+ 样式对象，如果未设置，则返回 NULL。

函数 `gtk_ctree_node_set_row_style()`：

```c
void
gtk_ctree_node_set_row_style(GtkCTree *ctree, GtkCTreeNode *node,
    GtkStyle *style);
```

可用于与行关联的样式对象（如果有）替换为您选择的样式对象。参数再次标识要附加样式的树和节点。参数 `style` 是将附加到指定节点上的样式对象。

以下代码片段从树中的节点读取样式对象，如果它存在则对其进行复制（如果不存在则创建一个新的），然后将字体更改为默认 Gtk+ 类似的字体，但不加粗和斜体。它调用 `gtk_ctree_node_set_row_style()` 将新样式对象附加到获取原始样式对象的行上。

```c
GtkStyle *style, *new_style;
GdkFont *font;
```

```c
...
```

```c
// 向树中添加一个节点
text[0] = "Ralph", text[1] = "888"; text[2] = "666-444";
node = gtk_ctree_insert_node(GTK_CTREE(root), parent, NULL, text,
    5, NULL, NULL, NULL, FALSE, TRUE);
```

```c
// 读取样式对象 -- 这是 NULL，但接下来的
// 代码说明了如何处理 NULL 和非 NULL 返回值
```

```c
style = gtk_ctree_node_get_row_style(GTK_CTREE(root), node);
if ( style ) {
    new_style = gtk_style_copy( style ); // 复制读取到的
else
    new_style = gtk_style_new()); // 创建一个新的
```

```c
// 加载 Gtk+ 默认字体，但不加粗和斜体
font = gdk_font_load();
```

# "-adobe-helvetica-bold-o-normal--*-120--*-*-*-iso8859-1";

```c
// 如果上述加载成功，则更改字体
```

```c
if (font) {
    gdk_font_unref(new_style->font);
    new_style->font = font;
    gdk_font_ref(new_style->font);
}
```

```c
// 将样式对象附加到行
gtk_ctree_node_set_row_style(GTK_CTREE(root), node, new_style);
```

*(注：OCR 文本在后面的页面中有很多重复和片段。我将根据提供的文本逻辑重新生成整洁的版本。）*
