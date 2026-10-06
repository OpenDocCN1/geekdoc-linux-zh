

# NFS: 网络文件系统

NFS（Network Filesystem，见第 391 页）协议由太阳微系统（Sun Microsystems）开发，允许你与远程机器共享本地文件，并从本地机器访问文件。在 NFS 下，很难区分远程文件和本地文件。NFS 是一种事实标准，并支持异构环境.³32

在 NFS 下，文件的物理位置对用户来说并不重要。传统上每台机器上都存储一个程序的副本。为了升级程序，你需要在每台机器上进行升级。使用 NFS，你可以在一台机器上存储程序的一个副本，并通过网络让其他用户访问。这种场景通过减少相同数据需要存储的位置，更有效地利用了存储。除了效率外，NFS 还允许网络上的用户访问相同的数据（而不仅仅是应用程序），提高了数据的一致性和可靠性。通过整合数据，NFS 减少了系统管理和开销，并提高了安全性。

在使用 NFS 之前，请确保必要的守护守护进程正在运行：

```
# service nfs status
```

```
...
```

```
# /etc/rc.d/init.d/nfs status pc.mount(pid 15795) is running...
nfsid (pid 15813 15812 15811 15810 15808 15807 15806) is running...
rpc.quotad (pid 15784) is running...
```

当 NFS 未运行时，你将看到提示守护进程已停止的消息。要启动守护进程，执行命令 `service nfs start`。如果没有输出，可能是 `/etc/exports` 中没有任何条。

# exports: 存储挂载本地文件系统的权限

/etc/exports 文件控制哪些远程系统可以访问目录。你可以直接编辑此文件。以下简单的 exports 文件赋予 bravo 对 `/home` 下所有文件的读写权限，并赋予 kudos 对 `/home/alex` 的访问权限。在每情况下，所有子目录都隐式地授予了访问权限。最新版本的 exports（见下文）更改了默认提交过程以符合 NFS 协议³³³，并在你未进行同步（sync）或异步（async）操作时发出警告。

- 32. NFS 运行在 UNIX 上
- 33. 在高于 1.0.0 的版本中，sync 是默认。

```
# cat /etc/exports
/home bravo.tcorp.com(rw,sync)
/home/alex kudos tcorp.com(ro,sync)
```

你可以在一行中包含多台机器。其他选项请参考 exports 的 man page。

exports 工具维护位于 `/var/lib/nfs/stab` 的 NFS 文件系统记录。通常，该文件在系统启动时从 `/etc/exports` 自动初始化，并由使用 NFS 的远程系统和卸载的文件系统保持更新。在不更改 `/etc/exports` 的情况下，exports 工具可以从可挂载的文件系统列表中添加或删除文件系统。

以下命令导出 `/etc/exports` 中的所有条目：

```
# exports -a
```

将 `a` 替换为 `-r` 以重新导出或同步内核在 `/var/lib/nfs/stab` 中监控的条目与 `/etc/exports` 中的同步。使用 `-u` 选项删除已导出的目录。详情和其他选项请参考 exports 的 man page。

# mount: 挂载远程文件系统

本节涵盖了远程系统需要执行的操作。为了在本地机器上使用远程文件系统，必须对其进行挂载。以下示例显示了挂载远程文件系统的两种方法，假设名为 `don` 的机器与本地机器在同一网络中，并向本地机器共享其 `/export/home`、`/export/apps` 和 `/export/apps/oracle` 文件系统。在任何情况下，都使用 `mkdir` 创建作为挂载点的目录：

```
# mkdir /myhome /apps
```

如果你只想挂载一次文件系统，手动挂载它们非常简单：

```
# mount:/export/home /myhome
# mount -o r,nosuid=donald:/export/apps /apps
# mount -o r donald:/export/oracle /apps/oracle
```

默认情况下，文件系统是可读写的（假设此处的 NFS 服务器 `donald` 是以读写权限导出的）。第一条前面的命令行将名为 `don` 的机器的 `/export/home` 目录挂载到本地目录 `/myhome`。第二和第三条挂载使用 `-o ro` 强制进行只读挂载。第二次挂载还通过使用 `-o` 选项的多选项形式增加了 `-o nosuid` 选项。nosuid 选项强制被挂载的 setuid 可执行文件在本地机器上以普通权限运行。

