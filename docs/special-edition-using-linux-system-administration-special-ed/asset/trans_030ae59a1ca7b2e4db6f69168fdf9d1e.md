
> **注意**  
> `lp=/dev/lp1` 条目必须指向一个有效设备，尽管 smbprint 脚本会将打印作业重定向到远程打印机，而不是打印到指定的本地打印机。

以下是 smbprint 脚本的源代码。如果你的 Samba 发行版尚未包含此脚本，请将其创建在 `/usr/bin/smbprint`，并使用命令 `chmod +x /usr/bin/smbprint` 使其可执行：

```
#!/bin/sh

# This script is an input filter for printcap printing on a unix machine. It
# uses the smbclient program to print the file to the specified smb-based
# server and service.
# For example you could have a printcap entry like this
#
# smb:lp=/dev/null:sd=/usr/spool/smb:sh:if=/usr/local/samba/smbprint
# which would create a unix printer called "smb" that will print via this
# script. You will need to create the spool directory /usr/spool/smb with
# appropriate permissions and ownerships for your system.

# Set these to the server and service you wish to print to
# In this example I have a WfWG PC called "lapland" that has a printer
# exported called "printer" with no password.
#
#
# Script further altered by hamilton@ecnz.co.nz (Michael Hamilton)
# so that the server, service, and password can be read from
# a /var/spool/lpd/PRINTNAME/.config file.
#
# In order for this to work, the /etc/printcap entry must include an
# accounting file (af=...):
#
#   cdcolour:\
#     :cm=CD IBM Colorjet on 6th:\
#     :sd=/var/spool/lpd/cdcolour:\
#     :af=/usr/local/etc/smbprint/acct:\
#     :if=/usr/local/etc/smbprint:\
#     :mx=0:\
#     :lp=/dev/null:
#
# The /var/spool/lpd/PRINTNAME/.config file should contain:
#   server=PC_SERVER
#   service=PR_SHARENAME
#   password="password"
#
# E.g.
#   server=PAULS_PC
#   service=CJET_371
#   password=""
#
# Debugging log file, change to /dev/null if you like.
#
# logfile=/tmp/smb-print.log
logfile=/dev/null

#
# The last parameter to the filter is the accounting file name.
# Extract the directory name from the file name.
# Contact with this w/config to get the config file.

eval acct_file=\${$#}
spool_dir=`dirname $acct_file`
config_file=$spool_dir/.config

# Should read the following variables set in the config file:
#   server
#   service
#   password
eval `cat $config_file`

#
# Some debugging help, change the >> to > if you want to save space.
#
echo "server $server, service $service" >> $logfile

(
# NOTE You may wish to add the line `echo translate` if you want automatic
# CR/LF translation when printing.
#       echo translate
echo 'print .'
cat
) | /usr/bin/smbclient "\\\\$server\\$service" $password -U $server -N -P >>
$logfile
```

> **注意：** 某些 Linux 发行版（如 Red Hat Linux 和 Corel Linux）提供了简单的图形化工具，用于设置与共享 SMB 打印机的连接。

## 什么是 NFS？

NFS 代表 *网络文件系统*（Network File System）。它最初由 Sun Microsystems 为其 UNIX 系统开发，现在已成为通过 TCP/IP 网络协议在 UNIX 和 Linux 系统之间共享文件和目录的事实标准。除了用于在 Linux 和 UNIX 系统之间共享文件和目录外，还有其他操作系统（如 Windows 和 Novell NetWare）的扩展，使它们能够与 NFS 服务器通信，并与 NFS 客户端共享文件和目录。

如果你不需要与基于 SMB 的 Windows 网络共享文件和目录，可以考虑使用 NFS 进行文件和目录共享，因为它更紧密地集成到 Linux 网络环境的核心中，并且更容易配置和保持平稳运行。

> **警告：** NFS 存在一些众所周知的安全问题，应谨慎使用，并且仅在必要时使用。通常，你只应考虑在防火墙后面的受保护内网中使用 NFS。

## 配置 NFS

维护一个正在运行的 NFS 服务器需要多个程序。这些程序包括：

- **portmap（或 rpc.portmap，取决于你的 Linux 发行版）：** 该程序提供端口到远程过程调用（RPC）程序的映射，以便 NFS 能够工作。如果你打算运行 NFS 服务器，应在引导时启动该程序。请参阅第4章“启动与关闭”，了解如何将系统配置为在引导时启动 portmap。你可以使用以下命令检查 portmap 是否正在运行：

  ```
  # rpcinfo -p
      program vers proto  port
      100000  2   tcp    111 portmapper
      100000  2   udp    111 portmapper
  ```

- **mountd（或 rpc.mountd，取决于你的 Linux 发行版）：** 如果你正在运行 Linux NFS 服务器，该程序应在引导时启动。

- **nfsd（或 rpc.nfsd，取决于你的 Linux 发行版）：** 如果你正在运行 Linux NFS 服务器，该程序应在引导时启动。

在 mountd 和 nfsd 运行之后，`rpcinfo -p` 应报告它们的存在：

