
## PHP 表单身份验证

如果 PHP 基本身份验证（Basic Authentication）对你来说不是可行的解决方案，或者你不喜欢浏览器登录面板的外观，请不要担心；你还有另一个选项。与其依赖浏览器自带的标准内置登录窗口，你可以轻松创建自己的登录表单，甚至可以复用之前大部分 PHP 身份验证代码。将以下内容输入到 `phpauthforms.php` 文件中。请注意，其中大部分内容直接提取自你之前使用的 `phpauthbasic.php` 文件：

```php
<?php
// Define database constants
define('AUTH_HOST', 'localhost');
define('AUTH_USER', 'WebAuth');
define('AUTH_PASS', 'AuthPass');
define('AUTH_DB',   'WebAuth');

function check_login($username, $password)
{
   $ret = false;

   if ($username && $password)
   {
      // Check if login matches database values
      $conn = mysql_connect(AUTH_HOST, AUTH_USER, AUTH_PASS);

      if (mysql_select_db(AUTH_DB, $conn))
      {
         // Search for matches
         $result =
              mysql_query('SELECT COUNT(username) AS ucount
                           FROM Users
                           WHERE username="' . addslashes($username) . '"'
                           '  AND passwmd5="'   . md5($password)     . '"'
                           '  AND passwd_sha1="' . sha1($password)    . '"',
                           $conn);

         // Check if a match was found
         if (($row = mysql_fetch_array($result)) && $row['ucount'])
         {
            $ret = true;
            $_SESSION['username'] = $username;
         }
      }

      // Close connection
      mysql_close($conn);
   }

   return $ret;
}

session_start();
// Check if using valid credentials
if (! (isset($_SESSION['username']) || 
check_login($_POST['username'],
$_POST['passwd'])))
{
?>
<form method="post" action="testforms.php">
<label for="username">Username:</label>
<input type="text" id="username" name="username" maxlength="50" /><br />
<label for="passwd">Password:</label>
<input type="password" id="passwd" name="passwd" /><br />
<input type="submit" value="Log in" />
</form>
<?php
}
```

发生了什么变化？实际上并没有太多。关键的修改是在文件的末尾进行的：

```php
// Check if using valid credentials
if (! (isset($_SESSION['username']) || 
check_login($_POST['username'],
$_POST['passwd'])))
{
    exit;
}
```

与检查服务器变量 `PHP_AUTH_USER` 和 `PHP_AUTH_PW` 不同，你通过 HTTP POST 检查传递的登录凭据，其名称为 `username` 和 `passwd`。然后，就像基本身份验证示例一样，如果登录无效或未提供，则会向用户显示登录提示。在这种情况下，`attempt_auth()` 函数已被移除，在它原来被调用的位置，取而代之的是一个简单的 HTML 表单：

```php
?>
<form method="post" action="testforms.php">
<label for="username">Username:</label>
<input type="text" id="username" name="username" maxlength="50" /><br />
<label for="passwd">Password:</label>
<input type="password" id="passwd" name="passwd" /><br />
<input type="submit" value="Log in" />
</form>
<?php
exit;
}
```

## 第 7 章

若要使用此身份验证方法，你只需在想要保护的任意页面顶部包含此脚本即可。将此文件命名为 *testforms.php*（它必须与之前使用的表单的目标相匹配）：

```php
<?php
require_once 'phpauthforms.php';
echo "Authentication Successful";
?>
```

那么这种方法的优势是什么？首先是兼容性。使用简单的基于表单的 PHP 身份验证在几乎任何情况下都能正常工作，无论是否启用了 *safe_mode*，或者 Apache 是否使用其自身的 `.htaccess` 身份验证。这种解决方案唯一的实际缺点是，你必须自己编写登录表单，并按照你想要的方式设置样式，而不是依赖浏览器/操作系统来为你完成这些工作。

### 其他访问限制

