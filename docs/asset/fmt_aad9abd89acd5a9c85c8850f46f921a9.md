
要使用这种认证方法，你只需将此类脚本包含在任何你想要保护的页面顶部即可。将此文件命名为 `testforms.php`（它必须与之前使用的表单目标相匹配）：

```php
<?php

require_once 'phpauthforms.php';

echo "Authentication Successful!";
?>
```

那么这种方法的优点是什么？首先是兼容性。使用简单的基于表单的 PHP 认证几乎适用于任何情况，无论是否启用 `safe_mode`，或者 Apache 是否使用其自身的 `.htaccess` 认证。这种解决方案唯一的真正缺点是，你必须自己编写登录表单，并按需进行样式设置，而不是依赖浏览器/操作系统来完成这项工作。

## 其他访问限制

除了通过用户名和密码限制访问外，你还可以使用 PHP 检查其他用户参数。一个常见的检查变量是用户的源 IP。通过引用服务器变量 `$_SERVER['REMOTE_ADDR']`，你可以确保只有特定的 IP 范围可以查看资源，或者相反，你可以屏蔽特定的 IP。如果你正在为公司内网创建网站，你可以将访问权限限制在内部 IP（假设你的网络使用了它们）。例如，你可以决定只有 10.0.1.x 网络的成员才能查看你网站的特定区域。另一个例子是 BBS 站点或网络论坛。通常，如果某人（例如）在论坛上发送垃圾信息，它们需要按 IP 封禁特定用户。

另一个值得检查的服务器变量是 `$_SERVER['HTTP_REFERER']` 变量。此变量保存了之前查看的页面的名称，可以帮助你消除某些类型的网络攻击。假设你创建了一个简单的表单，用于将数据保存到数据库、发送电子邮件或任何依赖有效用户输入的操作。你可能已经付出了很大努力来执行客户端输入验证，并指定了表单的最大长度。不幸的是，任何你可能期望从 Web 客户端接收的输入都可以通过外部表单轻松被破坏。任何网站攻击者都可以轻松复制你的表单 HTML 标记，然后按其需要修改它——无论是用于信息收集、跨站脚本、SQL 注入，还是其他任何目的。

他们所需要做的只是制作该表单的副本，以便向你的网站提交不当数据，将其托管在他们自己的机器上，但使用绝对 URL 作为方法将其发布到你的表单。当使用隐藏表单变量且在 `php.ini` 中启用了 `register_globals` 时，这种攻击可能特别有害。

通过检查 `HTTP_REFERER` 值，你可以消除大多数欺骗性表单攻击，只要你确保输入确实来自你网站上的页面即可。

若要查看 `HTTP_REFERER` 检查和 `REMOTE_ADDR` 验证的示例，请查看以下代码：

```php
<?php

// Check the referrer
if (!preg_match('/^http:\/\/(localhost)|' .
'(www\.example\.com)/i',
            $_SERVER['HTTP_REFERER']) )
        {
            echo 'Invalid referer! '
                  "We don't take kindly to spoofed forms in these parts.\n";
        }
        // Check to see if request came from internal users
        if ( !preg_match('/\b(\d{1,3}\.\d{1,3}\.\d{1,3})\b' .
                    '(172\.16\.\d{1,3}|192\.168\.\d{1,3}|' .
                    '$_SERVER['REMOTE_ADDR'])))
        {
            echo 'Invalid client address! '
                  "Who let YOU in here?\n";
        }
        ?>
```

此代码首先检查引用页面，以确保其来自 localhost 或预期域名（假设你已将其更改为匹配你自己的域名），然后检查用户的 IP 地址，以确保其来自内部/私有 IP 范围。

PHP 能做的另一件事，有助于限制某些类型的访问，是为注册表单提供 CAPTCHA 图像。CAPTCHA，即“用于区分计算机和人类的完全自动公共图灵测试”，是一种测试，通常会在图像中显示稍微扭曲的文本。其想法是，尽管外观扭曲，人类应该能够弄清楚文本实际说了什么，而计算机则不能。许多免费电子邮件和公告板站点使用这种技术来防止自动机器人脚本注册并利用服务发送垃圾信息等。

尽管目前处于 alpha 开发阶段，PHP Pear 仓库中的 `Text_CAPTCHA` 包提供了实现 CAPTCHA 功能的简单接口。`Text_CAPTCHA` 可在 http://pear.php.net/package/Text_CAPTCHA 找到。

如果你想尝试 `Text_CAPTCHA`，你可以简单地使用 `pear install` 命令安装它：

```bash
pear install -f Text_CAPTCHA
```

你需要使用 `-f` 标志来强制安装，因为 Pear 团队目前认为 `Text_CAPTCHA` 不稳定，所以普通的非强制安装将会失败。另外请注意，`Text_CAPTCHA` 依赖于 `Text_Password` 和 `Image_Text`（也是 alpha 版）Pear 包，因此如果你尚未安装这些包，需要先安装它们。

安装好所有包后，创建以下文件作为 `captchatest.php`：

```php
<?php

// Include the Pear class
require_once('Text/CAPTCHA.php');

// Set the options for the generated text;
$opts = array(
```

# 第 7 章

'font_size' => 25,

'font_path' => './../',

'font_file' => 'VerdanaMono.TTF'

);

// 创建 CAPTCHA 对象

$cap = Text_CAPTCHA::factory('Image');

// 使用随机文本初始化 CAPTCHA 对象

$r = $cap->init(250,100, null, $opts);

// 检查 CAPTCHA 对象是否有效

if (PEAR::isError($r))

{

 echo 'CAPTCHA 生成失败。';

 exit;

}

// 生成 PNG 格式的 CAPTCHA 图像

$png = $cap->getCAPTCHAasPNG();

// 在浏览器中显示图像

header('Content-type: image/png');

echo $png;

?>
```

当你在浏览器中运行这段代码时，你应该看到类似图 7.1 的内容。

![](img/fd2e7361878181c2b12e30301ff3e182_201_0.png)

`Text_CAPTCHA` 是如何知道你想要使用什么字符串的？它并不知道。当你初始化 CAPTCHA 对象时，你将 `null` 作为测试字符串传入：

```
// 使用随机文本初始化 CAPTCHA 对象
$r = $cap->init(250,100, null, $opts);
```

如果你想显式设置 `Text_CAPTCHA` 要渲染的文本字符串，只需将输入字符串从 `null` 更改为你想要的值：

```
// 使用随机文本初始化 CAPTCHA 对象
$r = $cap->init(250,100, 'computers be gone!', $opts);
```

在你的 PHP 脚本中需要检查的其他关键点包括本地文件名及其访问方式。请查看以下代码：

```
<?php

$content = file_get_contents('/path/to/content/' . $_POST['file']);

echo $content;

?>
```

这种代码经常可以在许多自制的 CMS 系统或某种自定义文档检索脚本中找到。不幸的是，这是一个巨大的安全风险。如果攻击者为 `file` 提交了值 `../../../../../etc/passwd` 会发生什么？如果服务器没有正确加固——很多服务器都没有——系统密码文件的内容将被直接回显到屏幕上。

你可以采取一些简单的步骤来帮助防止这种攻击。首先，如果你可以控制 Apache Web 服务器，请确保它作为一个非特权用户运行。无论 Apache 以什么用户身份运行——apache、nobody、www，都无所谓——确保该用户没有权限访问除合法网站文件以外的任何文件。

其次，确保你转义文件路径中提供的任何父目录访问点号，如下所示：