# 1020 第17章 红 Hat Linux 系统管理

如果你将频繁挂载系统，编辑 `/etc/fstab` 文件（第 978 页）会更方便。以下 `/etc/fstab` 条目会在每次机器启动时自动挂载相同的目录。

| donald:/export/home | /myhome nfs 0 |
| donald:/export/apps | /apps nfs r,nosuid |
| donald:/export/oracle | /apps/oracle nfs |

# 符号链接和设备文件

本节涵盖了远程系统上需要做的操作。为了在本地机器上使用远程文件系统，它必须被挂载。以下示例显示了挂载远程文件系统的两种方法，假设名为 `don` 的机器与本地机器在同一网络中，并向本地机器共享其 `/export/home`、`/export/apps` 和 `/export/apps/oracle` 文件系统。在任何情况下，都使用 `mkdir` 创建作为挂载点的目录：

```
# mkdir /myhome /apps
```

如果你只想挂载一次文件系统，手动挂载它们非常简单：

```
# mount:/export/home /myhome
# mount -o r,nosuid=donald:/export/apps /apps
# mount -o r donald:/export/oracle /apps/oracle
```

默认情况下，文件系统是可读写的（假设此处的 NFS 服务器 `donald` 是以读写权限导出的）。第一条前面的命令行将名为 `don` 的机器的 `/export/home` 目录挂载到本地目录 `/myhome`。第二和第三条挂载使用 `-o ro` 强制进行只读挂载。第二次挂载还通过使用 `-o` 选项的多选项形式增加了 `-o nosuid` 选项。nosuid 选项强制被挂载的 setuid 可执行文件在本地机器上以普通权限运行。

# 1020 第17章 红 Hat Linux 系统管理

如果你将频繁挂载系统，编辑 `/etc/fstab` 文件（第 978 页）会更方便。以下 `/etc/fstab` 条目会在每次机器启动时自动挂载相同的目录。

| donald:/export/home | /myhome nfs 0 |
| donald:/export/apps | /apps nfs r,nosuid |
| donald:/export/oracle | /apps/oracle nfs |

# 符号链接和设备文件

本节涵盖了远程系统上需要做的操作。为了在本地机器上使用远程文件系统，它必须被挂载。以下示例显示了挂载远程文件系统的两种方法，假设名为 `don` 的机器与本地机器在同一网络中，并向本地机器共享其 `/export/home`、`/export/apps` 和 `/export/apps/oracle` 文件系统。在任何情况下，都使用 `mkdir` 创建作为挂载点的目录：

```
# mkdir /myhome /apps
```

如果你只想挂载一次文件系统，手动挂载它们非常简单：

```
# mount:/export/home /myhome
# mount -o r,nosuid=donald:/export/apps /apps
# mount -o r donald:/export/oracle /apps/oracle
```

默认情况下，文件系统是可读写的（假设此处的 NFS 服务器 `donald` 是以读写权限导出的）。第一条前面的命令行将名为 `don` 的机器的 `/export/home` 目录挂载到本地目录 `/myhome`。第二和第三条挂载使用 `-o ro` 强制进行只读挂载。第二次挂载还通过使用 `-o` 选项的多选项形式增加了 `-o nosuid` 选项。nosuid 选项强制被挂载的 setuid 可执行文件在本地机器上以普通权限运行。

# 1020 第17章 红 Hat Linux 系统管理

如果你将频繁挂载系统，编辑 `/etc/fstab` 文件（第 978 页）会更方便。以下 `/etc/fstab` 条目会在每次机器启动时自动挂载相同的目录。

| donald:/export/home | /myhome nfs 0 |
| donald:/export/apps | /apps nfs r,nosuid |
| donald:/export/oracle | /apps/oracle nfs |

# 符号链接和设备文件

