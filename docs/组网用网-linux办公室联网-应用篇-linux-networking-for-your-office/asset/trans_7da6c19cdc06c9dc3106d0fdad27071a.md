

你可以通过以加密形式发送密码来降低这种风险。其工作原理如下：服务器在收到访问请求时，会向客户端发送一个随机选择的密钥值。客户端随后使用算法将该值与实际密码组合，并将结果作为密码通过网络发送。服务器随后可以解密此回复并将其与文件中保存的密码进行比较。由于除非使用服务器保留的信息（或使用远超普通破解者能力的计算机）否则无法解密回复，因此线路上的窃听者无法从此类交换中提取密码。如果企图破解者试图进入服务器，他或她会遇到不同的密钥值，因此捕获的回复对破解者没有任何用处。

大多数版本的 Windows 95 默认发送明文密码，意味着它们未加密。Windows 95 的后期版本以及 Windows 的后续版本均默认发送加密密码。你可以更改这些默认值，也可以配置 Samba 以接受你需要的任一种方式。无论你使用明文密码还是加密密码，都会对你在 Linux 服务器上维护用户密码的方式产生重大影响，如第 11 章所述。

AppleTalk 也提供多级密码安全，但在 Linux 上配置 Netatalk 使用加密密码相当棘手。因此，对于 Macintosh/Netatalk 网络来说，确保网络没有窃听者更为重要，通过配置一个完全私有的网络，并通过某种网关连接到整个互联网。

## Summary

文件共享是 Linux 做得非常出色的工作之一，特别是如果你需要一台计算机为各种不同的操作系统提供文件服务。你可以使用 Linux 为 DOS、Windows、OS/2、Macintosh 和 UNIX 客户端，或任何使用这些操作系统文件共享机制的操作系统提供相同的服务。

正确配置 Linux 系统以进行文件共享需要你了解 Linux 如何处理目录、分区和可移动媒体。你还必须了解 Linux 与你的客户端操作系统在处理文件名和文件所有权及权限方面的差异。由于 Linux 比大多数客户端操作系统提供更精细的所有权和权限控制，因此你可以使用 Linux 的权限功能提供一定程度的局域网安全，防止用户查看其他用户的文件。然而，这种安全性仅与客户端计算机的安全性一样好，因此，如果此事对你很重要，你应该研究客户端操作系统的附加安全产品。

## NFS: Sharing Files with Other UNIXes

## CHAPTER 10

## IN THIS CHAPTER
- Kernel Configuration for NFS 242
- The NFS Daemon 242
- Setting NFS Options 244
- How Permissions Work with NFS 248
- Mounting Remote NFS Volumes in Linux 251
- Summary 254

### NOTE

nfs-server 包不需要内核支持，但内核支持的存在也不会对其造成损害。如果你已编译内核并带有 NFS 服务器支持，你可以选择使用任一包。

如果你遇到 knfsd 问题，你有两个选择：
- Downgrade—你可以使用 Red Hat Linux 6.0，并使用随 Red Hat Linux 5.2 提供的旧版 nfs-server 包。
- Upgrade—比随 Red Hat 6.0 发行版本更近的 knfsd 版本存在，并且在许多情况下这些版本似乎更可靠。

### NOTE

如果你是从 Red Hat 5.2 安装升级系统，而不是在空分区上安装 Red Hat 6.0，你更有可能遇到 knfsd 问题。

随本书附带的 CD-ROM 在 sams-extras/nfs 目录中同时包含较旧的 nfs-server 包和较新的 knfsd 包。如果你尝试升级路线，你需要同时升级 knfsd 和 knfsd-clients 包。如果你尝试降级，你需要删除这些包（如果已安装）并安装 nfs-server 包。在任何情况下，在开始之前你都应输入

```
/etc/rc.d/init.d/nfs stop
```

此命令关闭现有的 NFS 服务器。在更新你的 RPM 后，你应输入以下命令以启动更新后的服务器：

```
/etc/rc.d/init.d/nfs start
```

无论你选择安装哪个包，NFS 守护进程都驻留在后台，等待远程系统尝试连接。当它看到此类尝试时，守护进程会检查 /etc/exports 以查看连接的计算机是否被授权挂载请求的系统。假设连接已获授权，守护进程会为远程系统提供访问权限。

