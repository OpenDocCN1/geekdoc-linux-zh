

# 附件 B 使用 SSH 进行 X 转发

![](img/14d78e3cecac4581d37024baf1e94cca_1066_0.png)

你的 DISPLAY 变量和身份验证信息会由 ssh 自动设置。显示编号从 :10.0 开始，并随着每一次转发 X 流量的 SSH 连接而递增。

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

你可以看到从最后两行，客户端正在请求 X11 应用的转发。X 转发必须在 SSH 服务器和 SSH 客户端上同时启用，并且客户端仍必须拥有 X 服务器的正确 cookie。如果事情似乎没有正常工作，请尝试如上所示的 -X 和 -v 标志（适用于 OpenSSH）以显式启用 X 转发并请求详细输出。4 同时检查 /etc/ssh 中的全局 SSH 配置文件，以确保 X11 转发未被管理上禁用。登录后，你可以检查你的显示和 magic cookie：

```
x-client$ echo $DISPLAY
localhost:12.0
x-client$ xauth list
x-client/unix:12  MIT-MAGIC-COOKIE-1  a54b67121eb94c8a807f3ab0a67a51f2
```

> 4. 请注意 ssh 还有一个 -Y 标志，它信任所有客户端连接。此功能可能解决一些转发问题，但请仅在极端谨慎的情况下使用。

请注意 DISPLAY 指向 SSH 服务器上的虚拟显示。其他 SSH 连接（来自你本人和来自其他用户）会被分配不同的虚拟显示编号。DISPLAY 和 cookie 设置正确后，客户端应用程序现在可以运行。

```
x-client$ xeyes
debug1: client_input_channel_open: ctype x11 rchan 4 win 65536 max 16384
debug1: client_request_x11: request from 127.0.0.1 35411
debug1: channel 1: new [x11]
debug1: confirm x11
debug1: channel 1: FORCE input drain
```

使用 ssh -v 启用调试信息后，你可以看到 ssh 已收到 X 连接请求并忠实地将其转发到 X 服务器。转发在远距离链路上可能有点慢，但应用程序最终应该会出现在你的屏幕上。

## 25.3 X 服务器配置

X.Org 服务器 Xorg 曾经以难以为特定硬件环境配置而臭名昭著。然而，投入了大量精力使其开箱即用，许多现代系统在没有任何配置文件的情况下也能成功运行它。但是，仍然可以手动将 Xorg 服务器适配到各种图形硬件、输入设备、视频模式、分辨率和颜色深度。

如果你的系统在没有 Xorg 配置文件的情况下运行良好，太好了！它可能正在使用稍后在本章中描述的 KMS 模块。否则，你有两个选择。选项一是手动配置 xorg.conf 文件。下面的各节描述了手动配置。说实话，在某些情况下，这可能是你唯一真正的选择。选项二是使用 xrandr 工具配置你的服务器；它从第 1025 页开始介绍。

Xorg 配置文件通常位于 /etc/X11/xorg.conf，但 X 服务器会在多个目录中搜索它。man 手册列出了完整列表，但有一点需要注意的是，Xorg 搜索的一些路径包含主机名和全局变量，这使得你可以轻松地将多个系统的配置文件存储在中央位置。

AIX 在没有 xorg.conf 配置文件的情况下运行，并尝试自动识别所有 AIX 硬件显示类型。你可以作为参数传递给 X 服务器的配置提示。

有几个程序可以帮助你配置 X（例如 xorgconfig），但了解配置文件是如何结构化的是个好主意，以防你需要直接查看或编辑配置。你可以通过运行 Xorg -probeonly 并查看输出来收集一些有用的初始信息，以识别你的视频芯片组和任何其他探测到的值。你也可以

