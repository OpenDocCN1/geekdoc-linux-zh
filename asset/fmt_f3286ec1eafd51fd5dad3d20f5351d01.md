
## 2.2 XUL 布局原理

### 2.2.3 常用 Box 布局属性

与 HTML 类似，布局可以交给浏览器，也可以由你来控制。使用一组标准的标签属性来分发 `<box>` 标签的内容。这些属性适用于任何容器标签，因为大多数 XUL 标签的行为都像是一个框（box）。图 2.4 显示了这些属性的概念布局。

图 2.4 阐释了 `orient="horizontal"` 的情况，这是 `<box>` 的默认值。要查看 `orient="vertical"` 的情况，请将此书顺时针旋转 90 度。图中每个单词都是一个 XUL 属性，影响着 `<box>` 内容的位置。`<box>` 内部的每一个项目都必须是一个独立的标签。

从历史角度看，这些属性中某些源自 CSS2 标准的属性，有些很快变得令人困惑，另一些则是完全独立的。特别是，应该避免使用 `valign` CSS2 属性，尽管它是被支持的。公认的布局属性如下。请参见表 2.5 获取对应的插图。

- `orient = "horizontal" | "vertical"`：状态内容是跨页面布局还是向下布局，并决定主方向。主方向在水平方向时向右，垂直方向时向下。`horizontal` 是默认值。

- `dir = "ltr" | "rtl" | "normal" | "reverse"`：`dir` 属性类似于 HTML 中的 `dir`。内容将沿主方向从右或从右向左布局。`normal` 等同于 `ltr`；`reverse` 等同于 `rtl`。对于垂直框，`left`意味着从右到上，`bottom`意味着从左到上。`ltr` 是默认值。

- `pack = "start" | "center" | "end"`：`pack` 属性沿主方向对齐框的内容，类似于文字处理器中的对齐。`start` 表示左对齐或顶部对齐，`center` 表示内容居中，`end` 表示右对齐或底部对齐。通常，box 会沿长度扩展以适应可用空间。在这种情况下，`pack` 是很有用的；如果 box 没有扩展，`pack` 则不起作用。扩展取决于 `align="stretch"` 属性。`start` 是 `pack` 的默认值。

![](img/319913ee3703286e2c03d285fbfc49c7_76_0.png)

**图 2.4** XUL 容器标签的标准布局属性。

- `align = "start" | "center" | "end" | "baseline" | "stretch"`：（横向）方向。`align` 属性在框的交叉方向上对齐框的内容。沿框的任何点，在该方向上只有一个内容项目，因此 `align` 会移动每个上/下或左/右。只有当框的横向尺寸大于内容的某部分时，它才有意义。对于水平框，`baseline` 将内容移动到 CSS2 文本基基线，这会对齐所有文本，但会将其他项目放在框的底部。`stretch` 实现完全对齐，但由于每个横向点只有一个内容项目，该项目会被放大，直到触及起始和结束侧。适用于嵌套框、图像和小部件（widgets）。默认值是 `stretch`。

- `equalsize = "always"`：如果此属性被设置为 `always`，且如果所有子元素都有 `flex` 属性，那么框的所有内容在主方向上的尺寸将相等。这对于表格化或网格状布局非常有用。任何其他值都会关闭 `equalsize`。

Mozilla 还有 `ordinal` 属性。当 Mozilla 通过 `persist` 属性保存和调用有关 XUL 文档的信息时，该属性会被自动记录。持久化系统在第 12 章“覆盖层与 Chrome”中讨论。它对于应用程序程序员并不是特别相关。尽管如此，这里是它的用法。

- `ordinal` 适用于任何给定标签的子标签，并持有一个整数，最小值为零。它指定了子标签在其父级中的顺序。通常情况下，该顺序自动遵循 XUL 文档中标签的顺序。`ordinal` 有时用于记录 `<tree>` 列的状态。

对于所有这些属性，`inherit` 的值与 CSS2 中的含义相同：该值将从标签的样式信息获取。然而，`inherit` 值只能从与这些标签等效的 CSS 样式（“样式选项”部分）指定。图 2.5 显示了这些标签的效果：

图 2.5 中的截图总共需要 82 个 `<box>` 标签，在这种情况下，布局是某种任意的。其他常用的布局适用于所有标签，而不仅仅是用作 box 容器。这些布局如下：

- `collapsed = "true" | "false"`：设置为 `true`，标签将像使用了 CSS2 样式 `visibility: collapse` 一样被折叠。它在屏幕上不占用任何空间，这会影响容器框布局其子元素。设置为 `false` 或任何其他值，标签将重新出现。动态更改 `collapsed` 会导致重流（reflow），这对于 Mozilla 来说是一项繁重的处理工作。CSS2 的 `collapse` 是现在时；XUL 的 `collapsed` 是过去时。

- `hidden = "true" | "false"`：设置为 `true`，标签将从屏幕上消失，仿佛设置了 CSS2 的 `display: none`。标签仍然占据空间。

| orient="horizontal" | | | | orient="vertical" | | | | pack="start" | pack="center" | pack="end" |
|---|---|---|---|---|---|---|---|---|---|---|---|
| dir="ltr" | 一 | 二 | | dir="ltr" | | | | | | |
| dir="rtl" | | 二 | 一 | | | | | | | | |
| pack="start" | | 一 | 二 | | | | | | | | |
| pack="center" | | 一 | 二 | | | | | | | | |
| pack="end" | | 一 | 二 | | | | | | | | |
| align="start" | 一 | 二 | 三 | | | | | | | | |
| align="center" | 一 | 二 | 三 | | | | | | | | |
| align="end" | | | | | | | | | | | | |
| align="baseline" | | | | | | | | | | | | |
| align="stretch" | | | | 一 | 二 | 三 | | | | |

**图 2.5** 这些标签的效果。

图 2.5 中的截图总共需要 82 个 `<box>` 标签，在这种情况下，布局是有些任意的。其他常用的布局适用于所有标签，而不仅仅是用作 box 容器。这些布局如下：

- `collapsed = "true" | "false"`：设置为 `true`，标签将像使用了 CSS2 样式 `visibility: collapse` 一样被折叠。它在屏幕上不占用任何空间，这会影响容器框布局其子元素。设置为 `false` 或任何其他值，标签将重新出现。动态更改 `collapsed` 会导致重流（reflow），这对于 Mozilla 来说是一项繁重的处理工作。CSS2 的 `collapse` 是现在时；XUL 的 `collapsed` 是过去时。

- `hidden = "true" | "false"`：设置为 `true`，标签将从屏幕上消失，仿佛设置了 CSS2 的 `display: none`。标签仍然占据空间。
