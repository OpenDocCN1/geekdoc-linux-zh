

将 PAM 及其库和配置文件、`sudo`（或 `su`）以及 `/etc/passwd` 文件全部放入沙箱中。或者，你可以重新编译 `su` 或 `sudo`。但是，源代码调用了 PAM，因此你需要修改源代码以使其不调用 PAM。这两种方法中的任何一种都耗时，并且会引入可能导致沙箱不安全的复杂性。

以下 C 程序<sup>1</sup> 在 `chroot` 沙箱中运行具有减少特权的程序。由于该程序在调用 `chroot()` 之前获取你在命令行指定的用户的 UID 和 GID，因此你不需要将 `/etc/passwd` 放入沙箱中。该程序将指定程序的权限降低为指定用户的权限。此程序作为上述问题的简单解决方案呈现，以便你可以实验 `chroot` 沙箱并更好地理解其工作原理。

```c
/* See svn.gna.org/viewcvs/etoile/trunk/Etoile/LiveCD/uchroot.c for terms of use. */
#include <stdio.h>
#include <stdlib.h>
#include <pwd.h>

int main(int argc, char * argv[])
{
    if(argc < 4)
    {
        printf("Usage: %s {username} {directory} {program} [arguments]\n", argv[0]);
        return 1;
    }

    /* Parse arguments */
    struct passwd * pass = getpwnam(argv[1]);
    if(pass == NULL)
    {
        printf("Unknown user %s\n", argv[1]);
        return 2;
    }

    /* Set the required UID */
    chdir(argv[2]);
    if(chroot(argv[2]))
        ||
        setgid(pass->pw_gid)
        ||
        setuid(pass->pw_uid))
    {
        printf("%s must be run as root. Current uid=%d, euid=%d\n",
            argv[0],
            (int)getuid(),
            (int)geteuid()
        );
        return 3;
    }

    return execv(argv[3], argv + 3);
}
```

1. 感谢 David Chisnall 和 Étoilé 项目（etoileos.com）提供的 **uchroot.c** 程序。

以下命令中的第一个使用 `cc`（gcc 包）编译 **uchroot.c**，创建一个名为 **uchroot** 的可执行文件。后续命令将 **uchroot** 移动到 /usr/local/bin 并赋予其适当的归属权。

```bash
$ cc -o uchroot uchroot.c
$ su
password:
# mv uchroot /usr/local/bin
# chown root:root /usr/local/bin/uchroot
# exit
$ ls -l /usr/local/bin/uchroot
-rwxr-xr-x. 1 root root 8924 07-26 14:24 /usr/local/bin/uchroot
```

使用本节前面的设置，运行以下命令以在 `chroot` 沙箱内以用户 **sam** 的权限运行 shell：

```bash
# /usr/local/bin/uchroot sam /home/sam/jail /usr/bin/bash
```

## 维护多个 chroot 沙箱

> 如果你计划部署多个 `chroot` 沙箱，最好在其他位置保留 **bin** 和 **lib** 目录的干净副本，而不是在一个活动的沙箱中保留。

## 在 chroot 沙箱中运行服务

在沙箱内运行 shell 的实用性有限。实际上，你更有可能想要在沙箱内运行特定的服务。要在沙箱内运行服务，请确保该服务所需的所有文件都在沙箱内。使用 **uchroot**，在 `chroot` 沙箱中启动服务的命令格式为

```bash
# /usr/local/bin/uchroot user jailpath daemonname
```

其中 *jailpath* 是沙箱目录的路径名，*user* 是运行守护进程的的用户名，*daemonname* 是提供服务的守护进程的路径名（在沙箱内）。

一些服务器已经设置好可以利用 `chroot` 沙箱。例如，你可以设置 DNS，使 **named** 在沙箱中运行（第 883 页），并且 **vsftpd** FTP 服务器可以自动为客户机启动 `chroot` 沙箱（第 729 页）。

## 安全考虑

某些服务需要由具有 root 权限的用户或进程运行，但在启动后释放其 root 权限（Apache、Procrail 和 **vsftpd** 是示例）。如果你在运行此类服务，则不需要使用 **uchroot** 或将 **su** 或 **sudo** 放入沙箱中。

以 root 权限运行的进程可能会逃离 `chroot` 沙箱。因此，在启动在沙箱内运行的程序之前，你应该减少权限。此外，要注意允许在沙箱内使用哪些 setuid（第 196 页）二进制文件——其中任何一个的安全漏洞都可能破坏沙箱的安全性。此外，确保用户无法访问他上传到沙箱的可执行文件。

