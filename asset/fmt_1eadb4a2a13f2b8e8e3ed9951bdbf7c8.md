
代码列表 13.1 指定了一个包含三个项目的单列列表框，其标题显示为“Sole Column”。它没有图标或复选框。它与偏好设置（Preferences）对话框中的许多框类似；例如，在外观（Appearance）、主题（Themes）面板中，或者在导航器（Navigator）的语言（Languages）面板中。这些示例没有标题。

Mozilla 为此列表构建的 XML 包含许多额外的标签，如图图 13.4 所示。

在这个完全展开的树中，颜色较暗的标签与代码列表 13.2 匹配。带有前缀的浅色标签是 `listbox` 生成的额外内容。这是 `listbox` 的一个复杂分解，除非存在两列，否则 `<xul:list>`、`<xul:listadditem>` 和 `<xul:listcell>` 标签会在每个树位置出现两次，而不是只出现一次。

这棵树显示代码列表 13.2 是一个使用非常密集标签的规范，最终 `listbox` 中的许多标签是隐含的而非显式指定的。它还显示了 `<listbox>` 和 `<grid>` 之间的相似与差异。虽然两者都有列和行，但 `<listbox>` 最多只有

![](img/319913ee3703286e2c03d285fbfc49c7_468_0.png)

两行，而 `<grid>` 可以有任意数量的行。`listbox` 中显示的项目嵌套在第二行中，仿佛它是一个 `<vbox>` 一样。第一行包含标题行，或者在未指定标题时省略。

以下是 `<listbox>` 构建的一些基本规则：

- 1. 对于每个 `<listbox>`，最多有一个 `<listcols>`，且最多有一个 `<list>`。
- 2. 对于 `<listcol>`，如果它存在，则至少有一个 `<listcol>`。
- 3. 对于 `<listbox>`，如果它存在，则至少有一个 `<list-header>`。
- 4. 每个 `<listitem>` 的项目数应等于 `<listcols>` 的数量，或者如果存在 `<listitem>` 则为 1。
- 5. 不要显式说明 `<listrows>`、`<listbody>` 和 `<listheaditem>`。这些标签仅内部使用。

这种复杂的构建过程存在陷阱。主要的陷阱是 XUL 无法处理它为 `<listbox>` 生成的标签组合。如果你创建了一个与图 13.5 所示标签和结构匹配的显式 XUL，它将无法作为 `listbox` 运行，并且 Mozilla 可能会崩溃。这意味着 `listbox` 的 XML 规范和它的 XUL 实现是分开且不同的。

如果你使用构建规则 5 中的任何标签，Mozilla 也可能崩溃。如果你为 `<listcol>` 标签指定了任何内容，它将会崩溃。如果你稍微偏离了 XULXB 处理器在看到 `<listbox>` 标签后所做的假设，它可能会变得困惑、产生糟糕的布局或可能崩溃。

代码列表 13.2 显示了 XUL 支持的最扩展 `listbox` 规范。

代码列表 13.2 显示所有选项的扩展 `<listbox>`。

```xml
<listbox>
  <listcols> // 标签和内容可选
    <listcol/> // 可以重复
  </listcols>

  <listhead> // 标签和内容可选
    <listheader> // 可以重复
    </listheader>
  </listhead>

  <listitem> // 可以重复
    <listcell> // 可以重复
  </listitem>

</listbox>
```

## 13.2 Listboxes (列表框)

`<list>`、`<listcell>` 和 `<list-header>` 的开始和结束标签可以合并为单例 `<tag/>` 标签，并可以使用属性代替被移除的标签内容。这些属性在各个标签下进行了讨论。所有这些标签在 `chrome` 的 `toolkit.jar` 中的 `listbox.xml` 中都有 XBL 定义。

### 13.2.3 `<listbox>`

`<listbox>` 具有以下特殊属性：

| `rows` | `setype` `suppression` `select` `disableKeyNavigation` |

`rows` 和 `size` 决定了 `listbox` 以行项目数计算的高度。`size` 计算是基于存在的最高项目乘以该属性的值。这与为每行设置 `minheight` 属性的固定像素值相同。每行项目都将扩展到最高项目的高度，因此行项目的大小相等。`size` 属性在 XUL 中已弃用；请使用 `rows`。可以通过 JavaScript 选择 `rows` 属性来动态调整 `listbox` 的大小。

`<listbox>` 使用 `maxheight` 属性的效果不佳。如果 `<listbox>` 在 `<listbox>` 内部，且 `listbox` 的兄弟节点的 `maxheight` 小于该 `listbox` 的 `maxheight`，则内容可能会溢出，导致混乱的布局。当 `listbox` 有兄弟节点时，推荐的方法是完全设置 `<listbox>` 的 `height` 和 `size` 属性。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。

`setype` 属性决定了 `listbox` 的多行是否可以被用户选中。如果它设置为 `multiple`，则是可能的。如果它设置为 `select`，则只会选中某行。这种安排的动态性在第 13.2.11 节中讨论。
