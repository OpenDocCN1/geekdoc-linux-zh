
接下来，复制 Public key（公钥）中的文本，打开记事本并将文本粘贴到新文件中。将其保存为 `\servername\.ssh\authorized_keys`，如图 7.7 所示。确保给文件名加上双引号，否则记事本会为文件名添加 .txt 扩展名。

### 图 7.7. 保存 `\servername\sharename\.ssh\authorized_keys`

![](img/9bce1c0d54b562ab7f16793d6011fa55_253_0.png)

## 使用 PuTTY 客户端

现在我们需要保存私钥。此时，建议你输入密钥短语（passphrase）以确保私钥的安全。点击 Save private key（保存私钥）按钮，并将其保存到本地硬盘的某处。

要使用此公私钥对，启动 PuTTY 并像以前一样输入服务器名称。在 PuTTY 配置窗口左侧的 Category 列表中选择 Auth（身份验证）。在 Private key file for authentication（身份验证私钥文件）字段中，选择你从 PuTTYgen 保存的私钥，如图 7.8 所示。

### 图 7.8. 选择私钥。

![](img/9bce1c0d54b562ab7f16793d6011fa55_254_0.png)

# 第 7 章：远程管理

## VNC

如果 SSH 之于命令行，那么 VNC 之于桌面：VNC 允许你远程查看并控制另一台机器的图形桌面。这对于控制远程服务器非常有用，特别是你可以控制你想要指定的机器，而不再局限于命令行。

### 设置 VNC 服务器

Fedora Core 内置了简单的 VNC 支持，但这种简单的支持仅应用于网络内部的服务器。VNC 本身是非常不安全的，但我们可以利用 SSH 的安全特性来使其变得安全。我们将在本章稍后的部分介绍如何实现这一点。

要启动简单的 VNC 服务器，通过选择“桌面 (Desktop) > 首选项 (Preferences) > 远程桌面 (Remote Desktop)”启动图 7.9 显示的远程桌面首选项工具。

勾选“允许其他用户查看你的桌面 (Allow other users to view your desktop)”和“允许其他用户控制你的桌面 (Allow other users to control your desktop)”，取消勾选“询问确认 (Ask you for confirmation)”。你可以选择提供一个用户在连接到 VNC 服务器之前必须输入的密码——勾选“要求用户输入此密码 (Require the user to enter this password)”并输入密码——但记住，此 VNC 服务器仅在用户登录服务器时运行；如果服务器停留在登录界面，则无法使用此工具通过该方法建立 VNC 连接。

客户端将通过端口5900–5906 的 TCP 连接到你的 VNC 服务器，因此你需要在防火墙中开放这些端口：在“安全层级配置 (Security Level Configuration)”工具的“其他端口 (Other Ports)”列表中添加 `5900:tcp`、`5901:tcp` ... `5906:tcp`。完成后，即可通过 VNC 访问服务器。

### 图 7.9 远程桌面首选项工具。

![](img/9bce1c0d54b562ab7f16793d6011fa55_258_0.png)

### VNC 视器

如果你没有可以访问它的客户端，那么设置 VNC 服务器将是无用武之地。在这里，我们将简要查看三个 VNC 视器：用于 Windows 的 TightVNC、用于 Mac OS X 的 Chicken of the VNC 以及 Fedora Core 的终端服务器客户端 (Terminal Server Client)。

### TightVNC

### 图 7.10. TightVNC 选择组件屏幕。

![](img/9bce1c0d54b562ab7f16793d6011fa55_259_0.png)

TightVNC 是一个用于 Linux 和 Windows 的流行开源 VNC 服务器和视器包，可以从 http://www.tightvnc.com/ 下载。双击安装程序并按照标准的 Windows 安装程序继续操作。当你到达图 7.10 所示的“选择组件 (Select Components)”屏幕时，选择 TightVNC Viewer。继续完成向导的其余部分，即可视好 TightVNC Viewer。

当你启动 TightVNC 视器时，你会在“所有程序 (All Programs)”菜单中看到三个项目，如图 7.11 所示：最佳压缩 (Best Compression)、快速压缩 (Fast Compression) 和监听模式 (Listen Mode)。最佳压缩和快速压缩都是指向同一个程序的快捷方式，但参数不同；监听模式会在系统托盘中放置一个图标，以便快速启动视器。选择“最佳压缩”或“快速压缩”来启动视器。

### 图 7.11 所有程序菜单中的 TightVNC。

![](img/9bce1c0d54b562ab7f16793d6011fa55_260_0.png)

连接到 VNC 服务器是一项简单的任务：输入服务器名称并点击确定。远程服务器的桌面将出现在你桌面的一个窗口中，如图 7.12 所示。只需将鼠标移动到窗口上即可开始交互；你可以像坐在机器面前一样控制远程服务器。要关闭 VNC 连接，只需点击窗口标题栏中的交叉叉图标即可。

### 图 7.12 使用 TightVNC 视器。

![](img/9bce1c0d54b562ab7f16793d6011fa55_260_1.png)

### Chicken of the VNC

Chicken of the VNC 是另一个开源 VNC 视器，但它是为 Mac OS X 开发的。你可以从 http://cotvnc.sourceforge.net/ 下载它。它以磁盘镜像的形式分发，因此安装非常简单，只需打开镜像并将应用程序复制到你的 Applications 文件夹即可。启动应用程序，输入你的 VNC 服务器名称并点击连接。远程桌面将出现在自己的桌面上；它看起来与图 7.13 所示类似。

### 图 7.13 使用 Chicken of the VNC。

![](img/9bce1c0d54b562ab7f16793d6011fa55_261_0.png)

### Fedora Core 的终端服务器客户端

### 图 7.14 连接到 VNC 服务器。

![](img/9bce1c0d54b562ab7f16793d6011fa55_262_0.png)

Fedora Core 提供了一个终端服务器客户端。要连接到 VNC 服务器，请使用图 7.14 所示的终端服务器客户端。远程服务器的桌面将出现在你桌面的一个窗口中，如图 7.12 所示。只需将鼠标移动到窗口上即可开始交互；你可以像坐在机器面前一样控制远程服务器。要关闭 VNC 连接，只需点击窗口标题栏中的交叉图标即可。

### 图 7.12 使用 TightVNC 视器。

![](img/9bce1c0d54b562ab7f16793d6011fa55_260_1.png)

### 使用 SSH 保护 VNC

VNC 本身是不安全的，但我们可以利用 SSH 的安全特性来使其变得安全。我们将在本章稍后的部分介绍如何实现这一点。

SSH 隧道是一种技术，通过它通过 SSH 将通信重定向到特定端口（在本例中为端口 5901）到本地机器，从而加密跨该端口的通信。

### 图 7.15 使用 VNC。

![](img/9bce1c0d54b562ab7f16793d6011fa55_263_0.png)

### 图 7.16 一个 VNC 连接。

![](img/9bce1c0d54b562ab7f16793d6011fa55_264_0.png)

SSH 隧道实际上设置非常简单。使用 SSH 的步骤如下：

- 设置隧道。
- 启动 VNC 服务器。
- 连接 SSH 隧道。
- 使用 VNC。
- 断开 VNC 连接。
- 停止 VNC 服务器。
- 关闭 SSH 连接。

### 使用 ssh 客户端隧道

使用命令行 `ssh` 客户端，通过如下使用 `-L` 选项设置隧道：

```
mymac:-6 ssh -L 5901:swinetrek:5901 kermit@swinetrek

kermit@swinetrek's password:

Last login: Sun Oct 16 20:46:10 2005 from 192.168.69.36

[kermit@swinetrek ~]$
```
