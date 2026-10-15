
所有 `/modules` 和 `/static` 之后会被删除。在此期间，这些目录包含了设置所需的组件。要查看这些目录以及其他组件，你可以从解压初始 RAM 磁盘并将其挂载开始。在运行 Kpix 系统时，以下是检查初始 RAM 磁盘的方法：

1. 解压并挂载 `minert.gz` 初始 RAM 磁盘：

```
$ cd /cdrom/boot/isolux
$ gunzip -dc minert.gz > /tmp/mininert.ext2
$ sudo mkdir /tmp/mini
$ sudo mount -o loop -t ext2 /tmp/mininert.ext2 /mnt/mini
```

2. 列出初始 RAM 磁盘的内容：

```
$ ls -cf /mnt/mini
```

`KNOPPIX/` `bin@` `dev/` `lib/` `media/` `modules/` `proc/`
`static/` `tmp/` `mini@` `cdrom/` `etc/` `linuxc*` `mnt/` `opt@` `sbin@` `sys/` `usr/`

制作如第 6 节“构建自定义 Kpix 现场版 CD”所示，你可能会决定制作自己的初始 RAM 磁盘以包含（或排除）驱动程序或添加要运行的命令。在文件被解压并如前已挂载后，你可以进行任何修改。完成后，卸载该文件（`umount /mnt/mini`）并重新压缩文件（`gzip /tmp/mininert`）。

### 注意

从现在开始，不再使用初始 RAM 磁盘的文件系统，使用 kadisci 构建的 Knoppix 现场 CD 会独立于初始 RAM 磁盘设置持久文件系统结构。当新环境建立后，将运行 `pivot_root` 命令以使运行中的内核使用新的文件系统结构。

### linuxrc 脚本

初始 RAM 磁盘文件根目录下的 `linuxrc` 脚本（在 Knoppix 中为 `init.gz`）引导了现场环境的大部分初始设置。该脚本的大部分工作是挂载启动过程完成后 CD 将使用的文件系统。然而，在 Knoppix 中，`linuxrc` 脚本还确保加载模块以处理现场 CD 可能会遇到的任何特殊硬件需求（如 SCSI 设备）。

`linuxrc` 在此阶段的工作是通过此时可有限命令和模块完成的。大部分工作是使用内置于 Linux 内核的命令、`ash` shell 以及用于添加和删除模块的命令（`insmod`、`rmod` 和 `modprobe`）完成的。这些是 `linuxrc` 脚本执行执行的一些内容：

- **设置颜色**——随着 Knoppix 的启动，你会发现不同类型的消息以不同的颜色显示。这些颜色的变化使得 Knoppix 启动时更容易看到发生了什么。在 `linuxrc` 脚本中，以下变量被设置为它们所代表的颜色名称，以输出不同类型的消息：`RED`（失败或错误消息）、`GREEN`（成功消息）、`YELLOW`（描述）、`BLUE`（系统消息）、`MAGENTA`（找到的设备或驱动程序）、`CYAN`（问题）和 `WHITE`（提示）。你注意到 Knoppix 以一些有趣的方式使用这些颜色。“Welcome to KNOPPIX”消息将 KNOPPIX 的每个字母显示为单独的颜色。

- **挂载系统文件系统**——在 `linuxrc` 脚本中挂载了 `/proc` 和 `/sys` 文件系统。`/proc` 文件系统提供了访问内核使用的数据结构的接口。`/sys` 文件系统包含内置驱动注册的数据，可以从用户空间的进程进行访问。

- **检查选项**——`linuxrc` 脚本检查用户或 `isolinux.cfg` 文件可能设置的选项。这些值会导致环境变量被设置，并在随后的 `linuxrc` 脚本中使用。这里消耗的许多值关闭某些功能（例如 `nosci`、`nosi` 或 `nofirewire`）或设置运行模式（如调试或专家模式）。

## 第 4 章 理解现场 Linux CD 的工作原理

- **设置 KNOPPIX 的位置**——`KNOPPIX_DIR` 变量设置包含 KNOPPIX 镜像文件的目录（默认为 `KNOPPIX` 目录）。`KNOPPIX_NAME` 变量设置 Knopix 存档的名称（默认为 `KNOPPIX`）。此镜像包含了运行 Knopix 使用的大部分文件系统（文件、目录、应用程序、设置）的压缩存档。因此，Knopix 镜像位于 CD 文件系统根目录下的 `/KNOPPIX/KNOPPIX`。

