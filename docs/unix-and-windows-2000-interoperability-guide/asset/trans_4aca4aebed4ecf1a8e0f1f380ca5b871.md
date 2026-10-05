
# 第 10 章 • UNIX 的 Windows 服务

**用户名映射。** 此组件将基于 Windows 的网络用户名映射到基于 UNIX 的网络用户名。Server for NFS、Client for NFS 和 Gateway for NFS 都使用用户名映射来进行 NFS 身份验证和访问。

SFU 包含很多内容，让我们来看看它提供的一些功能，从 Telnet 和 Server for NFS 开始。由于 NFS 涉及文件共享问题，我们将讨论推迟到下一个章节。

SFU 随光光光盘提供；将其插入您的 CD-ROM 驱动器后将启动 Windows 安装程序。如果您的系统安装了 Windows 2000 专业版，则会安装以下标准产品：Telnet 客户端、Telnet 服务器、Client for NFS、Korn Shell 和工具（Utilities）。在 Windows 2000 上的上的标准安装也允许安装 Server for NFS。SFU 的自定义安装（Custom Install）允许您安装其他组件。如果您想同步域帐户的密码，则无法安装 Client for NFS 和 Gateway for NFS，您必须在域控制器上安装密码同步（Password Synchronization）。此外，您必须在域控制器上安装 Server for NFS。默认情况下，安装程序会将 SFU 置于 *SFU* 目录中并创建环境变量 SFUDIR。如果您选择不同的目录，请确保该目录不包含空格（例如 Program Files）。空格可能会导致快捷方式和 NFS 功能出现问题。

SFU 通过 Microsoft 管理控制（MMC）进行管理。一旦您安装了组件，运行“开始→程序→Windows Services for UNIX→服务管理”来获取图 10–1 所示的 MMC。

![](img/1c1e7552b53cca888836b6c6895bdb48_163_0.png)

**图 10–1** UNIX 服务管理。您可以在此处管理的已安装组件包括 Server for NFS、Client for NFS、Telnet 服务器、密码同步和 Server for NIS。

## 10.1 Telnet 客户端

SFU Telnet 客户端的命令具有捆绑客户端不具备的选项。前者的语法如下：

```
telnet [-a] [-e escapeChar] [-f logfile] [-l user] [-t term] [host [port]]
```

-a 和 一l 选项尝试自动登录，这仅在 Telnet 服务器支持 ENVIRON 选项时有效。在我尝试使用这些选项连接到 HP-UX 11 或 Solaris 8 时，我发现这两个系统上的 Telnet 服务器都不识别 ENVIRON 选项。您可以使用 -e 选项将转义字符（在连接时将您带到 Microsoft Telnet> 提示符的键盘序列）设置为默认 CTRL+ 以外的其他字符。您可以使用 -f 选项设置连接日志文件。您指定的日志文件会记录 Telnet 会话的输入和输出。对于此 Telnet 客户端，默认是 VT100。如果您想指定不同的类型，请使用 -l 选项并将 VT52、ANSI 和 VTNT 作为终端类型。您可以指定主机名或 IP 地址来连接到远程系统，如果不使用默认的 23 端口，还可以指定端口号。

Telnet 子命令与标准 Telnet 客户端也略有不同。表 10–1 列出了微软文档说明的子命令。我还在括号中指示了命令缩写。

| 表 10–1 SFU Telnet 客户端子命令 |
|---|---|
| open (o) | 与主机建立 Telnet 连接。 |
| close (c) | 关闭现有的 Telnet 连接。 |
| display (d) | 生成 Telnet 客户端当前设置的列表。 |
| quit (q) | 退出 Telnet。 |
| set | 设置连接的终端类型，开启本地回显，设置身份验证为 NTLM，设置转义字符并设置日志。 |
| unset (u) | 关闭本地回显或 NTLM 身份验证。 |
| status | 确定 Telnet 客户端是否已连接。 |

SFU Telnet 客户端的 display 子命令提供以下输出：

```
Microsoft Telnet> d
Escape Character is 'CTRL+'
Will auth (ntlm Authentication)

Local echo off

Line feed mode - Causes return key to send 0x0D

Current mode: Console

Will term type

Preferred term type is VT100

```

这些参数与标准 Telnet 客户端的参数相似。如果您在 Telnet 提示符处输入 SET NTLM，您的身份将通过 NTLM 进行身份验证。如果您正在连接到 Windows 2000 Telnet 服务器，将不会提示输入密码。然而，即使您在 HP-UX 上使用 PAM NTLM，也将会被提示输入用户名和密码，因为 HP-UX Telnet 服务器不识别 NTLM 选项。此客户端的默认终端类型是 VT100，通常用于连接 UNIX 系统已经足够。如果您将连接到 Windows 2000 Telnet 服务器并计划使用如 EDIT 等应用程序，那么您会将终端类型设置为 VTNT。在我使用此 Telnet 客户端连接 HP-UX 或 Solaris 时，不需要更改换行模式。

## 10.2 Telnet 服务器

当您安装 SFU Telnet 服务器时，可以使用 MMC 程序对其进行配置，如图 10–2 所示。

![](img/1c1e7552b53cca888836b6c6895bdb48_165_0.png)

图 10–2 Telnet 服务器向程序。该向程序打开后显示身份验证界面。

### 10.2.1 身份验证

Telnet 服务器支持 NTLM 和明文身份验证。NTLM 身份验证在 Windows Telnet 客户端上运行良好；它避免了输入用户名和密码，从而在网络上保持密码加密。在 HP-UX 上，即使您使用 PAM NTLM 进行身份验证，也会提示用户名和密码。这是因为 Telnet 客户端和服务器会在会话启动时协商采用哪些选项。Windows 2000 Telnet 客户端和服务器支持选项 37（身份验证选项）以启用 NTLM。HP-UX 客户端和服务器不支持。因此，即使您在登录工作站时通过 PAM NTLM 身份验证，Telnet 服务器仍会询问用户名密码。

身份验证后，Windows 2000 会运行 %SYSTEMROOT%\system32\login.cmd 脚本，其默认内容如下：

```
@echo off
rem
 Telnet 服务器的全局登录脚本
rem 在默认设置下，此脚本在调用命令 shell 时执行。它反过来会尝试调用用户的登录脚本。
rem
```

```
echo ====================================================
Welcome to Microsoft Telnet Server.
echo ====================================================
```

```
cd /d %HOMEDRIVE%\HOMEPATH%
```

### 10.2.2 日志

Telnet 服务器 MMC 向程序的日志界面（见图 10–3）允许您将事件记录在应用程序日志或文件中（或两者都有）。

![](img/1c1e7552b53cca888836b6c6895bdb48_167_0.png)

图 10–3 Telnet 服务器 MMC 向程序的日志界面。

### 10.2.3 服务器设置

在服务器设置页面上，您可以设置多个参数，如图 10–4 所示。如果您需要运行可能需要按下 ALT 键的应用程序，必须确保在此页面上勾选了“将 CTRL+A 解析为 ALT”。

