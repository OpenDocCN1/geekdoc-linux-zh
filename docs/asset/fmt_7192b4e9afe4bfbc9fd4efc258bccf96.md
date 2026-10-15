
`client$ DISPLAY=servername.domain.com:10;export DISPLAY`

此设置将 X 应用程序指向机器 `servername.domain.com`，显示器 10，屏幕 2。应用程序将在端口号 6000 加上显示器编号（在本例中，端口为 6010）的服务器上建立 TCP 连接，处理显示的 X 服务器应该在该端口上监听。

请记住，每个进程都有自己的环境变量。当你为 shell 设置 `DISPLAY` 变量时，它的值只会被你从它中运行的程序继承。如果你在一个 `xterm` 中执行上述命令，然后尝试从另一个 `xterm` 运行你喜爱的 X 应用程序，该应用程序将无法访问你精心构建的 `DISPLAY` 变量。

另一个值得提及点是，尽管 X 将其图形显示发送到指定的 X 服务器，但它们仍然拥有本地标准错误（`stderr`）。某些错误输出可能仍然来自运行 X 应用程序的终端窗口。

有关 DNS 解析器配置的更多信息，请参阅第 561 页。

如果客户端和服务器都属于你的本地组织，根据服务器解析器的配置方式，你通常可以从 `DISPLAY` 变量中省略服务器的全名。此外，如果大多数系统只运行单个 X 服务器，则显示器为 0。屏幕编号可以省略，在这种情况下假设屏幕为 0。因此，大多数时候将 `DISPLAY` 的值设置为 `servername:0` 是可以的。

## 第25 章

## X 窗口系统

如果客户端应用程序恰好运行在与 X 服务器相同的机器上，你可以通过省略主机名来进一步简化 `DISPLAY` 变量。此功能不仅仅是为了美观：通过空主机名，库将使用 UNIX 域套接字而不是网络套接字连接到 X 服务器。这种连接方法不仅更快、更高效，还绕过了本地系统上任何试图阻止 X 连接的防火墙限制。`DISPLAY` 环境变量最简单的值仅仅是 `"0"`。

## 客户端身份验证

尽管 X 环境通常被认为相对不安全，但预防措施有助于防止未经授权的访问。在安全性还不是如此紧迫的问题的时代，X 服务器欢迎来自运行在通过 `xhost` 命令标记为安全的主机上的任何客户端的连接是常见现象。但由于该主机上的任何用户都可以连接到你的显示器并造成破坏（无论无意还是由于混淆），使用 `xhost` 方法授予客户端访问权限最终被废弃。我们不再对其进行讨论。

基于主机的安全的最常见替代方案是魔术 Cookie（magic cookie）身份验证。虽然魔术 Cookie 可能会让我们某些读者产生回溯，但在在此背景下，它们被用于身份验证连接。基本思想是 X 显示管理器在登录过程早期生成一个巨大的随机数，称为 cookie。该 cookie 被写入用户主目录下的 `~/.Xauthority` 文件中。任何拥有 cookie 的客户端都被允许连接。用户可以运行 `xauth` 命令查看现有的 cookie 并向此文件添加新的 cookie。

展示这种工作原理的最简单方法是使用示例。假设你在客户端系统上设置了 `DISPLAY` 变量，以便在你所在的机器上显示 X 应用程序。然而，当你运行一个程序时，你会得到一个类似下面的错误：

```
client$ xprogram -display=:0

Xlib: connection to "server:0.0" refused by server

xprogram: unable to open display 'server:0'
```

此消息告诉你客户端没有正确的 cookie，远程服务器拒绝了连接。要获得正确的 cookie，请登录到服务器（如果你正在尝试显示，你可能已经登录了），并通过运行 `xauth list` 列出服务器的 cookie：

```
server$ xauth list

server:0 MIT-MAGIC-COOKIE-1 f9d888df6077819ef4d788fat778dc9f

server/unix:0 MIT-MAGIC-COOKIE-1 f9d888df6077819ef4d788fat778dc9f

localhost:0 MIT-MAGIC-COOKIE-1 cb6cbf9e524128749fedd4f0ee279
```

