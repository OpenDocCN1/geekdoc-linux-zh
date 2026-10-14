

## X 窗口系统

X 窗口系统又被称为“X”，这种图形用户界面提供了当今大多数计算机系统常见的“桌面上的窗口”隐喻。在 X 下，应用程序充当客户端，访问 X 服务器，而 X 服务器管理着所有屏幕活动。此外，客户端应用程序可以与 X 服务器位于不同的系统上，从而允许远程显示该应用程序的图形用户界面。

## XFree86

X 窗口系统的一个免费实现。

## 附录 F：Kickstart 安装

由于需要自动化安装，Red Hat Software 创建了 Kickstart 安装方法。使用这种方法，系统管理员可以创建一个单独的文件，其中包含通常在一次典型的 Red Hat Linux 安装过程中会被询问的所有问题的答案。Kickstart 安装方法非常强大，通常只需一个 Kickstart 文件即可在多台机器上安装 Red Hat Linux。

**请注意：** Kickstart 安装只能使用 CD-ROM 和 NFS 安装方法执行。FTP、HTTP、SMB 或本地硬盘安装无法使用 Kickstart 模式自动完成。

### Kickstart 文件的放置位置

要使用 Kickstart 模式，必须首先创建一个 Kickstart 文件，并使其可供 Red Hat Linux 安装程序使用。通常，这可以通过将 Kickstart 文件复制到启动软盘，或将其放到网络上完成。基于网络的方法最为常用，因为大多数 Kickstart 安装都是在联网计算机上进行的。这也使得在多台计算机上安装 Red Hat Linux 更加容易，因为 Kickstart 文件可以保存在单个服务器系统上，并在安装过程中由各计算机读取。下面更深入地了解 Kickstart 文件可以放置的位置。

### 放在软盘上

要执行基于软盘的 Kickstart 安装，Kickstart 文件必须命名为 `ks.cfg`，并位于启动软盘的顶层目录中。请注意，Red Hat Linux 启动软盘采用 MS-DOS 格式，因此可以轻松地在 Linux 下使用 `mcopy` 命令复制 Kickstart 文件（如果你坚持，也可以使用 Windows）。尽管技术上没有此要求，但大多数基于软盘的 Kickstart 安装都是从 CD-ROM 安装 Red Hat Linux。

### 放在网络上

使用 Kickstart 的网络安装相当常见，因为系统管理员可以轻松快速地自动安装许多联网计算机，而且不会带来麻烦。通常，最常用的做法是让管理员在本地网络中同时拥有 BOOTP/DHCP 服务器和 NFS 服务器。BOOTP/DHCP 服务器用于向客户端系统提供网络信息，而 NFS 服务器则提供安装过程中实际使用的文件。通常这两个服务器运行在同一台物理机器上，但这不是必需的。要进行基于网络的 Kickstart 安装，你的网络中必须有一台 BOOTP/DHCP 服务器，并且该服务器必须包含你要安装的机器的配置信息。BOOTP/DHCP 服务器将用于向客户端提供其网络信息以及 Kickstart 文件的位置。如果 BOOTP/DHCP 服务器指定了 Kickstart 文件，客户端系统将尝试对该文件路径进行 NFS 挂载，并将指定文件复制到客户端，将其用作 Kickstart 文件。所需的具体设置因你使用的 BOOTP/DHCP 服务器而异。以下是随 Red Hat Linux 附带的 DHCP 服务器的一个示例：

```
filename "/usr/new-machine/kickstart/";
next-server blarg.redhat.com;
```

请注意，应使用 `filename` 指定 Kickstart 文件的名称（或 Kickstart 文件所在的目录），并使用 `next-server` 设置 NFS 服务器名称。如果 BOOTP/DHCP 服务器返回的文件名以斜杠（`"/"`）结尾，则它仅被解释为路径。在这种情况下，客户端系统会使用 NFS 挂载该路径，并查找一个具有特定名称的文件。客户端查找的文件名为：

```
<ip-addr>-kickstart
```

文件名中的 `<ip-addr>` 部分应替换为客户端 IP 地址的点分十进制表示法。例如，IP 地址为 10.10.0.1 的计算机对应的文件名为：

```
10.10.0.1-kickstart
```

