
在此例中，`send()` 方法几乎几乎立即返回，此时 HTTP 请求仍在进行中。`finished()` 函数被安装为事件处理程序，当响应最终完成时就会触发。在这两个时间之间，`setTimeout` 被简单地用于检查请求进度。当发送此类异步请求时，用户可能不需要进度报告。尽管如此，程序员必须小心确保用户随后采取的操作不会在响应到达时干扰响应处理。例如，用户在购买股票时，不应能够在购买进行期间清空他们的银行账户。

## 7.4 菜单

菜单和表单就像葡萄酒和奶酪一样般配。Mozilla 的菜单标签是由简单的 XUL 标签构建的，与目前为止讨论的其他 XUL 标签一样。然而，由于几个原因，菜单要复杂一些：

- 弹出菜单不符合二维 XML 文档的正常流。
- 菜单包含许多独立的值（菜单项），而不仅仅是一个值。

菜单具有复杂的内部结构。菜单可以独立于表单使用，但它们仍然需要符合其他元素实施的限制。

Mozilla 不使用 XUL 菜单来实现所谓的列表框（listboxes），后者平铺在 XML 文档内部。`<listbox>` 标签充当这一角色。XUL 菜单仅用于弹出式菜单。

### Mozilla 平台在处理菜单操作时识别此标签。

### 7.4.3 `<arrowbox>` 和 `<scrollbox>`

`<arrowbox>` 和 `<scrollbox>` 标签允许用户导航到一个无法完全适应屏幕的矩形内容区域。两者在第 8 章“导航”中都得到了讨论，但它们在菜单中也有应用。当指定菜单时，会自动创建每个标签中的一个。

`<arrowbox>` 标签用于显示由于过长而无法容纳在屏幕上的菜单。如果菜单很长，那么 `<autorepeat>` 就是该箭头的一部分。查看滚动效果最简单的方法是使用 Mozilla Navigator 的个人工具栏（Personal Toolbar）。

要查看滚动效果，请确保工具栏中的某个书签文件夹包含足够的项目，使其超过滚动区域高度的一半。导航到个人工具栏位于屏幕中间的位置，然后点击包含许多项目的书签文件夹。将出现一个顶部和底部带有 `<arrowbox>` 图标的书签列表。如果你将 `<menubarup>` 的 `maxheight` 属性设置为较小值（例如 200px），它们也会出现。

`<scrollbox>` 标签实现了 `<arrowbox>` 内部的移动区域。它仅在用于 `<textbox type="autocomplete">` 标签内部时才会滚动。在 `<scrollbox>` 内部使用时，它没有样式类，通常应该保持原样。

`<arrowbox>` 上的按钮可以进行样式化。`<arrowscroll-box>` 无法左右滚动，只能上下滚动。

### 7.4.4 `<menubarup>`

`<menubarup>` 标签是 XUL 菜单系统的核心。它负责创建一个位于 XUL 文档布局正常流之外的窗口，并可能扩展到整个 Mozilla 窗口边界之外。为了实现这一点，它使用了原生 GUI 工具包的功能。`<menubarup>` 得到了 Mozilla C++/C 侧的大力支持。它还有一个 XBL 定义。

`<menubarup>` 标签是非常通用的。在它创建的小型窗口内，它的作用类似于 `<div>`，大多数简单的 XUL 内容都可以包含在内。这样做的原因尚不明确，但此功能允许创建装饰性菜单。在 `<menuitem>` 和 `<menu>` 标签内是可以被选择的内容。可以指定 `<menubarup>` 标签而不包含任何内容。该内容稍后可以通过 JavaScript、模板或其他 XUL 技术添加。

在创建菜单时，应用程序程序员必须指定此标签。对 `<menubarup>` 有特殊含义的属性有：

`popupanchor` `popalign` `position` `allowevents`

`onopuppushing` `onopupeshown` `onopuphiding` `onopuphidden`

`popupanchor` 选择父标签中使 `<popup>` 出现在附近的角——即所谓的锚点（anchor point）。`popalign` 选择弹出窗口中将固定在锚点之上的位置的角。因此，弹出窗口与其父标签的角对齐。这两个属性都取以下这些值之一：

- `toleft` `topright` `bottomleft` `bottomright` 这种指定对齐的方式非常不灵活，应该避免使用。它是已过时的。
- `allows` 属性可以设置为 true，但在普通用法中建议不要设置。Mozilla 平台对菜单有特殊的事件处理。图 7.4 所示了构成菜单的标签集。如果完整的 DOM 模型应用这些标签，选择菜单项将产生许多事件。Mozilla 将这些许多事件减少为单个的可命令事件。

其余四个属性是前面 DOM 事件的事件处理器。它们是成对的事件标签。`showing` 和 `shown` 变体在弹出窗口的开始和结束触发。`hiding` 和 `hidden` 变体在隐藏过程的开始和结束触发。显示过程分三个阶段工作，Mozilla 代码通过将这些临时属性之一设置为 true 来标记每个阶段：

`menubodedisplayed` `mengenerated` `menactive`

第一个表示某些事情将要发生但尚未发生。第二个表示内容已为菜单组装完毕。第三个表示菜单已显示并获得了焦点。

### 7.4.5 `<menu>`

`<popup>` 可以包含的有用内容有三种标签：`<menuitem>`、`<menuseparator>` 和 `<menu>`。`<menu>` 与 `<menuitem>` 非常相似，但它会在现有菜单的侧面生成一个新菜单。`<menu>` 的特定属性为：

```
label accesskey acceltext disabled
```

这些属性的含义与它们在 `<menuitem>` 中相同。`<menu>` 标签不能包含代表菜单动作的图标作为内容，但可以通过合适的样式“溜进去”图标。它包含一个自动提供的类似箭头图标，提供存在子菜单的提示。`<menu>` 标签内部可以出现的唯一标签是 `<popup>`。`<menu>` 标签也用于菜单栏：

```
<menlist id="foo" editable="true">
```

### 7.4.6 `<menlist>`

`<menlist>` 标签是简单 XUL 菜单的顶层标签。它是 `<popup>` 标签的包装器。当弹出窗口未显示时，它为用户提供了可以观察和交互的对象。它显示一个显示当前选中菜单项的类按钮控件和一个用于显示菜单的下拉标记（dropmarker）。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```

这些属性与 `<menu>` 完全相同，只是 `disabled` 设置为 true 会禁用菜单。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```

这些属性与 `<menu>` 相同，只是 `disabled` 设置为 true 会禁用菜单。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```

这些属性与 `<menu>` 相同，只是 `disabled` 设置为 true 会禁用菜单。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```

这些属性与 `<menu>` 相同，只是 `disabled` 设置为 true 会禁用菜单。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```

这些属性与 `<menu>` 相同，只是 `disabled` 设置为 true 会禁用菜单。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```

这些属性与 `<menu>` 相同，只是 `disabled` 设置为 true 会禁用菜单。`<menlist>` 始终有一个选中的菜单项，只能包含一个 `<popup>` 标签。对 `<menlist>` 有特殊含义的属性有：

```
src label accesskey editable value
```
