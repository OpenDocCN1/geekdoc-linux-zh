
| [x] Meet with friends and hang out |

## 图 5-4 用户可以从选框列表中选择多个属性。

单选按钮（Radio buttons）与复选框类似，它们都允许访问者根据预设选项进行选择。然而，在单选按钮的情况下，访问者仅允许选择一个选项，而不是一个或多个选项。这是通过使用相同的 `name` 值（在此例中性别）并在单选按钮中使用 `value` 属性来区分选项的。你必须在单选按钮中使用 `value` 属性，否则唯一选择功能将无法工作（见示例 5-6）。

### 示例 5-6 在表单中添加单选按钮

```html
<form method="get" action="http://www.myserver.com/cgi-bin/mailscript">
<h2>性别：</h2>

<input type="radio" value="female" name="gender" id="female" />女性<br />\n<input type="radio" value="male" name="gender" id="male" />男性<br />\n<input type="radio" value="undisclosed" name="gender" id="undisclosed" />不清楚
</form>
```

图 5-5 显示了示例 5-6 中描述的一系列单选按钮。

![](img/516568206e0e220ce5a120446a34b48d_90_0.png)

图 5-5 从单选按钮列表中进行选择。

复选框和单选按钮可以根据你的需要任何组合使用，以最好满足你的表单需求。主要的点是要记住，复选框可以用于多次提交，而单选按钮仅限于单次选择。

## 预选选中项目

在某些情况下，你会使用单选按钮或复选框，并希望某些项目被预先选中。例如，如果你的表单主要面向女性运动员，你可以通过 `checked` 属性显示带有预选选项的复选框或单选按钮。这会在预选选项中放置一个勾选标记或一个圆点（见示例 5-7）。

### 示例 5-7 在表单中添加单选按钮

```html
<form method="get" action="http://www.myserver.com/cgi-bin/mailscript/">
<p>请选择您最喜欢的放松方式：</p>

<input type="checkbox" name="reading" id="reading"br />
<input type="checkbox" name="sports" id="sports" checked="checked" />运动<br />
<input type="checkbox" name="games" id="games">电脑游戏

<p>您的性别是？</p>

<input type="radio" value="female" name="gender" id="female" checked="checked" />女性<br />
<input type="radio" value="male" name="gender" id="male" />男性<br />
<input type="radio" value="undisclosed" name="gender" id="undisclosed" />不清楚
</form>
```

图 5-6 显示了预选结果。

| 请选择您最喜欢的放松方式： | 您的性别是？ |

| :--- | :--- |

| ☐ 阅读 | ○ 女性 |

| ☑ 运动 | ○ 男性 |

| ☐ 电脑游戏 | ○ 不清楚 |

| | |

**图 5-6** 预选复选框和单选按钮选项。

## 使用表单菜单

存在两种类型的表单菜单：下拉菜单和列表菜单。两者都非常有用，并且可以通过多种方式进行修改以适应各种需求。

在表单中提供选项的最流行方法之一下拉菜单。当你有许多选项时，这类菜单特别有帮助，它们通常出现在州、国家等标准菜单中。

下拉菜单是通过将你的选择与 `select` 和 `option` 元素结合创建的（示例 5-8）。

### 示例 5-8 下拉菜单

```html
<form method="get" action="http://www.myserver.com/cgi-bin/mailscript/">
<p>州（美国西部地区）：</p>

<select>
  <option value="Arizona">亚利桑那</option>
  <option value="California">加利福尼亚</option>
  <option value="Colorado">科罗拉多</option>
  <option value="Nevada">内华达</option>
  <option value="Texas">德克萨斯</option>
  <option value="Utah">犹他</option>
</select>
</form>
```

图 5-7 显示了下拉菜单。

![](img/516568206e0e220ce5a120446a34b48d_92_0.png)

**图 5-7** 从下拉菜单中选择。

你可以为你的下拉菜单添加其他功能，包括用于复选框的 `checked` 属性，预选可以通过提供自定义方法来帮助提高表单的易用性。要在表单菜单中预选特定选项，只需使用 `selected` 属性即可：

```html
<option value="Nevada" selected="selected">内华达</option>
```

这会导致内华达显示为下拉菜单中的默认选择（见图 5-8）。

```
州（美国西部地区）：内华达
```

**图 5-8** 使用 `select` 属性在下拉菜单中创建默认选择。

你还可以创建一个列表菜单。它的制备方式与下拉菜单完全相同，但你可以在起始的 `select` 标签中添加一个与选项数量匹配的数值型 `size` 属性：

```html
<select size="4">
```

你可以通过将选择与 `select` 和 `option` 元素结合来创建下拉菜单（示例 5-8）。

（注：此处原文文本似乎不完整，已根据上下文逻辑翻译可见部分）

## 使用图形提交按钮

如果你希望提交按钮看起来与你的视觉设计融合得更紧密，可以创建一个图像并用它来代替提交过程。需要注意的是，这种技术并不同样适用于重置按钮，除非你添加了 JavaScript。在 HTML 本身方面，如果你愿意，可以使用自定义的按钮进行提交。

如示例 5-12 所示，我为表单创建了一个图形提交按钮，并使用带有图像属性的 `input` 元素将其插入表单中。

### 示例 5-12 使用图形提交按钮

```
<form method="get" action="http://www.myserver.com/cgi-bin/mailscript/">
  <input type="image" src="submit-button.gif" width="75" height="25" alt="submit" />
</form>
```

你会注意到标记中包含一个 `type` 属性的值 `image`。然后，你提供了按钮的图像源、宽度、高度、值以及备用文本（alternative text）。记住，这是一张图片，所以务必无论备用文本是什么都要进行区分。

图 5-14 显示了鼠标悬停在上面的样式化图形按钮。你会注意到鼠标指针变成了手形，就像任何其他链接一样，而且还会显示备用文本。

![](img/516568206e0e220ce5a120446a34b48d_97_0.png)

**图 5-14** 实现图形提交按钮。

> 飞跃

在大多数现代网页设计中，图像通常配合 CSS 用于提交按钮。你一定注意到，尽管目前为止描述的表单控件在实现方面既有效又简单，但它们并不美观。当你从本书后面开始为表单元素设置样式时，这个问题将会解决。

## 使用 label 提高表单的可访问性

从本质上，表单在可访问性方面比其他 HTML 元素更有要求。这很大程度上是因为本章中讨论的所有项目都与表单控件有关，这些是浏览器内置并由相应的 HTML 调用的组件。

对于视觉型的人来说，这是合理的。但对于那些通过朗读而非视觉查看表单的人来说，可能会可能会上下文。

`label` 元素允许将信息附加到指定的控件上。将此与属性结合使用，可以更详细地描述所使用的表单控件（参见示例 5-13）。

示例 5-13 使用 `label` 元素添加上下文