除了通过用户名和密码限制访问外，你还可以使用 PHP 检查其他用户参数。一个常见的检查变量是用户的源 IP 地址。通过引用服务器变量 `$_SERVER['REMOTE_ADDR']`，你可以确保只有特定的 IP 范围被允许查看资源，或者相反，你可以阻止特定的 IP 地址。如果你正在为企业内网创建网站，你可以将访问限制在内部 IP 地址（假设你的网络使用了内部 IP）。例如，你可以决定只有 10.0.1.x 网络的成员可以查看网站的特定区域。另一个例子是 BBS 网站或网络论坛。很多时候，如果某人正在论坛发布垃圾信息，它们需要按 IP 地址禁止特定用户。

另一个值得检查的服务器变量是 `$_SERVER['HTTP_REFERER']` 变量。该变量持有之前查看的页面名称，可以帮助你消除某些类型的网络攻击。假设你创建了一个简单的表单，用于将数据保存到数据库、发送电子邮件，或者任何依赖有效用户输入的操作。你甚至可能付出了巨大努力来执行客户端输入验证，并指定了表单的最大长度。不幸的是，来自 Web 客户端的任何预期输入都可以轻松地通过外部表单进行破坏。任何站点攻击者都可以轻松复制你的表单 HTML 标记，然后根据需要对其进行修改——无论是用于信息收集、跨站脚本、SQL 注入，还是其他任何事情。

他们所需要做的只是制作该表单的副本，使其能够向你的站点提交不当数据，将其托管在他们自己的机器上，但使用绝对 URL 作为方法来向你的表单提交。当使用隐藏表单变量时，以及在 `php.ini` 中启用了 *register_globals* 时，这种类型的攻击可能会特别有害。

通过检查 `HTTP_REFERER` 值，只要确保输入来自你网站上的实际页面，你就可以消除大多数伪造表单攻击。

要查看 `HTTP_REFERER` 检查和 `REMOTE_ADDR` 验证的实际示例，请查看以下代码：

```php
<?php
// Check the referer
if (!preg_match('/http:\/\/localhost|
' (www\.example\.com/i/',
$_SERVER['HTTP_REFERER'] ))
{
    echo 'Invalid referer! ' .
    'We don't take kindly to spoofed forms in these parts.';
}

// Check to see if request came from internal users
if ( !preg_match( '/ (10\.\d(1,3)\.\d(1,3)\.\d(1,3))|
'( 172\.16\.\d(1,3)\.\d(1,3) )|
'( 192\.168\.\d(1,3)\.\d(1,3) ) /i' ,
$_SERVER['REMOTE_ADDR'] })
{
    echo 'Invalid client address! ' .
    'Who let YOU in here?';
}
?>
```

这段代码首先检查引用页面，以确保它来自 localhost 或预期的域（假设你已将其更改为匹配你自己的域），然后检查用户的 IP 地址，以确保它来自内部/私有 IP 范围。

PHP 可以做的另一件有助于限制某些类型访问的事情是，提供 CAPTCHA 图像用于注册表单。CAPTCHA 的全称是 "Completely Automatic Public Turing Test to Tell Computers and Humans Apart"（完全自动公共图灵测试，用于区分计算机和人类），这是一种测试，通常会在图像中呈现略带扭曲的文本。其想法是，尽管外观扭曲，但人类应该能够识别出文本实际内容，而计算机则不能。许多免费电子邮件和公告板网站使用此类技术来阻止自动机器人脚本注册滥用服务（例如发送垃圾邮件等）。

尽管目前处于 alpha 开发阶段，PHP Pear 库中的 `Text_CAPTCHA` 包提供了实现 CAPTCHA 功能的简单接口。可以在 http://pear.php.net/package/Text_CAPTCHA 找到 `Text_CAPTCHA`。

如果你想尝试 `Text_CAPTCHA`，你可以简单地使用 `pear install` 命令安装它：

```bash
pear install -f Text_CAPTCHA
```

你需要使用 `-f` 标志强制安装，因为 `Text_CAPTCHA` 目前不被 Pear 团队视为稳定版本，所以普通的非强制安装将会失败。还要注意，`Text_CAPTCHA` 依赖于 `Text_Password` 和 `Image_Text`（也是 alpha 版本）Pear 包，因此如果你还没有它们，你需要先安装这些包。

一旦它们都安装完毕，创建以下内容作为 `captchatest.php`：

```php
<?php
// Include the Pear class
require_once('Text/CAPTCHA.php');

// Set the options for the generated text;
$options = array(
```
