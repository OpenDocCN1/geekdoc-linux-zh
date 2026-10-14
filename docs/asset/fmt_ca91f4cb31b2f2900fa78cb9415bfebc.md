
```
$ xdpyinfo | fgrep display
name of display:      dell.home.org:0.0
```

如果服务器上本地运行了多个 X 会话，你可能会看到类似的内容：

```
name of display:      1.0
```

在此示例中，用户已登录并正在使用该工作站的第二个 X 会话（显示）。

## 远程客户端执行

在 X 网络上启动客户端也有多种方法。例如，如果你登录 Linux 并在本地启动 X 会话，你可以使用 `-display` X Toolkit 选项配合远程计算机的显示名称，在远程显示器上显示本地客户端。如果你坐在名为 `greenie` 的工作站前，你可以启动 `xcalc` 客户端并将其显示在 `stinky` 上的远程 X 显示上，如下：

```
$ xcalc -display stinky:0.0 &
```

然而，如果你没有在远程计算机上运行客户端的访问或权限，你会看到类似的内容：

```
Xlib: connection to "stinky:0.0" refused by server
Xlib: Client is not authorized to connect to Server
Error: Can't open display: stinky:0.0
```

`xhost` 命令用于控制 X 下的服务器访问。使用此客户端向服务器的连接列表添加或删除主机名或用户名。在上一个示例中，你将在远程计算机 `stinky` 上如下使用 `xhost`：

```
$ xhost + greenie
```

`greenie` 已被添加到访问控制列表中。

在你按下回车键后，`greenie` 上的用户就可以执行 `xcalc` 客户端，`xcalc` 就会出现在 `stinky` 的显示器上。然而，在使用 `xcalc` 客户端后，你应该移除 `greenie` 的权限，如下：

```
$ xhost - greenie
```

`greenie` 已从访问控制列表中移除。

一种更常见的方法（特别是在小型网络中）是首先授予功能更强大的工作站或服务器访问权限，然后使用 `telnet` 会话登录，如下：

```bash
[bball@thinkpad ball]$ xhost + dell
dell added to access control list
[bball@thinkpad ball]$ telnet dell
Trying 192.168.2.35...
Connected to dell.home.org.
Escape character is '^'.
Welcome to SuSE Linux 7.0 (i386) - Kernel 2.2.16 (3).
ndell login: bball
Password:
Last login: Mon Oct 30
```

在某些情况下，你可能必须手动设置 `$DISPLAY` 变量，特别是当你使用 `rlogin` 或 `ssh` 命令登录到远程机器时。你可以通过 shell 的变量赋值在命令行中轻松完成这一点。登录远程后，如果你使用 `bash` shell，使用 `bash export` 命令后跟定义，如下：

```bash
$ export DISPLAY=hostname:0.0
```

在你按下回车键后，你的工作站将在本地显示在远程计算机上启动的任何客户端（再次，你可能需要先使用 `xhost` 获取访问）。

## 通过 PPP 使用 X

另一种允许远程访问的方法是使用 `lbx-proxy` 客户端使用低带宽 X。这种方法通常用于通过调制解调器拨号提供远程 X 会话，并允许 X 通过链路互联网协议 (SLIP)、压缩 SLIP 或更常见的点对点协议 (PPP) 运行。

一种通过拨号轻松建立 X 会话并获得更好性能的方法是使用 `dxpe` 客户端（根据命令行选项充当客户端或服务器）。该软件最初由 `Zachary Vonler` 编写，现在由 `Brian Pane` 维护，它通过缓存 X 协议消息以便在较慢的传输线路上提供压缩的 X 请求。这种卓越的性能极大加快了客户端的显示，即使是在使用慢速串口线时也是如此。

首先，你需要下载并安装 `dxpc` 软件包。该软件可以通过 `http://www.vigor.nu/dxpc/` 获取，它以源码形式分发在一个 `123K` 的压缩 tar 包中。若要编译并安装该软件，请像如下所示使用 `tar`、`cd`、`configure` 和 `make` 命令（以 `root` 权限运行）：

