
存储库。对于基于 Debian 的系统，apt 工具套件允许你查询存储库中的软件包信息，并下载任何新或已更新的软件包。基于 Red Hat 的系统使用 yum 或 dnf 工具与其存储库进行交互。这三种工具都允许你查询远程存储库中的软件包、查询本地软件包管理数据库，并根据需要安装或删除软件包。

**解释应用容器与包管理系统有何不同。** 像 snap 和 flatpak 这样的应用容器将运行应用程序所需的所有文件（包括任何依赖的应用程序）打包到一个单一的软件包中。虽然这可能会创建依赖应用程序的重复副本，但它确保了每个应用程序都安装了精确正确版本的库和依赖应用程序以使其正常工作，从而使应用程序从一个系统迁移到另一个系统变得轻而易举。

## 复习题

- 1. 你应该使用哪两个程序从应用程序的网站下载 tarball？（选择两项。）
  - A. `wget`
  - B. `cURL`
  - C. `dpkg`
  - D. `rpm`
  - E. `yum`

- 2. Fred 收到了以源代码形式提供的应用程序。他应该运行什么脚本来创建可执行的应用程序？
  - A. `dpkg`
  - B. `rpm`
  - C. `yum`
  - D. `make`
  - E. `wget`

- 3. Sherri 正在尝试从源代码编译一个应用程序。在她创建应用程序可执行文件之前，她应该运行什么脚本来创建 `make` 脚本？
  - A. `make`
  - B. `make install`
  - C. `configure`
  - D. `gcc`
  - E. `dpkg`

- 4. 开源 Linux 应用程序最常用的编译器是什么？
  - A. `gcc`
  - B. `make`
  - C. `configure`
  - D. `dpkg`
  - E. `rpm`

- 5. Harry 已经完成了他的应用程序源代码，但需要对其进行打包以进行分发。他应该使用什么工具，以便它可以在任何 Linux 发行版中提取？
  - A. `dpkg`
  - B. `rpm`
  - C. `yum`
  - D. `apt-get`
  - E. `tar`

- 6. 通常一起使用哪些 `tar` 命令行选项从 tarball 文件中提取和解压文件？
  - A. `-Uvh`
  - B. `-zxvf`
  - C. `-xvf`
  - D. `-zcxf`
  - E. `-cvf`

- 7. Rocky Linux 发行版为软件包使用哪种文件扩展名？
  - A. `.deb`
  - B. `.rpm`
  - C. `.tgz`
  - D. `.tar`
  - E. `.gz`

- 8. Sally 需要在她的 Ubuntu Linux 系统上安装一个新软件包。该软件包以 DEB 文件形式分发。她应该使用什么工具？
  - A. `rpm`
  - B. `yum`
  - C. `dnf`
  - D. `dpkg`
  - E. `tar`

- 9. 你使用什么工具从基于 Red Hat 的存储库中安装软件包？（选择两项。）
  - A. `dpkg`
  - B. `tar`
  - C. `yum`
  - D. `apt-get`
  - E. `dnf`

- 10. 基于 Red Hat 的 Linux 发行版使用什么应用容器格式来安装应用程序？
  - A. `flatpak`
  - B. `rpm`
  - C. `dpkg`
  - D. `snap`
  - E. `gcc`

# 第 14 章

# 维护内核模块

✓ 目标 1.7：给定场景，管理软件配置。

![](img/c0a399aca0d18f8822d714ad0a173123_488_0.png)

![](img/c0a399aca0d18f8822d714ad0a173123_489_0.png)

模块（也称为内核模块）是一个自包含的驱动程序库文件。使用模块而不是将所有功能编译进内核的优点在于，它们使 Linux 内核更轻量、更灵活。因为模块可以动态地加载和卸载到内核中，所以我们可以在需要时或按需添加某些内核功能。它们在不重启系统的情况下扩展了内核的功能。

我们将查看各种内核模块类型、它们的文件存储位置以及模块配置文件的位置。本章还将探讨如何动态链接和取消链接模块，查看模块信息，以及移除模块。

### 探索内核模块

内核模块有不同的形式。它们如下：

- 设备驱动程序：促进与硬件设备的通信。
- 文件系统驱动程序：文件系统 I/O 所必需的。
- 网络驱动程序：用于实现网络协议。
- 系统调用：提供额外的功能以增加/修改系统服务。
- 可执行文件加载器：允许加载额外的可执行文件格式。

在处理模块时，你应该熟悉几个不同的文件和目录。支持内核所需的模块存储在 `/lib/modules/` 目录树中。系统中可用的每个 Linux 内核版本在 `/lib/modules/` 目录中都有自己的子目录。Ubuntu 20.04 发行版中此目录及其内核版本子目录的示例如清单 14.1 所示。

**清单 14.1：** 查看 /lib/modules 目录

