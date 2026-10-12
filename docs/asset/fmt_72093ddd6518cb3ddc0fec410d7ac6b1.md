
```html
if (document.survey.firstname.value.length <= 2) {
  alert("Please enter your full name.")
  return false;
}
```
<!-- -->
</script>
</head>
<body onload="checkout()">
<h1>Framed Document</h1>
<p>Content goes here</p>
</body>
</html>

- 2. 命名您要使用的函数，并在打开的 `body` 元素中添加 `onload` 事件处理器：
```html
<body onload="checkout()">
```
- 3. 添加 `if` 语句来确定文档是否在框架组内：
```html
<script type="text/javascript" language="javascript">
function checkout() {
  if (window.location != "top") {
    window.location = "top";
  }
}
</script>
```
- 4. 添加 `if` 语句执行时要执行的操作：
```html
<script type="text/javascript" language="javascript">
function checkout() {
  if (window.location != "top") {
    window.location = "top";
  }
}
</script>
```
- 5. 在脚本中函数处添加 `return` 语句：
```html
<script type="text/javascript" language="javascript">
function checkout() {
  if (window.location != "top") {
    window.location = "top";
  }
  return false;
}
</script>
```
- 6. 脚本已就绪，您需要在 `body` 元素中调用它：
```html
<body onload="checkout()">
```

### 列表 3.3：JavaScript 使用 onload 事件处理器
```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>Framed Document</title>
<script type="text/javascript" language="javascript">
<!--
function checkout() {
  for (x = 0; x < document.survey.elements.length; x++) {
    if (document.survey.elements[x].value == "")
alert("Sorry, you forgot one of the required fields. Please try again.")
break;
  }
  }
  return false;
  if (document.survey.firstname.value.length <= 2) {
  alert("Please enter your full name.")
  return false;
}
}
//-->
</script>
</head>
<body onload="checkout()">
<h1>Framed Document</h1>
<p>Content goes here</p>
</body>
</html>
```

### 使用 Cookie 追踪用户

`onload` 事件处理器在文档在 Web 浏览器中加载时激活。当用户点击链接（或遵循书签等）后，新页面将从服务器传输并加载到浏览器中。一旦必要的函数和打开的 `body` 元素加载，`onload` 事件处理器就会激活。

您可以使用此事件处理器来播放音频文件或启动烦人的弹出广告，但您也可以将其用于更实用的目的。例如，如果您有一个不使用框架（frames）的网站，您可能想使用 `onload` 事件处理器来确保您的页面没有加载到框架中。换句话，如果您负责 ASR Outfitters 网站，您不希望像图 3.1 所示被“框架化”。

Cookie 是您用来存储有关用户信息的对象，并可以通过 JavaScript 访问。您可以将 Cookie 视为识别浏览器的高科技标签，并向服务器传递其他信息。例如，如果您使用 Opera 浏览器访问 Amazon.com 并购买了一本书，Amazon 服务器会在您的计算机上放置 Cookie。当您下次使用该浏览器访问网站时，服务器会查找 Cookie 以识别您。计算机上的 Cookie 与存储在服务器上的关于您的信息匹配，例如您提供的信息和购买的书。在这种情况下，Cookie 可以帮助后续访问变得更容易，因为用户不需要重新输入信息。

尽管对用户的安全风险很小，但许多人对他人存储并读取关于他们的信息感到（理解地）敏感。由于由于，浏览器现在提供了处理 Cookie 的列表。早期版本的 Netscape Navigator 直接接受所有 Cookie。现在，大多数浏览器都能识别 Cookie 并在创建 Cookie 时警告用户，并允许用户接受或拒绝单个 Cookie，或者拒绝并非来自当前浏览网站的 Cookie。

> 提示
> 大多数浏览器包含处理 Cookie 的选项。在 Netscape Navigator 中，选择 Edit > Preferences > Advanced 来指定浏览器如何处理 Cookie。在 IE 中，前往 Tools > Internet Options > Privacy 查看 Cookie 选项。浏览器的默认设置都是启用 Cookie，因此只有当您想禁用 Cookie 或想在允许 Cookie 放置在计算机之前接收消息时，才需要更改选项。

![](img/6e99147f217994f89499215b2cff677f_112_0.png)

无论如何，Cookie 信息都不是公共财产；Cookie 仅为您存储信息，而不是供公开广播。此外，Cookie 通常只包含向服务器识别您的信息，然后服务器会将该信息（例如“啊，是 Jane Doe，来买更多书了”）与您的地址和购书历史相关联。当服务器向您的浏览器请求 Cookie 时，它只能读取它放置的 Cookie，而不能读取其他 Cookie、文件或信息。

# 第三章

你可以使用两种类型的 Cookie 来跟踪访问你网站的用户：

- 会话型 Cookie（Session cookies），它们仅持续到用户关闭浏览器为止
- 持久型 Cookie（Persistent cookies），它们会持续到你设置的过期日期为止

### 会话型 Cookie (Session Cookies)

假设你想保留一些关于用户浏览会话的信息，例如浏览过的页面或查看过的产品。你可以使用会话型 Cookie 实现。这段 JavaScript 不仅记录了用户的会话信息，还在用户进入和离开你的网站时向其发送消息。

![](img/6e99147f217994f89499215b2cff677f_113_0.png)

#### 提示

此此示例展示了 Cookie 的某些功能和威力。这可能会让某些用户反感。即使他们知道可以设置和使用 Cookie，他们可能也不希望被明显地提醒这一事实。

要实现会话型 Cookie，首先在页面加载时创建一个空 Cookie。从一个功能性文档开始，如下所示：

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<title>ASR Outfitters Cookie Form</title>
</head>
<body>
Cookie Bearing Document
</body>
</html>
```

现在，按照以下步骤操作：

1. 在文档 `head` 元素中添加一个函数，将 document cookie 设置为本地时间和日期：

```javascript
<script type="text/javascript" language="javascript">
<!--
function homeMadeCookies() {
```
