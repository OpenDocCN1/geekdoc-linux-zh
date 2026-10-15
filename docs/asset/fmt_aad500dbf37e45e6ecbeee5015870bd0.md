
`setfacl` 的 `-b` 选项在添加 `file.acl` 中列出的访问控制项之前删除现有的 ACL。包含此选项允许你通过从文本文件中删除它们来简单的删除项。

# 第 6 章 软件安装与管理

## 软件安装与管理

![](img/d87305f54c4a442cf382141acae4b84f_200_0.png)

软件的安装、配置和管理是大多数系统管理员工作的大部分。管理员响应用户的安装和配置请求：

- 自动化操作系统安装
- 维护系统更新
- 管理软件

## 操作系统安装

请参第 402 页关于 DHCP 的信息。

PXE 的外部（网络）部分非常与其他架构类似。主机广播“发现”请求并开启 PXE 标志，DHCP 服务器响应包含 PXE 选项的包。

## 设置 PXE

DHCP、TFTP 和文件服务器都可以位于不同的主机上。TFTP 提供的引导文件包含一个指向可用操作系统镜像的菜单，这些镜像可以通过 HTTP、FTP、NFS 或其他网络协议从文件服务器获取。

### 图 A PXE 启动与安装过程

![](img/d87305f54c4a442cf382141acae4b84f_202_0.png)

### 表 6.1 系统与文档

| 系统 | 文档 |
| :--- | :--- |
| Red Hat | `redhat.com/docs/manual` |
| CentOS | `centos.org/wiki/ReleaseNotes` |
| Debian | `debian.org/releases/stable` |
| Ubuntu | `ubuntu.com/help/center` |
| FreeBSD | `freebsd.org/doc/handbook` |

`PXELINUX` 使用 PXE API 进行下载，因此在整个启动过程中都是硬件无关的。尽管名称如此，但 `PXELINUX` 并不限于启动 Linux。你可以部署 `PXELINUX` 来安装 FreeBSD 以及其他操作系统，包括 Windows。

在 DHCP 方面，ISC（互联网系统联盟）的 DHCP 服务器是提供 PXE信息的最佳选择。或者，可以尝试 `Dnsmasq` (`goo.gl/FNk7a`)，这是一款支持 DNS、DHCP 和网络启动的轻量级服务器。可以使用下文提到的 `Cobydler`。

关于 DHCP 服务器软件的更多信息，请参第 403 页。

## 使用 kickstart，Red Hat 和 CentOS 的自动化安装器

![](img/d87305f54c4a442cf382141acae4b84f_203_0.png)

Kickstart 是 Red Hat 开发的用于执行自动化安装的工具。它实际上只是标准 Red Hat 安装程序 `Anaconda` 的一个脚本接口，并依赖于发行版和 `RPM` 包。Kickstart 非常灵活，并且在自动检测系统硬件方面非常智能，因此它对裸机和虚拟机都同样适用。Kickstart 安装可以从光介质、本地硬盘、NFS、FTP 或 HTTP 执行。

## 设置 kickstart 配置文件

Kickstart 的行为由单一配置文件控制，通常称为 `ks.cfg`。该文件的格式非常直观。如果你倾向于可视化操作，Red Hat 方便的 GUI 工具 `system-config-kickstart` 可以让你通过点击达到 `ks.cfg` 的完美境界。

一个 kickstart 文件由三个顺序部分组成。第一部分是命令部分，指定了语言、键盘和时区等选项。该部分还通过 `url` 选项指定发行版的来源。在下面的示例中，它是一个主机 `installedserver`。

以下是一个完整的命令部分的示例：

```text
lang en_US # lang 在安装期间使用...

langsupport en_US # ...andsupport 在运行时使用

keyboard us # 使用美国标准键盘

timezone --utc America/EST # --utc 意味着硬件时钟为 GMT

rootpw --isencrypted=$G6sNaC1$X5jREi90CXjHP075/

reboot # 安装后重启。这总是明智的。

bootloader --location=mbr # 在 MBR 中安装默认引导程序

install # 安装新系统，不升级

url --url http://installserver/redhat

clearpart --all --initabel # 清除所有现有分区

part /fstype --size 4096

part swap --size 1024

var /fstype ext3 -size 1 --grow

network --bootproto dhcp
```

## 操作系统安装

```text
auth --useshadow --enablemd5

firewall --disabled

xxconfig --defaultdesktop=GNOME --startxonboot --resolution 1280x1024

--depth 24
```