> 注意
>
> 如果你曾为多个版本的 Knopix（或其派生版本）设置了现场 DVD，通过更改每个版本的初始 RAM 磁盘的 `linuxrc` 脚本中 `KNOPPIX_DIR` 的值，可以允许多个 Knoppix 发行版在同一块磁盘上共存（并可启动）。例如，一个发行版可以使用 `/KNOPPIX/a` 作为 KNOPPIX 文件镜像系统的位置。另一个可能使用 `/KNOPPIX/b`，依此类推。如果你为初始 RAM 磁盘命名不同的名称（`inita.gz`、`initb.gz` 等），不同的标签可以指向不同的版本。

- **以不同的模式运行**——如果 `debug` 被设置为启动选项，`linuxrc` 会设置一个特殊的 shell 以调试模式启动现场 CD。如果专家模式（expert mode）被设置为启动选项，运行现场 CD 的人员将被询问是否想从软盘安装额外的模块。

- **探测并配置设备**——`linuxrc` 脚本检查 PCI 设备（`/proc/pci`）并搜索可能需要模块才能使用的输出 SCSI 设备。它还会检查并尝试为任何 IDE 设备、USB 设备和 Firewire 设备安装模块。

- **寻找 KNOPPIX**——在所有可用的 CD 和硬盘存储设备（IDE、SCSI 等）现在都已正确检测并配置后，`linuxrc` 脚本尝试寻找将用于使大部分文件系统（包括应用程序和设置）变得可用的 `KNOPPIX` 存档。

- **挂载 KNOPPIX**——找到后，将挂载 KNOPPIX 镜像。如果找到多个 KNOPPIX 镜像，它们将分别挂载为 `KNOPPIX2`、`KNOPPIX3` 等。每个镜像都被挂载为一个设备，当从这些文件系统请求文件和目录时，它们可以动态解压缩。如果人员请求 knoppix 将 KNOPPIX 镜像写入并从硬盘（hd）或内存（ram）运行，`linuxrc` 会提供可用写入空间。

- **挂载 RAM**——在检查合理大小后，`linuxrc` 创建了一个 RAM 磁盘（`/ramdisk`）。在 `/ramdisk` 上创建了可写目录，这些目录可以通过（符号链接）在文件系统中。这些位置包括 `/home` 和 `/tmp`。

- **创建 UnionFS 系统**——为了让现场 CD 的所有只读目录作为读写目录可用，`linuxrc` 使用 UnionFS 与 `/ramdisk` 上的可写目录。要查看从 UnionFS 系统（`/UNIONFS`）链接了哪些目录，请在 knoppix 启动后输入 `ls -l /`。第 5 章描述了如何使用 UnionFS 合并只读目录（来自 CD）和读写目录（来自内存磁盘）。

- **设置 /etc 目录**——`/etc` 目录中的某些文件和目录不能链接而必须是只读文件。为了确保这一点，`linuxrc` 脚本从 CD 复制这些文件的版本：`passwd`、`sudoers`、`gshadow`、`group`、`dhcp`、`localtime` 和 `fstabconf`。

- **执行最终清理**——为了清理 `/etc/stab` 文件，`linuxrc` 脚本从 `/proc/mounts` 获取信息。然后删除 `/linuxrc` 文件并退出。随着 `linuxrc` 脚本完成，启动过程的控制权交给 Linux 内核。内核将控制权交给 `init` 进程。

### 启动 init（以及 initrc 文件）

`init` 进程接管启动过程以引导服务的启动并设置系统参数。事实上，`init` 的进程 ID 被称为所有进程的父进程。`init` 之所以是 1，是因为它是运行系统上第一个启动的进程，并启动了所有其他进程。

`init` 进程的关键依据是 `/etc/initrc` 文件的内容。`init` 运行的服务基于传递给 `init` 的运行级别（run level）以及设置为在该运行级别下启动的服务。对于 knoppix，默认是启动到桌面运行级别（运行级别 5）并运行至少一个特定于 knoppix 的启动脚本。

要理解 `init` 启动后发生了什么，请遵循 `/etc/initrc` 文件中的设置。除非被覆盖，否则 knoppix 根据 `/etc/initrc` 文件中的此项启动到运行级别 5：

```
5:initdefault:
```

被标识为 `sysinit` 进程的项在 `init` 启动时执行。`/etc/initrc` 中的以下条目会导致 `rcS` 脚本运行所有以字母 S 开头并位于 `/etc/init.d/rcS` 目录的 init 脚本：

