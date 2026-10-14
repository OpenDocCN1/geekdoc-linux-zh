
此工具用于为 Samba 创建用户帐户。如果你想设置需要身份验证的 Samba 共享，则使用此工具创建 Samba 用户数据库。你添加的 Samba 用户名也需要在系统上已存在。例如，要将 `ubuntu` 用户添加到 Samba，我会输入

```
$ sudo smbpasswd -a ubuntu
```

我也可以在想要更改特定用户的密码时使用此命令。要从 Samba 中删除用户，请将 `-a` 选项替换为 `-x`。你也可以在不删除其帐户的情况下暂时禁用 Samba 用户。为此，使用 `-d` 和 `-e` 选项分别禁用和启用用户。

- `/usr/share/doc/samba-doc/`

  如果你安装了 `samba-doc` 程序，你将在此目录下找到 Samba 文档和示例配置文件。

- `/var/lib/samba`

  该目录包含 Samba 使用的所有不同数据库，包括 `smbpasswd` 使用的用户和密码数据库。

- `/var/log/samba/`

  Samba 记录到自己的目录，并为 `smbd` 和 `nmbd` 进程分别创建单独的日志文件（`log.nmbd` 和 `log.smbd`），以及为访问 Samba 的每个主机创建单独的日志。这种组织方式可以更轻松地缩小到你需要的日志信息。

## 示例 Samba 配置

设置新的 Samba 共享的一个好方法是阅读 `/etc/samba/smb.conf` 文件中的注释。其中有许多不同的示例，展示了如何共享用户主目录或 CD-ROM 驱动器等。在此示例中，我将展示如何共享位于 `/mnt/share` 的目录，以便网络上的每个人都可以访问并写入它作为通用存储位置。打开 `/etc/samba/smb.conf` 并移动到文件底部。然后添加以下内容：

```
[general]
    path = /mnt/share
    comment = General Storage
    writeable = Yes
    browseable = Yes
    guest ok = Yes
    force user = ubuntu
```

在此示例中，我将 `/mnt/share` 目录设置为网络上的任何人都可以写入（`writeable = Yes`，`guest ok = Yes`），并使用 `force user = ubuntu` 选项，以便当用户在共享上创建文件时，它将归本地名为 `ubuntu` 的用户所有。当然，你需要将此用户从 `ubuntu` 更改为系统上存在的用户。现在我可以创建共享目录并确保其权限设置正确，以便本地 `ubuntu` 用户可以写入它：

```
$ sudo mkdir /mnt/share
$ sudo chown ubuntu:ubuntu /mnt/share
```

Samba 的一个不错功能是，我可以在不重启 Samba 的情况下添加或调整像上面这样的共享。这很方便，因为当你重启 Samba 时，任何访问共享上文件的用户都会暂时与文件断开连接。某些程序对断开连接的反应非常糟糕，他们的文件被临时从下面抽走，我甚至见过有些系统在这种情况下直接崩溃。

现在 Samba 已经配置好了，去网络上的另一台主机尝试连接你的 Samba 服务器。在 Ubuntu 桌面上，你会点击 Places > Connect to Server...，然后从“Service type”下拉菜单中选择“Windows share”。最后输入你的 Samba 服务器的 IP 地址或主机名，然后在 share 名称处输入 `general`（或你在 `smb.conf` 中方括号之间指定的其他名称）。点击 Connect，Ubuntu 就会挂载并在桌面上显示已挂载的共享。

### NFS

NFS 是一种源自 UNIX 而非 Windows 的文件共享服务。如今 Linux 和 Windows 都可以挂载 NFS 共享，但你仍然倾向于在 Linux 或 UNIX 客户端网络中使用 NFS。正如你将看到的，如果你想通过 NFS 共享一个目录，并没有太多复杂之处。

### 安装 NFS

要安装 NFS，在你的包管理器中选择 `nfs-kernel-server`。这将下载并安装该服务以及你需要的任何额外依赖项。

```
$ sudo apt-get install nfs-kernel-server
```

安装包后，NFS 就准备好进行配置了。默认情况下不会配置任何 NFS 导出，因此在你明确配置之前不会共享任何内容。

