
最普遍的基于主机的安全替代方案称为 `magic cookie` 认证。虽然 `magic cookies` 这个名字可能会让部分读者想起童年的回忆，但在这种情况下，它们用于验证 X 连接。其基本思想是 X 显示管理器在登录过程早期生成一个大随机数，称为 `cookie`。服务器的 `cookie` 会写入用户主目录下的 `~/.Xauthority` 文件。任何知道 `cookie` 的客户端都被允许连接。用户可以运行 `xauth` 命令来查看现有 `cookie` 并向此文件添加新的 `cookie`。

最简单展示其工作原理的方法是通过示例。假设你在客户端系统上设置了 `DISPLAY` 变量，以便在你所在的机器上显示 X 应用程序。然而，当你运行程序时，会出现类似如下的错误：

```
client$ xprogram -display server:0
Xlib: connection to "server:0.0" refused by server
xprogram: unable to open display 'server:0'
```

此消息告诉你客户端没有正确的 `cookie`，因此远程服务器拒绝了连接。要获取正确的 `cookie`，请登录到服务器（如果你试图在该服务器上显示，那么你可能已经登录了），并通过运行 `xauth list` 列出服务器的 `cookie`：

```
server$ xauth list
server0 MIT-MAGIC-COOKIE-1 f9d88df6077819ef4d788fab778dc9f
server/unix:0 MIT-MAGIC-COOKIE-1 f9d88df6077819ef4d788fab778dc9f
localhost:0 MIT-MAGIC-COOKIE-1 cb6cbf96e5c24128749feddd47f0e0779
```

服务器上的每个网络接口都有一个条目。此示例显示了以太网的 `cookie`、用于本地连接的 UNIX 域套接字的 `cookie`，以及 `localhost` 回环网络接口的 `cookie`。

将 `cookie` 传输到客户端的最简单方法（不使用 SSH，后者会为你协商 `cookie`）就是使用老式的复制粘贴。大多数终端仿真器（例如 `xterm`）允许你用鼠标选择文本并将其粘贴到另一个窗口，通常通过按下鼠标中键。方便的是，`xauth add` 命令接受的输入格式与 `xauth list` 显示的格式相同。你可以这样将 `cookie` 添加到客户端：

```
client$ xauth add server:0  MIT-MAGIC-COOKIE-1
9d88df6077819e4d788fab778dc9f
```

你应该通过在客户端上运行 `xauth list` 来验证 `cookie` 是否已正确添加。设置好 `DISPLAY` 环境变量并在客户端添加正确的 `magic cookie` 后，应用程序现在应该能正确显示在服务器上。

如果你在让 `cookie` 正常工作方面遇到困难，可以暂时退回到 `xhost` 认证，以验证是否存在其他问题（例如防火墙或本地网络限制阻止客户端访问服务器）。一旦测试完成，务必运行 `xhost -`（即 `xhost` 仅带一个连字符作为参数）来禁用 `xhost` 认证。

### 使用 SSH 进行 X 连接转发

`Magic cookies` 提高了安全性，但远非万无一失。任何能够获取你显示器 `cookie` 的用户都可以连接到该显示器并运行监视你活动的程序。即使没有你的 `cookie`，X 协议也会在网络上传输未加密的数据，几乎任何人都可以嗅探。

你可以使用 SSH，即安全 shell 协议来增强安全性。SSH 提供经过身份验证和加密的终端服务。然而，SSH 还可以转发任意网络数据，包括 X 协议数据，通过安全通道。X 转发与通用的 SSH 端口转发类似，但由于 SSH 具备 X 感知能力，你获得了额外的功能，包括远程机器上的伪显示以及 `magic cookie` 的协商传输。

