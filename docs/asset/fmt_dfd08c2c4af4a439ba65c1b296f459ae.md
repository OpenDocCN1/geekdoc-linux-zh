
这些参数与标准 Telnet 客户端的参数相似。如果您在 Telnet 提示符处输入 `SET NTLM`，您的身份将通过 NTLM 进行身份验证。如果您正在连接到 Windows 2000 Telnet 服务器，将不会提示输入密码。然而，即使您在 HP-UX 上使用 PAM NTLM，也将会被提示输入用户名和密码，因为 HP-UX Telnet 服务器不识别 NTLM 选项。此客户端的默认终端类型是 `VT100`，通常用于连接 UNIX 系统已经足够。如果您将连接到 Windows 2000 Telnet 服务器并计划使用如 `EDIT` 等应用程序，那么您会将终端类型设置为 `VTNT`。在我使用此 Telnet 客户端连接 HP-UX 或 Solaris 时，不需要更改换行模式。

## 10.2 Telnet 服务器

当您安装 SFU Telnet 服务器时，可以使用 MMC 程序对其进行配置，如图 10–2 所示。

![](img/1c1e7552b53cca888836b6c6895bdb48_165_0.png)

图 10–2 Telnet 服务器向程序。该向程序打开后显示身份验证界面。

### 10.2.1 身份验证

Telnet 服务器支持 NTLM 和明文身份验证。NTLM 身份验证在 Windows Telnet 客户端上运行良好；它避免了输入用户名和密码，从而在网络上保持密码加密。在 HP-UX 上，即使您使用 PAM NTLM 进行身份验证，也会提示用户名和密码。这是因为 Telnet 客户端和服务器会在会话启动时协商采用哪些选项。Windows 2000 Telnet 客户端和服务器支持选项 37（身份验证选项）以启用 NTLM。HP-UX 客户端和服务器不支持。因此，即使您在登录工作站时通过 PAM NTLM 身份验证，Telnet 服务器仍会询问用户名密码。

身份验证后，Windows 2000 会运行 `%SYSTEMROOT%\system32\login.cmd` 脚本，其默认内容如下：

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

![](img/1c1e7552b53cca888836b6c6895bdb48_168_0.png)

图 10–4 Telnet 服务器 MMC 插入程序的设置页面。

### 10.2.4 会话

会话页允许您查看谁已登录，并为您提供断开用户连接和向用户发送消息的方法。图 10–5 显示了会话页示例。

![](img/1c1e7552b53cca888836b6c6895bdb48_168_1.png)

图 10–5 Telnet 服务器 MMC 插入程序的会话页。

### 10.2.5 使用 UNIX Telnet 客户端连接 Telnet 服务器

虽然 HP-UX 系统提供了书中大部分 UNIX 示例，但我发现其他 UNIX Telnet 客户端的行为也值得提及。为了说明每个过程，我在 UNIX Telnet 客户端中使用了 `toggle options` 子命令。

#### 10.2.5.1 AIX

在同时启用 NTLM 和明文认证的情况下，我得到了以下输出。注意，AIX 从 Windows 2000 Telnet 服务器收到了 `do 37` 消息（我已用加粗字体标记）。这意味着 Windows 2000 服务器希望 AIX 进行身份验证协商（以便进行 NTLM 认证）。AIX 复（（同样加粗）表示它不会进行身份验证协商（因为它不识别或不支持它）。

```
Trying.

Conected to w2kserv.book.local.

Escape character is '^'.

SEND DO ECHO

SEND DO SUPRESS GO AHEAD

SEND WILL TERMINAL TYPE (don't reply)

SEND DO SUPORT SAK

SEND WILL NEGOTIATE WINDOW SIZE (don't reply)

RCVD do 37 (reply)

SEND wout 37 (don't reply)

RCVD will ECHO (reply)

RCVD do ECHO (don't reply)

RCVD will SUPRESS GO AHEAD (reply)

SEND DO SUPRESS GO AHEAD (don't reply)

RCVD do 39 (reply)

SEND wout 39 (don't reply)

RCVD do NEGOTIATE WINDOW SIZE (don't reply)

SEND suboption TELOPT-NAWS Width 91, Height 28

RCVD do BINARY (reply)

SEND WILL BINARY (don't reply)

RCVD will BINARY (reply)

SEND do BINARY (don't reply)

RCVD do TERMINAL TYPE (don't reply)

RCVD wout SUPORT SAK (don't reply)

Microsoft (R) Windows 20 (TM) Version 5.0 (Build 2195)

Welcome to Microsoft Telnet Service

Telnet Server Build 5.20.0412.1

login:
```

这次交互的结果是 AIX 客户端最终得到了登录提示符。在禁用 NTLM 认证的情况下，会发生以下交换：

```
Trying.

Conected to w2kserv.book.local.

Escape character is '^'.

SEND DO ECHO

SEND do SUPRESS GO AHEAD

SEND will TERMINAL TYPE (don't reply)

SEND do SUPORT SAK

SEND will NEGOTIATE WINDOW SIZE (don't reply)

RCVD will ECHO (reply)

SEND do ECHO (don't reply)

RCVD will SUPRESS GO AHEAD (reply)

SEND do SUPRESS GO AHEAD (don't reply)

RCVD do 39 (reply)

SEND vont 39 (don't reply)

RCVD do NEGOTIATE WINDOW SIZE (don't reply)

SEND suboption TELOPT NAWS Width 80, Height 24

RCVD do BINARY (reply)

SEND WILL BINARY (don't reply)

RCVD will BINARY (reply)

SEND do BINARY (don't reply)

RCVD do TERMINAL TYPE (don't reply)

RCVD vont suport SAK (don't reply)

Microsoft (R) Windows 20 (TM) Version 5.0 (Build 2195)

Welcome to Microsoft Telnet Service

Telnet Server Build 5.20.0412.1
```

注意，选项 35 并没有发生。

#### 10.2.5 Solaris

在同时启用 NTLM 和明文认证的情况下，我得到了以下输出。注意，Solaris 识别了选项（通过调用名称而非数字），但不支持它。

```
Trying...

Connected to w2kserv.

Escape character is '^'.

SENT DO SUPRESS GO AHEAD
```
