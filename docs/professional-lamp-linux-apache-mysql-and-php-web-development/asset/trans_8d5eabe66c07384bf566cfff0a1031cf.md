
# 第 11 章

```javascript
// interface or false on failure.
return req;
}
</script>
```

这段代码隐藏了在实例化 XMLHttpRequest 和 XMLHttpRequestRequest 接口时浏览器之间的差异，并返回当前可用的任何版本。

如前所述，对 XMLHttpRequest 请求的响应接收是通过触发事件和激活相应的事件处理程序来处理的。下面这组代码展示了处理 ReadyStateChange 事件触发的典型方式，并且只在你感兴趣的事件上执行操作：

```javascript
<script type="text/javascript">
function handleReadyStateChange() {
  if (!request) return;
  // ignore unless complete readyState
  if (request.readyState == 4) {
    // ignore unless successful.
    // You might choose to handle errors
    // rather than ignore them.
    if (request.status == 200) {
      // act on the response
      var xmlbody = request.responseXML;
      request = false;
      processResponse(xmlbody);
    }
  }
}
</script>
```

该函数被指定为 onreadystatechange 处理程序，并在 ReadyStateChange 事件触发时被调用。它忽略所有 readyState 不为 4（完成）以及 HTTP 状态码不为 200（OK）的事件。完整且成功响应的 XML 主体被提取并传递给另一个函数进行处理。请注意，在获取 XML 主体后，请求对象被设置为 false。这是为了避免 Opera 浏览器中的一个 bug，该 bug 有时会在 readyState 变为 4 时触发多个 ReadyStateChange 事件。这可能导致对单个响应多次执行操作。

## 处理响应

前面各节中的代码相对标准。AJAX 应用的复杂性通常在于解释响应并根据其内容采取适当的操作。通常，适当的操作是通过 JavaScript 对 DOM 进行操纵。例如，如果你向服务器发出请求以检查用户名是否可用，而服务器回复了此处所示的 XML 响应，那么你可能希望向用户显示一条消息，指示他或她需要选择不同的用户名。你可能还希望基于 XML 响应中包含的备选方案提供建议：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<usernameResult>
  <username value="jessica" available="false" />
  <username value="jess" available="true" />
  <username name="jessica2005" available="true" />
  <username name="jessie" available="true" />
