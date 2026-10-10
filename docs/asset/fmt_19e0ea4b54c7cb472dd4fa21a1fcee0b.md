
下一条规则定义了对话框的 `QLineEdit` 和其 `QListView` 的外观：

```
QLineEdit,

ListView {

  font: 9pt;

  color: rgb(0, 0, 127);

}
```

为了让对话框的 `QLineEdit` 和其 `QListView` 边界突出，我们指定了 2 像素的凹槽边界。为了确保 `QLineEdit` 和 `QListView` 的内容不与边界碰撞，我们使用了 `padding`。图 19.8 提供了边界的示意图

![](img/930c1c6fda99d425284503ebcbc940ea_469_1.png)

图 19.8. 边界结构

## 448

## 19. 外观与感觉自定义

圆角边界，我们指定了垂直 2 像素、水平 4 像素的内边距。对于 `ListView`，垂直内边距看起来不太对，所以我们这样覆盖：

```
ListView {

  padding: 5px 4px;

}
```

当多个规则设置同一个属性时，最后一个规则生效。

对于 `QPushButton`，我们将使用完全不同的方法。我们不是使用样式表规则绘制按钮，而是使用一个现成的图像作为背景。此外，为了使按钮可扩展，按钮背景使用了边界图像机制。

与使用 `background-image` 指定边界图像不同，边界图像被切割成 3×3 的网格，如图 19.9 所示。当填充小部件背景时，角（图中的 `A`、`C`、`G` 和 `I`）原样保留，而其他五个单元被拉伸或平铺以填充可用空间。

| A | B | C |
| --- | --- | --- |
| D | E | F |
| G | H | I |

(a) 图像

(b) 结果图像

图 19.9. 边界图像切割

边界图像使用 `border-image` 属性指定，我们需要指定图像文件和定义九个单元的四个“切割”。切割定义为距离顶、右、下、左边缘的像素距离。距离顶、右、下、左边缘分别为 4、8、12 和 16 像素的 `border.png` 边界图像指定为

```
border-image: url(border.png) 4 8 12 16;
```

使用边界图像时，我们显式设置 `border-width` 属性。通常，`border-width` 应该对应于切割的位置；否则角单元将被拉伸或缩小以适应 `border-width`。对于边界示例，我们这样指定边界宽度：

```
border-width: 4px 8px 12px 16px;
```

现在我们已经了解了边界图像机制的工作原理，让我们看看它是如何

## 使用 Qt 样式表

用于设置 `Qt QPushButtons` 的样式。以下是定义推按钮在普通状态下渲染的规则：

```
QPushButton {

  color: white;

  font: bold 10pt;

  border-image: url(/images/button.png); 16px;

  border-width: 16px;

  padding: -16px 0px;

  min-height: 32px;

  min-width: 60px;

}
```

在 `Candy` 样式中，`QPushButton` 边框图像的四个切口距离 $34 \times 34$ 像素边框图像边缘 16 像素处，如图 19.10 (a) 所示。由于四个切口是均匀的，我们只需要为切口编写“16”，为边框宽度编写“16px”。

在图 19.10 (b) 所示的 `QPushButton` 示例中，对应 $\mathcal{D}$、$\mathcal{E}$ 和 $\mathcal{F}$ 的边框图像单元格被丢弃，因为调整大小后的按钮不够高，不需要它们，而单元格 $\mathcal{B}$ 和 $\mathcal{H}$ 被水平拉伸以占据额外的宽度。

![](img/930c1c6fda99d425284503ebcbc940ea_471_0.png)

**图 19.10.** `QPushButton` 的边框图像

边框图像的标准用法是为控件提供一个边框，控件位于边框内部。但我们颠覆了边框图像机制，用它来创建控件本身的背景。因此，单元格 $\mathcal{L}$ 被删除，填充矩形的高度为 0。为了给推按钮的文本留空间，我们指定了 -16 像素的垂直内边距。图 19.11 描述了这种情况。如果我们使用边框图像机制来定义实际边框，我们可能不希望文本与其碰撞——但由于我们使用它来创建一个可缩放的背景，我们希望文本位于其上方，而不是内部。

## 19. 外观与外观定制

![](img/930c1c6fda99d425284503ebcbc940ea_472_0.png)

图 19.11. `QPushButton` 的结构

