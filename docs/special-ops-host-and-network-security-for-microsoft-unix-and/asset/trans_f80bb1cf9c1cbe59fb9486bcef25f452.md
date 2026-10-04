

# 第 9 章 • 攻击与防御 Microsoft Terminal Services

由于你可以从 Terminal Services 会话内部远程控制会话，因此在尝试镜像（shadow）之前，你需要先连接到 Terminal Server。下一个命令显示了 shadow 命令的语法：

```
C:\shadow
```

监控另一个 Terminal Services 会话。

```
SHADOW (sessionname   | sessionid) [{/SERVER:servername] [/V]
sessionname             标识名为 sessionname 的会话。
sessionid               标识 ID 为 sessionid 的会话。
/SERVER:servername      包含会话的服务器（默认为当前）。
/V                       显示操作信息。
```

例如，要镜像 rdp-tcp#2 会话，你需要输入以下命令：

```
C:\shadow rdp-tcp#2
```

在协商远程控制许可时，你的会话可能会冻结。请等待...

> 注意
要结束远程控制会话，请按 Ctrl + 数字键盘上的 * 键。如果你使用的是笔记本电脑且没有数字键盘，你可能需要使用 Ctrl+Fn+0 来模拟转义序列。

如果权限正确，你还可以在 TS 会话内部使用 tcon 命令连接到另一个用户的会话：

```
C:\tcon
将用户会话附加到终端会话。
```

```
TSCON {sessionid | sessionname} [{/DEST:sessionname]
[/PASSWORD:pw] [/V]
sessionid               会话的 ID。
sessionname             会话的。
```

![](img/729efc56f204a2ebffb8295c3a2dfdfb_492_0.png)

# 攻击与防御 Microsoft Terminal Services • 第 9 章 469

```
/DEST:sessionname 将会话连接到目标会话 sessionname。
/PASSWORD:pw 标识会话的所有用户的密码。
/V 显示所执行操作的信息。
:\>
```

# Terminal Services Manager

图 9.13 显示的 Terminal Services Manager允许管理员监控 Terminal 服务器的会话、用户和进程。在这里可以很好地执行连接到另一个用户会话以及断开用户等操作。不要忘记控制台无法使用 Shadow 连接到会话；你需要处于 TS 会话中。

# 图 9.13 Terminal Services Manager

![](img/729efc56f204a2ebffb8295c3a2dfdfb_493_0.png)

# Terminal Services Configuration Connections

Terminal Services Configuration Connections (TSCC) 允许配置服务器设置（如图 9.14 所示）以及 RDP-Tcp Properties（如图 9.15 所示）。该工具在 Windows 2000、Windows XP 和 Windows Server 2003 中可用。你应该能够在 RDP-Tcp Properties 中设置以下基本设置：

- 通用加密级别：高
- 登录设置：始终提示密码
- 网络适配器：基于网卡指定属性

RDP-Tcp 属性在 Windows 2000 和 Windows XP/Server 2003 之间存在细微差异，两者都允许将连接权限应用于用户和组。图 9.16 显示了 Windows 2000 Server 上的权限卡。

# 图 9.14 TSCC 可以配置服务器设置

![](img/729efc56f204a2ebffb8295c3a2dfdfb_494_0.png)

# 图 9.15 .NET 下的 TSCC RDP-Tcp Properties (Windows Server 2003)

![](img/729efc56f204a2ebffb8295c3a2dfdfb_494_1.png)

# 图 9.16 Windows Server 权限设置

![](img/729efc56f204a2ebffb8295c3a2dfdfb_494_2.png)

# 第 9 章 • 攻击与防御 Microsoft Terminal Services 467

## 攻击 Terminal Servers

使用 Windows 2000 作为生产服务器系统的组织很可能使用 Terminal Services 进行远程管理或作为进入其安全网络的跳板。如果配置得当，它将很好地满足这些用途。然而，如果安装在不安全的系统上，它将帮助黑客攻击其他可能受内部路由器或防火墙保护的主机或网络。如果攻击者面临命令行挑战，她现在将拥有一个 GUI，可以在其中下载并安装她选择的应用程序（自动化漏洞扫描工具等）。

