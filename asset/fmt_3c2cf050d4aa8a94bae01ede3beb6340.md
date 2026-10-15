
## 列表 640 - 显示数据库中所有有效凭据

太棒了！Metasploit 自动在数据库中为我们存储了有效凭据。它还向我们显示了相关的主机、服务和凭据类型。

辅助模块在此结束。我们学习了如何搜索模块以及如何设置选项以符合我们的需求。我们运行了两个模块并探索了 Metasploit 如何显示和存储结果。Metasploit 提供了多种辅助模块，涵盖了各种协议和技术，如端口扫描、模糊和执行密码攻击。

## 20.1.3 利用模块 (Exploit Modules)

现在我们已经掌握了基础 MSF 使用和辅助模块的使用，让我们深入研究 MSF 的核心部分：利用模块。

### OffSec

使用 Kali Linux 进行渗透测试

利用模块通常包含针对漏洞应用程序和服务的利用代码。在本文编写时，Metasploit 包含超过 2200 个利用程序。每个程序都经过了仔细的开发和测试，使得 MSF 能够成功利用各种漏洞的服务。这些利用程序的调用方式与辅助模块相同。

在示例中，我们将利用一个利用模块获取目标系统 WEB1 的访问。假设我们识别出系统运行着 Apache2.4.49 Web 服务器，并且容易受到 CVE-2021-40739 漏洞扫描的影响。我们将尝试使用 Metasploit 及其利用模块来利用此漏洞并获取执行权限。

为此部分创建一个新的工作空间，并搜索与“Apache 2.4.9”相关的 Metasploit 模块。

```
msf6 auxiliary(scanner/ssh/ssh_login) > workspace -a exploits
```

```
[+] 添加工作空间: exploit

[+] 工作空间: exploit
```

```
msf6 auxiliary(scanner/ssh/ssh_login) > search Apache 2.4.49
```
