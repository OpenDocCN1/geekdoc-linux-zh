

# 使用网络文件系统

要让 Red Hat 在启动时自动启动 NFS，请使用命令行或图形化管理工具，例如 chkconfig、ntsys 或 redhat-config-services。请确保 portmap 服务已启动，因为它是服务的一部分。你可以通过直接调用其服务控制脚本 `nfs` 来手动启动或停止 NFS，如下所示：

```
# /etc/rc.init.d/nfs start
Starting NFS services: [ OK ]
Starting NFS quotas: [ OK ]
Starting NFS daemon: [ OK ]
Starting NFS mounted: [ OK ]
```

在此例中，NFS 已经启动。使用 `stop` 关键字可以停止该服务。这种这种控制 NFS 的方法非常方便，特别是在进行了配置更改之后。请参阅下一节，了解如何在您的 Red Hat 系统上配置 NFS 支持。

# NFS 服务器配置

可以通过编辑 `/etc/exports` 文件来配置服务器。该文件与 `/etc/fstab` 文件类似，都用于设置被导出的文件系统的权限。条目格式如下：

```
/file/systemyour(options) *.yourdomain.com(options) 192.15.69.0/24(options)
```

这显示了三个共享 `/file/system` 的常见客户端。第一个 `your` 仅向一个主机共享 `/file/system`。第二个 `.yourdomain.com` 使用星号 (*) 作为通配符，允许 `yourdomain.com` 中的所有主机访问 `/file/system`。第三个共享允许所有 C 类网络（192.15.69.0）的主机访问 `/file/share`。出于安全性考虑，最好不要在互联网上使用最后那样的共享，因为所有数据都可以被数据所经过的任何网络读取。

表 13.3 显示了一些选项。

| 选项 | 目的 |
| :--- | :--- |
| rw | 提供读和写权限 |
| ro | 提供只读权限 |
| async | 在服务器认为需要时写入数据，而不是客户端 |
| sync | 在接收到数据时立即写入 |

以下是 `/etc/exports` 文件的示例：

```
# /etc/exports file for myhost.mydomain.com
/usr/local host(ro,show)
/home/jkennedy *.yourdomain.com(rw,hide,sync)
```

# 第 13 章 网络连接

此文件导出（并可用）`/usr/local/ localhost`。该挂载是只读的（这对于不需要写入的二进制文件目录是有好处的）。它允许允许主机上的用户查看可能挂载在 `/usr/local` 的文件系统内容。第二个导出将 `/home/kennedy` 挂载到 `yourdomain.com` 中的任何主机。它不允许查看子文件系统，但你可以对该文件系统进行读写。

在你完成 `/etc/exports` 文件后，运行以下命令

```
# /usr/sbin/exportsfs -r
```

会将 `/etc/exports` 文件中的所有文件系统导出到 `/var/lib/nfs` 目录下名为 `xtab` 的列表中，该列表作为远程计算机请求导出目录时的挂载指南。命令 `-r` 选项读取 `/etc/exports` 文件并挂载所有条目。`exportsfs` 命令也可以用于临时导出特定文件。使用 exports 导出文件系统的示例为：

```
/usr/sbin/exportsfs -o async localhost:/usr/tmp
```

此命令将带有 `async` 选项将 `/usr/tmp` 重启到 localhost。

在对 `/etc/exports` 进行任何更改后，请确保重启 NFS 服务器。如果你愿意，可以在使用 X 系统中使用 Red Hat 的 `redhat-config-nfs` 图形客户端来设置 NFS。从点击桌面面板上的 Server 设置菜单中的 NFS Server 项开始。你也可以从 X 终端窗口的命令行启动客户端，如下：

```
$ redhat-config-nfs &
```

按下回车键后，系统会提示输入 root 密码。输入密码，点击 OK，点击 Add 按钮，你将看到 Add NFS Share 对话框，如图13.4 所示。

