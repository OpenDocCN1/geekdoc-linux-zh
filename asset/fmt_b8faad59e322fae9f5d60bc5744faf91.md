
<script type="text/javascript"> 

function getXMLHTTP() {

  var req = false;

  // first, try to instantiate the native object

  if (window.XMLHttpRequest) {

    try {

      req = new XMLHttpRequest();

    }

    catch(e) {}

  }

  // otherwise, try instantiating the ActiveX

  // object for IE.

  else if (window.ActiveXObject) {

    // just because creation of ActiveX objects

    // is supported, doesn't mean the XMLHttpRequest

    // object is available. So, let's try it.

    try {

      // try instantiating the newer version

      req = new ActiveXObject("Msxml2.XMLHTTP");

    }

    catch(e) {

      try {

        // otherwise, try the older version

        req = new ActiveXObject("Microsoft.XMLHTTP");

      }

      catch(e) {}

    }

  }

  // req will either be the reference to the

```

# 第 11 章

这段代码隐藏了在实例化 `XMLHTTP` 和 `XMLHttpRequest` 接口时浏览器的差异，并返回可用的版本。

如前所述，接收 `XMLHTTP` 请求的响应是通过触发事件和调用相应的事件处理器来处理的。下面的一组代码展示了处理 `ReadyStateChange` 事件触发的典型方式，并仅针对感兴趣的事件采取措施：

```javascript
<script type="text/javascript">
function handleReadyStateChange() {
    if (!request) return; // ignore unless complete
    if (request.readyState == 4) { // ignore unless successful.
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

此函数被分配为 `onreadystatechange` 处理器，并在 `ReadyStateChange` 事件触发时调用。它会忽略所有 `readyState` 不是 4（完成）且 HTTP 状态码不是 200（OK）的事件。完整且成功响应的 XML 主体被提取并传递给另一个函数进行处理。请注意，在获取 XML 主体后，`request` 对象被设置为 `false`。这是为了避免 Opera 浏览器中的一个 bug，该 bug 会导致当 `readyState` 变为 4 时有时触发多个 `ReadyStateChange` 事件。这可能会导致对单个响应多次执行操作。

### 处理响应

前几节中的代码相对标准。AJAX 应用的复杂性通常在于解释响应并根据其内容采取适当的操作。通常，适当的操作是通过 JavaScript 进行 DOM 操作。例如，如果你向服务器发出请求以检查用户名是否可用，并且服务器响应了此处所示的 XML 响应，那么你可能希望向用户显示一条消息，表明他或她需要选择不同的用户名。你还可能希望根据 XML 响应中包含的备选方案提供建议：

```xml
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<usernameResults>
    <username value="jessica" available="false" />
    <username value="jess" available="true" />
    <username name="jessica2005" available="true" />
    <username name="jessie" available="true" />
</usernameResults>
```

在此 XML 响应中，服务器指示该用户名不可用。此外，服务器还建议了可用的用户名变体。

你可以采用的传达此信息给用户的一种方法是使用 JavaScript 的 `alert()` 函数打开一个对话框。然而，一种更用户友好的方法可能是使用 DOM 操作在页面的某个部分添加一个 `DIV` 或 `UL` 元素。这提供了一种侵入性更小的消息形式，允许用户继续他正在与应用进行的交互，并在其方便时处理该消息。以下代码展示了如何遍历 XML 树并适当操作的示例：

```javascript
<script type="text/javascript">
function processResponse(oXML) {
    // exit if xml is undefined or doesn't have a documentElement
    if (!oXML) return;
    if (!oXML.documentElement) return;
    var doc = oXML.documentElement;
    // return a nodeList of all elements named username
    var unames = doc.getElementsByTagName('username');
    var msgs = new Array();
    // iterate through the username nodeList
    for (var i = 0; i < unames.length; i++) {
        var u = unames.item(i);
        var username = u.getAttribute('value');
        var availability = u.getAttribute('available');
        // make the available attribute more user-friendly
        if (availability == 'true') {
            availability = 'available';
        } else {
            availability = 'not available';
        }
        msgs[msgs.length] = 'Username ' + username + ' is ' + availability;
    }
    // create an unordered list element
    var ul = document.createElement('ul');
    ul.id = 'msg';
    // for each message, create a list item element and a text node containing
    // the message. The text node is a child node of the list item element, and the
    // list item is a child node of the unordered list element.
    for (var k = 0; k < msgs.length; k++) {
        var li = document.createElement('li');
        var txt = document.createTextNode(msgs[k]);
        li.appendChild(txt);
        ul.appendChild(li);
    }
```
