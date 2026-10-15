
以自定义的方式渲染日期/时间或其他类型的模型数据，可以通过创建自定义代理并重实现 `paint()` 方法轻松实现，正如我们在这里所的那样。而且，就像 Qt 中的大多数绘制工作一样，我们必须的工作主要涉及使用适当的颜色以及尺寸和定位的数学计算。但当我们有可编辑项目时，我们可能倾向于提供自己的编辑小部件，这要求我们重实现某些方法，正如我们在下一个节中将看到的。

### 可编辑列或行代理

自定义代理可以用于渲染项目或编辑项目，或者二者兼之。在渲染情况下，我们只需要重实现 `paint()` 方法，但如果我们想支持编辑，就必须实现表 5.1 所示的 `QStyledItemDelegate` API 中的——至少包括 `createEditor()`、`setEditorData()` 和 `setModelData()` 方法。

`sizeHint()` 和 `updateGeometry()` 的基类实现几乎总是足够的，因此我们很少需要重实现它们。同样，没有必要重实现 `paint()` 方法，特别是当数据是简单的纯文本、日期、时间或数字时。

在第 4 章中查看的时间线应用程序中，我们使用了“富文本”——一种支持加粗、斜体和颜色等基本效果的 HTML 子集。此外，富文本项目（任务）是可以复选的。为了提供这种支持，我们创建了 `RichTextDelegate`，其内容在图 5.3 中所示。

`RichTextDelegate` 同时提供渲染和编辑。该类实现了大部分 `QStyledItemDelegate` API——具体来说 `paint()`、`sizeHint()`、`createEditor()`、`setEditorData()` 和 `setModelData()`。此外，它还有一个私有槽函数 `closeAndCommitEditor()` 和两个私有数据项——一个复选框指针和一个 `QLabel`。我们将从构造函数开始复习所有方法。

```cpp
RichTextDelegate(QObject *parent)
    : QStyledItemDelegate(parent)
{
    checkbox = new QCheckBox;
    checkbox->setFixedSize(
        qRound(1.3 * checkbox->sizeHint().height()),
        checkbox->sizeHint().height());
    label = new QLabel;
    label->setTextFormat(Qt::RichText);
    label->setTextWrap(false);
}
```

在自定义代理中渲染项目时，我们有三种方法可以使用。一种是自己绘制一切——我们在 `DateEdit` (188) 中就是这样做——这种方法的缺点是我们必须自己考虑平台差异。另一种是使用 Qt 的 `Style` 类，例如使用 `Style::drawControl()`、`Style::drawComplexControl()` 等——这是一种强大但相当底层的方法，需要大量的心力和相当的代码。在这里，我们选择了更简单、更高层次的路线：我们将绘制小部件（在这种情况下是复选框和标签），让 Qt 处理平台差异，并保持我们的代码尽可能清洁简单。

### 特定数据类型的代理

`Timelog` `timelog.tlg`

195

![](img/74b321c00e6b987639de429f0799cff9_211_0.png)

图 5.3 运行中的 `RichTextDelegate`

如果我们只想渲染纯文本，我们只需要一个复选框小部件，因为它显示了一个复选框和一个关联文本。但由于我们想显示富文本，我们纯粹使用复选框来显示框（不给它任何显示的文本），并使用标签来显示富文本。

我们让复选框占据比实际需要的稍微宽一点，以提供一些边距，以便它不会与标签对齐。我们告诉标签将其任何文本视为富文本（HTML）并且不要进行任何单词换行。

```cpp
RichTextDelegate() { delete checkbox; delete label; }
```

当代理被销毁时，我们会删除复选框和标签——这在头文件中可以很容易实现。为了方便解释，我们将分四个部分复习 `paint()` 方法：

```cpp
void RichTextDelegate::paint(QPainter *painter, const QStyleOptionView &option, const QModelIndex &index) const
{
    bool selected = option.state & QStyle::State_Selected;
    QPalette palette(option.palette);
    palette.setColor(QPalette::Active, QPalette::Window,
        selected ? option.palette.highlight().color() : option.palette.base().color());
    palette.setColor(QPalette::Active, QPalette::Text,
        selected ? option.palette.highlightedText().color() : option.palette.text().color());

    int yoffset = checkbox->height() < option.rect().height()
    ? (option.rect().y() - checkbox->height()) / 2 : 0;
    QRect checkboxRect(option.rect().x(), option.rect().y() + yoffset,
        checkbox->width(), checkbox->height());
    checkbox->setPalette(palette);
    
                                                              [196]
    bool checked = index.model()->data(index, Q::CheckState).toInt() == Q::Checked;
    checkbox->setChecked(checked);
    checkbox->render(checkboxRect);

    QRect labelRect(option.rect().x() + checkbox->width(), option.rect().y(),
        option.rect().width() - checkbox->width(),
option.rect().height());
    label->setPalette(palette);
    label->setFixedSize(max(0, labelRect.width()),
        labelRect.height());
    QString text = index.model()->data(index, Q::DisplayRole).toString();
    label->setText(text);
    label->render(labelRect);
}
```