在 Directory 文本框中输入要导出的目录名称；在 Host(s) 文本框中输入允许访问目录的远程主机主机名或 IP 地址。默认情况下，目录是只读导出的，但你可以点击对话框 Basic Permissions 区域中的任一导出选项来选择读写访问。完成后，点击 OK 按钮，点击 Apply 按钮，然后使用 File 菜单退出。

# NFS 客户端配置

要将你的主机配置为 NFS 客户端（获取远程文件或目录），请像挂载任何本地文件系统一样编辑 `/etc/fstab` 文件。然而，不要使用设备名称挂载（例如 `/dev/hda1`），而是移除远程主机和想要导入的文件系统。例如，一个条目可能如下：

| 设备 | 挂载点 | 类型 | 选项 | 频率 | 通过 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| yourhost:/usr/local | /usr/local | nfs | nvers=3,ro | 0 | 0 |

# 使用网络文件系统

![](img/446debe023486a07fde575245cf7a3ff_456_0.png)

**图 13.4** Red Hat 的 `redhat-config-nfs` 客户端可用于 NFS 快速设置本地目录。

选项列使用与 `fstab` 文件条目相同的名称，并带有额外的条目 `nvers=3`，这指定了 NFS 的第三版本。你也可以使用 `mount` 命令通过远程主机名称和导出目录将远程目录快速挂载到本地文件系统。例如，

```
# mount -t nfs 192.168.2.167:/music
```

按下回车后，整个远程目录将出现在你的文件系统中。你可以使用 `df` 命令验证导入的文件系统，如下：

```
# df
Filesystem 1k-blocks Available Use% Mounted on
/dev/hda2 18714368 9462600 8121124 55% /
/dev/hda1 46636 13247 30981 30% /boot
none 120016 0 120016 0% /
```

对 `/etc/exports` 进行任何更改后，请确保重启 NFS 服务器。如果你愿意，可以在 X Window中使用 Red Hat 的 `redhat-config-nfs` 图形客户端来设置 NFS。从点击桌面面板上的 Server 设置菜单中的 NFS Server 项开始。你也可以从 X 终端窗口的命令行启动客户端，如下：

```
$ redhat-config-nfs &
```

按下回车键后，系统会提示输入 root 密码。输入密码，点击 OK，点击 Add 按钮，你将看到 Add NFS Share 对话框，如图13.4 所示。

在 Directory 文本框中输入要导出的目录名称；在 Host(s) 文本框中输入允许访问目录的远程主机主机名或 IP 地址。默认情况下，目录是只读导出的，但你可以点击对话框 Basic Permissions 区域中的任一导出选项来选择读写访问。完成后，点击 OK 按钮，点击 Apply 按钮，然后使用 File 菜单退出。

# NFS 客户端配置

要将你的主机配置为 NFS 客户端（获取远程文件或目录），请像挂载任何本地文件系统一样编辑 `/etc/fstab` 文件。然而，不要使用设备名称挂载（例如 `/dev/hda1`），而是移除远程主机和想要的文件的文件。例如，一个条目可能如下：

| 设备 | 挂载点 | 类型 | 选项 | 频率 | 通过 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| yourhost:/usr/local | /usr/local | nfs | nvers=3,ro | 0 | 0 |

# 使用网络文件系统

![](img/446debe023486a07fde575245cf7a3ff_456_0.png)

**图 13.4** Red Hat 的 `redhat-config-nfs` 客户端可用于 NFS 快速设置本地目录。

选项列使用与标准 `fstab` 文件条目相同的名称，并带有额外的条目 `nfsvers=3`，这指定了 NFS 的第三版本。你也可以使用 `mount` 命令通过远程主机名称和导出目录将远程目录快速挂载到本地文件系统。对于，

```
# mount -t nfs 192.168.2.167:/music /music
```

按下回车后，整个远程目录将出现在你的文件系统中。你可以使用 `df` 命令验证导入的文件系统，如下：

```
# df
Filesystem 1k-blocks Available Use% Mounted on
/dev/hda2 18714368 9462600 8121124 55% /
/dev/hda1 46636 13247 30981 30% /boot
none 120016 0 120016 0% /
```