本节涵盖了远程系统上需要做的操作。为了在本地机器上使用远程文件系统，它必须被挂载。以下示例显示了挂载远程文件系统的两种方法，假设名为 `don` 的机器与本地机器在同一网络中，并向本地机器共享其 `/export/home`、`/export/apps` 和 `/export/apps/oracle` 文件系统。在任何情况下，都使用 `mkdir` 创建作为挂载点的目录：

```
# mkdir /myhome /apps
```

如果你只想挂载一次文件系统，手动挂载它们非常简单：

```
# mount:/export/home /myhome
# mount -o r,nosuid=donald:/export/apps /apps
# mount -o r donald:/export/oracle /apps/oracle
```

默认情况下，文件系统是可读写的（假设此处的 NFS 服务器 `donald` 是以读写权限导出的）。第一条前面的命令行将名为 `don` 的机器的 `/export/home` 目录挂载到本地目录 `/myhome`。第二和第三条挂载使用 `-o ro` 强制进行只读挂载。第二次挂载还通过使用 `-o` 选项的多选项形式增加了 `-o nosuid` 选项。nosuid 选项强制被挂载的 setuid 可执行文件在本地机器上以普通权限运行。

（由于提供的文本中存在大量重复段落，此处根据逻辑仅翻译核心内容部分示例）

# NFS: 网络文件系统

NFS（Network Filesystem，见第 391 页）协议由太阳微系统（Sun Microsystems）开发，允许你与远程机器共享本地文件，并从本地机器访问文件。在 NFS 下，很难区分远程文件和本地文件。NFS 是一种事实标准，并支持异构环境.³32

在 NFS 下，文件的物理位置对用户来说并不重要。传统上每台机器上都存储一个程序的副本。为了升级程序，你需要在每台机器上进行升级。使用 NFS，你可以在一台机器上存储程序的一个副本，并通过网络让其他用户访问。这种场景通过减少相同数据需要存储的位置，更有效地利用了存储。除了效率外，NFS 还允许网络上的用户访问相同的数据（而不仅仅是应用程序），提高了数据的一致性和可靠性。通过整合数据，NFS 减少了系统管理和开销，并提高了安全性。

在使用 NFS 之前，请确保必要的守护进程正在运行：

```
# service nfs status
```

```
...
```

```
# /etc/rc.d/init.d/nfs status pc.mount(pid 15795) is running...
nfsid (pid 15813 15812 15811 15810 15808 15807 15806) is running...
rpc.quotad (pid 15784) is running...
```

当 NFS 未运行时，你将看到提示守护进程已停止的消息。要启动守护进程，执行命令 `service nfs start`。如果没有输出，可能是 `/etc/exports` 中没有任何条。

# exports: 存储挂载本地文件系统的权限

/etc/exports 文件控制哪些远程系统可以访问目录。你可以直接编辑此文件。以下简单的 exports 文件赋予 bravo 对 `/home` 下所有文件的读写权限，并赋予 kudos 对 `/home/alex` 的访问权限。在每情况下，所有子目录都隐式地授予了访问权限。最新版本的 exports（见下文）更改了默认提交过程以符合 NFS 协议³³³，并在你未进行同步（sync）或异步（async）操作时发出警告。

- 32. NFS 运行在 UNIX 上
- 33. 在高于 1.0.0 的版本中，sync 是默认。

```
# cat /etc/exports
/home bravo.tcorp.com(rw,sync)
/home/alex kudos tcorp.com(ro,sync)
```

你可以在一行中包含多台机器。其他选项请参考 exports 的 man page。

exports 工具维护位于 `/var/lib/nfs/stab` 的 NFS 文件系统记录。通常，该文件在系统启动时从 `/etc/exports` 自动初始化，并由使用 NFS 的远程系统和卸载的文件系统保持更新。在不更改 `/etc/exports` 的情况下，exports 工具可以从可挂载的文件系统列表中添加或删除文件系统。

以下命令导出 `/etc/exports` 中的所有条目：

```
# exports -a
```

将 `a` 替换为 `-r` 以重新导出或同步内核在 `/var/lib/nfs/stab` 中监控的条目与 `/etc/exports` 中的同步。使用 `-u` 选项删除已导出的目录。详情和其他选项请参考 exports 的 man page。