```
~:~sysinit:/etc/init.d/rcS
```

默认情况下，唯一设置为在系统初始化时启动（来自 `/etc/rcS` 目录）的脚本是 `knoppix-autoconfig` 脚本。链接指向 `/etc/init.d/knoppix-autoconfig`。这是 knoppix 配置发生的地方。（`knoppix-autoconfig` 将稍后描述。）

`/etc/initrc` 中的下一组指示了根据当前运行级别启动的内容。要使运行级别不是 5，你必须更改 `initdefault` 行的值或传递运行数字作为启动选项。以下是这些行：

```
### 在单用户模式下做什么。
~:S:respawn:/bin/bash -login /dev/tty1 2>&1 </dev/tty1

### /etc/init.d 在更改时执行 S 和 K 脚本
#
### 运行级别 0 是停止。
### 运行级别 1 是单用户。
### 运行级别 2-5 是多用户。
### 运行级别 6 是重启。
```

```
10:0:wait:/etc/init.d/knoppix-halt
11:1:wait:/etc/init.d/rc 1
12:2:wait:/etc/init.d/rc 2
13:3:wait:/etc/init.d/rc 3
14:4:wait:/etc/init.d/rc 4
15:5:wait:/etc/init.d/rc 5
16:6:wait:/etc/init.d/knoppix-reboot
```

有效的运行状态允许你进入单用户模式（S 或 1）和多用户模式（2、3、4 或 5）。在单用户模式（S）下，knoppix 打开 root shell 且不启动其他服务。在单用户模式（1）下，knoppix 运行 `/etc/init.d/rc` 脚本并将 1 作为选项。

### 现场 Linux CD

在 `/etc/rc1.d` 目录中的脚本将被启动。同样，你可能启动到的其他运行状态（2, 3, 4 或 5）也会从其运行级别目录（`/etc/rc2.d`、`/etc/rc3.d` 等）中启动以 S 开头的运行脚本。

在 Knoppix 中，它主要是一个桌面系统，这些目录中可能在服务器系统上运行的服务（例如 Web 服务器、FTP 服务器、MySQL 服务器等）默认是未启用的（即不会被添加到这些目录中）。

> 注意
>
> Knoppix 中许多代表服务的脚本在 `/etc/init.d` 目录中均都是可用的。因此，如果你正在创建自己的自定义 Knoppix，你可以将其中任何一个脚本链接到任何运行级别下的一个文件中，以便在相应的运行级别下获取它。例如，如果你正在自定义 Knoppix，可以输入以下命令：
>
> ```
> ### ln -s /etc/init.d/apache2 /etc/rc5.d/S85apache
> ```
>
> 此命令创建了从 `apache2` 脚本（用于启动 Apache Web 服务器）到 `/etc/rc5.d` 目录下一个文件的链接。当计算机下次进入运行级别 5（默认桌面运行级别）时，Apache Web 服务将启动。

当运行级别开始时，运行的其他脚本以字母 K 开头。例如，如果你从运行级别 5 切换到运行级别 3，`K10session` 脚本将关闭你的 X 服务器（桌面界面）并让你返回到 shell。除了运行级别 5 之外，每个运行级别都会关闭桌面，因此这是当你关闭电脑（运行级别 0）或重启（运行级别 6）时最先启动的几个之一。

正如你可能从上一句中推测的那样，你不应该将运行级别设置为 0 或 6。这样的话，你的系统将直接关闭，`init` 会介入。如果设置为 6，它将不断重启。大多数 Linux 系统被设置为 5（启动到桌面）或 3（启动到一组预定义的服务，且无桌面）。运行状态 2 和 4 在旧的 UNIX 系统中具有历史含义，但现在已经没有太大意义了。

`/etc/initabb` 文件中用于启动 Knoppix 的下一组行代码与启动虚拟终端有关：

```
### 4 virtual consoles with /bin/bash -login >dev/tty1 2&1 </dev/tty1
2:2345:respawn:/bin/bash -login >dev/tty2 2&1 </dev/tty2
3:2345:respawn:/bin/bash -login >dev/tty3 2&1 </dev/tty3
4:2345:respawn:/bin/bash -login >dev/tty4 2&1 </dev/tty4
```

## 第 4 章理解现场 Linux CD 的工作原理