首先，我们开始处理复选框相关的内容。我们首先创建之后绘制复选框所需的矩形。当我们创建矩形时，如果选项矩形比复选框高，则在可用空间内垂直居中。然后我们将复选框的调色板设置为创建的调色板，最后设置复选框的勾选状态与项目匹配。

尽管我们在构造函数中将复选框设置为固定大小并且我们更改了它，尽管我们也将其设置了固定大小——我们必须按项目设置尺寸。为标签创建的 `labelRect` 是基于 `option` 参数生成的矩形，但向右偏移（并减少偏移量宽度），以便为复选框留出空间。这种减少会导致负宽度——例如，如果用户足够缩小了容器窗口的宽度——我们

使用 `qMax()` 修正此项。一旦标签设置了调色板和大小，我们就获取项的文本（HTML 格式）并设置标签的文本。

此时，复选框和标签已经有了正确的调色板、大小和内容，并且我们有了可以在其中绘制它们的矩形区域。

```cpp
QString checkbox = QString("CHECKBOX:%1.%2").arg(selected)
    .arg(checked);
paintWidget(painter, checkboxRect, checkbox, checkbox);
QString labelKey = QString("LABEL:%1.%2%3x%4").arg(selected)
    .arg(html).arg(labelRect.width()).arg(labelRect.height());
paintWidget(painter, labelRect, labelKey, label);
```

我们将小部件的绘制逻辑提取到了私有辅助方法 `paintWidget()` 中。此外，我们还使用了 Qt 的 `QPixmapCache` 来重复保存相同的像素图。缓存使用一个键来标识每个像素图——为此我们同时使用了被选中状态和内容（复选框的选中状态和标签的文本）。因此，在复选框的情况下，缓存中最多会有三个像素图：(选中, 未选中)、(选中, 已选中, 未选中, 未勾选) 以及 (未选中, 已选中)。一旦我们有了缓存的键字符串，就可以调用 `paintWidget()`。

```cpp
void RichtDelegate::paintWidget(QPainter *painter,
    const QRect &rect, QString &cacheKey,
    QWidget *widget)
{
    QPixmap pixmap(widget->size());
    if (!QPixmapCache::find(cacheKey, &pixmap)) {
        QPixmapCache::insert(cacheKey, pixmap);
    }
    painter->drawPixmap(rect, pixmap);
}
```

通过创建一个正确大小的空像素图， `QPixmapCache::find()` 方法根据给定的键从缓存中检索像素图。如果找到键，该方法返回 `true` 并通过指针（或非常量引用，即不带 `&`）填充所传递的 `QPixmap`；否则返回 `false`。因此，当我们第一次请求某个特定的像素图键时，我们将小部件渲染到空像素图上并将其插入缓存。最后，我们在给定的矩形中绘制该像素图。（获取小部件像素图的另一种方法是使用 `QPixmap::grabWidget()`，将小部件作为参数传递）。

这种方法的主要处是它将几乎所有的绘制样式工作都交给了 Qt，使得我们的代码比其他方式简单得多，并且得益于像素图缓存更加高效。

```cpp
QSize RichTextDelegate::sizeHint(const QStyleOptionViewItem &option,
                             const QModelIndex &index) const
{
  QString html = index.model()->data(index, Qt::DisplayRole)
                .toString();
  
  document.setDefaultFont(option.font);
  document.setHTML(html);
  return QSize(document.idealWidth(), option.fontMetrics.height());
}
```

在不需要重新实现 `QStyledDelegate::sizeHint(method)` 的情况下，我们遇到了一个特殊情况。例如，假设我们有 HTML 文本 `b<font color='#000ff'>blue</font> bear`。这段文本包含 54 个字符，但只有其中 18 个会被显示。标准的 `sizeHint()` 实现会非常合理地根据全部 54 个字符计算必要的宽度，因此我们必须重新实现它以产生更准确的结果。