取决于 TS 的配置，破解可能简单到攻击者尝试在没有密码的情况下以 Guest 登录。如本文稍后所示，一旦攻击者获得了对受害者 TS 的交互式访问，就可以轻松地上传并执行权限提升漏洞来成为管理员。如果攻击者足够狡猾，他可以在不产生任何真实 IP 地址日志的情况下做到这一点。一旦他拥有了服务器，他将拥有一个可以发起未来攻击的据点。

在大约年前的一次内部渗透测试中，我被指派从用户 LAN 渗透安全的管理网络。导致胜利的步骤可以使用其他技术完成，但在这种情况下，破解双网卡 Terminal Server 上的 IIS Web 服务器就完成了任务。Terminal Server 本身并没有错，但一旦我利用 Web 服务器漏洞创建了属于自己的管理员账户，它确实为我的攻势增添了助力。由于这个原因，我认为 TS 是 Windows 服务器的漏洞催化剂。

## 端口扫描

在内部网络中寻找 Terminal Servers 通常并不。尽管存在将它们迁移到备 TCP 端口的能力，但管理员并没有花时间进行此类配置更改。

如你所知，TS 默认运行在 TCP 3389 上。可以使用任何端口扫描器来查找在该端口运行的 TS。以下示例显示了对网络段进行简单的 TCP 端口扫描，以识别运行在端口 3389上的 Terminal Servers：

```
C:\>fscan -p 3389 10.0.6.0-10.0.6.254
```

FScan v1.14 - 命令行端口扫描器。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_495_0.png)

```
10.0.6.3 3389/tcp
10.0.6.8 3389/tcp
10.0.6.36 3389/tcp
10.0.6.38 3389/tcp
10.0.6.69 3389/tcp
10.0.6.80 3389/tcp
10.0.6.99 3389/tcp
10.0.6.240 3389/tcp
```

看来我发现了一个 TS 丰富的环境。如果你不确定网络中有多少个 Terminal Server 实例，建议你执行一些端口扫描来识别你的暴露情况。Terminal Server 可以配置为运行在 3389 以外的端口。

## 识别隐藏服务器

当服务器/工作站加入域时，它会在主浏览器中注册自己。注册的一部分包括服务器类型，可以通过 NetServerEnum 函数检索。Tim "Thor" Mullen 创建了一个名为 TSEnum.exe 的工具，它使用该函数来识别域中的 Terminal Servers。这在对域进行验证时效果最好，但即使你没有凭据有时也能生效。

### Terminal Services 宣告
在远程管理模式下的 Windows XP 服务器不会宣告自己为 Terminal Services。因此，如果你使用 TSEnum.exe 等枚举技术，请注意某些未补补的服务器可能是不可见的。永远不要依赖单一工具进行枚举活动。应用程序服务器模式下的 Windows XP Terminal Services 以及 Microsoft Windows 2000 Terminal Services 会正常宣告自己。

# 图 9.17 TSEnum.exe 寻找 Terminal Servers

![](img/729efc56f204a2ebffb8295c3a2dfdfb_496_0.png)

## 访问其他网段的 Windows 服务器

管理员经常在 Windows 服务器上安装多个网卡（双网卡）来连接网段以便方便工作。这从不是好事，但如果服务器是 TS，情况会更糟。我建议不要对服务器使用双网卡。然而，既然它们确实存在，让我们谈谈寻找它们的方法。如果你发现了这些服务器，可以集结力量找到罪魁祸首。另一种选择是通过物理连接服务器来修复暴露。

### 使用 Windows 终端

以下步骤描述了一种我成功用于寻找双网卡 Windows 系统的技术。一旦我识别了它们，就会使用端口扫描器查看它们是否正在运行 Terminal Services。

1. 确定你要扫描的网络。在例句中，假设它是 10.0.6.0/24。
2. 对 10.0.6.0/24 进行 TCP 135（微软远程过程调用 [MSRPC]）扫描，并将响应的 IP 地址保存到名为 tcp135.txt 的文件中。该文件将在下一步中为你提供帮助。
3. 使用 cmd.exe 中的 for 循环处理此 IP 地址列表（tcp135.txt），并使用微软 RPC 端点映射提取工具 rpcdump.exe 进行。