使用 `min-width` 和 `min-height`，我们设置了推按钮内容的最小尺寸。所选的值确保有足够的空间放置边框图像角，并确保 OK 按钮比需要的稍微宽一点，使其在取消（Cancel）按钮旁边看起来更好。

之前的 `QPushButton` 规则适用于所有推按钮。现在，我们将定义几条仅在按钮处于某些状态时才应用的额外规则。

```
QPushButton:hover {

  border-image: url(:/images/button-hover.png) 16;

}
```

当鼠标指针悬停在 `QPushButton` 上时，`:hover` 状态评估为真，并覆盖任何其他选择器优先级更低的规则。我们使用这种技术来指定一个稍微亮一点图像作为边框图像，以获得良好的悬停效果。指定的其他 `QPushButton` 属性继续生效；只有 `border-image` 属性发生了变化。

```
QPushButton:pressed {

  color: lightgray;

  border-image: url(:/images/button-pressed.png) 16;

  padding-top: -15px;

  padding-bottom: -17px;

}
```

当用户按下推按钮时，我们将前景色颜色改为浅灰色，并通过调整内边距将推按钮的文本向下移动一个像素。

我们最终的样式规则将自定义 `QComboBox` 的外观。为了展示使用样式表所能实现的控制和精确性，我们将区分只读和可编辑的组合框，如图 19.12 所示。只读的组合框被渲染为一个右侧带有向下箭头的 `QPushButton`，而可编辑的组合框则由一个类似 `LineEdit` 的组件和一个小的圆角按钮组成。事实证明，我们可以复用已经为 `LineEdit`、`QListViews` 和 `QPushButton` 定义的大部分规则。

- 定义 `QLineEdit` 外观的规则可以用于样式化可编辑组合框：

![](img/930c1c6fda99d425284503ebcbc940ea_473_0.png)

![](img/930c1c6fda99d425284503ebcbc940ea_473_1.png)

(a) 只读

(b) 可编辑

**图 19.12.** `Candy` 样式下的 `QComboBox`

```
QComboBox::editable,

QLineEdit,

QListView {

  color: rgb(127, 0, 63);

  background-color: rgb(255, 255, 241);

  selection-color: white;

  selection-background-color: rgb(191, 31, 127);

  border: 2px groove gray;

  border-radius: 10px;

  padding: 2px;

}
```

- 定义 `QPushButton` 在普通状态下外观的规则可以扩展到适用于只读组合框：

```
QComboBox::editable,

QPushButton {

  color: white;

  font: bold 10pt;

  border-image: url(:images/button.png) 16;

  border-width: 16px;

  padding: -16px;

  min-height: 32px;

  min-width: 60px;

}
```

- 悬停在只读组合框上或可编辑组合框的下拉按钮上应该改变背景图像，就像对 `QComboBox` 一一样：

```
QComboBox::editable:hover,

QComboBox::drop-down:editable:hover,

QPushButton:hover {

  border-image: url(:images/button-hover.png) 16;

}
```

- 按下只读组合框就像按下 `QPushButton`：

```
QComboBox::editable:on,

QPushButton:pressed {

  color: lightgray;

  border-image: url(:images/button-pressed.png) 16;

  padding-top: -15px;

  padding-bottom: -17px;

}
```

复用规则 R3、R5 和 R6 可以节省时间并有助于保持我们的一致性。我们还没有定义任何绘制下拉按钮的规则，所以我们现在来创建它们。

```
QComboBox::down-arrow {

    image: url(:images/down-arrow.png);

}
```

我们提供了自己的向下箭头，以便它比标准的大一点。

```
QComboBox::down-arrow:on {

    top: 1px;

}
```

如果组合框是打开的，向下箭头会移动一个像素。

```
QComboBox * {

    font: 9pt;

}
```

当用户点击组合框时，它会显示项目列表。规则 R10 确保组合框的弹出（或任何子控件）不会继承规则 R5 应用于组合框的大字体。

```
QComboBox::drop-down::editable {

    subcontrol-origin: padding;

    subcontrol-position: center right;

    width: 11px;

    height: 6px;

    background: none;

}
```

使用 `subcontrol-origin` 和 `subcontrol-position` 属性，我们将下拉箭头垂直居中放置在右侧，这对于只读组合框是这样设置的。我们指定：

```
QComboBox {

    padding-right: 15px;

}
```

对于只读组合框，我们指定 15 像素的内边距以确保文本不会与下拉箭头冲突。图 19.13 显示了这些是如何相互作用的。对于可编辑组合框，我们需要样式表来使其看起来像一个 `QPushButton`：