你通常从运行 X 服务器的机器 `ssh` 到想要运行 X 程序的机器上。这种安排读起来可能令人困惑，因为 SSH 客户端运行在与 X 服务器相同的机器上，并且它连接到与 X 客户端应用程序相同的机器上的 SSH 服务器。更糟糕的是，SSH 为你的 X 服务器创建的虚拟显示是本地于远程系统的。下页的图 B 显示了 X 流量如何通过 SSH 连接传输。

请参阅第 926 页了解有关 SSH 的更多信息。

### 附件 B 使用 SSH 进行 X 转发

![](img/14d78e3cecac4581d37024baf1e94cca_1066_0.png)

你的 `DISPLAY` 变量和身份验证信息会由 `ssh` 自动设置。显示编号从 `:10.0` 开始，并随着每一次转发 X 流量的 SSH 连接而递增。

一个示例可能有助于说明该序列。

```
x-server$ ssh -v -X x-client.mydomain.com
SSH-2.0-OpenSSH_5.1
debug1: Reading configuration data /home/boggs/.ssh/config
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for *
debug1: Connecting to x-client.mydomain.com [192.168.15.9] port 22.
debug1: Connection established.
Enter passphrase for key '/home/boggs/.ssh/id_rsa':
debug1: read PEM private key done: type RSA
debug1: Authentication succeeded (publickey).
debug1: Entering interactive session.
debug1: Requesting X11 forwarding with authentication spoofing.
debug1: Requesting authentication agent forwarding.
x-client$
```

你可以看到从最后两行，客户端正在请求 X11 应用的转发。X 转发必须在 SSH 服务器和 SSH 客户端上同时启用，并且客户端仍必须拥有 X 服务器的正确 `cookie`。如果事情似乎没有正常工作，请尝试如上所示的 `-X` 和 `-v` 标志（适用于 OpenSSH）以显式启用 X 转发并请求详细输出。4 同时检查 `/etc/ssh` 中的全局 SSH 配置文件，以确保 X11 转发未被管理上禁用。登录后，你可以检查你的显示和 `magic cookie`：

```
x-client$ echo $DISPLAY
localhost:12.0
x-client$ xauth list
x-client/unix:12  MIT-MAGIC-COOKIE-1  a54b67121eb94c8a807f3ab0a67a51f2
```

> 4. 请注意 `ssh` 还有一个 `-Y` 标志，它信任所有客户端连接。此功能可能解决一些转发问题，但请仅在极端谨慎的情况下使用。

请注意 `DISPLAY` 指向 SSH 服务器上的虚拟显示。其他 SSH 连接（来自你本人和来自其他用户）会被分配不同的虚拟显示编号。`DISPLAY` 和 `cookie` 设置正确后，客户端应用程序现在可以运行。

```
x-client$ xeyes
debug1: client_input_channel_open: ctype x11 rchan 4 win 65536 max 16384
debug1: client_request_x11: request from 127.0.0.1 35411
debug1: channel 1: new [x11]
debug1: confirm x11
debug1: channel 1: FORCE input drain
```

使用 `ssh -v` 启用调试信息后，你可以看到 `ssh` 已收到 X 连接请求并忠实地将其转发到 X 服务器。转发在远距离链路上可能有点慢，但应用程序最终应该会出现在你的屏幕上。

## 25.3 X 服务器配置

`X.Org` 服务器 `Xorg` 曾经以难以为特定硬件环境配置而臭名昭著。然而，投入了大量精力使其开箱即用，许多现代系统在没有任何配置文件的情况下也能成功运行它。但是，仍然可以手动将 `Xorg` 服务器适配到各种图形硬件、输入设备、视频模式、分辨率和颜色深度。

如果你的系统在没有 `Xorg` 配置文件的情况下运行良好，太好了！它可能正在使用稍后在本章中描述的 KMS 模块。否则，你有两个选择。选项一是手动配置 `xorg.conf` 文件。下面的各节描述了手动配置。说实话，在某些情况下，这可能是你唯一真正的选择。选项二是使用 `xrandr` 工具配置你的服务器；它从第 1025 页开始介绍。
