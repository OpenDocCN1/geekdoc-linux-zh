
你可以通过访问你想要修改的项并更新 `checked` 属性的值为 `FALSE`（如果是取消选中）或 `TRUE`（如果是选中）来选择或取消选择选项。

在 `SELECT` 输入框的情况下，你可以单独访问每个选项，甚至可以添加或删除选项。要访问特定选项，我们使用 `options` 数组，该数组由每个 `select` 对象自动生成。每个选项的值可以通过 `.value` 进行修改，或者选项旁边的文本可以通过 `.text` 进行修改。要从 `select` 菜单中删除一个选项，只需将该选项设置为 `null` 即可。要添加新选项，我们创建一个 `Option` 类型的对象，为它的构造函数提供显示在旁边的文本以及与该选项关联的值。注意，所有创建的选项都放置在菜单的末尾，但由于所有选项都在 `options` 数组中，你可以使用数组操作来交换元素。你也可以随时通过访问 `select` 区域的数据成员 `selectedIndex` 来检查哪个选项被选中了。例如，当你选择菜单时更改其中的文本，你可以：

```javascript
document.myForm.mySelect.options[document.myForm.mySelect.selectedIndex].text = "This was the selected option";
```

在 JavaScript 中你可以做的最后的一件事是强制提交表单（即使没有“提交”按钮！）。只需直接使用表单对象的 `submit()` 方法即可。例如

```javascript
document.myForm.submit();
```

# 194 浏览器编程

这在表单上非常有用，因为你可以在提交表单之前验证表单的内容，并告知用户任何错误，以便他们在通过表单发送数据之前进行修正。要实现这一点，你只需要在“提交”按钮上添加一个 `onClick` 事件，调用验证所有数据的方法，如果遇到问题则返回 `false`。

对于包含文本区域的表单，有两种方法非常有用。理想情况下，在编写表单时，你应该包含一些 JavaScript 在将任何数据发送到 PHP 脚本之前对表单进行验证。这允许在客户端完成第一层数据验证，这比将数据传输到 PHP 脚本快得多；PHP 脚本将验证数据；如果发现错误，则将客户端重定向回第一个页面。在 JavaScript 中进行验证可以让你避免（例如，避免与服务器频繁往返的负担）。表单中常见的典型问题是文本框中输入的数据类型错误；例如，你可能期望一个电子邮件地址，但用户留空了字段，或者输入了不是地址的文本。在你想告知用户错误并更改数据的情况下，可以调用 `focus()` 和 `select()` 方法，将用户置于需要更改的字段中。这些方法应该从表单元素对象调用；例如 `document.myForm.input.focus()`。`focus()` 方法将赋予输入框焦点，而 `select()` 方法允许你选择整个输入的文本。当字段需要更改时，没有比比对问题字段执行 `focus()` 然后执行 `select()` 更好的做法了。这样用户只需要输入新数据，就会自动覆盖之前的文本。

最后一个有用的点是，意识到任何通过 `document` 访问的对象都可以存储在变量中，以便决定其输入类型。例如，你可以：

```javascript
var myButton = document.myForm.button;
```

之后，你就可以通过简单输入 `myButton` 来访问你的按钮了。

## 定时器

JavaScript 有创建两种主要类型定时器的能力：单次定时器和被称为“间隔”`intervals` 的定期定时器。单次定时器允许你决定在调用函数之前等待特定的毫秒数。例如，使用函数 `setTimeout`，你可以这样操作：

```javascript
var timerID = setTimeout("myFunction()", 5000);
```

这将创建一个定时器，它将在等待 5 秒后调用 `myFunction()`。返回的 ID 非常重要，因为如果你想停止定时器，将需要它。只需使用 `clearTimeout(timerID)` 即可停止超时。

定期定时器类似于超时，区别在于它们在每次超时后都会重启定时器。情况下使用的函数是 `setInterval('functionName', time)`；例如：

```javascript
var timerID = setInterval('alert('Hello'), 5000);
```

这将每 5 秒运行一次 `alert('Hello')`。对于超时任务，你可以通过执行 `clearInterval(timerID)` 来清除间隔。

# 练习时间！

现在你已经了解了事件编程的基础知识，尝试编写一个包含按钮的脚本，记录它被点击的次数。注意定义在函数外的变量被视为全局变量。它们在任何函数内部都是可访问的，因此你可以利用这一点作为优势。还要记住，按钮上的文本是由其属性值定义的。

另一项工作是创建一个事件日志。创建一个带有不同类型输入的表单，例如单选按钮、普通按钮、密码字段以及文本区域。现在，确保你至少有一个大型文本区域，用它跟踪你想测试的所有事件，并让每个事件在大型文本区域的末尾显示最新事件。记住，你可以通过标签的 `value` 字段访问文本区域的内容，还可以使用加号 `+` 符号拼接文本。此外，如果你想包含一个“清除”按钮，可以包含一个“重置”按钮，也可以创建一个带有事件的普通按钮，通过以下操作在文本区域的 `value` 字段写入空字符串 `""`：

```javascript
document.myForm.textArea1 = "";
```

最后，使用间隔或超时创建一个焦点切换器。将一组图片的 URL 存储在数组中，并设置一个定时器每几秒切换一次图片。

# 16

# 窗口与帧

在上一章中，我们学习了 `window` 对象及其内容，专注于 `document` 对象。本章的目标是查看 JavaScript 如何在窗口和帧之间进行通信，这实际上意味着在网页之间进行通信。

## 帧与 JavaScript

当你在网页中创建一个帧时，每个帧都有自己的 `window` 对象；因此，可以访问每个独立帧包含的任何窗口对象。你可以通过访问帧的 `name` 字段来检查任何已创建帧的名称，访问方式为编写 `window.name`。为了让我们开发者更方便，你还可以访问任何帧的父帧以及任何子帧。想象你创建了一个包含 `frameLeft` 和 `frameRight` 两个帧的帧集。当你处于任何一个帧中时，只需输入 `window.parent` 即可访问创建这些帧的页面。这将引用父窗口对象；从那里，你可以访问父页面中定义的任何内容，就像你在父页面中一样，包括函数、变量和表单引用。

# 200 窗口与框架

## frameMenu:

```html
<HTML>
<HEAD>
<SCRIPT LANGUAGE="JavaScript">
  function select_onclick() {
    window.top.frameTitle.change_button();
    window.parent.frameBody.change_text();
  }
  var test = 0;
</SCRIPT>
</HEAD>
<BODY>
<FORM name="myForm">
  <SELECT name="mySelect" onchange="select_onclick()">
    <OPTION value=0>阿利坎特
    <OPTION value=1>霍霍肯
    <OPTION value=2>纽约
    <OPTION value=3>巴塞罗那
  </SELECT>
</FORM>
</BODY>
</HTML>
```

## frameBody:

```html
<HTML>
<HEAD>
<SCRIPT LANGUAGE="JavaScript">
  function change_text() {
    var myTextArea = document.myForm.myText;
    var menuSelect = window.parent.frameBody.document.myForm.mySelect;
    myTextArea.value = myTextArea.value + menuSelect.options[menuSelect.selectedIndex].text + "\n"
  }
</SCRIPT>
</HEAD>
<BODY>
<FORM name="myForm">
  <TEXTAREA name="myText" COLS=65 ROWS=25></TEXTAREA>
</FORM>
</BODY>
</HTML>
```