# DHCP：配置网络接口

DHCP（动态主机配置协议）允许客户端系统在每次连接到网络时从 DHCP 服务器获取必要的网络配置信息，而不是将网络配置信息存储在每个系统的本地文件中。DHCP 服务器根据需要从地址池中向客户端分配 IP 地址。分配的地址通常是暂时的，但不一定如此。与将网络配置信息存储在本地文件中相比，这种技术有几个优点：

- 新用户无需处理 IP 地址、子网掩码、DNS 地址和其他技术细节即可设置互联网连接。经验丰富的用户可以更快地设置连接。
- DHCP 通过在服务器上集中处理过程来促进 IP 地址和相关网络信息的分配和管理。系统管理员可以配置新系统（包括从不同位置连接到网络的笔记本电脑）使用 DHCP；然后 DHCP 仅在每个系统连接到网络时分配 IP 地址。IP 地址池在 DHCP 服务器上作为一个组进行管理。
- DHCP 促进多个系统使用 IP 地址，减少了所需的 IP 地址总数。这种地址保护很重要，因为互联网已经用完了 IPv4 地址。虽然特定的 IP 地址一次只能由一个系统使用，但许多最终用户系统仅在连接到互联网时才需要地址。通过重用 IP 地址，DHCP 延长了 IPv4 协议的生命周期。

DHCP 对于负责维护大量系统的管理员特别有用，因为新系统不再需要设置唯一的配置信息。

## DHCP 工作原理

使用 `dhclient`，客户端联系服务器守护进程 `dhcpd` 以获取 IP 地址、子网掩码、广播地址、名称服务器地址和其他网络参数。反过来，服务器向客户端提供 IP 地址的*租约*。客户端可以请求租约的具体条款，包括其持续时间；服务器可以限制这些条款。在连接到网络时，客户端通常根据需要请求其租约的延长，以便其 IP 地址保持不变。一旦客户端从网络断开连接，此租约必须过期，服务器在客户端请求新租约时提供新的 IP 地址。你还可以设置 DHCP 服务器为特定客户端提供静态 IP 地址（参见第 298 页的“静态与动态 IP 地址”）。

当你启动 Fedora/RHEL 时，系统会运行一个 DHCP 客户端，如果它找到一个，就会连接到 DHCP 服务器，并配置其网络接口。

# DHCP 客户端

DHCP 客户端从 DHCP 服务器请求网络配置参数，并使用这些参数来配置其网络接口。

## 前提条件

确保安装了以下软件包：

- dhclient

## dhclient：DHCP 客户端

当 DHCP 客户端系统连接到网络时，dhclient 从 DHCP 服务器请求租约并配置客户端的网络接口。一旦 DHCP 客户端请求并建立了租约，它将租约信息存储在一个名为 dhclient-*-interface.lease 的文件中，该文件位于 /var/lib/NetworkManager 目录中。interface 是客户端使用的接口名称，例如 eth0。系统使用这些信息在服务器或客户端需要重启时重新建立租约。DHCP 客户端配置文件 /etc/dhcp/dhclient.conf 仅用于自定义配置。/usr/share/doc/dhclient* 目录包含一个注释良好的 dhclient.conf 文件。

以下 dhclient.conf 文件指定了单个接口，ens33：

```bash
$ cat /etc/dhcp/dhclient.conf
interface "ens33" {
    send dhcp-client-identifier 1:xx:xx:xx:xx:xx:xx:xx;
    send dhcp-lease-time 86400;
}
```

在上面的文件中，dhcp-client-identifier 中的 1 指定了以太网网络，xx:xx:xx:xx:xx:xx 是控制该接口的设备的 MAC 地址（第 1259 页）。关于如何确定设备 MAC 地址的说明，请参阅第 494 页。dhcp-lease-time 是 IP 地址租约的持续时间（以秒为单位）。在客户端连接到网络期间，每当租约时间过去一半时，dhclient 会自动更新租约。对于工作站来说，86,400 秒（一天）的租约时间是一个合理的选择。

# DHCP 服务器

DHCP 服务器维护一个 IP 地址和其他配置参数的列表。客户端从服务器请求网络配置参数。DHCP 服务器不提供可工作的配置。请参考 /usr/share/doc/dhcp/*/example 文件中的示例 dhcpd.conf 文件，这些文件包含大量文档。

## 前提条件

安装以下软件包：

- dhcp

