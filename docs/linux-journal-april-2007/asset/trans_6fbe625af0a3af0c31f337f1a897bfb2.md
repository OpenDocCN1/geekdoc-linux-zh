

# Dojo 事件与 Ajax

你的 Dojo 项目质量取决于你所建立的连接。

**Reuven M. Lerner**

上个月，我们开始探讨 Dojo，这是过去一两年间出现的最流行的开源 JavaScript 工具包之一。尽管如果你希望在 Web 应用程序中包含 Ajax 或复杂的客户端功能，使用工具包并非强制性要求，但它确实让事情变得更加轻松。特别是，这类工具包通常知道如何处理不同浏览器上 JavaScript 实现之间的许多细微差异。JavaScript 的标准化程度远高于过去，但在尝试跨多个平台工作时，仍然存在一些陷阱，而使用工具包可以免去你自己处理这些问题的麻烦。

在上个月的文章中，我们探讨了 Dojo 的打包系统、其对 JavaScript 语言的一些增强功能以及其富文本编辑器。本月，我们将探讨 Dojo 的其他一些功能，这些功能可能会引起现代 Web 开发者的兴趣，包括对事件和 Ajax 的支持。

## 事件处理器

JavaScript 编程的基石之一是使用事件处理器——即当特定事件发生时被调用的函数。例如，我们可以定义一个打开警报框的函数：

```javascript
<script type="text/javascript">
 function openAlert() {
 alert('Hello! This is an alert!');
 }
</script>
```

然后，我们可以告诉用户的浏览器，每当有人点击一段文本时，就调用我们的 openAlert 函数：

```html
<p onclick="openAlert();">This is a paragraph.</p>
```

在这个简短的示例中，有几个有趣的点需要注意。首先，在这种情况下，我们设置了 onclick 事件处理器。还有大约六个其他可选的事件处理器。在许多情况下，我们可能会设置多个事件处理器。这在 CSS 普及之前的日子里尤为普遍，当时 JavaScript 事件处理器常用于在鼠标悬停时改变图标的样式。

其次，事件处理器有时可以用在你意想不到的上下文中。例如，上面的 `<p>` 标签有一个 onclick 处理器。通常你不会想到点击一段文本，但我们可以这样做。这是现代一些拖放事件的基础。

第三，虽然 JavaScript 使得将处理器附加到特定事件变得相当容易，但仍存在一些繁琐之处。我们无法轻松定义多个事件处理器，也无法断开已定义的处理器连接。

## Dojo 事件

读到这里，你可能会好奇 JavaScript 事件处理器与使用 Dojo 进行 Ajax 和现代 Web 应用程序开发有什么关系。答案是，Dojo 在其众多包中的大部分功能都依赖于事件系统。例如，如果你想要使用 Dojo 的 Ajax 包，你需要使用 Dojo 事件将其连接起来。乍一看，这似乎有些限制；然而，Dojo 事件意外地容易理解。

作为一个简单的例子，让我们看看如何使用 Dojo 事件实现之前的 onclick 处理器。首先，我们需要修改事件处理函数，使其接受一个参数，即事件本身：

```javascript
<script type="text/javascript">
	function openAlert(e evt) {
		alert("Hello! This is an alert from Dojo!");
	}
</script>
```

接下来，我们必须将段落连接到该事件。而不是直接通过设置 onconnect 处理器来完成，我们为段落赋予一个 id 标签：

```html
<p id="para">This is a paragraph.</p>
```

现在，我们可以使用 Dojo 的 dojo.byId 函数——在某些方面类似于 Prototype 的 `$()` 函数——来获取节点本身：

```javascript
var para = dojo.byId('para');
```

最后，我们将段落连接到我们创建的处理器函数：

```javascript
dojo.event.connect(para, 'onclick', openAlert);
```

如果我们把所有内容组合在一起，就得到了清单 1 中所示的程序，我将其命名为 test-dojo.html。

### 清单 1. test-dojo.html

```html
<html>
<head>
<title>Testing JavaScript with Dojo</title>
<script type="text/javascript" src="/javascript/dojo.js"></script>
<script type="text/javascript">
dojo.require("dojo.event");
</script>

function openAlert(evt) {
alert('Hello! This is an alert from Dojo!');
}
</script>
</head>
<body>
<p id="para">This is a paragraph.</p>
<script type="text/javascript">
var para = dojo.byId("para");
dojo.event.connect(para, "onclick", openAlert);
</script>
</body>
</html>
```

你可能会注意到的一件事是该文件中有三个 `<script>` 标签。第一个位于文档头部，从服务器下载 dojo.js（Dojo 的主源文件）。第二个也位于文档头部，导入 Dojo 的事件包并定义我们的事件处理函数 openAlert。第三个也是最后一部分 JavaScript，用于将节点附加到事件，位于文档主体部分，紧跟在我们的 `<p>` 标签定义之后。这是因为我们只能为已经存在的对象设置事件处理器，这意味着必须在 `<p>` 标签本身之后。

