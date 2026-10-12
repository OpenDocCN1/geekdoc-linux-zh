
- 2. 为 `a` 元素添加 `onmouseover` 事件处理器：
`<a href="http://www.nytimes.com/" onmouseover="">Visit the New York Times.</a>`

- 3. 在事件处理器中添加 `window.status=`。`window.status` 属性指定了状态栏中显示的内容：
`<a href="http://www.nytimes.com/" onmouseover="window.status=''">Visit the New York Times.</a>`

- 4. 添加要在状态栏中显示的文本，并用单引号 ('') 括起来。你使用单引号，而 `window.status` 语句被包含在双引号中，你必须将不同的引号嵌套使用：
`<a href="http://www.nytimes.com/" onmouseover="window.status='The latest news!''">Visit the New York Times.</a>`

- 5. 添加分号（表示语句结束），并在末尾添加 `return true`（紧在结束引号之前）。这告诉 JavaScript 解释器操作已完成并执行它：
`<a href="http://www.nytimes.com/" onmouseover="window.status='The latest news!';">Visit the New York Times.</a>`

如果你尝试这个示例，你会发现当鼠标悬停在链接上时，latest news! 语句出现在浏览器状态栏中。为了在鼠标离开链接时恢复状态栏，添加 `onmouseout` 事件处理器：

```
<a href="http://www.nytimes.com/" onmouseover="window.status='The latest news!';">
return true;"
onmouseout="window.status=''; return true;">
Visit the New York Times.</a>
```

#### JavaScript 中的注释

在 JavaScript 中添加注释（自己的笔记，而非标记）来跟踪脚本的作用。注释对于未来的参考非常有用，并且对分享 JavaScript 函数的人很有帮助。JavaScript 中的注释以两个斜杠开头：`//`。你需要在每行注释开头添加这些斜杠，如下代码段：

```
<script type="text/javascript" language="javascript">
function checkOut() {
  // 下面的循环如果在
  // 字段未填写则拒绝表单
  for (x=0; x<document.survey.elements.length;x++) {
    if (document.survey.elements[x].value == "") {
      alert("Sorry, 你忘记了一个必填字段。请再次试一次。");
      break;
    }
  }
  return false;
  if (document.survey.firstname.value.length <= 2) {
    alert("请输入您的全名。");
    return false;
  }
}
</script>
```

#### 为页面增加趣味

#### 切换图像

你可以使用 `mouseover` 和 `mouseout` 事件处理器来切换图像。这是一种常用技术，用户悬停在元素上时提供视觉反馈。例如，你可以在鼠标悬停在按钮上时更改图像，或者更改链接的颜色。

对于一组图像，你可以在函数中使用一系列 `if` 语句来执行更改。使用 `if` 语句可以让你的代码更易读，并方便日后修改脚本。你可以通过在文档的头部部分添加如下函数，添加更多语句，以便在不同的语文中重新排列图像：

```
function imagereplacer(place) {
  if (place==1) document.catbtn.src="image2.gif";
  if (place==2) document.catbtn.src="image1.gif";
}
```

`if` 语句检查 `place` 的值并相应地更改图像。你可以在文档的主体部分调用此函数。不需要在元素中编写完整的 `imagereplacer` 函数，只需在属性值中放入函数名，并在参数中为 `place` 设置所需的设置，如下所示：

```
<a href="http://www.example.com/">
<img src="image1.gif" width="50" height="10" border="0"
mouseover="imagereplacer(1)" alt="catbtn"
name="catbtn" onmouseout="imagereplacer(2)" />
</a>
```

如果你想做更多——例如更改图像并更改状态栏，或者如果你有多个不同的情况需要处理，而不想一个接一个地写 `if` 语句——你可以使用特殊的 JavaScript 关键字 `switch`，如下所示：

```
function imagereplacer(place) {
  case(1): document.catbtn.src="image2.gif";n  window.status="Second Image";  break;
  case(2): document.catbtn.src="image1.gif";n  window.status="First Image";  break; } }
```

使用这种技术，你可以列出所有选项。与之前的方法类似，`switch`语句列出了每个选项和要执行的操作，但使用 `switch`更容易执行多个或复杂的操作。在 `switch` 语句中，每个选项都是一个 `case`。在这个示例中，第一行调用了函数并包含了变量 `place` 的数字。你在 `switch` 语句中使用 `place`，它包含两个 `case`。如果 `place` 等于 1，则使用 `case(1)`，它将名为 `catbtn` 的图像的源属性（`catbtn.src`）设置为 `image2.gif`。

> 提示 如果你使用的是 JavaScript 早期版本的对象、方法、属性或事件处理程序，则不需要在语言属性中添加版本号。然而，如果你在使用较后版本的扩展功能（如你在这里使用的 `switch` 语句那样），并且函数定义在文档中，请在属性中包含版本号；例如，`language="javascript1.5"`。

从 `if` 语句版本的 `imagereplacer` 函数到 `case` 语句版本不需要对你的文档主体进行任何更改。当你将 JavaScript 函数放在文档头部时，你可以在不编辑代码中所有元素的情况下进行更改。

> 警告 尽可能在许多浏览器中测试你的 JavaScript 代码很重要。列表 3.2 中的代码在 Netscape Navigator 3 及更高版本以及 IE 4 及更高版本中均有效。然而，使用 `switch` 语句的代码在 IE 4 及更高版本中有效，但在 Netscape Navigator 中仅 更高版本有效。

#### 使用 onclick 和 onChange 事件处理程序

除了 `mouseover` 和 `mouseout` 事件处理程序外，你还可以使用 `onclick` 和 `onChange` 事件处理程序，它们分别在用户点击对象或按钮或更改表单字段时激活。包含这些事件处理程序与使用 `mouseover` 和 `mouseout` 事件处理程序类似。你可以使用 `onChange` 或 `onclick` 事件处理程序设置表单中的链接目标等。

#### 使用 onclick 提示用户

`onclick` 事件的一个方便用途是警报框（alert box），它是一个包含消息和 OK 按钮的小型对话框。例如，一个警报可以是关于该对象的扩展通知，例如“访问此页获取更多关于今年计划的消息！”

在最简单的情况下，你可以将事件处理程序（启动进程）与 `alert` 结合，如下：

```
<img src="infolink.jpg" alt="link" onclick="alert('Visit NYT!'); return true;" />
```
