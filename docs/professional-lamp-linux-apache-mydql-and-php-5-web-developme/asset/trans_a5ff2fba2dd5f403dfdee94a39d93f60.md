
# 第 7 章

## 站点安全

当你在浏览器中运行这段代码时，你应该看到类似图 7.1 的效果。

![](img/ab27c6ac898db1f934d39fa127b14657_201_0.png)

```php
'font_size' => 25,
'font_path' => './../',
'font_file' => 'VerMono.ttf'
);

// Create a CAPTCHA object
$c = Text_CAPTCHA::factory('Image');

// Initialize the CAPTCHA object with random text
$r = $c->init(250,100, null, $opts);

// Check if CAPTCHA object is valid
if (PEAR::isError($r)) {
    echo 'CAPTCHA Generation failed.';
    exit;
}

// Generate the PNG CAPTCHA image
$png = $c->getCAPTCHAasPNG();

// Show the image in the browser
header('Content-type: image/png');
echo $png;
```

Text_CAPTCHA 是如何知道你想要使用的字符串的？它并不知道。当你初始化验证码对象时，你传入的测试字符串是 `null`：

```php
// Initialize the CAPTCHA object with random text
$r = $cap->init(250,100, null, $opts);
```

如果你想显式地设置由 Text_CAPTCHA 渲染的文本字符串，只需将输入字符串从 `null` 更改为你想要的值：

```php
// Initialize the CAPTCHA object with random text
$r = $cap->init(250,100, 'computers be gone!', $opts);
```

在你的 PHP 脚本中，其他需要检查的关键点包括本地文件名及其访问方式。请查看以下代码：

```php
<?php

$contents = file_get_contents('/path/to/content/' . $_POST['file']);

echo $contents;

?>
```

这种类型的代码经常出现在许多自制的内容管理系统（CMS）或某种自定义文档检索脚本中。不幸的是，它存在巨大的安全风险。如果攻击者提交文件值 `../../../../../etc/passwd` 会发生什么？如果服务器没有妥善锁定——而许多服务器并没有——系统密码文件的内容将会直接回显到屏幕上。

你可以采取几个简单的步骤来帮助防止此类攻击。首先，如果你能控制 Apache Web 服务器，请确保它以非特权用户身份运行。无论 Apache 以哪个用户身份运行——apache、nobody、www，都无所谓——请确保该用户没有权限访问除合法网站文件以外的任何文件。

其次，确保你转义文件路径中提供的父目录访问点，如下所示：

```php
<?php
$file = str_replace('../../', '', $_POST['file']);
$contents = file_get_contents('/path/to/content/' . $file);

echo $contents;

?>
```

如果可能，最好是给你的转义文件名加上路径前缀。这样，如果攻击者为文件值提供了绝对路径，它仍然会相对于指定文件夹运行。

## 网站攻击

每当你在公共互联网上发布一个站点时，它就面临被攻击的风险。虽然没有任何应用程序能真正达到 100% 的安全，因为新的漏洞利用和黑客技术每天都在被发现，但有一些类型的攻击你可以在 PHP 脚本中相对容易地加以防范。

### 滥用 register_globals

如果每一篇谈论 `register_globals` 的文章、书籍或文档片段都没有将其灌输到你的脑中，那么这里再次强调：将 `register_globals` 设置为 `on` 是一场等待发生的灾难。

如果你不熟悉 `register_globals`，它是 php.ini 中的一个设置，用于控制具有与表单元素或 Cookie 相同名称的变量的自动填充。在本章前面创建的登录表单中，有一个名为 `username` 的字段。通常，在禁用 `register_globals` 的情况下，在表单提交后访问 `username` 字段的唯一方法是使用 `$_POST` 或 `$_GET` 数组，具体取决于表单的方法。当启用 `register_globals` 时，`username` 字段可以通过 `$_POST` 或 `$_GET` 再次访问，但也可以作为 `$username` 使用。

自 PHP 4.2.0 以来，`register_globals` 的默认值是 *off*，但通常 Web 主机为了提供与假定存在且依赖 `register_globals`=`on` 的旧脚本的兼容性，会重新启用 `register_globals`。不幸的是，这为恶意用户提供了主要的攻击途径。当启用 `register_globals` 时，PHP 按照 `variables_order` 设置中指定的顺序评估环境、表单、`cookie` 和服务器变量。如果服务器使用“推荐”的设置文件，首先设置 `GET` 变量，然后设置 `POST` 并覆盖任何匹配的 `GET` 值。接着设置 `cookie` 值，随后是服务器变量，覆盖之前设置的任何匹配值。

虽然这种行为看起来很方便，但使用克隆表单或伪造的 Cookie 信息很容易对其进行利用。关于它可能被如何利用的例子，请查看以下 PHP 代码：

```php
<?php
    if (user_is_admin())
    {
        $access_level = 10;
    }
    show_menu($access_level);
    // ... and so on ...
?>
```

在这种假设情况下，脚本调用 `user_is_admin()` 函数来确定用户是否为管理员。如果是，`$access_level` 变量会被设置为 10，并且可以想象，随后脚本中可能会显示完整的管理人员界面。

如果启用了 `register_globals`，请求文件并将期望的访问级别附加到查询字符串中是一件极其简单的事情，如下所示：

```
http://www.example.com/file.php?access_level=10
```

现在，如果脚本被调用并附加了该 `access_level`，无论用户是否真的是管理员，由于 `register_globals` 以及 PHP 不要求变量初始化，`$access_level` 变量会在脚本开始时自动设置为 10。

幸运的是，避免此类陷阱相对容易。请确保在禁用 `register_globals` 的情况下编写代码，使用正确的 `$_GET` 和 `$_POST` 超全局变量，初始化可能不安全的变量，并确保在开发和测试站点时将 `error_reporting` 设置为 `E_ALL`。

如果你无法在 php.ini 中禁用 `register_globals`，如果 Apache 中正确启用了该功能，你可以使用 `.htaccess` 文件将其关闭：

```
php_flag register_globals off
```

### SQL 注入攻击

另一种具有更高潜在破坏性的脏数据攻击是 SQL 注入攻击。与 `register_globals` 攻击结合使用，或者仅仅通过普通的 Web 表单，SQL 注入攻击就是在本应输入无害数据的地方插入恶意 SQL 语句。

SQL 注入利用的是输入清洗和数据验证的缺失——即在 PHP 构建的 SQL 查询中盲目使用数据。请查看以下访问本章前面创建的 WebAuth 数据库的例子：

```php
<?php
$username = $_POST['username'];
$conn = mysql_connect(AUTH_DB, AUTH_USER, AUTH_PASS);
mysql_select_db(AUTH_DB, $conn);
$sql = "SELECT * FROM Users WHERE username='" . $username . "'";
mysql_close($conn);
?>
```

看起来相当无害，对吧？你会期望它愉快地接受表单发送的 `username` 变量值，并查找与该特定用户名相关的所有列。这段代码的问题在于 SQL 查询。注意 `$username` 变量在发送到数据库之前没有任何形式的验证、清洗或准备。在大多数情况下，你可能不会注意到任何异常，而且它几乎不会抛出错误。

然而，当在发送表单的用户名字段中输入以下值时，事情会迅速变得恶劣：

```
'; DELETE FROM Users; SELECT '0wmjD' AS username FROM Users WHERE '1'='1
```

仔细观察这个值正在发生什么。它首先终止 `$username` 变量附加之前的查询部分，删除 `Users` 表中的所有信息，然后执行攻击者选择的查询，只是为了结束查询并匹配最终的单引号。