确定宽度的最明显的方法是将文本转换为纯文本并对其调用 `QFontMetrics::width()`。遗憾的是，这种方法没有考虑到细微细节，例如上标或下标字符（它们的字体大小通常较小），或者粗体或斜体字符（它们通常比普通字符宽），亦混合使用不同字体的情况。幸运的是，我们所需的精确计算——并考虑了我们提到的所有细节及更多细节——已经可以通过我们这里使用的 `QTextDocument::width()` 方法来完成。

在某些平台上，为每次 `size hint` 调用创建并销毁 `QTextDocument` 是相当昂贵的，因此在类的私有数据中，我们声明了一个 `mutable QTextDocument`；这意味着我们每次都复用同一个 `QTextDocument`。

```cpp
QWidget RichTextDelegate::createEditor(QWidget *parent,
                             const QStyleOptionViewItem &option, const QModelIndex &index) const
{
  RichTextLineEdit *editor = new RichTextLineEdit(parent);
  editor->viewport()->setFixedHeight(option.rect.height());
  connect(editor, SIGNAL(returnPressed()),
          this, SLOT(closeAndCommitEditor));
  return editor;
}
```

此方法用于为给定模型索引的项创建一个合适的编辑器。由于该代理被用作持有富文本的列的列代理，我们不需要知道具体是为哪个项需要编辑器。（稍后我们将看到该方法的另一种实现，其中返回的编辑器类型取决于项的某个方面——例如，当其列为...时；201页）。

我们创建了一个 `RichTextEdit` 小部件（在第 9 章；342 页中介绍）来编辑 HTML 代理预期的处理内容。在这种情况下，将编辑器的视口高度设置为 own值是关重要的。

如果用户按下回车键，我们将 `QTextEdit` 的 `returnPressed()` 连接到自定义的 `closeAndCommitEditor()`。

```cpp
void RichTextDelegate::setEditorData(QWidget *editor, const QModelIndex &index) const
{
    QString html = index.model()->data(index, Qt::DisplayRole)
                .toString();
    RichTextEdit *lineEdit = q_cast<RichTextEdit*>(editor);

    Q_ASSERT(lineEdit);
    lineEdit->setHtml(html);
}
```

一旦创建编辑器，代理就会调用 `setEditorData` 用模型对其进行初始化。在这里，我们获取文本（HTML 格式）、指向创建的 `QTextEdit` 指针并设置编辑器的文本。

用户确认他们的编辑。

```cpp
void RichTextDelegate::closeAndCommitEditor()
{
    RichTextEdit *lineEdit = q_cast<RichTextEdit*>(sender());

    QASSERT(lineEdit);
    emit commitData(lineEdit);
    emit closeEditor(lineEdit);
}
```

实现这样的槽函数对于具有指示编辑已完成的信号的编辑器来说通常很有用——例如 `QLineEdit::returnPressed()`。

我们结合 `q_cast<>` 和 `QObject::sender()` 方法来获取 `RichTextLineEdit` 的指针，然后发射两个信号：一个告诉代理提交编辑器数据——即将编辑器数据复制到模型；另一个告诉代理关闭编辑器，因为它不再需要了。

```cpp
void RichTextDelegate::setData(QWidget *editor, QAbstractItemModel *model, const QModelIndex &index) const
{
    RichTextLineEdit *lineEdit = q_cast<RichTextLineEdit*>(editor);

    Q_ASSERT(lineEdit);
    model->setData(index, lineEdit->toHtml());
}
```

如果用户确认他们的编辑——通过点击编辑器、跳转到另一个项或按下回车/执行键——就会调用此方法。（用户可以通过按 Esc 键取消编辑。）在这里，我们获取 `RichTextLineEdit` 指针并将编辑器的 HTML 设置模型。正如我们在第 9 章（►342）中将看到的，`toHtml()` 方法产生的 HTML 更简单、更紧凑，但缺点是只能处理非常有限的 HTML 子集。

这完成了 `RichTextDelegate` 的实现。除了 `paint()` 方法外，所有的方法实现都是非常直观的。这直接由于该代理被用作特定数据类型（在本例中是富列或富行）代理，这意味着它永远不需要检查给定的项的行或列来确定要处理的数据类型，并且总是以相同的方式处理给它的每一个项。

## 模型特定委托 (Model-Specific Delegates)
