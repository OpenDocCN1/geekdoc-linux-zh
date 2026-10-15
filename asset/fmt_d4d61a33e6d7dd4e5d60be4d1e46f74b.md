
如果你删除注释符号（`#`）将 `user1` 和 `user2` 更改为系统上的真实用户，FTP 服务器会在这些用户登录时将他们发送到相应的家目录——并且他们拥有 root（`/`）权限访问更层级的目录。

如果你希望所有用户都从 `/var/ftp` 目录开始访问你的 FTP 服务器，请在 `/etc/ftpaccess` 中注释掉这一行。

## 理解 chroot 监狱 (chroot Jail)

保护 FTP 服务器上其他目录的概念是 `chroot` 监狱。根据定义，没有比根目录（`/`）更高的目录。`chroot /abc/def` 命令将有效根目录更改为 `/abc/def`。

在匿名 FTP 服务器上，`/var/ftp` 目录看起来就像根目录（`/`）。匿名 FTP 服务器的配置将 `chroot /var/ftp` 命令作用于所有登录到该服务器的用户。如果匿名用户尝试运行如 `cd /var` 或 `cd /etc` 等命令，它将不起，因为更层级的目录受到了 `chroot` 监狱的保护。

## 设置命令限制

对危险命令的访问也可以被限制。默认情况下，`/etc/ftpaccess` 限制对四个命令的访问，所示。你可能想向列表中添加其他命令。例如，如果你允许授权用户执行某条命令，可以将其添加到此列表中以防止匿名用户访问。

```
chmod      no      guest, anonymous
delete     no      anonymous
overwrite  no      anonymous
rename    no      anonymous
```

## 配置网络文件系统

网络文件系统 (NFS) 是 Linux 的基础。事实上，一个基础 NFS 配置文件包含与 `/etc/passwd` 和 `/etc/profile` 相同的 setup-RPM 包中。然而，许多 NFS 意味着你需要注意许多不同的守护进程。

设置 NFS 服务器的导出 (exports) 相对简单。基本上，你只需要为每个共享目录在 `/etc/exports` 中添加一行并将其与网络共享，任务就完成了。但请注意语法；正确的命令可以帮助加固你通过 NFS 共享的目录。

NFS 的一个关键是过程调用 (RPC)，它允许你在远程挂载目录上无缝运行命令。所有的 NFS 守护进程都使用 RPC。

NFS 的 GUI 工具 `redhat-config-nfs` 可以帮助你配置简单的共享目录。记住，这个 GUI 工具只是你在本章中将学习内容的前端。

## NFS 包

所需的 NFS 包可能已经安装。

| 表 22.5：NFS 相关包 |
|---|---|
| 包 | 功能 |
| setup-* | 共享目录 |
| initscripts-* | 支持 de |
| nfs-utils-* | 包括 rpc-bind |
| portmap-* | 包括 de |
| quota-* | 包括 de |

## 基础守护进程

网络文件系统 (NFS) 是 Linux 的基础。事实上，一个基础 NFS 配置文件包含与 `/etc/passwd` 和 `/etc/profile` 相同的 setup-RPM 包中。然而，许多 NFS 意味着你需要注意许多不同的守护进程。

设置 NFS 服务器的导出相对简单。基本上，你只需要为每个共享目录在 `/etc/exports` 中添加一行并将其与网络共享，任务就完成了。但请注意语法；正确的命令可以帮助加固你通过 NFS 共享的目录。

NFS 的一个关键是过程调用 (RPC)，它允许你在远程挂载目录上无缝运行命令。所有的 NFS 守护进程都使用 RPC。

NFS 的 GUI 工具 `redhat-config-nfs` 可以帮助你配置简单的共享目录。记住，这个 GUI 工具只是你在本章中将学习内容的前端。

## 共享服务：FTP 和 NFS

网络文件系统 (NFS) 是 Linux 的基础。事实上，一个基础 NFS 配置文件包含与 `/etc/passwd` 和 `/etc/profile` 相同的 setup-RPM 包中。然而，许多 NFS 意味着你需要注意许多不同的守护进程。

设置 NFS 服务器的导出相对简单。基本上，你只需要为每个共享目录在 `/etc/exports` 中添加一行并将其与网络共享，任务就完成了。但请注意语法；正确的命令可以帮助加固你通过 NFS 共享的目录。

NFS 的一个关键是过程调用 (RPC)，它允许你在远程挂载目录上无缝运行命令。所有的 NFS 守护进程都使用 RPC。

NFS 的 GUI 工具 `redhat-config-nfs` 可以帮助你配置简单的共享目录。记住，这个 GUI 工具只是你在本章中将学习内容的前端。

## 设置导出

共享的 NFS 目录列在 `/etc/exports` 中。例如，你的服务器上有一个光驱你想与局域网内的其他计算机共享。通常，光驱挂载在 `/mnt/cdrom`。你还想共享 `/tmp` 目录。格式为：

```
sharedirectory hosts(specs)
```

换句话说，在 `/etc/exports` 中，你指定要共享的目录、与之共享的计算机以及需要的限制。让我们来看几个你可以执行的示例：

```
/mnt/inst *example.com(ro,sync)
big.example.com(rw,sync)
tmp *(rw,insecure,sync,no_wdelay,anonuid=600)
```