```
# tar xvf dxpc*.gz
### cd dxpc*
./configure ; make install
```

接下来，你需要在目标服务器上设置 PPP 服务，在本例中将其命名为 `stinky`。你可以通过创建一个名为 `ppp` 的用户账户来快速完成此设置（以 `root` 权限）。接着，在 `/etc/passwd` 条目中，将 `shell` 条目替换为 shell 脚本的路径（在本例中名为 `dopp`）：

```
ppp:x:502:502::/ppp:/usr/local/bin/dopppp
```

不要忘记使用 `password` 命令为新的 PPP 用户分配密码。接下来，使用以下命令创建 shell 脚本：

```
exec /usr/sbin/ppppd -detach
```

保存文件并使用 `chmod` 命令赋予其执行权限。你的系统 `/etc/inittab` 文件应该已经设置好接受通过调制调器拨入。以下条目使用 `getty` 标签名称，允许在 `/dev/ttyS2` 上以 `38400` 的速率拨入：

```
3:2345:respawn:/usr/local/bin/agetty -w -I ATE001&D2&CISO=1'015' \
115200 tty2 vt100
```

接下来，为拨号用户分配静态 IP 地址，使用以下命令在 `/etc/ppp` 目录下创建一个名为 `options.tty2` 文件：

```
192.168.2.37:192.168.2.41
```

在本例中，远程拨号者将被分配 IP `192.168.2.41`，而服务器主机（`stinky`）的 IP 地址为 `192.168.2.37`。最后，使用以下命令创建 `/etc/ppp/options` 文件：

```
asyncmap 0
netmask 255.255.255.0
proxyarp
lock
crcts
modem
```

保存文件。此时，你可以从远程计算机（在本例中名为 `greenie`）拨入你的服务器。要执行操作，请输入用户名和密码，然后使用分配的 IP 地址建立 PPP 连接。

## 限制 Shell 账户！

虽然 shell 账户在用当的情况下是一个非常方便的工具，但你的局域网（或公司）中并不是每个人都应该拥有 shell 的权限。出于安全考虑，请始终限制 shell 账户。

现在拨入名为 `stinky` 的服务器并建立连接。在远程计算机（`greenie`）上打开两个 X 终端窗口。在其中一个窗口，使用 `telnet` 命令登录服务器，并确保 `$DISPLAY` 变量设置为远程计算机的 `$DISPLAY`，如下：

```
[stinky]$ export DISPLAY=greenie:0.0
```

接下来，在该窗口中作为客户端运行 `dxpc` 程序：

```
[stinky]$ dxpc -f s1
dxpc proxy running in CLIENT mode
```

`dxpc` 命令将显示状态报告（在远程服务器上的客户端模式）。额外的选项可以处理 `for` 并启用将压缩报告到标准输出。接下来，按如下方式重置 `DISPLAY` 变量：

```
[stinky]$ export DISPLAY=unix:8
```

`dxpc` 命令所使用的 `unix:8` 显示（当计算机作为服务器运行时）提供了一个用于显示客户端的地址——`dxpc` 命令正在“模拟一个 X 服务器，并使用 `unix:8` 显示”。现在，在远程计算机（`greenie`）的终端窗口中，使用服务器模式运行 `dxpc` 命令，并指定远程计算机如下：

```
[greenie]$ dxpc -f stinky
dxpc proxy running in SERVER mode
```

按下回车键后，`dxpc` 命令将作为服务器运行并拦截来自远程客户端的请求，并在本地显示。你现在可以从服务器的终端窗口（在本例中为 `stinky`）启动客户端，它们将通过你的串口 PPP 连接运行。`dxpc` 的多个版本适用于计算机平台和操作系统，包括 Solaris、Windows、HP/UX 和 Digital Unix。你可以使用此软件轻松地建立连接，并且在更快的串口线上，甚至可以以可接受的性能远程运行。访问 `http://www.vigor.nu/dxpc/` 了解更多信息。

### 虚拟网络

例如，在局域网中运行 Linux 的远程计算机上如下所示启动 `Xvnc` 服务器：