# mount: 挂载远程文件系统

本节涵盖了远程系统上需要执行的操作。为了在本地机器上使用远程文件系统，必须对其进行挂载。以下示例显示了挂载远程文件系统的两种方法，假设名为 `don` 的机器与本地机器在同一网络中，并向本地机器共享其 `/export/home`、`/export/apps` 和 `/export/apps/oracle` 文件系统。在任何情况下，都使用 `mkdir` 创建作为挂载点的目录：

```
# mkdir /myhome /apps
```

如果你只想挂载一次文件系统，手动挂载它们非常简单：

```
# mount:/export/home /myhome
# mount -o r,nosuid=donald:/export/apps /apps
# mount -o r donald:/export/oracle /apps/oracle
```

默认情况下，文件系统是可读写的（假设此处的 NFS 服务器 `donald` 是以读写权限导出的）。第一条前面的命令行将名为 `don` 的机器的 `/export/home` 目录挂载到本地目录 `/myhome`。第二和第三条挂载使用 `-o ro` 强制进行只读挂载。第二次挂载还通过使用 `-o` 选项的多选项形式增加了 `-o nosuid` 选项。nosuid 选项强制被挂载的 setuid 可执行文件在本地机器上以普通权限运行。

# 1020 第17章 红 Hat Linux 系统管理

如果你将频繁挂载系统，编辑 `/etc/fstab` 文件（第 978 页）会更方便。以下 `/etc/fstab` 条目会在每次机器启动时自动挂载相同的目录。

| donald:/export/home | /myhome nfs 0 |
| donald:/export/apps | /apps nfs r,nosuid |
| donald:/export/oracle | /apps/oracle nfs |

# 符号链接和设备文件

（此处省略重复的段落翻译）

# umount: 卸载远程文件系统

使用 umount 卸载远程文件系统，与卸载本地文件系统相同（第 977 页）。

# showmount: 显示 NFS 状态

showmount 工具 NFS 状态信息。调用 showmount 并传入你想获取信息的机器主机名。不带参数或传入 localhost 会 showmount 报告本地机器。传入远程机器名称会报告该机器。在无任何选项的情况下，showmount 显示允许挂载的机器列表。在以下示例中，kudos 和 bravo 可以挂载本地目录：

```
# /usr/sbin/showmount localhost
Hosts on localhost:
kudos.tcorp.com
vo.tcorp.com
```

-a 选项告诉你哪些目录导出到了远程机器。这些信息存储在 /etc/exports 中。虽然这个示例很简单，但请记住 mountpoint 可以报告 NFS 服务器的信息：

```
# /usr/sbin/mountpoint -a
All mount points on localhost:
kudos.tcorp.com:/home
bravo.tcorp.com:/home
```

从另一个视角来看：本地 /home 目录导出 (-e) 到 kudos 和 bravo：

```
# /usr/sbin/mountpoint -e
Export list for localhost:
/home kudos.tcorp.com,bravo.tcorp.com
```

# NIS: 网络信息服务

NIS（第 390 页）是太阳微系统的一种客户端/服务器协议，用于在网络计算机之间分发系统配置数据，如主机名、密码、组、服务名、别名、自动挂载映射以及一些不常用的表。NIS 允许轻松地添加、删除和移动资源。更多信息请参考 NIS-HOWTO。

# DNS: 域名服务

DNS（第 388 页）是分布在成千上万计算机上的域名数据库。要使用 DNS 进行主机名解析，你需要创建一个名为 /etc/resolv.conf（下文）的文件并编辑 /etc/nsswitch.conf（第 1022 页）。同时也参考 DNS-HOWTO。

resolv.conf: 解析主机名

以下示例显示了 tcorp 域的解析器配置文件 (/etc/resolv.conf）。一个 resolv.conf 文件通常至少两行：域行和服务器行：

```
# cat /etc/resolv.conf
domain tcorp.com
nameserver 10.0.0.50
nameserver 10.0.0.51
```

