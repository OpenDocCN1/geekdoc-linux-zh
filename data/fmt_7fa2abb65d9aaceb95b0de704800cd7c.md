
- 此问题专门针对 `Ubuntu` 和 `Ubuntu Linux` 系统。成功完成此问题将让你能够将 `Universe` 和 `Multiverse` 存储添加到你的`/etc/apt/sources.list`文件中。

向`/etc/apt/sources.list`目录下的列表文件添加以下一个或所有额外的软件库：

```
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial universe
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial universe
deb http://us.archive.ubuntu.com/ubuntu/ xenial-updates universe
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial-updates universe
deb http://us.archive.ubuntu.com/ubuntu/ xenial multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial multiverse
deb http://us.archive.ubuntu.com/ubuntu/ xenial-updates multiverse
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial-updates multiverse
```

你应该将 `"us."` 替换为另一个代码，指向你所在地区的镜像服务器。不要忘记使用 `sudo apt-get update` 命令获取更新后的包列表。

- 19. 根据以下约束，为你的 `Linux` 系统详细执行第 17.3.4 节所示的用户和组创建方法的各个步骤：

  a. 你的系统容纳额外持久性介质的能力，

  b. 是否想使用基于 `ZFS` 的或传统的分区/文件系统创建/文件挂载方法，

  c. 你的安全模型（关于它如何隔离用户和组相互隔离），

  d. 影响用户和组的系统性能模型，

  e. 你计划容纳多少个用户和组。

例如，你可以在系统中添加一个或多个额外的硬盘，并在基于 `ZFS` 的单个或多个虚拟池中，限制普通用户的权限，允许他们从家目录运行自己的可执行程序，并拥有一小规模的用户账户和组。

# 高级问题与项目

- 20. 使用 17.8.1.2 和 17.8.1.3 节的 `systemd` `cgroups` 方法，以及你特定情况的限制，首先检查并评估你 `Linux` 系统上最关键和重要的应用程序默认使用的 `CPU` 和内存资源。然后，列出你认为在访问 `CPU` 和内存方面比默认具有更高“权重”的应用程序。例如，如果你正在运行一个使用 `nginx` 服务 `Web` 页面的服务器，如何让 `nginx` 应用程序及其工作进程在访问 `CPU` 和系统内存方面获得更高的权重？你的计算机 `CPU` 和核心数量如何影响你对 `CPU` 使用的重新分配，你如何修改重新分配以利用这些 `CPU` 和核心？这可能包括利用 `CPU` 亲和性，如果你想给你自己开发的程序更高的权重。

在下载并安装 `Webber`（如附录 A `W26.1.2` 所示），测试到本地机器、互联网或另一台机器的连接。使用哪个 `URL` 访问本地机器上的 `Webber`？使用哪个 `URL` 从互联网上的另一台机器访问 `Webber`？使用哪个 `URL` 从互联网上的另一台机器访问 `Webber`？列出你应该采取的几个预防措施，以确保互联网上无人登录你的系统界面。

在阅读网站上的 `W26` 节第 4.8 节“创建和管理 `RAID` ”后，完成 `W26.8b`“添加 `RAID1` 镜像”中的示例。使用第 1 步中的适当管理命令在系统上安装 `mdadm`，如附录 A `W26.4.8` 所示。

- 23. 检查`/lib/systemd/system/cups.service`文件，用自己的话简要说明在没有插入打印机时 `CUPS` 如何处于未激活状态。

- 24. 阅读网站上的 `W26` 节第 4.8 节“创建和管理 `RAID` ”后，完成 `W26.8b`“添加 `RAID1` 镜像”中的示例。使用第 1 步中的适当管理命令在系统上安装 `mdadm`，如附录 A `W26.4.8` 所示。

# Linux 基础

- b. 你如何让 `CUPS` 可用？

- a. 使用系统上的 `top` 命令查看顶部进程：

```
| PID | USER | PR | NI | S | VIRT | RES | SHR | %CPU | %MEM | TIME | TIME+ | COMMAND |
|---|---|---|---|---|---|---|---|---|---|---|---||
| 15159 | root | 20 | 0 | S | 485236 | 31610 | 27676 | 0.0 | 0.5 | 00:00:03 | 00:00:03 | rcu_sched |
| 15079 | root | 20 | 0 | S | 185604 | 61616 | 31896 | 0.0 | 0.6 | 00:00:07 | 00:00:07 | gnome-theme- |
| 2228 | root | 20 | 0 | S | 399344 | 92040 | 51544 | 0.4 | 1.5 | 00:14:56 | 00:25:28 | us-d |
| 2570 | root | 20 | 0 | S | 157696 | 19304 | 17496 | 0.3 | 0.2 | 00:03:35 | 00:35:24 | kworker-/
```

在 `top` 显示中，哪些是顶部进程，为什么？

用自己的话并尽可能通过验证的方式定义“合成文件系统”（`synthetic file system`）。

回答以下问题：

在 17.4 节我们划分的 `Linux` 存储虚拟层中，伪文件和特殊文件系统的内容是跨启动的，还是说定义它们的数据结构及其特定内容在每次系统构建并重启时都会重新创建？它们的数据结构和内容在系统构建时是固定不可变的，还是其内容会随时间变化？如何变化？

在回答前面的问题时，列出几个伪文件和特殊文件系统的示例，你如何发现它们的哪些部分是易失的、持久的，或者在多大程度上是？你如何知道哪些是固定的，如果在系统构建时如果是的话？

# 项目

# 项目 1

对你的 `Linux` 系统进行“裸机”安装，使整个系统在安装时被加密。

例如，我们在网站上的 `W26` 节第 9.7.2 节中为 `Linux Mint` 展示了此过程。

这在系统安全方面提供了哪些优势，特别是在对抗特定形式的安全泄露方面？

# 项目 2

在你的 `Linux` 系统上，将一个内部挂载的、非系统盘的 `SATA` 硬盘镜像到 `USB` 驱动器上。该 `SATA` 硬盘可以作为你最初创建 `zpool` 的第一个 `vdev`，而 `USB` 闪存盘则作为镜像附加到 `zpool` 的新 `vdev`。以下是关于如何成功完成此项目的建议：

- a. 确保你拥有系统盘的逻辑设备名称，例如 `/dev/sda`。

  不要在该问题中误用该驱动器，否则将导致你的系统盘无法使用！
