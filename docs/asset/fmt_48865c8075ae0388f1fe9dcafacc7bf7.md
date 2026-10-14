
`$ sudo /etc/init.d/nfs-kernel-server start`

```
- NFS 服务：[ OK ]
- NFS 配额：[ OK ]
- NFS 进程：[ OK ]
- NFS 挂载：[ OK ]
```

在此示例中，NFS 已经启动。使用 `stop` 关键字停止服务，或使用 `restart` 重启服务器。这种控制 NFS 的方法在更改配置后非常有用。请看下一节了解如何在你的 Ubuntu 系统上配置 NFS 支持。

# NFS 服务器配置

你可以通过编辑 `/etc/exports` 文件来配置 NFS 服务器。该文件与 `/etc/fstab` 文件类似，它用于为被导出的文件系统设置权限。条目格式如下：

```
/file/system yourhost(options) *.yourdomain.com(options) 192.168.0.0/24(options)
```

这显示了三个共享 `/file/system` 的常见客户端。第一个 `yourhost` 仅向此处的一个主机共享 `/file/system`。第二个 `.yourdomain.com` 使用星号 (`*`) 作为通配符，允许 `yourdomain.com` 中的所有主机访问 `/file/system`。第三个允许整个 C 类网络 `192.168.0.0` 的所有主机访问 `/file/share`。出于安全起见，最好不要在互联网上使用后两个共享，因为所有数据将被数据经过的任何网络读取。

表 16.1 /etc/fstab 选项

| 选项 | 用途 |
| --- | --- |
| rw | 赋予读写权限 |
| ro | 赋予只读权限 |
| async | 当服务器（而非客户端）认为需要时写入数据 |
| sync | 接收时写入数据 |

以下是 `/etc/exports` 文件的示例：

```
# /etc/exports: 可能导出给 NFS 客户端的文件系统访问控制列表

# 参见 exports(5).

/home/andrew 192.168.0.0/24(rw,no_root_squash)
```

此文件向 `192.168.0.*` 中的主机导出（可用）`/home/hadson`，并允许用户对 `/home/andrew` 进行读取和写入。

完成 `/etc/exports` 文件的操作后，执行以下命令

```
$ sudo exportfs -a
```

会将 `/etc/exports` 文件中的所有文件系统导出到 `/var/lib/nfs` 目录下的名为 `xtstab` 的列表中，该列表作为远程计算机请求导出目录时的挂载指南。命令的 `-r` 选项会读取你定义的条目，你也可以使用 `exportfs` 命令临时导出特定文件。这里有一个使用 `exportfs` 导出文件系统的示例：

```
/usr/sbin/exportfs -o async yourhost:/tmp
```

此命令带有 `async` 选项将 `/usr/tmp` 导出到 `yourhost`。

在对 `/etc/exports` 进行任何更改后，请确保重启 NFS 服务器。如果你愿意，可以使用 Ubuntu 的 `shares-admin` 客户端在使用 X Window 系统时设置 NFS。点击“系统”菜单并从“管理”菜单中选择“共享文件夹”菜单开始。

按下回车后，系统会提示你输入密码。输入密码并点击确定；主窗口将显示。点击“添加”按钮打开“添加共享”对话框，如图 16.1 所示。

![](img/92338f4b411c2c2b03a4b8b5ff1a50b2_412_0.png)

图 16.1。你可以使用 Ubuntu 的 `shares-admin` 客户端快速设置用于 NFS 导出的本地目录。

在“路径”下拉框中，选择你想要共享的目录；在“共享”下拉框中，选择 NFS。点击“添加主机”按钮指定允许哪些主机、IP 地址或网络访问该目录。默认情况下，目录以读/写方式导出，但你可以通过勾选“只读”选项来选择只读。完成后，点击“确定”按钮，点击“应用”，然后使用“文件”菜单退出。

# NFS 客户端配置

作为 NFS 客户端（获取远程文件或目录），你需要确保已安装了 `NFS-common` 包，以便访问 NFS 共享。一旦你使用 `synaptic` 或 `apt-get` 安装了该包，请像挂载任何本地文件系统一样编辑 `/etc/fstab` 文件。然而，不要使用设备名称挂载（例如 `/dev/sda1`），而是输入远程主机名和要导入的文件系统。例如，一个条目可能如下：

| 设备 | 挂载点 | 类型 | 选项 | 频率 | 检查 |
| --- | --- | --- | --- | --- | --- |
| yourhost:/usr/local | /usr/local | nfs | nfsvers=3,ro | 0 | 0 |

> 如果你在系统上使用了 `autofs`，则需要为远程 NFS 挂载配置适当的 `autofs` 条目。使用 `df` 命令验证导入的文件系统。

“选项”列使用了与标准 `fstab` 文件条目相同的选项，并带有额外的条目，例如 `nvers=3`，它指定 NFS 的第三版本。你也可以以 root 身份使用 `mount` 命令，通过远程主机名和导出目录快速将远程目录挂载到本地系统。

```
$ sudo mount -t nfs 192.168.2.67:/music /music
```

按下回车后，整个远程目录将出现在你的文件系统上。按如下方式验证 `df` 命令：

| 文件系统 | 1k-块 | 已用 | 可用 | 使用率% | 挂载在 |
| --- | --- | --- | --- | --- | --- |
| /dev/hda2 | 1871368 | 964260 | 812124 | 55% | / |
| /dev/hda1 | 1871368 | 964260 | 812124 | 55% | /dev/hda1 |
| /dev/hda2 | 1871368 | 964260 | 812124 | 55% | /dev/hda2 |
| /dev/hda1 | 1871368 | 964260 | 812124 | 55% | /dev/hda1 |

# 通过 /etc/samba/smb.conf 手动配置 Samba

`/etc/samba/smb.conf` 文件被分为多个部分。每个部分都是共享资源（share）的描述，并应恰当地命名。三个特殊部分如下：

- `[global]`—建立全局配置设置（详细信息请参考 `smb.conf` man 页面和 Samba 文档，可在 `/usr/share/doc/samba/docs` 目录下找到）
- `[homes]`—共享用户的家目录，并指定目录路径和权限
- `[printers]`—通过定义共享打印机和打印机访问权限来处理打印任务

在你的 `/etc/samba/smb.conf` 配置文件中，每个部分都应该根据共享的资源命名。例如，如果共享资源是 `/usr/local/programs`，你可以将该部分命名为 `[programs]`。当 Windows 看到该共享时，它将显示为你为该部分命名的名称（在本例中为 programs）。设置此项最简单快的方法是使用以下 `smb.conf` 示例：

```
[programs]

path = /usr/local/programs

writable = true
```

这段配置将 `/usr/local/programs` 目录共享给任何请求的有效用户，并使该目录可写。这是最基本的共享，因为它没有对目录设置任何限制。

以下是你可以在部分中设置的某些参数：

- 要求用户在访问共享目录前输入密码
- 限制允许访问共享目录的主机
- 修改用户对目录拥有的权限
- 限制可以访问目录的时间

可能性几乎是无限的。在各个部分中设置的任何参数都会覆盖在 `[global]` 部分设置的参数。以下部分为 `[programs]` 部分添加了一些限制：

```
[programs]

path = /usr/local/programs

writable = true

valid users = hudson

browseable = yes

create mode = 0700
```