![](img/930c1c6fda99d425284503ebcbc940ea_474.png)

使用 `subcontrol-origin` 和 `subcontrol-position` 属性，我们指定：

```
QComboBox::drop-down {

    subcontrol-origin: padding;

    subcontrol-position: center right;

    width: 11px;

    height: 6px;

    background: none;

}
```

我们使用 `button.png` 来使其看起来像一个下拉按钮。图 19.14 显示了我们所做的示意图：

![](img/930c1c6fda99d425284503ebcbc940ea_475.png)

如果组合框是打开的，我们使用更深色的图像作为下拉按钮：

```
QComboBox::drop-down:editable:open {

  border-image: url(:images/button-pressed.png) 16;

}
```

对于可编辑组合框，我们指定 29 像素的右边距以给下拉按钮留空间，如图 19.15 所示：

```
QComboBox:editable {

  margin-right: 29px;

}
```

![](img/930c1c6fda99d425284503ebcbc940ea_476.png)

我们现在完成了 `Candy` 样式表的创建。该样式表大约有 100 行，并使用了几个自定义索引。结果是一个独特的对话框。

## QStyle 子类化

![](img/930c1c6fda99d425284503ebcbc940ea_477_0.png)

**图 19.16.** `Qt` 内置样式的继承树

要绘制的部件（例如其调色板）以及特定于部件的信息（例如按钮的文本）。这些函数还接收一个可选的 `QWidget` 指针，以应对 `QStyleOption` 无法提供所有必要信息的情况。

假设我们要创建一个 `MyPushButton` 类，它看起来像一个标准的 `Qt` 推送按钮，但又不是派自 `QPushButton`。（这个例子有些牵生硬，但它将帮助我们理清小部件与样式式之间的关系。）在 `MyPushButton` 的绘制事件处理器中，我们将设置一个 `QStyleOption`（实际上是 `QStyleButton`）并按如下方式调用 `QStyle::drawControl()`：

```
void MyPushButton::paintEvent(QPaintEvent * /* * event * */)

{

  QPainter painter(this);

  QStyleOptionButton option;

  option.initFrom(this);

  if (isFlat()) {

    option.features |= QStyleOptionButton::Flat;

    option.text = text;

  }

  style()->drawControl(QStyle::PushButton, &option, &painter, this);

}
```

`QStyleOption::initFrom` 函数初始化了代表部件的基础成员变量，如 `rect`、`state`（启用、聚焦等）和 `palette`。`QStyleOption` 特有的成员变量必须手动初始化。在 `MyPushButton` 示例中，我们手动初始化了 `features` 和 `text`，并让 `icon` 和 `iconSize` 采用默认值。

`Widget::style()` 函数返回用于绘制该部件的相应样式。样式通常使用 `QApplication::setStyle()` 为整个应用程序设置，但也可以通过 `Widget::setStyle()` 为单个部件对其进行重写。

## 456 19. 外观与感受自定义

`drawControl()` 由各种 `QStyle` 子类实现，用于绘制 `QPushButton` 和其他简单部件。一个典型的实现可能如下所示：

```
void QStyle::drawControl(ControlElement element,

                               const QStyleOption *option,

                               QPainter *painter,

                               const QWidget *widget) const

{

    switch (element) {

        case CE_CheckBox:

            ...

        case CE_RadioButton:

            ...

        case CE_PushButton:

            if (const QStyleOptionButton *buttonOption =

                    qstylecast<const QStyleOptionButton *>(option)) {

                // 绘制按钮

                break;

            }

...

    }

}
```

第一个参数 `element` 指明要绘制的部件类型。如果类型是 `CE_PushButton`，样式会尝试将 `option` 参数强制转换为 `QStyleOptionButton`。如果转换成功，它将绘制由 `QStyleOptionButton` 描述的按钮。从 `const QStyleOption *` 到 `const QStyleOptionButton *` 的强制转换通过 `qstylecast<T>()` 执行，如果 `option` 不指向 `QStyleOption` 实例，则它返回空指针。

`QStyle` 子类不一定依赖于 `QStyleOption`，也可以直接查询部件：

```
case CE_PushButton:

    if (const QPushButton *button =

            qstylecast<const QPushButton *>(widget)) {

        // 绘制按钮

    }

break;
```
