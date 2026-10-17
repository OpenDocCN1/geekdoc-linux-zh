
```
$ app_name profile
mkdir ~/, directory_name
whitelist ~/directory_name
include /etc/firejail/whitelist-common.inc
include /etc/firejail/default.profile
```

在这里，我们将 `directory_name` 加入白名单，它位于 `app_name` 目录结构内。会话配置从 `whitelist-common.inc` 中包含。

## 08 Firefox 沙箱化

通过执行以下命令启动 Firefox 进程：

```bash
$ firejail firefox
```

Firefox 的单个实例可以有多个浏览器窗口。因此，如果 Firefox 已经在运行，并且你想在 Firejail 中启动一个新会话，请执行：

```bash
$ firejail firefox --no-remote
```

沙箱仅允许 Firefox 访问少量文件和目录。如果 Firefox 试图访问被列入黑名单的文件，日志消息将发送到 syslog。默认启用的安全过滤器减少了内核的攻击面。seccomp 过滤器通常默认使用。如果你不信任浏览器中安装的扩展和插件，请使用 `--private` 选项并在沙箱级别配置 DNS。这可以防止来自重新配置 DNS 的攻击。

```bash
$ firejail --private --dns=8.8.8.8 --dns=8.8.4.4 firefox --no-remote
```

要创建新的 TCP/IP 栈，连接到你的以太网网络并指定明确的 IP 地址：

```bash
$ firejail --net=eth0 --ip=192.168.1.207 firefox
```

Firejail 用 Xpra 或 Xephyr 服务器替换常规 X11 服务器，防止 X11 键盘记录器和截图实用程序访问主 X11 服务器。

```bash
$ firejail --x11 --net=eth0 firefox
```

## 09 Seccomp 过滤器

Firejail 默认使用 Seccomp-bpf。它代表安全计算模式，以 Berkeley 数据包过滤器 (BPF) 格式表示。使用 Firejail 沙箱构建白名单 seccomp 过滤器并将其附加到用户程序。Firejail 需要 seccomp 过滤器的系统调用详细信息。我们使用 strace 来获取系统调用。让我们以 VLC 媒体播放器为例：

```bash
$ strace -qc vlc
```

这会打开 VLC；一旦你关闭它，strace 就会打印系统调用列表。将所有系统调用的列表复制到文本编辑器中，并将它们转换为无空格的逗号分隔形式。现在将此逗号分隔的系统调用字符串用于 `--seccomp`。保留以下值：

```bash
$ firejail --shell=none --seccomp=keep=poll,futex,[...] vlc
```

该命令看起来很长，但请确保包含所有系统调用。如果出现错误，添加遗漏的系统调用。现在在 `/etc/firejail` 中创建一个白名单配置文件。将默认的 VLC 配置文件复制到这里，并添加以下两行：

```
shell none
seccomp keep poll,futex,rt_sigreturn,stat,read,[...]
```

请注意，点号表示其余的逗号分隔的系统调用名称。

## 10 AppImage 支持

AppImage 是由 Simon Peter 开发的通用软件打包格式。

使用以下命令在 Firejail 中启动你的 AppImage 应用程序：

```bash
$ firejail --appimage=Firefox-50.1.0.g1ibc2.3.3-x86_64.AppImage
```

所有沙箱选项都可用，例如 `--private` 或 `--x11`。假设你已从 AppImage 项目仓库下载了 Firefox；要启动沙箱，请使用：

```bash
$ firejail --appimage --private --net=eth0 --x11 ~/Downloads/Firefox-50.1.0.g1ibc2.3.3-x86_64.AppImage
```

`--appimage` 用于进入 AppImage 模式，`--private` 创建空主目录，`--net=eth0` 创建新的网络命名空间，`--x11` 用于基于 Xpra 的沙箱化。