如果你将该页面加载到浏览器窗口中，你会发现它的运行方式与之前的版本完全相同。鉴于这个版本更复杂，它为何更好可能并不显而易见：

### 高级 Dojo 事件

那么，这里有一个例子。假设你希望在事件处理器中调用某个特定对象的方法，而不是简单的函数调用。JavaScript 使得直接从事件处理器执行此操作变得困难。然而，dojo.event.connect 处理得相当简单，其四参数版本可以做到这一点。与之前一样，前两个参数是触发处理器的节点和事件。第三和第四个参数是被调用的对象和函数。例如：

```javascript
dojo.event.connect(eventObject, "onclick", handlerObject, "handlerMethod");
```

Dojo 还允许将一个事件连接到多个处理器。在非 Dojo 的 JavaScript 中，你只能通过使事件处理器成为一个进而调用其他函数的函数来实现这一点。使用 Dojo 事件，你可以连接任意数量的方法：

```javascript
dojo.event.connect(para, "onclick", testFormContents);
dojo.event.connect(para, "onlick", submitFormContents);
```

事件按照连接顺序触发。因此，在上述例子中，testFormContents 将在 submitFormContents 之前被调用。

请注意，Dojo 允许你根据需要添加相同的事件处理器两次。因此，请确保对于每个事件-处理器组合只调用一次 dojo.event.connect，以避免潜在奇怪且难以调试的问题。

Dojo 事件甚至有一种主题机制，允许你为事件通知创建多个通道。

假设你想为用户提供专家模式，这样他们就不必看到我们生成的所有烦人的警报框了。我们可以创建一个按钮，按下时从对象中移除事件处理器——哦，但这变得有点棘手了，特别是当我们有多个事件需要处理时。

解决方案是使用 dojo.event.disconnect，它的作用正如你预期的那样：

```javascript
dojo.event.disconnect(para, "onlick", testFormContents);
```

dojo.event.disconnect 要求参数与在 dojo.event.connect 中使用的参数完全相同。然而，一旦调用，该事件即被断开连接。事件系统的一个高级部分称为 advice（建议/切面），这个术语一直让我困惑，但在 Lisp 和面向切面编程的世界中很常见。Advice 的基本思想是你可以告诉系统在另一个函数之前或之后调用某个函数。（如果你使用过 Ruby on Rails，这就类似于过滤器。）这确实是一个高级功能，但在调试应用程序时可能很有用——而不是手动将有问题的函数中插入日志语句，你可以简单地为该函数添加 advice，在函数调用之前或之后调用记录器。甚至有一种针对 Dojo 事件的主题机制，允许你为事件通知创建多个通道。（这在某些方面类似于 Linux 和 UNIX 中的 syslog 设施。）因此，当特定事件在另一个对象上发生时，特定对象可以注册其兴趣。

### 清单 2 dojo-ajax.html

```html
<html>
<head>
  <title>Testing Ajax with Dojo</title>
  <script type="text/javascript" src="/javascript/dojo.js"></script>
  <script type="text/javascript"> 
    dojo.require("dojo.io.*");
    dojo.require("dojo.event.*");
    function ajaxAlert(evt) {
      var ajaxArgs = {
        url: "hello.php",
        error: function(type, data, evt){
          alert("An error occurred");
        },
        load: function(type, data, evt){
          alert(data);
        },
        mimeType: "text/plain",
        formNode: document.getElementById("myForm")
      };
      dojo.io.bind(ajaxArgs);
    }
  </script>
</head>
<body>
  <form id="theForm">
    <input type="button" id="theButton"
           value="Press here" />
  </form>
  <script type="text/javascript">
    var theButton = dojo.byId("theButton");
    dojo.event.connect(theButton, "onlick", ajaxAlert);
  </script>
</body>
</html>
```

![](img/3c4d8a97b5d96c835281dc0dacbc8551_24_0.png)

# 专家随行。

我们的产品开发团队不断同时处理多个截止日期紧张的项目。
作为团队的重要组成部分，Patrick 负责硬件兼容性、电源和性能测试以及操作系统验证，仅仅举几个例子而已。
他是 Rackform nSery AA43 的粉丝，该服务器配备了四颗下一代 AMD Opteron™ 处理器，因为他欣赏 AMD 的 Direct Connect Architecture（直接连接架构）在跨多个处理器分发工作负载方面的优势。Patrick 有许多工作要做，这就是他喜欢一款能处理大量工作的服务器的原因。

当你与 Silicon Mechanics 合作时，你获得的不仅仅是一台企业级质量的服务器——你还获得了一位像 Patrick 这样的专家。

![](img/3c4d8a97b5d96c835281dc0dacbc8551_24_1.png)

请访问 www.siliconmechanics.com
或拨打免费电话 866-352-1173

