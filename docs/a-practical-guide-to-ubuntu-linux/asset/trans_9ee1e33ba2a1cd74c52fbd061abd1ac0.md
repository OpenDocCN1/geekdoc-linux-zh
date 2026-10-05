

# 设置服务器 469

该程序将指定程序的权限降低到指定用户的权限。此程序作为解决上述问题的简单方案提供，你可以通过实验使用 chroot 监狱（chroot jail）来更好地理解它的工作原理。

```
$ cat uchroot.c
```

* 使用条款请参阅 svn.gna.org/viewcs/etoile/trunk/Etoile/LiveCD/uchroot.c。 */

```c
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
    /* 解析参数 */
    struct passwd *pass = getpwnam(argv[1]);
    if(pass == NULL)
    {
        printf("Unknown user %s\n", argv[1]);
        return 2;
    }
    /* 设置所需的 UID */
    chdir(argv[2]);
    if(chroot(argv[2]))
    {
        setgid(pass->pw_gid);
        setuid(pass->pw_uid);
    }
    printf("%s must be run as root. Current uid=%d, eid=%d\n",
        argv[0],
        (int)getuid(),
        (int)geteguid());
    return 3;
    }
    char buf[100];
    return execv(argv[3], argv + 3);
}
```

以下命令的第一条编译 uchroot.c，创建一个名为 uchroot 的可执行文件。随后的命令将 uchroot 移动到 /usr/local/bin 并赋予其适当的所有权。

```
$ cc -o uchroot uchroot.c
$ sudo mv uchroot /usr/local/bin
$ sudo chown root /usr/local/bin/uchroot
$ ls -l /usr/local/bin/uchroot
rwxr-xr-x 1 root 7922 2010-07-17 08:26 /usr/local/bin/uchroot
```

使用本节之前的设置，执行以下命令在 chroot 监狱中以用户 sam 的权限运行 shell：

```
$ sudo /usr/local/bin/uchroot sam /tmp/jail /bin/bash
```

# 维护多个 chroot 监狱

提示：如果你计划部署多个 chroot 监狱，最好在某个活动监狱之外的其他地方保留一份 bin 和 lib 目录的干净副本。

# 在 chroot 监狱中运行服务

在监狱内运行 shell 的用处有限。在实际操作中，你可能更想在监狱内运行某个特定的服务。要在监狱内运行服务，请确保该服务所需的所有文件都在监狱中。使用 uchroot，在 chroot 监狱中启动服务的命令格式如下：

```
$ sudo /usr/local/bin/uchroot user jailpath daemonname
```



其中，jailpath 是监狱目录的路径，user 是运行守护进程（daemon）的用户名，daemonname 是提供服务的守护进程的（监狱内部）路径。

某些服务器已设置为利用 chroot 监狱。例如，你设置了 DNS 在监狱中运行（详见第 847 页），且 vsftpd FTP 服务器可以为客户端自动启动 chroot 监狱（详见第 703 页）。

# 安全考虑

某些服务需要由具有 root 权限的用户或进程运行，但在启动后会释放 root 权限（Apache、Procmail 和 vsftpd 都是示例）。如果你正在运行此类服务，则不需要使用 uchroot 或在监狱内放置 su 或 sudo。

具有 root 权限的进程可能会逃离 chroot 监狱。因此，你会在启动运行在监狱内部的程序之前降低其权限。此外，要小心允许在监狱内部的 setuid（详见第 218 页）二进制文件——其中任何一个的安全漏洞都可能危及监狱的安全。此外，确保用户无法访问其上传到监狱的可执行文件。

# DHCP：配置网络接口

与其在每个系统的本地文件上存储网络配置信息相比，DHCP（动态主机配置协议）允许客户端在每次连接到网络时，从 DHCP 服务器检索必要的网络配置信息。DHCP 服务器根据需要从地址池中向客户端分配 IP 地址。分配的地址通常是临时的，但并非必须如此。

与在本地文件中存储网络配置信息相比，这种技术具有以下优点：

# 设置服务器

- 新用户可以建立 Internet 连接，而无需处理 IP 地址、子网掩码、DNS 地址和其他技术细节。经验用户可以更快地建立连接。

- DHCP 通过在服务器上集中处理过程，便于 IP 地址及相关网络信息的分配和管理。系统管理员可以配置新系统（包括从不同位置连接网络的笔记本电脑）使用 DHCP；DHCP 只在每个系统连接到网络时才分配 IP 地址。地址池在 DHCP 服务器上作为一个组进行管理。

- DHCP 有助于多个系统使用 IP 地址，减少了所需的 IP 地址总数。这种地址的节省非常重要，因为 IPv4 地址正在迅速耗尽。虽然一个特定的 IP 地址一次只能被一个系统使用，但许多终端系统在连接互联网时偶尔需要地址。通过重用 IP 地址，DHCP 延长了 IPv4 协议的寿命。DHCP 适用于 IPv4，因为 IPv6（详见第 387 页）强制系统在连接到网络时自动配置 IP 地址（称为自动配置）。

对于负责维护大量系统的管理员来说，DHCP 特别有用，因为个人不再需要存储每个唯一的配置信息。通过 DHCP，管理员可以设置一个主系统，并使用主系统的磁盘副本部署新系统。在教育机构和其他开放访问设施中，硬盘镜像可以存储在共享驱动器上，该镜像可以在每天结束时自动恢复到原始状态。

# 更多信息

Web www.dhcp.org
DHCP FAQ: www.dhcp-handbook.com/dhcp_faq.html

HOWTO DHCP Mini HowTO

# DHCP 如何工作

使用 DHCP，客户端联系服务器守护进程 dhcpd 以获取 IP 地址、广播地址、名称服务器地址和其他网络参数。作为交换，服务器向客户端提供租约（lease）。当客户端连接到网络时，客户端会在每个租约期的过半自动更新租约。当客户端断开网络时，租约可能会过期。你也可以使用 firestarter（详见第 866 页）来配置和运行 DHCP 服务器。

# DHCP 客户端

DHCP 客户端从服务器请求网络参数并配置其接口。

# 前提条件

确保安装了软件包：

- dhcp3-client

dhclient: DHCP 客户端
当 DHCP 客户端连接到网络时，它会请求租约并配置接口。一旦 DHCP 客户端请求建立了租约，它会将租约存储在 /var/lib/dhcp3/leases 文件中。接口是客户端使用的接口名称，例如 eth0。当服务器或客户端需要重启时，系统将使用这些信息重新建立租约。只有在需要自定义配置时，才修改默认 DHCP 客户端配置文件 /etc/dhcp3/dhclient.conf。以下 /etc/dhcp3/dhclient.conf 指定了单一接口 eth0：

```
interface "eth0"
{
send dhcp-client-identifier 1:xxxxxxxxxxxx;
send dhcp-lease-time 86400;
}
```

```

在前面的文件中，dhcp-client-identifier 中的 1 表示以太网，xxxxxxxxxxxxx 是控制该接口的设备的 MAC 地址（第 1158 页）。请参考第 474 页有关确定设备 MAC 地址的说明。dhcp-lease-time 是 IP 地址租约的持续时间（秒为单位）。对于工作站来说，86400 秒（或一天）是一个合理的选择。

