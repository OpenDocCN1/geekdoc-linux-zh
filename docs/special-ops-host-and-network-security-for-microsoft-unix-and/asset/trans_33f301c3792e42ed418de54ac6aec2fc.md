

# 攻击与防御微软终端服务 • 第 9 章

让你的终端服务器变得更难以捉摸。Windows .NET Server 2003 将引入对终端服务会话强制智能卡认证的能力。对于部署了深度终端服务的用户，可能希望考虑智能卡来增加安全性。

## 幕后 (The_Curtain_Call)

- 在 http://softlabs.spaceitch.com/tscrack 查找 TScrack。
- 在 http://ackers.org.uk/tscrack/tscrack.2.0.37.txt 查找 TScrack 帮助文件。
- 在 http://hem.js/~-de96kilda/NeuralNetworks.htm 了解神经网络。

## 应用程序服务器攻击

如果你允许用户以应用程序服务器模式（Application Server mode）连接到你的终端服务器，那么你应该为服务器被攻破做好准备。除非你保持着近乎偏执的警惕，否则攻击者将能够破坏你的安全控制措施并获得 `cmd.exe` shell 的访问权限。一旦攻击者访问了该 shell，他极有可能通过权限提升攻击获得成功，从而获得管理员权限。

首先，我将讨论用户可能尝试跳出应用程序以获取对底层终端服务器访问权限的一些方法。接下来，我将展示攻击者可能如何提升权限成为管理员（或 LocalSystem）。

## 跳出特定的 Internet Explorer 应用程序

作为攻击者，如果你发现自己被困在 Internet Explorer (IE) 应用程序中，一种实用的尝试技术是在 IE 中对链接点击右键，然后在新窗口中打开该链接。一旦新窗口打开，输入 `e:\` 的 URL，你就获得了对文件系统的访问权限。接着，浏览到 `c:\winnt\system32\cmd.exe` 并获取自己的命令行访问权限（见图 9.19）。当然，如果该文件/目录的权限设置得当，或者在终端服务器上禁用了右键菜单，这种方法将无效。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_505_0.png)

## 图 9.19 使用 IE 访问 cmd.exe

![](img/729efc56f204a2ebffb8295c3a2dfdfb_506_0.png)

## 使用任务管理器获取 Shell

另一种有效跳出 TS 应用程序的技术是利用 Windows 的默认功能作为跳板。当被困在应用程序中或被限制访问 `cmd.exe` 时，尝试使用 `Ctrl+Alt+End` 打开任务管理器。如果成功，点击**新建**任务，然后执行 `cmd.exe` 或 `explorer.exe`。只要管理员没有使用“禁用任务管理器”策略设置，这种技术就有效。

## 使用 WinZip 获取 Shell

获取 Shell 的另一种选择是使用 `Alt+Home` 打开开始菜单然后打开 WinZip。创建一个新的压缩包并将 `cmd.exe` 复制到 `.zip` 文件中（图 9.20）。双击该文件运行它。如果系统中没有 WinZip，这种技术将告失效。此外，可以使用组策略设置来禁用开始菜单。

## 图 9.20 使用 WinZip 获取 Shell

![](img/729efc56f204a2ebffb8295c3a2dfdfb_506_1.png)

## 权限提升攻击

许多漏洞可用于将低权限账户提升为管理员或 LocalSystem。在本节中，我将讨论这些漏洞中的两个（GetAd.exe 和 DebPloit[ERunAsX.exe]），用以证明允许用户连接到未安装当前微软发布补丁的终端服务的巨大危险性。

如果你需要终端服务的应用程序共享，防止此类漏洞的最佳方法是保持高度警惕的补丁管理。你环境中的所有终端服务都应该更新到当前的补丁版本，可以使用 http://windowsupdate.com。

## 运行 GetAd.exe

该漏洞的 Bug ID 为 5927。由 Serus 于 2002 年 10 月 9 日发现。该漏洞影响 Windows 2000（包括 SP3）。无权限本地攻击者可以利用 Win NetDDE 获取权限。这是通过向 NetDDE 发送 WM_COPYDATA 消息实现的，当发送 WM_TIMER 消息时，将以 Local System 权限执行。更多信息请见微软官网。

## 在 TS 中运行 DebPloit 漏洞获取管理员

此权限提升攻击由 Radim “EliCZ” Picha 于 2002 年 3 月 9 日发现。该漏洞通过使用复制句柄伪装 `snmss.exe` (SYSTEM) 的安全上下文，即使是在 TS 会话中也是如此。带有 SP3 的 Windows 2000 不此漏洞影响。此外，实施了特定微软补丁的服务器也是安全的。该补丁可以从微软官网下载（MS02-24），它通过对调试服务的请求实施正确的验证来消除了该漏洞。

在图 9.21 所示的示例中，我检查了用户账户并显示它不在管理员组中，然后运行它使用户成为管理员，如下：

![](img/729efc56f204a2ebffb8295c3a2dfdfb_507_0.png)

## 图 9.21 ERunAsX 

![](img/729efc56f204a2ebffb8295c3a2dfdfb_508_0.png)

## 图 9.22 用户权限提升

![](img/729efc56f204a2ebffb8295c3a2dfdfb_508_1.png)

## 图 9.23 无权限登录到终端服务器

![](img/729efc56f204a2ebffb8295c3a2dfdfb_508_2.png)

## 利用终端服务器最大化 SQL 攻击成果

在进行渗透测试时，如果你在系统中发现了常见的 SA 空密码，你可以轻松地使用 `XP_CmdShell` 扩展存储过程来添加用户，然后让该用户成为管理员，如下：

![](img/729efc56f204a2ebffb8295c3a2dfdfb_509_0.png)