```
# rpcinfo -p
    program vers proto  port
    100000  2   tcp    111 portmapper
    100000  2   udp    111 portmapper
    100005  1   tcp    747 mountd
    100005  1   udp    745 mountd
    100003  2   tcp    2049 nfs
    100003  2   udp    2049 nfs
```

所有导出目录的配置都在 `/etc/exports` 文件中完成。exports 文件包含一系列条目，每行一个，一般形式为：

```
<directory> <host name>(<permissions>) <host name>(<permissions>) \
<host name>(<permissions>) ...
```

指定的 directory 就是要共享的目录。每个 hostname 是被授予访问共享目录权限的主机名称，权限列表是一个逗号分隔的列表，列出了授予指定主机上用户的权限，这些权限取自你在表 14.4 中看到的权限列表。

| 权限 | 描述 |
| --- | --- |
| `rw` | 允许以读写模式访问该目录 |
| `ro` | 允许以只读模式访问该目录 |
| `insecure` | 允许所有未经认证的访问该目录 |
| `kerberos` | 使用 Kerberos 认证来访问该目录 |
| `link_absolute` | 保持符号链接不变 |
| `link_relative` | 根据需要将符号链接转换为相对链接 |
| `root_squash` | 拒绝远程客户端上的 root 用户在 NFS 服务器上获得 root 访问权限 |
| `secure-rpc` | 使用 RPC 认证来访问该目录（默认开启） |

通常，如果 `root_squash` 提供的额外安全性是必需的，则只需 `rw` 或 `ro` 之一。例如，要使用 NFS 共享目录 /somedir，并允许 host1 上的用户具有完全读写访问权限，host2 上的用户具有受限的只读访问权限且不进行根账户映射，请在 /etc/exports 中使用以下条目：

```
/somedir host1(rw) host2(ro,root_squash)
```

/etc/exports 文件中的主机名也可以使用通配符指定。例如，要允许所有以 mydomain.com 结尾的主机访问相关目录，请在 /etc/exports 文件的条目中使用 `*.mydomain.com` 作为主机名。

每当你更改 /etc/exports 文件时，通过向 mountd 和 nfsd 发送 SIGHUP 信号，强制它们重新加载该文件：

```
# killall -HUP /usr/sbin/mountd
# killall -HUP /usr/sbin/nfsd
```

## 用户权限与 NFS

当远程系统上的用户尝试通过 NFS 访问共享目录时，NFS 服务器首先检查 /etc/exports 文件，以确定客户端主机上的用户是否被允许访问该目录。如果允许，则进行用户和组映射。如果 NFS 客户端和服务器共享相同的用户和组 ID 号，则使用尝试挂载目录的用户的 UID 和 GID，根据目录的本地 Linux 文件权限来确定该用户是否具有足够的访问权限来连接该目录。

当客户端和服务器具有不同的 UID 和 GID 编号空间时，NFS 守护进程会尝试在客户端的 UID 和 GID 空间与服务器的空间之间进行转换，以确定是否应授予访问权限。

## 使用 NFS 访问远程共享目录

要访问远程 NFS 服务器共享的目录，请在客户端使用 mount 命令。mount 命令可用于挂载本地文件系统，也可用于挂载使用 nfs 文件系统类型的远程 NFS 文件系统。要挂载远程文件系统，请使用以下语法：

```
# mount -t nfs <host name>:<directory> <local mount point> -o <options>
```

`<host name>:<directory>` 组合是远程共享目录的主机名和目录。例如，要访问远程 NFS 服务器 someserver 上的 /somedir 目录，你需要挂载 someserver:/somedir。本地挂载点是本地系统上某个目录的路径，最好为空目录，远程目录应通过该路径挂载并使其可访问。

一系列选项是可选的，是从表 14.5 中给出的选项列表中选取的逗号分隔列表。

**表 14.5 使用 mount 挂载 NFS 目录的选项**

| 选项 | 描述 |
| --- | --- |
| `hard` | 创建硬挂载。这是默认选项。当硬挂载目录的尝试失败时，它会超时并生成错误消息，然后以更大的超时值再次尝试。此过程将重复进行，直到挂载成功。 |
| `intr` | 允许对 NFS 调用进行中断。这通常不是必需的。 |
| `rsize=<datagram size>` | 指定读请求的数据报大小（以字节为单位）。默认值 1024 字节通常就足够了。 |
| `soft` | 创建软挂载。当软挂载目录的尝试失败时，仅生成主要的超时，且不会报告。你通常可以更快地重新控制系统。 |
| `timeo=<time>` | 以十分之一秒为单位指定 NFS 请求的超时时间。默认值为十分之七秒。 |
| `wsize=<datagram size>` | 指定写请求的数据报大小（以字节为单位）。默认值 1024 字节通常就足够了。 |

例如，要将 someserver:/somedir 目录本地挂载到 /nfsmount，并为较差的网络连接指定 1 秒的超时时间，请使用以下命令：

```
# mount -t nfs someserver:/somedir /nfsmount -o timeo=10
```

## 配置 lpd 以实现远程打印

Linux 通常使用 lpd 守护进程进行打印。lpd 可以管理一个或多个本地和远程打印机的打印队列。在本章前面讨论 Samba 时，你看到了
