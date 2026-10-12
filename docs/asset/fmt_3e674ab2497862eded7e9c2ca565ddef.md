
```
setcookie("count","1",time()+14400,"//","yourdomain.com",0);
setcookie("valid","yes",time()+14400,"/","yourdomain.com",0);
```

要访问会话变量，只需调用变量名，例如 `$count` 或 `$valid`。当你编写类似下面的代码时，PHP 会执行“魔术”：

```
echo "<$count</p>";
```

PHP 引擎获取 `$PHPESSID` 的值（存储在 cookie 中的唯一用户会话 ID），将其匹配到对应的临时会话文件，查找 `count`，找到它的值（假设为 "76"），并将其返回给你：

```
<p>76</p>
```

发送给用户的唯一 cookie 是持有 `$PHPESSID` 值的 cookie。

![](img/f8bb5053a1d20d75df488da4d4dbfceb_176_0.png)

如果问题是“如何在不设置多个 cookie 和频繁调用数据库的情况下维护用户特定信息？”，那么答案是使用 PHP4 中的会话管理函数。

## 启动会话并注册变量

我们将使用一个简单的访问计数器来熟悉会话和会话变量的概念。在页面的开始，调用 `session_start()` 函数。该函数有两个作用：第一，它检查该用户是否已启动会话；第二，它通知 PHP 引擎将在特定脚本内使用会话变量和其他会话相关的函数。

打开你喜喜欢的文本编辑器，创建一个名为 `count_me.php` 的文件并输入以下内容：

```php
<?php
// count_me.php
// 如果该用户不存在会话，则启动一个
session_start();
?>
```

接下来，在你的会话对象内部注册 `count` 变量：

`session_register('count');`

现在，只要这个会话存在，名为 `count` 的变量就存在。目前，该变量没有值。然而，如果你递增它，它的值将变为 "1"：

`$count++;`

将这些部分组合在一起，你就完成了以下操作：如果会话尚未启动则启动它；如果用户没有会话 ID 则为其分配一个会话 ID；注册名为 `count` 的变量并将其加 1，以表示用户首次访问页面的次数。

接下来，要显示 `$count` 会话变量的值并向用户展示他在当前会话中访问此面的次数，只需打印 `$count` 的值：

`echo "<P>You've been here $count times. Thanks!</p>"`

整个访问计数代码应该像这样：

```php
<?php
// count_me.php
// 如果该用户不存在会话，则启动一个
session_start();
session_register('count');
$count++;
echo "<P>You've been here $count times. Thanks!</p>"
?>
```

多次刷新页面，观察 `$count` 的值每次如何加 1。

## 使用会话管理用户偏好

除了简单的访问计数器之外，你还可以使用会话在用户访问网站时管理他们的偏好。例如，你可以让用户选择背景颜色、文本颜色以及显示网站内容的喜好字体。在这个三步示例中，你将启动一个会话，询问用户的显示偏好，在随后的页面中显示这些偏好，并允许用户更改主意并重置值。

第一步，创建一个名为 `session1.php` 的文件。在这一步中，如果会话不存在则启动并注册我们稍后使用的变量：`$body_color`、`$text_color` 和 `$font_family`：

```php
// 文件名：session1.php
// 如果该用户尚不存在会话，则启动一个
session_start();
if (!$PHPPSESSID) {
    session_register('body_color');
    session_register('text_color');
    session_register('font_family');
} else if ($body_color || $text_color) {
    __register('body_color');
    session_register('text_color');
    session_register('font_family');
}
?>
```

在这个示例中，`if-else` 循环非常重要。它只在 `$PHPPSESSID` 值不存在，或者 `$body_color`、`$text_color` 和 `$font_family` 未被创建或注册时才注册会话。由于用户将返回此会话显示他们的偏好，我们必须考虑到变量的值必须从会话中提取。如果我们只说：

```php
session_start();
session_register('body_color');
session_register('text_color');
session_register('font_family');
```

### 第 6 章：用户跟踪与会话管理

在页面顶部，每当页面加载时，这些变量的值都会被覆盖为空或新注册的值。接下来，创建一个简单的 HTML 表单，让用户选择他的偏好：

```html
<html>
<head>
<title>我的显示偏好</title>
<style>
P {font-family:Arial;font-size:10pt;font-weight:normal;}
H1 {font-family:Arial;font-size:16pt;font-weight:bold;}
</style>
</head>
<body BGCOLOR="#FFFFFF" TEXT="#000000">
<h1>设置偏好</h1>
<form method="POST" action="session2.php">
<p>选择背景颜色：<br>
<input type="radio" name="sel_body_color" value="#FFFFFF" checked></p>
<p>选择文本颜色：<br>
<input type="radio" name="sel_text_color" value="#000000" checked></p>
<p>选择字体：<br>
<input type="radio" name="sel_font_family" value="Arial" checked></p>
<p><input type="submit" name="submit" value="设置偏好"></p>
</form>
</body>
</html>
```

### PHP4 会话处理

等等！由于用户以后会返回此页面修改偏好，你还希望使用他的偏好来显示此页面。在 `<HTML>` 标签之前，添加以下代码来确定用户的偏好颜色，或者在尚未设置时定义默认值：

```php
if (!$body_color) {
    $body_color = "#FFFFFF";
}
if (!$text_color) {
    $text_color = "#00000";
}
if (!$font_family) {
    $font_family = "Arial";
}
```

如果这是用户第一次访问此页面，会话变量 `$body_color`、`$text_color` 和 `$font_family` 将被注册，但因为我们还没有给它们赋值。由于我们需要在第一个屏幕上显示某些颜色和字体，我们通过这些语句分配临时值。

为了让你的代码动态化，将原始的样式表代码替换为以下代码：

```css
<style type="text/css">
P {font-family:<?php echo $font_family; ?>;font-size:10pt;font-weight:normal;}
H1 {font-family:<?php echo $font_family; ?>;font-size:16pt;font-weight:bold;}
</style>
```

同时，将原始的 HTML BODY 标签替换为以下代码：

```html
<body BGCOLOR="<?php echo $body_color; ?>" TEXT="<?php echo $text_color; ?>">
```

你的代码应该像这样：

```php
<?php
// 文件名：session1.php
// 如果该用户不存在会话，则启动一个
session_start();

if (!$PHPPSESSID) {
    session_register('body_color');
    session_register('text_color');
    session_register('font_family');
}
?>
```

# 160 第6章：用户跟踪与会话管理
