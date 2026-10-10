
边框图像使用 `border-image` 属性指定，这要求我们指定图像文件名和定义九个单元格的四个“切点”。切点定义为距离顶部、右、底部和左边缘的像素距离。一个距离顶部、右、底部和左边缘均为 4、8、12 和 16 像素的 `border.png` 边框图像指定如下：

```css
border-image: url(border.png) 4 8 12 16;
```

使用边框图像时，我们还必须显式设置 `border-width` 属性。通常，`border-width` 应该对应切点的位置；否则，角单元格将被拉伸或收缩以适应 `border-width`。对于 `border.png` 示例，我们将如下指定边框宽度：

```css
border-width: 4px 8px 12px 16px;
```

现在我们已经知道了边框图像机制的工作原理，让我们看看如何使用它来为 `Candy` `QPushButton` 设置样式。以下是定义推送按钮在普通状态下渲染的规则：

```css
QPushButton {
  color: white;
  font: bold 10pt;
  border-image: url(:/images/button.png) 16;
  border-width: 16px;
  padding: -16px 0px;
  min-height: 32px;
  min-width: 60px;
}
```

在 `Candy` 样式中，`QPushButton` 边框图像的四个切点距离 34 x 34 像素图像的边缘 16 像素，如图 19.10 (a) 所示。因为四个切点是均匀的，我们只需要为切点写“16”，为边框宽度写“16px”。在图 19.10 (b) 显示的 `QPushButton` 示例中，对应 D、E 和 F 的边框图像单元格被丢弃了，因为调整大小后的按钮足够高需要它们，而 B 和 H 单元格被水平拉伸以占据额外的宽度。

**图 19.10. `QPushButton` 的边框图像**

![](img/1bc72df8c60cf85926d3aefcc273027d_738_0.png)

标准用法是使用边框图像来设置控件的外观，但我们这里使用边框图像是为了为了让对话框的 `QLineEdit` 和 `QListView` 这种效果。图 19.11 展示了由于我们使用了 `min-width` 和 `min-height`，可扩展的按钮看起来更好。此外，我们还通过 `border` 属性指定了一个灰色 2 像素宽的“凹槽”边框。与其使用 `border`，我们可以单独设置 `border-width`、`border-style` 和 `border-color`。我们可以通过指定 `border-radius` 来圆角边框，我们在这里就使用了 10 像素的半径。图 19.8 提供了对控件边框和内边距属性更改后的示意图。为了确保控件内容不与边框圆角碰撞，我们指定了垂直 2 像素、水平 4 像素的内部内边距。对于 `QListView`，垂直内边距看起来不太对，因此我们对其进行了如下覆盖：

```css
QListView {
  padding: 5px 4px; [R4]
}
```

**图 19.11. `QPushButton` 的结构**

![](img/1bc72df8c60cf85926d3aefcc273027d_739_0.png)

当一个属性被多个具有相同选择器的规则设置时，最后一个规则将生效。

对于 `QPushButton` 的样式设置，我们将使用完全不同的方法。我们不再使用样式表规则来绘制按钮，而是使用一张现成的图像作为背景。此外，为了让按钮可扩展，按钮背景是使用 CSS 边框图像机制定义的。

与使用 `background-image` 指定的背景图像不同，边框图像被切割成 3 x 3 的网格，如图 19.9 所示。在填充控件背景时，四个角（图中的 A、C、G 和 I 单元格）被原样保留，而其他五个单元格被拉伸或平铺以填充可用空间。

边框图像使用 `border-image` 属性指定，这要求我们指定图像文件名和定义九个单元格的四个“切点”。切点定义为距离顶部、右、底部和左边缘的像素距离。一个距离顶部、右、底部和左边缘均为 4、8、12 和 16 像素的 `border.png` 边框图像指定如下：

```css
border-image: url(border.png) 4 8 12 16;
```

使用边框图像时，我们还必须显式设置 `border-width` 属性。通常，`border-width` 应该对应切点的位置；否则，角单元格将被拉伸或收缩以适应 `border-width`。对于 `border.png` 示例，我们将如下指定边框宽度：

```css
border-width: 4px 8px 12px 16px;
```

现在我们已经知道了边框图像机制的工作原理，让我们看看如何使用它来为 `Candy` `QPushButton` 设置样式。以下是定义推送按钮在普通状态下渲染的规则：

```css
QPushButton {
  color: white;
  font: bold 10pt;
  border-image: url(:/images/button.png) 16;
  border-width: 16px;
  padding: -16px 0px;
  min-height: 32px;
  min-width: 60px;
}
```