</usernameResult>
```

在这个 XML 响应中，服务器指示该用户名不可用。此外，服务器还建议了一些可用的用户名变体。

向用户传达这些信息的一种方法可能是使用 JavaScript 的 alert() 函数打开一个对话框。然而，一种更用户友好的方法可能是使用 DOM 操纵在页面的某一部分添加一个 DIV 或 UL 元素。这提供了一种侵入性更小的消息形式，并允许用户继续他正在与你的应用进行的任何交互，并在他方便的时候处理该消息。以下代码提供了如何遍历 XML 树并适当操作的一个示例：

```javascript
<script type="text/javascript">
function processResponse(oXML) {
  // exit if xml is undefined or
  // doesn't have a documentElement
  if (!oXML) return;
  if (!oXML.documentElement) return;
  var doc = oXML.documentElement;
  // return a nodeList of all elements
  // named username
  var unames = doc.getElementsByTagName('username');
  var msgs = new Array();
  // iterate through the username nodeList
  for (var i = 0; i < unames.length; i++) {
    var u = unames.item(i);
    var username = u.getAttribute('value');
    var availability = u.getAttribute('available');
    // make the available attribute
    // more user-friendly
    if (availability == 'true') {
      availability = 'available';
    } else {
      availability = 'not available';
    }
    msgs[msgs.length] = 'Username ' + username + ' is ' + availability;
  }
  // create an unordered list element
  ul = document.createElement('ul');
  ul.id = 'msg';
  // for each message, create a list item
  // element and a text node containing
  // the message. The text node is a child
  // node of the list item element, and the
  // list item is a child node of the
  // unordered list element.
  for (var k = 0; k < msgs.length; k++) {
    var li = document.createElement('li');
    var txt = document.createTextNode(msgs[k]);
    li.appendChild(txt);
    ul.appendChild(li);
  }
  // obtain a reference to the main div element
  // and insert our new unordered list just before it
  var maindiv = document.getElementById('maindiv');
  maindiv.parentNode.insertBefore(ul, maindiv);
}
</script>
```

该函数处理来自请求 responseXML 属性的 XML，并向 DOM 添加一个 `UL` 元素。

正如你所见，DOM 操纵可能相当复杂。这个特定响应的优势在于，你可以收集用户名元素，无论它们在 XML 响应中的位置如何。通常，你无法直接做到这一点，你必须对 XML 响应的预期结构有一个了解，或者至少知道各种元素与其他元素的对应关系。如果 XML 格式发生任何修改，这可能会引起问题。将响应处理程序附加到 XML *元素* 级别，而不是响应级别，在抽象整个 XML 文档的细节方面显示出一些前景，允许客户端脚本专注于与该特定 DOM 操纵相关的局部结构。

例如，你可能希望在单独的 DOM 元素中显示替代的用户名，在这种情况下，你需要区分那些有或没有 `usernamealts` 父元素的用户名元素。然而，你不需要知道 XML 文档的其余部分是如何结构的，以及这些用户名元素在文档树中的位置在哪里。实现这个想法需要 XML 元素名称和处理函数之间的映射。这种实现的细节超出了本章的范围，但有一些文章更深入地探讨了这一主题。

## AJAX 库

如果这一切看起来令人不知所措，不要害怕。因为 *AJAX* 作为一种开发方法并不是全新的，有大量可用的库可以处理这些繁琐的工作。最近，随着对 *AJAX* 兴趣的复兴，可用的库数量急剧增加，现有的库也在迅速成熟。

### SAJAX

SAJAX (http://www.modernmethod.com/sajax/) 是简单的 AJAX 工具包，它在 PHP（以及许多其他语言中）有一个服务器端实现。本质上，使用该库，你可以在 PHP 中定义函数并通过 XMLHTTP 请求从客户端调用它们。要使给定函数支持远程过程调用，只需要调用一个 *SAJAX* 函数：`sajax_export('phpFunctionName');`。

不幸的是，当涉及到必要的 DOM 操纵时，SAJAX 并不能提供帮助。事实上，由于 *SAJAX* 将响应视为文本，并使用给定元素的 `innerHTML` 属性直接将响应插入到文档中（这通常被认为不如 DOM 操纵好），除非你自己实现字符串解析算法，否则无法进行 DOM 操纵。在 *SAJAX* 的常见问题解答页面（http://www.modernmethod.com/sajax/faq.php#ml）上，开发者将“不过度抽象”列为一个特性。XMLHTTP 通信的许多方面可以从抽象中受益匪浅，因此你可能认为 SAJAX 缺乏抽象是一个缺点。尽管如此，SAJAX 提供了一种简化客户端 AJAX 请求的服务器端处理以及客户端实例化 XMLHTTP 请求对象和发出必要请求的处理的方法。

### CPAINT

CPAINT (http://cpaint.sourceforge.net/) 是跨平台异步接口工具包。它支持纯文本和 XML 响应类型。此外，它还支持将响应直接作为 JavaScript 对象检索。该库成熟且积极开发中。

CPAINT 从函数调用中为你生成 XML，结果是某种非语义结构。另外，出于某种未知原因，生成的 XML 元素都是大写的。如果你提供的元素名称不是全大写的，该库会将其转换为全大写。库使用的文档有点难读，但每个部分都解释得很好，并为每个部分提供了一个简单的示例，帮助你理解其思想。

### JPSPAN

JPSPAN (http://jpspan.sourceforge.net) 的主要目标是弥补 JavaScript 和 PHP 之间的差距。它允许无缝将 PHP 类导入到 JavaScript 中。这意味着你可以在 PHP 中定义一个类，并像调用本地 JavaScript 对象一样调用其方法。在幕后，JPSPAN 正在向服务器发出请求以远程执行方法。其他库提供类似的功能，但它们无法接近 JPSPAN 所提供的抽象。JPSPAN 的文档和示例代码丰富且清晰。两者都是 wiki 格式，因此不断增长。代码本身干净易读，就像它生成的 XML 一样。此外，目前正在开发将 JPSPAN 嵌入 PHP 框架的初步工作，以使其更容易开发富客户端应用程序。

该库并没有减轻 DOM 操纵任务，但它确实很好地抽象了 XML-HTTP 的使用。不幸的是，它似乎存在支持 Opera 的问题，但它很好地支持基于 Mozilla 的浏览器和微软的 IE。此外，根据你的应用程序，JavaScript 和 PHP 之间的桥接可能对你没有多大好处，只是用对象和本地 JavaScript 访问替代了 XML 树遍历。由于创建 PHP 类的本地 JavaScript 版本涉及额外的开销，好处可能并不抵得上成本。然而，由于对抽象的出色利用，JPSPAN 可以让你几乎完全忽略 PHP 类如何提供给 JavaScript 的细节，并将注意力集中在应用程序本身的功能上。

还有许多其他支持 PHP 的 AJAX 库。你可以在 http://www.ajaxpatterns.org/AJAXFrameworks 了解各种 AJAX 库的更多信息。

## 何时不使用 AJAX

对 AJAX 的爆炸性兴趣是一把双刃剑。Macromedia 的 Flash 产品的使用也曾出现过类似的繁荣。客户因为 Flash 看起来很酷而要求使用它。与 Flash 一样，AJAX 引入了可用性和可访问性问题，其中许多问题在传统 Web 应用程序中已经得到解决。