```
$ ls -F /lib/modules
5.11.0-40-generic/ 5.4.0-31-generic/ 5.4.0-47-generic/
5.4.0-26-generic/ 5.4.0-42-generic/ 5.4.0-48-generic/
$
```

请注意，发行版可能会略有不同地实现此目录。例如，基于 Red Hat 的发行版将 `/lib/modules/` 目录硬链接到 `/usr/lib/modules/` 目录。因此，它们是同一个目录，但有两个不同的名称。Rocky Linux 8.5 系统上的示例片段如清单 14.2 所示。

**清单 14.2：** 查看 `/lib/modules` 和 `/usr/lib/modules` 目录

```
$ ls -F /lib/modules
4.18.0-305.19.1.el8_4.x86_64/  4.18.0-348.2.1.el8_5.x86_64/
4.18.0-305.3.1.el8_4.x86_64/     4.18.0-348.el8.x86_64/
$ ls -F /usr/lib/modules
4.18.0-305.19.1.el8_4.x86_64/  4.18.0-348.2.1.el8_5.x86_64/
4.18.0-305.3.1.el8_4.x86_64/   4.18.0-348.el8.x86_64/
$ ls -id /lib/modules
16808755 /lib/modules
$ ls -id /usr/lib/modules
16808755 /usr/lib/modules
$
```

注意清单 14.2 中这两个目录共享相同的 inode 号。硬链接在第 3 章“管理文件、目录和文本”中已经介绍过。如果需要，你可以自定义模块以定义所需的任何独特参数，例如设备运行所必需的硬件设置。在一些较旧的 Linux 发行版中有一个单一的配置文件 `/etc/modules.conf`，而在较现代的发行版中则有配置目录：

- `/etc/modprobe.d/` 或 `/etc/modules-load.d/` 包含在系统安装时生成或由管理员创建的配置文件。
- `/lib/modprobe.d/` 存储由第三方软件包生成的配置文件。
- `/usr/lib/modprobe.d/`，如果存在，通常硬链接到 `/lib/modprobe.d/` 目录。
- `/run/modprobe.d/` 存储在运行时生成的配置文件。

每个配置目录中都有多个具有 `.conf` 文件扩展名的配置文件。Rocky Linux 8.5 发行版上的示例如清单 14.3 所示。

**清单 14.3：** 查看 `/etc/modprobe` 目录

```
$ ls /etc/modprobe.d
firewalld-sysctls.conf  lockd.conf  nvidim-security.conf  tuned.conf
kvm.conf                ml4x.conf   truescale.conf        vhost.conf
$ ls /lib/modprobe.d
dist-alsa.conf  dist-blacklist.conf  libmlx4.conf  systemd.conf
$
```

在 Linux 虚拟目录系统中，内核模块以及模块配置文件有许多潜在位置。因此，明智的做法是查看一下你自己的 Linux 服务器，并记录它们的位置。

![](img/c0a399aca0d18f8822d714ad0a173123_491_0.png)

> 对于 systemd 系统，**systemd-modules-load.service** 负责在启动时加载内核模块。你可以使用 `grep` 在 service 单元文件中搜索 **ConditionDirectoryNotEmpty** 指令，以找到它可能从中加载模块的各种目录。

许多设备驱动程序内核模块要么在系统启动时加载，要么在硬件设备连接到系统时动态加载。如果出现问题，你需要知道使用哪些工具来帮助你诊断问题。有三个实用程序可以帮助处理模块：

- **dmesg** 显示当前的内核环形缓冲区。
- **lsmod** 显示简要的模块信息。
- **modinfo** 提供详细的模块数据。

就模块而言，模块故障有时会触发内核消息。dmesg 命令很方便，因为它可以查看与当前事件相关的内核消息。在启动时，你的发行版可能会快照内核环形缓冲区并将数据存储在文件中（通常是 `/var/log/dmesg` 文件）。这两个环形缓冲区信息来源都可以帮助你追踪内核模块问题。

![](img/c0a399aca0d18f8822d714ad0a173123_491_1.png)

> 环形缓冲区是内存中的固定大小数据结构。它不是环形的，而是更像是一个管子。在内核环形缓冲区中，随着新消息进入管子，旧消息会移向结构的末端，最旧的消息会从管子的末端“掉落”（被删除）。

dmesg 实用程序只需将当前内核环形缓冲区转储到 STDOUT。使用 grep 命令挖掘这些消息很有帮助。一个简短的示例如清单 14.4 所示。

**清单 14.4：** 使用 dmesg 和 grep 显示模块消息

```
$ dmesg | grep -i driver
[...]
[    1.674321] e1000: Intel(R) PRO/1000 Network Driver - version 7.3.21-k8-NAPI
[    3.614747] cdrom: Uniform CD-ROM driver Revision: 3.20
[...]
```