## 带 SSH 的 X 连接转发

服务器上的每个网络接口都有一个条目。此示例显示了以太网的 cookie、用于本地连接的 UNIX 域套接字的 cookie，以及本地回回环网络接口的 cookie。

将 cookie 获取到客户端的最简单方法（在不使用 SSH 时）是使用老式的复制粘贴。大多数终端模拟器（例如 `xterm`）允许你用鼠标选择文本并将其粘贴到另一个地方，通常是通过按下鼠标按钮。方便的是，`xauth add` 命令接受与 `xauth list` 显示相同的格式。你可以像这样向客户端添加 cookie：

```
$client xauth add server:0 MIT-MAGIC-COOKIE-1 9d88df6077819ef4fd88fat77dc9
```

你应该通过在客户端上运行 `xauth list` 来验证 cookie 是否正确添加。在设置了 `DISPLAY` 环境变量并向客户端了正确的 cookie 后，现在可以在服务器上显示了。如果你在使用 cookie 时遇到困难，可以临时退回到 `xhost` 身份验证，以验证是否存在其他问题（例如阻止客户端访问服务器的防火墙或网络限制）。测试完成后，始终运行 `xhost`（即以 dash 作为唯一参数的 `xhost`）来禁用 `xhost` 身份验证。

## 带 SSH 的 X 连接转发

魔术 Cookie 增加了安全性，但它们并非万无一失。任何获取你 cookie 的用户都可以连接到显示器并运行监控你活动的程序。如果没有你的 cookie，X 协议允许几乎任何人嗅探。

你可以使用 SSH（安全外壳协议）提升安全性。SSH 提供经过验证和加密的终端服务。然而， SSH 还可以通过安全通道转发任意网络数据。X 转发类似于 SSH 端口转发，但由于 SSH 是感知 X 的，你可以获得一些额外的功能，包括远程机器上的伪显示器以及协商的魔术 cookie 传输。

你通常从运行 X 服务器的机器 `ssh` 到你想运行 X 程序的机器。这种安排可能会令人困惑，因为 SSH 客户端运行在与 X 服务器相同的机器上，并连接到与 X 客户端应用程序位于同一机器上的 SSH 服务器。糟糕的是，SSH 为你的 X 服务器创建的虚拟显示器位于远程本地。下一页的图 B 显示了 X 流量如何通过 SSH 连接流动。

+ 3. 或者针对 AIX 使用 `aixterm`。很聪明，对吧？

## 附件 B 配合 SSH 使用 X

![](img/9b33263d3e7e36cd43da7756018c8735_1066_0.png)

你的 `DISPLAY` 变量和认证信息由 `ssh` 自动设置。显示数字从 -10.0 开始，对于每个转发 X 流量的 SSH 连接递增。

示例有助于理解这一序列。

```
x-server$ ssh -v -X x-client.mydomain.com

SSH-2.0-OpenSSH_5.1

debug1: Reading configuration data /home/boggs/ssh/config

debug1: Reading configuration data /etc/ssh/ssh_config

debug1: Applying options for *

debug1: Connecting to x-client.mydomain.com [192.168.1.99] port 22.

debug1: Connection established.

Enter passphrase for key '/home/boggs/ssh/id_rsa':

debug1: read private key done: RSA

debug1: Authentication succeeded (publickey).

debug1: Entering interactive session.

debug1: Requesting X forwarding with authentication.

debug1: Requesting authentication agent

x-client$
```

从最后两行可以看出，客户端正在请求为 X11 应用程序进行转发。SSH 服务器和客户端上都必须启用 X 转发，并且客户端必须拥有正确的 X 服务器代码。如果某些功能运行不正常，请尝试如上所示的 `-X` 和 `-v` 标志（OpenSSH），以显式启用 X 转发并请求详细输出。还要检查 `/etc/ssh` 中的全局配置文件，以确保 X11 未被禁用。登录后，你可以检查你的显示和 cookie：

```
x-client$ echo $DISPLAY

localhost:10.0

x-client$ xauth list
```
