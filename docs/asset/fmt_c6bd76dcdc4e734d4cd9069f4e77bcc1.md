
发送电子邮件和即时消息，试图收集其他用户的用户名和密码。解决这个问题的简单方法是发送一条消息，提醒 AOL 人员：在任何情况下都不会向用户索取此类信息。

## 构建功能性且安全的应用程序

```html
<html>
<head>
<title>demo form</title>
<script language="JavaScript">
// 检查邮箱地址：查找 @
function isEmail(elm) {
  if (elm.value.indexOf("@") != -1 &&
      elm.value.indexOf(".") != -1 &&
      elm.value != "")
    return true;
  else return false;
}

// 检查为空和空
function isFilled(elm) {
  if (elm.value == "" ||
      elm.value == null)
    return false;
  else return true;
}

// 检查电话格式
function isPhone(elm) {
  var elstr = elm.value + "";
  if (elstr.length != 12) return false;
  for (var i = 0; i < elstr.length; i++) {
    if ((i < 3 && i > -1) ||
        (i > 3 && i < 7) ||
        (i > 7 && i < 12)) {
      if (elstr.charAt(i) < "0" ||
          elstr.charAt(i) > "9") return false;
    }
    else if (elstr.charAt(i) != "-") return false;
  }
  return true;
}

function isReady(form) {
  if (isEmail(form.Tf_1) == false) {
    alert("请输入邮箱地址.");
    form.Tf_1.focus();
    return false;
  }
  if (isFilled(form.Tf_2) == false) {
    alert("请输入您的姓名.");
    form.Tf_2.focus();
    return false;
  }
  if (isPhone(form.Tf_3) == false) {
    alert("电话号码应为 xxx-xxx-xxxx.");
    form.Tf_3.focus();
    return false;
  }
  return true;
}
</script>
</head>
<body>
<form name="demo" onsubmit="return isReady(this)">
  邮箱: <input type="text" name="Tf_1"><br>
  姓名: <input type="text" name="Tf_2"><br>
  电话: <input type="text" name="Tf_3"><br>
  <input type="submit" value="提交">
</form>
</body>
</html>
```

## 图 2.5 Demo 表单

![](img/46354bfda2927ab470de2340d852da82_89_0.png)

## 图 2.5 续

## 欢迎来到奇的 CGI 世界

<form method="POST" name="demo" onSubmit="return isReady(this)" action="../cgi-bin/demo">

```
<table border="0" width="100%">
<tr>
  <td width="25%" align="right">电子邮件地址：</td>
  <td width="75%" align="left"><input type="text" name="Tf_1" size="32" maxLength="32"></td>
</tr>
<tr>
  <td width="25%" align="right">姓名：</td>
  <td width="75%" align="left"><input type="text" name="Tf_2" size="20" maxLength="30"></td>
</tr>
<tr>
  <td width="25%" align="right">电话号码（可选）：</td>
  <td width="75%" align="left"><input type="text" name="Tf_3" size="12" maxLength="12"></td>
</tr>
<tr>
  <td width="25%" align="right">评论：</td>
  <td width="75%" align="left"><textarea wrap="physical" name="Ta_1" rows="5" cols="20"></textarea></td>
</tr>
</table>
```

```
<tr>
  <td><input type="submit" value="搜索"></td>
</tr>
```

</table>

</form>

</body>

</html>

```

这里在这里，这里没有什么特别的，也绝对没有任何安全性可言。那么包含 JavaScript 呢？它没有为表单增加安全性吗？其实并没有。这种 JavaScript 非常常见，我正因为这个原因才包含它。很多人（错误地）认为它在强制安全检查，确保用户正在向必填字段中输入数据，甚至进行了一些格式检查。即使是技术最底浅的人，花一点点精力就能禁用 JavaScript。此外，许多公司会通过防火墙过滤作为 JavaScript 的活动脚本和 ActiveX，而有些人甚至使用完全不支持它们的浏览器！

我把 JavaScript 看作是给用户的便利工具，而不是安全措施。因为 JavaScript 是在客户端浏览器上执行的，它可以允许对表单数据进行即时验证，而无需等待 Web 服务器的响应。但因为它是运行在客户端机器上的，一切防线都失效了。你应该始终记住，客户端机器（通常来说）完全在你的控制之外，完全在他们的控制之下。他们可以对数据做任何他们想做的事。我会始终验证表单数据，对于可能犯了错误或拼写错误的良好用户，这段 JavaScript 会快速提醒他们并节省他们一二秒的时间。对于恶意用户或那些禁用了 JavaScript 的人，我们仍然想要确保数据是合理的。

![](img/46354bfda2927ab470de2340d852da82_91_0.png)

## 第 2 章 • 如何避免变成“代码行工”

所以，在图 2.5 中，我们有了 Web 表单。现在我们需要的是一个表单处理器。这就是网关接口（CGI）大用场。让我们从一个短小的 Perl 程序开始来收集上面的输入。

请记住，从现在开始我省略了几行代码。还要注意，由于我们需要存储收集的数据，我正将其放入一个简单的 MySQL 数据库中。Perl、Cold Fusion、PHP、ASP、C/C++ 等都非常擅长连接并与数据库通信。作为一个初露茅庐的应用开发者，你可能已经熟悉了一些简单的 SQL 语法，而这你理解这些示例所需的全部内容。

为了简洁起见，假设 Perl 示例的前几行代码如图 2.6 所示。

## 图 2.6 收集输入

```perl

#!/usr/bin/perl -w

use strict;

use CGI qw::standard;

use DBI;

use CGI::Carp qw/fatalsToBrowser;

```

所有代码示例均在运行 Solaris 8 的 Sun Microsystems 企业级机器上测试过，该机器使用 perl 5.03。Web 服务器是 Apache 1.3。对于我们中的新手来说，图 2.6 中的第一行代码告诉调用的 shell 去寻找 Perl 解释器；接四行导入了一些方便的模块来让我们的生活更轻松。从简洁的角度来看，这些中最重要的是由 Camel 开发的 CGI.pm 模块。CGI.pm 为我们提供了一个 `param()` 函数，它消除了处理晦涩数据的需要。随着我们的进展，我们将看到它是多么简单。这是我们的第一次尝试，如图 2.7 所示。

## 图 2.7 param() 函数

```perl

print header;

my $first = param('Tf_1');

my $second = param('Tf_2');

my $paragraph = param('Ta_1');

```

```perl

my $statement = "UPDATE demo SET

first = '$first',

second = '$second',
```