### Ubuntu NFS 惯例

- `/etc/exports` — 这是 NFS 的核心配置文件，包含 NFS 将导出给用户的所有文件系统的列表。

- `/etc/init.d/nfs-kernel-server` — 这个 init 脚本控制 NFS 服务器并接受标准的 init 脚本选项列表，包括 `reload`，这样你就可以在不重启服务的情况下重新加载配置。

#### `/var/log/syslog`

NFS 记录到标准的 `syslog` 文件中，作为 `NFSd` 进程。这是查找远程主机无法访问共享时具体失败原因的地方。要仅查看此文件中的 NFS 日志，运行 `sudo grep NFSd /var/log/syslog`。

### 示例 NFS 配置

添加 NFS 共享相对简单，你的所有工作都将在 `/etc/exports` 文件中完成。该文件的语法在 `exports` 手册页中有详细说明，你可以通过输入 `man 5 exports` 来访问。一般来说，文件每行包含一个导出，每行有两个列，由一个或多个空格分隔。第一列是要共享的目录的路径，第二列是可以访问共享的主机或网络以及在一对括号内的选项集。

我创建一个与我在 Samba 部分给出的示例类似的示例共享。我将 `ubuntu` 用户拥有的 `/mnt/share` 目录导出给 192.168.1.x 网络上的所有人。为此，我只需在 `/etc/exports` 中添加以下行：

```
/mnt/share 192.168.1.0/255.255.255.0(rw)
```

现在如果 `/mnt/share` 目录还不存在，我就创建它：

```
$ sudo mkdir /mnt/share
$ sudo chown ubuntu:ubuntu /mnt/share
```

最后，我可以重新加载 NFS 以启用此共享：

```
$ sudo service nfs-kernel-server reload
```

一旦 NFS 重新加载，我就可以在 192.168.1.0 网络上的任何主机上挂载该共享。如果 NFS 服务器位于 192.168.1.7，我想将其挂载到 `/mnt/local`，我会输入

```
$ sudo mount -t nfs 192.168.1.7:/mnt/share /mnt/local
```

如果你的 Ubuntu 主机出现关于错误文件系统类型的错误，你可能没有在系统上安装 NFS 客户端支持。只需运行

```
$ sudo apt-get install nfs-common
```

然后再次尝试挂载命令。

### NFS 用户权限

NFS 处理用户权限的一个有趣且有争议的特性。当你挂载 NFS 共享时，文件所有权将基于 NFS 服务器上用户的用户 ID。远程系统上的用户要能够读取和写入共享，他们的用户 ID 需要与 NFS 服务器匹配。如果你使用 LDAP 或其他系统在服务器之间保持用户 ID 一致，这不应该构成太大问题，但如果例如我的 NFS 服务器上的 `ubuntu` 用户的用户 ID 为 1000，而我的客户端上的 `ubuntu` 用户的用户 ID 为 1001，客户端将无法写入挂载点。

NFS 权限的另一个关注点是它如何处理 `root`。在 Ubuntu 上，默认情况下 `root` 账户会被压缩，因为 NFS 阻止远程 `root` 用户以其 `root` 权限访问共享。否则，网络上任何使用 Ubuntu live CD 的主机都可以启动它，挂载 NFS 共享，并读取和写入该共享上的任何文件，而不管权限如何。考虑到这个安全问题，你可能仍想禁用 `root` 压缩。要这样做，将 `no_root_squash` 选项添加到 `/etc/exports` 中的导出选项列表中。每个选项由逗号分隔，所以如果我想在之前创建的共享上禁用 `root` 压缩，该文件将如下所示：

```
/mnt/share 192.168.1.0/255.255.255.0(rw,no_root_squash)
```

## Edubuntu 和 LTSP

社区驱动的 Edubuntu 项目旨在为 Ubuntu 创建一个专门为初级和中学教育量身定制的插件。Edubuntu 作为教师和管理员工具的平台而存在。但真正的推动力，当然，也是真正的目的，是将自由和开源软件交到孩子们手中。在此过程中，Edubuntu 提供了
