
## 设置 [global] 参数

[global] 部分定义了适用于所有其他配置部分（即它们定义的服务）的 Samba 参数。默认的 [global] 配置如下：

```
[global]
    workgroup = MYGROUP
    server string = Samba Server
    printcap name = /etc/printcap
    load printers = yes
    printing = lprng
    log file = /var/log/samba/%m.log
    max log size = 0
    security = user
    socket options = TCP_NODELAY \
                  SO_RCVBUF=8192 \
                  SO_SNDBUF=8192
    dns proxy = no
```

以下各节将向您展示如何配置这些参数中的每一个。

### 工作组

将此参数设置为您希望 Samba 作为节点参与的 Windows 工作组或 Windows NT/2000 域名。例如，我使用 EVOKNOW 作为 Windows NT/2000 域名，因此可以将 workgroup 设置为 EVOKNOW。当我的网络上的 Windows 9x 或 Windows NT/2000 系统浏览网络邻居时，它会在 EVOKNOW Windows NT/2000 域下看到 Samba 服务器。将此设置为适合您局域网的工作组或域名。

### 服务器字符串

设置此参数以提供 Samba 服务器的描述。此描述将对 Samba 客户端（例如 Windows 9x 机器）可见。

### printcap 名称

使用此参数设置 printcap 文件路径。默认值 /etc/printcap 应该适合您。/etc/printcap 文件用于描述打印机功能。如果您有一台或多台打印机连接到 Linux 服务器，并且希望将所有打印机提供给局域网上的 Windows 系统，请设置此参数以及 load printers 参数。

### 加载打印机

使用此参数告诉 Samba 自动将本地打印机提供给网络上任何 SMB 客户端计算机。如果您想启用此功能，请将其设置为 yes；如果您希望在各个配置部分中指定打印机配置，请将其设置为 no。

### 打印

printing 参数用于设置打印命令。默认值 lprng 告诉 Samba 使用 lpr 命令。

### 日志文件

使用此参数设置 Samba 日志文件的名称。默认设置会为每个客户端写入一个日志文件。这是通过 %m 宏实现的，该宏会扩展为客户端名称。例如，如果您保持 log file 设置不变，并从名为 r2d2 的 Windows 机器访问 Samba 服务器，将会创建名为 /var/log/samba/r2d2.log 的日志文件。

### 最大日志大小

使用此参数控制日志文件的最大大小，以千字节为单位。

### 安全

security 参数是所有全局参数中最重要的。使用它来告诉 Samba 如何执行客户端身份验证。以下是 security 的四个可能值，以及 Samba 服务器在 security 设置为每个值时所执行的操作的描述：

- **user.** Samba 服务器会要求客户端提供用户名/密码对进行身份验证。如果您在 Windows 系统和 Linux 系统上使用相同的用户名/密码对，请将 security 参数设置为 user。例如，如果您在 Windows NT/2000 Server 上有一个名为 joe 的用户，并且在 Samba 服务器上也有相同密码的相同用户，请将此参数设置为 user。
- **share.** Samba 服务器期望每次服务请求都附带密码。不需要用户名。如果您的 Windows 系统和 Linux Samba 服务器没有相同的一组用户名/密码对，请使用此设置。
- **server.** Samba 服务器会要求客户端提供用户名/密码对，就像将此参数设置为 user 时一样，但 Samba 服务器本身不会验证用户名/密码对。它使用另一台 SMB 服务器对用户进行身份验证。因此，当您将 security 设置为 server 时，还必须设置 password server 参数，该参数用于命名将负责身份验证的 SMB 服务器。如果您希望将 SMB 活动的用户名/密码集中在 Windows NT/2000 服务器上，请将 password server 参数指向 Windows NT/2000 服务器。

![](img/9eb7e89292d2f85707b4d49102c865b7_530_0.png)

如果您使用 Windows NT/2000 作为密码服务器来为 Samba 执行所有身份验证，请确保您没有在 Windows NT/2000 系统上启用访客帐户。如果启用了访客帐户，只要用户名/密码对因密码错误而失败，Windows NT/2000 仍会向 Samba 服务器提供有效响应，因为 Windows NT/2000 只会将访客权限分配给失败的身份验证尝试并向 Samba 服务器返回成功响应。

- **Domain.** Samba 服务器使用域控制器对用户进行身份验证。密码必须以加密格式传输，因此 encrypted passwords 选项需要设置为 yes。

security 的默认设置是 user，这意味着客户端必须提供明文密码以及用户名。Samba 服务器通过使用 /etc/passwd 文件来验证此用户名/密码对。然而，后期的 Windows 9x 和 Windows NT/2000 默认不使用明文（也称为 clear-text）密码。微软决定将其作为操作系统服务包升级的一部分使用加密密码。由于这些 Windows 客户端不提供明文密码，因此无法验证；因此，Samba 服务器会拒绝为其提供服务。为了解决此问题，您有两个选择：

- 在 Windows 系统上启用明文密码。如果满足以下任何条件，此选项是可以接受的：
  - 您已允许 Windows 机器与 Red Hat Linux 服务器之间使用基于明文的服务，例如 FTP 和 Telnet。
  - 您的网络未连接到 Internet，因此使用明文密码不会对您的组织构成很大威胁。
  - 您只想先让 Samba 工作，然后再处理加密密码或计划在长期内将所有身份验证任务委托给 Windows NT/2000 系统。
- 使用加密密码进行身份验证。

您可能会选择第一个选项，因此接下来会进行描述。本章最后一节提供了使用加密密码进行身份验证的详细信息。

如果您使用的是 Windows 98、带有 Service Pack 3 或更高版本的 Windows 95，或带有 Service Pack 3 或更高版本的 Windows NT，请按照以下步骤启用明文密码：

1. 通过单击“开始”按钮，选择“运行”，在命令字段中输入 regedit，然后单击“确定”来运行名为 RegEdit 的 Windows 注册表编辑器程序。
2. 对于 Windows 9x，定位以下注册表项：

```
/HKEY_LOCAL_MACHINE
/System
/CurrentControlSet
/Services
/VxD
/VNETSUP
```

对于带有 Service Pack 3 或更高版本的 Windows NT/2000，定位以下注册表项：

```
/HKEY_LOCAL_MACHINE
/SYSTEM
/CurrentControlSet
/Services
/Rdr
/Parameters
```

3. 在注册表树中找到 VNETSUP 分支（适用于 Windows 9x）或 Parameters 分支（适用于 Windows NT/2000）后，选择 编辑 → 新建 并选择创建一个新的 DWORD 值。
4. RegEdit 将在注册表中插入一个名为 New Value #1 的新 DWORD 值。将此新值重命名为 EnablePlainTextPassword 并双击此新名称。
5. 弹出一个对话框，使您能够为刚刚创建的 EnablePlainTextPassword 设置值。输入 1 作为值并像往常一样关闭 RegEdit。
6. 重启您的 Windows 系统。

这可确保您的 Windows 系统能够为 SMB 身份验证使用明文密码。

### socket 选项

默认情况下，全局配置部分中的 socket options 参数设置为 TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192，这可在某些平台上增强 Samba 性能。保持此参数不变。

### dns 代理

此参数会影响 Samba 套件内置的 Windows Internet 名称服务器（nmbd）在 Windows 系统名称（NetBIOS