要验证安全参数，打开 Firetools 并点击 Firefox 沙箱以获取统计信息。查看 seccomp 统计信息已启用，以及 capability 字段为零？对于沙箱而言，这两个参数最为重要，其他一切均构建在此之上。如果有多个沙箱在运行，请按如下方式限制每个沙箱的带宽：

```bash
$ firejail --bandwidth=32119 set eth0 80 20
```

> Firejail 可以为沙箱附加一个新的 TCP/IP 网络栈，该栈拥有自己的路由表、防火墙和接口集。此栈独立于主机网络栈 [19]

## Firejail 对 X11 的沙箱化

Xpra 和 Xephyr 受 Firejail X11 沙箱化支持。常规 X11 由这些 X11 软件包替换：

```bash
$ firejail --x11=xpra --net=eth0 program-and-arguments

$ firejail --x11=xephyr --net=eth0 program-and-arguments
```

另一个选项是使用：

```bash
$ firejail --x11 --net=eth0 program-and-arguments
```

这样，Firejail 首先尝试使用 Xpra，如果未安装，则尝试查找 Xephyr。请注意，是以 root 用户身份启动 Xpra。不支持 X11 沙箱化功能。

# 使用 Erlang 编程：文件 I/O

![](img/6866071e033820549b214c239744aaa0_45_0.png)

Mihalis Tsoukalos 是一名 UNIX 管理员、程序员（UNIX 和 iOS）、数据库管理员（DBA）以及数学家。他自 1993 年起开始使用 Linux。你可以通过 Twitter 上的 @mactosouk 或他的网站 mtoukalos.eu 联系到他。

了解如何在 Erlang 中处理文件操作

## 资源

- Erlang 的安装环境

- 文本编辑器，例如 Emacs 或 vi

如果一种编程语言无法处理文本和二进制文件，那么它就不能被认为是一种重要的语言，因为如果不从现有文件中读取数据或将数据存储到文件中，你就无法开发实用的系统工具。因此，本教程的主题将使用 Erlang 处理文件和目录，这也包括允许你查找文件信息的 Erlang 函数。

下一篇 Erlang 教程将讨论 Erlang 中的网络编程，这也是一个非常重要且必不可少的任务，所以请继续阅读并尽可能多地编写 Erlang 代码。

## 关于文件 I/O

文件操作是系统编程的关键部分，因此它们必须可靠且快速；然而，在这种情况下，可靠性比速度更重要！可靠性的一部分来自于错误检查和错误报告代码，因为你无法确定什么会失败以及为什么会失败。

与文件操作相关的大多数函数都属于 `file` 模块，该模块为你提供文件系统接口。`file` 模块中与文件输入和输出相关的两个最重要的 Erlang 函数是 `file:read()` 和 `file:write()`。

第一个函数用于从打开的文件中读取，而第二个函数用于向文件写入数据。`file:read()` 函数接受两个参数：一个打开的文件描述符和你想要读取的字节数。`file:write()` 函数也需要两个参数：分别是你想要写入的文件的打开文件描述符以及你想要写入的数据。正如你将看到的，有更容易的方式来读取文件。

为了打开和关闭文件，你还需要另外两个函数，分别是 `open(File, Mode)` 和 `close(Device)`。`file:open()` 函数接受两个参数，即你想要打开的文件位置和你想要打开文件的方式（模式）。成功调用 `file:open()` 会返回一个类型为 `{ok, FD}` 的元组。第一个元素表示操作成功，第二个元素用于随后引用打开的文件。

`Mode`（模式）部分可以有四个值：`Read`、`Write`、`Append` 和 `Exclusive`。

Erlang 提供了 `file:read_file()` 函数，该函数接受一个参数，即文件名，并将其完整内容一次性存储到一个变量中。虽然此函数无法完全替代 `file:read()`，但它时不时非常实用！

## 处理命令行参数

本节将说明如何在 Erlang 中读取程序的命令行参数，这是一个非常重要的任务，因为大多数时候你都会将需要处理的文件名称作为参数传入。`cmdArgs.erl` 的 Erlang 代码如下所示。