这些行显示对于运行级别 1 到 5，`bash` shell 作为登录 shell 连接到特定的 tty 设备（`/dev/tty1`）启动。对于运行级别 2, 3, 4 和 5，创建了三个额外的运行级别（tty 到 tty4）。你可以通过按下 Ctrl+Alt+F1、Ctrl+Alt+F2 等进入这些不同的虚拟终端。如果你的桌面界面变得混乱，虚拟终端是获取 shell 的一种有用方法。

`/etc/initabb` 文件中与启动系统相关的最后一行与启动你的 X 桌面有关。当 knnoppix 进入运行级别 5（默认）时，以下行是最后执行的行：

```
### Run X Window session from CDROM in runlevel 5
w5:wait:/bin/sleep 2
x5:wait:/etc/xsession start
```

在暂停 2 秒（`sleep 2`）后，运行带有 `start` 的 `xsession` 脚本。你的 X 桌面界面基于启动期间确定的设置（存储在 `/etc/xconfig` 目录下的 `xserver` 和 `knnoppix` 文件中）。它还会尝试加载运行显卡可能所需的模块（例如加载 `AGPGART` 和 `DRM` 模块）。

此时，你的 Knoppix 桌面界面应该已经启动，你应该可以开始使用 Knoppix 了。

### 理解运行中的现场 Linux 系统

当 Linux 系统运行后，你可以进一步了解你的现场 Linux 系统是如何启动的。对于 Knoppix，如前所述，`knoppix-autoconfig` 脚本在现场 CD 首次启动时设置 knnoppix 值。你也可以在运行的系统上尝试命令来显示值是如何设置的。

### 理解 knnoppix-autoconfig

当 `init` 进程在 Knoppix 启动期间接管时，`knoppix-autoconfig` 脚本从系统初始化目录中的链接运行：`/etc/rc.S/S00knnoppix-autoconfig`。通过查看此文件，你可以看到 Knoppix 中许多运行时功能是如何设置的。当你自定义自己的现场 CD 时，这是一个你可能会考虑修改的脚本。

是 `knnoppix-autoconfig` 脚本中发生的处理亮点：

- `PATH`—`PATH`（shell 寻找你运行的命令的地方）被设置为包含 `/bin`, `/sbin`, `/usr/bin`, `/usr/sbin` 和 `/usr/X11R6/bin`。这非常重要，因为即使对于非 root 用户（例如），knoppix 也期望 `PATH` 中包含 `/sbin` 和 user。

- `Colors`—颜色在脚本中定义。当你自定义自己的现场 CD 时，这是一个你可能会考虑修改的脚本。

- `Boot options`—启动选项由此脚本读取。这对于...非常重要。

- `Config files`—配置文件在脚本中创建。

- `Language`—语言根据启动选项进行设置。

- `Desktop`—桌面在脚本中设置。

- `Hostname`—主机名被设置。

- `Clock`—时钟被设置为 GMT 或 UTC。

- `Live CD or installed`—如果 knnoppix 从硬盘运行，此脚本会对...执行操作。

- `Interactive setup`—如果你是以启动选项进入的，在启动过程的几个点你都会获得更改设置的机会。第一个机会出现在这一点，当你被给予选择...时

### Live Linux 光盘

重新配置鼠标的选项。当 X 配置完成后，你稍后将拥有重新配置图形子系统的选项。

- `X 配置`——最新版本的 Knoppix 使用 X.Org X 服务器。为了创建 Xorg 服务器进程使用的 X 配置文件（`/etc/X11/xorg.conf`），`knopix-autoconfig` 脚本会运行 `/sbin/mkxorgconfig`

`mkxorgconfig` 脚本读取启动选项，例如特定的垂直和水平刷新率（`xvrefresh` 和 `xrefresh`）、垂直和水平同步率（`vsync` 和 `hsync`）以及屏幕分辨率（`screen`），以配置 X 服务器。同样，任何特殊的鼠标和键盘选项都会被记录并整合到 `xorg.conf` 文件中。

在创建了新的 `xorg.conf.new` 文件后，它会被复制到其永久位置（`/etc/X11/xorg.conf`）。然后，屏幕上将显示有关所选 X 服务器和设置的信息。

- 运行级别（Run level）——此时，将运行 `runlevel1` 命令来确定当前的运行级别。默认情况下，这将运行级别 5（桌面）。如果在启动提示符处输入了其他运行级别（S, 1, 2, 3 或 4），则将使用该运行级别。