在 `Candy` 样式中，`QPushButton` 边框图像的四个切点距离 34 x 34 像素图像的边缘 16 像素，如图 19.10 (a) 所示。因为四个切点是均匀的，我们只需要为切点写“16”，为边框宽度写“16px”。在图 19.10 (b) 显示的 `QPushButton` 示例中，对应 D、E 和 F 的边框图像单元格被丢弃了，因为调整大小后的按钮足够高需要它们，而 B 和 H 单元格被水平拉伸以占据额外的宽度。

```css
QPushButton:hover {
  border-image: url(:/images/button-hover.png) 16; [R6]
}
```

点击只读的组合框就像点击 `QPushButton`：

```css
QComboBox:!editable:on,
```

```css
QPushButton:pressed {
  color: lightgray;
  border-image: url(:/images/button-pressed.png) 16; [R7]
  padding-top: -15px;
  padding-bottom: -17px;
}
```

复用规则 R3、R5、R6 和 R7 可以节省时间并有助于保持样式一致。

但我们还没有定义任何绘制下拉按钮的规则，所以我们现在创建它们。

```css
QComboBox::downarrow {
  image: url(:/images/downarrow.png); [R8]
}
```

我们提供了自己的向下箭头图像，使其比标准箭头大一点。

```css
QComboBox::downarrow:on {
  top: 1px; [R9]
}
```

如果组合框是打开的，向下箭头会向下移动一个像素。

```css
QComboBox * {
  font: 9pt; [R10]
}
```

当用户点击组合框时，它会显示项目列表。规则 R10 确保组合框的弹出窗口（或任何其他子控件）不会继承由规则 R5 应用于组合框的较大字体。

```css
QComboBox::drop-down:!editable {
  subcontrol-origin: padding;
  subcontrol-position: center right;
  width: 11px; [R11]
  height: 6px;
  background: none;
}
```

使用 `subcontrol-origin` 和 `subcontrol-position` 属性，我们将下拉箭头垂直居中置于只读组合框使用的内边距矩形的右侧。此外，我们还将其大小设置为与按钮内容的大小（即 11 x 6 像素的 `downarrow.png` 图像）对应，并禁用了背景，因为我们的下拉按钮仅由向下箭头组成。

```css
QComboBox:!editable {
  padding-right: 15px; [R12]
}
```

对于只读组合框，我们指定了 15 像素的右内边距，以确保组合框中文本不会与下拉箭头重叠。图 19.13 显示了这些维度是如何相互作用的。

**图 19.13 只读 `QComboBox` 的结构**

[查看全尺寸图像]

![](img/1bc72df8c60cf85926d3aefcc273027d_742_0.png)

对于可编辑的组合框，我们需要配置下拉按钮，使其看起来像一个微小的 `QPushButton`：

```css
QComboBox::drop-down:editable {
  border-image: url(:/images/button.png) 16;
  border-width: 10px;
  subcontrol-origin: margin;
  subcontrol-position: center right; [R13]
  width: 7px;
  height: 6px;
}
```

我们指定 `button.png` 为边框图像。然而，这次我们指定了 10 像素的边框宽度而不是 16 像素，以稍微缩小图像比例，并指定了水平 7 像素、垂直 6 像素的固定内容大小。图 19.14 显示了我们所做的示意图。

**图 19.14 可编辑 `QComboBox` 下拉按钮的边框图像**

![](img/1bc72df8c60cf85926d3aefcc273027d_743_0.png)

如果组合框是打开的，我们为下拉按钮使用不同的、更深的图像：

```css
QComboBox::drop-down:editable:open {
  border-image: url(:/images/button-pressed.png) 16; [R14]
}
```

对于可编辑的组合框，我们指定了 29 像素的右外边距为下拉按钮留出空间，如图 19.15 所示：

```css
QComboBox:editable {
  margin-right: 29px; [R15]
}
```

**图 19.15 可编辑 `QComboBox` 的结构**

![](img/1bc72df8c60cf85926d3aefcc273027d_743_1.png)

我们现在已经完成了 `Candy` 样式表的创建。样式表大约有 100 行，并使用了一些自定义图像。结果是一个极具特色的对话框。

使用样式表创建自定义样式可能涉及大量的尝试和错误，对于那些没有使用过 CSS 的人来说尤其是。样式表的挑战之一是 CSS 冲突解决和级联并不总是能给出直观的结果。更多详细信息，请参阅在线文档 `http://doc.trolltech.com/4.3/stylesheet.html`。它描述了 Qt 对样式表的支持并提供了指向 CSS 规范的链接。

## 子类 `QStyle`

`QStyle` 类在 Qt 2.0 中引入，用于提供一种封装应用程序外观和感受的方法。`QStyle` 类是一个抽象接口，定义了绘制小部件的方法。要创建一个自定义样式，你必须派生 `QStyle` 并实现其虚函数。

（由于原文后续存在大量重复的错误文本，此处已根据要求保留核心逻辑并翻译。）
