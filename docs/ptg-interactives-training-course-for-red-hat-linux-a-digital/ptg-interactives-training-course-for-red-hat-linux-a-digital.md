
# PTG Interactive Red Hat Linux 培训课程：CD-ROM 数字化研讨会（第2版）

## 第 1 节 安装

### 目标
- 理解使用 Linux 的需求
- Red Hat Linux 的选择
- 准备安装 Linux
- 安装 Linux

## 第 1.1 节理解 Linux 的需求
- Red Hat 是最好的 Linux 发行版之一；Red Hat 的 7.1 版本增加了许多新功能：
  - 最新的 2.4 内核。
  - 三种默认配置：“工作站 (workstation)”、“服务器 (server)”和“笔记本电脑 (laptop)”，以及一个允许更个性化配置的自定义。
  - `XFree86` 版本 4.0，包含了针对大多数 3D 显卡的集成 `OpenGL` 支持，以及对观看 DVD 的更好支持。
  - 支持许多常见的 `USB` 外设。
  - 内置防火墙配置可帮助保护您的机器。
  - 改进了对笔记本电脑的支持。
- 如果您已有一个 Red Hat 系统并想进行升级，请查看课程稍后关于升级的章节。

笔记：

## 第 1 节 安装

### 第 1.2 节 关于 Linux

### 什么是 Linux，你为什么应该使用它？

笔记：

### 第 1.3 节安装前的准备

### 获取 Linux
- Red Hat 有多个版本；这些版本在可用性、价格和支持选项上有所不同。
- 标准版 (Standard) 包含两张操作系统 CD、30 天网络技术支持，以及针对一个系统的 30 天 Red Hat 网络支持管理器 (Red Hat Network Support Manager) 权限。
- 豪华版 (Deluxe) 包含更多印刷版手册、60 天电话或网络支持，以及针对 5 个系统的 60 天 Red Hat 网络支持管理器访问权限。
- 专业版 (Professional) 将电话和网络支持增加到 90 天，并为 10 个系统提供 90 天 Red Hat 网络支持管理器访问权限。
- 关于每个版本之间差异的更完整列表，可以在 Red Hat 网站上找到：`http://www.redhat.com/products/software/linux/rhl_compare.html`。
- Linux 初手用户应该购买豪华版，因为它包含了支持。
- 这些版本可以在 CompUSA 和 Best Buy 等大型商店找到。
- Red Hat 在其 `FTP` 站点和各种镜像站上提供免费的发行版。
- 此版本可以免费分发。
- 由于 Red Hat 不销售此版本，因此没有手册、应用程序 CD 或支持。
- 如果您想通过 Internet 或 `LAN` 通过局 `FTP` 进行安装，也可以选择这种方法。
- 7.1 版本现在包含两张 CD，因此如果您选择此方案，会有更多内容需要下载和刻录。

### 准备安装
- Red Hat 提供的 `CD-ROM` 可启动的，因此您不需要制作启动软盘。请检查您的系统或主板文档，以确定如何从 `CD-ROM` 启动。
- 尽可能收集有关您系统硬件的所有信息。
- Red Hat 安装程序通常会自动检测您拥有的硬件。
- 如果安装程序无法识别硬件，它会提示您输入参数，这些参数可以在手册中找到。
- 准备好您的网络配置信息。

笔记：

### Kickstart（自动安装）
- Red Hat 的 `Kickstart` 安装允许您预配置安装并创建一个包含它的启动软盘。这大大提高了安装速度。
- `Kickstart` 功能仅适用于本地 `CD-ROM` 和 `NFS` 安装。
- 阅读 `doc/README.ks` 文件了解执行 `kickstart` 安装。

笔记：

## 第 1 节 安装

### 执行安装
- 将第一张 CD 插入 `CD-ROM` 驱动器。
- 选择安装方法。
  - 默认方法是图形化安装程序，最适合初学者。
  - 文本安装方法使用基于字符的安装，适用于不支持 Red Hat Linux 显卡的服务器。
  - “nofb” 选择使用不带帧缓冲 (framebuffer) 的 `SVGA`。
  - “rescue (救援)” 选择允许您尝试从 Linux 恢复。
  - “Custom (自定义)” 适用于对安装过程进行精确控制。
- 大多数硬件都适用于标准安装。
- 选择您的安装语言；默认是英语。
- 选择您的键盘布局。默认是 105 键。
- 在下一个屏幕设置您的鼠标。
- 窗口系统假设鼠标有三个按钮。
- 如果您已经安装了旧版本的 Red Hat，可以选择“Upgrade (升级)”。
- 对于新安装，可以选择三种预配置的设置：服务器、工作站和笔记本电脑。
工作站安装将清除所有分区并使用所有未分区空间；其他操作系统将不受影响。
服务器安装将清除所有硬盘上的所有分区，并且不会安装 X Windows 系统。
使用此安装方法时应谨慎，因为系统上的任何数据将被删除。
笔记本电脑安装与工作站安装类似，但增加了 `PCMCIA` 支持。

### 第一讲座 安装
- 屏幕底部有一个“检查坏块”（check for bad blocks）选项，这对于新硬盘或质量存疑的硬盘是建议的。
- 这会增加很多分区的时间，但可以防止数据丢失。
- `LILO` 是 Red Hat Linux 的启动加载器，它提供了一个图形界面，让你在启动时选择启动的操作系统。
- 选择了“线性模式”（linear mode），请保持现状，不要修改任何参数。
- 如果你有一个 `IDE` `CD-R` 或 `CD-RW` 驱动器，并在内核参数中使用“hbc-ide-scsi”或类似的字符串，Red Hat 已识别出你的 `CD-R/W`。
- 勾选框表示默认操作系统，即 Linux 安装程序。你可以通过选择另一个操作系统然后点击“默认启动镜像”（Default Boot Image）来更改它。
- 如果你有以太网卡被检测到，你可以在下一个服务器中对其进行配置。默认情况下，设备在启动时启动，并使用 `DHCP` 配置你的以太网地址和设置。
- 如果你没有 `DHCP` 服务器，请取消勾选 `DHCP` 并输入网络管理员提供给你的信息。
下一个屏幕将进入 Red Hat 的防火墙配置。
- 你现在可以配置系统可用的语言。默认将是你用于安装时使用的语言。
- 下一个是时区和位置信息。
- `UNIX`（以及 Linux）喜欢使用协调时（`UTC`）作为时间参考。
- 其他操作系统期望系统时间为本地时间而非 `UTC`。如果你仅将该系统用于 Linux，你可以选择“系统时钟使用 `UTC`”（System clock uses UTC），稍后适时设置时间。
- 通过在地图上点击你所在的大致位置来选择所在的洲，从而设置时区信息。
- 系统安全非常重要，所以 Red Hat 要求你设置 root 密码，允许你现在配置用户账户。
- 我们稍后将介绍 `MD5` 和影子密码；除非另有，否则你应该保持此屏幕上的选项不变。
Red Hat Linux 有许多可用软件包。
- 它们可以作为包的形式选择，这些包已经设置好了依赖关系。
- 许多软件包会告诉你它们是什么（例如，游戏）。
- 你可以滚动到列表底部并选择“全部”（Everything），或者点击“选择单个包”（select individual packages）来安装特定的包。
现在将配置 X 窗口系统。如果你有标准的显卡，它已经被识别并确定；请验证模型是否正确，板载 RAM 的数量也正确。
- 下一个屏幕也识别了你的显示器（如果可用）。如果没有，选择“通用”（Generic）并选择最接近你的显示器的显示器。
- 设置色彩深度和默认分辨率。默认值取决于你的显示器和显卡的组合。
- 你可以测试给定的设置看看看起来是否正确。
- 如果你选择了 `KDE` 和 `GNOME` 桌面环境，你可以选择默认使用的环境。
- 选择文本登录或友好的图形登录。

### Notes：

## 1.4 节

### 总结
- 如果你有一个较新的硬件相当标准的系统并且计划只在上面运行 Linux，安装 Red Hat 非常简单。
- 可以使用 `disk dru` 程序对你的硬盘进行分区。
- 考虑符合你 Red Hat 版本，包括支持性。

Notes：

## 第二讲座

### Linux 启动与关机

### 目标
- 分析启动过程
- 更改运行级别（Runlevels）
- 排除启动故障
- 正确关机/重启

## 2.1 节

### 配置 Linux 加载器
- `LILO` 允许你在内核启动之前向其发送启动参数。

Notes：

### 启动提示符
- 安装 Linux 后，启动你的机器可能会弹出一个图形窗口，让你选择启动哪种操作系统。
- 默认是“linux”，如果你不做选择，它将在几秒钟后自动启动。
- Linux 依赖于能够向内核传递选项，因此 `LILO` 让这变得非常简单。
- 你可以将这些选项中的许多添加到 `LILO` 文件中。
- 如果你需要在启动前向 Linux 内核传递额外选项，可以按 `CTRL-X` 访问 `LILO` 的文本界面；这是在启动时向 Linux 内核传递额外参数的唯一方法。



在文本界面中，你可以将许多配置参数添加到你启动 Linux 时使用的名称的末尾。默认情况下，这只是“`linux`”。这些参数允许你执行许多操作，包括更改根分区、决定根文件系统是只读还是读写、指定内存大小等。

# 第二讲座 Linux 启动与关机

## 配置 LILO

- 你可以配置 `LILO` 每次启动时都使用你喜的选项。
- `/etc/lilo.conf` 文件包含 `LILO` 在启动时使用的信息。这也是你配置想要启动的操作系统的地方。
- 下面是一个 `lilo.conf` 文件示例。

启动行告诉 `LILO` 安装到哪里。因为是第一块硬盘，`LILO` 被配置为主启动加载器。

如果你有另一个启动加载器，你可以配置 `LILO` 为启动加载器。

### 示例 lilo.conf

```
### 启动行告诉 LILO 安装主启动加载器
/dev/hda
### 如果你有另一个启动加载器，你可以配置 LILO 为启动加载器。
### 这一行是要安装的镜像
image = /dev/hda
### 第二字段是引用的运行级别
boot = /dev/hda
### 第三个字段是根分区
root = /dev/hda
### 第四个字段是 VGA 模式
vga = ask
```

- 一旦按照你的喜好配置了 `/etc/lilo.conf`，你就必须运行 `/sbin/lilo` 来安装你的配置文件。
- 从系统中移除 `LILO`：
  - 从 `DOS`（以及 `Windows 98`）使用 `fdisk /mbr` 命令。从 `Linux` 中，使用 `lilo -u` 命令将卸载。

## 2.2 节

### init

- `init` 是 `Linux` 内核进入内存并挂载根（`/`）分区后启动的第一个进程。
- `init` 进程始终是 1 号进程。杀死此进程的效果等同于运行 `halt` 或 `shutdown`。
- `init` 程序读取其配置文件，然后开始启动 `Linux` 系统的程序。
- `/etc/inittab` 文件由 `init` 读取，它告诉 `init` 在哪个级别上启动以及启动哪些进程。这将包括 `getty` 等程序；其他脚本将根据你输入的运行级别运行。
- `/etc/inittab` 文件中的条目有四个字段。

### /etc/inittab 示例

```
10:0:wait:/etc/rc.d/rc 0
```

- 字段由冒号分隔。
- 第字段是文件中唯一的，只是任意的两个字母（或数字）序列。
- 第二字段告诉 `init` 在哪个运行级别上引用此字段。
- 第三个字段是 `init` 在脚本运行时可以做什么的选项；`wait` 防止了多个运行级别更改脚本同时运行的问题，强制 `init` 在等待当前脚本完成后启动其他脚本；其他选项包括 `respawn` 和 `once`。
- 第四个字段列出了要运行的脚本或进程。

当 `init` 完成启动脚本后，`Linux` 现在已经可以使用了。

- `init` 继续运行，在需要时重启某些程序，并在运行级别更改时启动或停止其他程序。

## 第 2.3

### 什么是运行级别（Runlevel）？

- 机器的运行级别决定了系统应该提供哪些功能。
- `UNIX` 有一种单用户安全模式，以及其他可用配置。
- 在不同运行级别之间切换不需要重启。例如，你可以在单用户模式启动 `Linux` 以修复启动问题，然后在多用户模式下继续运行而无需重启内核。
- 无论你使用哪种运行级别，`init` 运行的第一个脚本都是 `/etc/rc.d/rc.d` 脚本，它会运行任何运行级别下都需要的所有程序。
- 一旦 `/etc/rc.d/rc.d` 脚本成功完成，`init` 将继续调用它，并传入要进入的运行级别选项（0-6）。
  - 在 `/etc/rc.d` 目录下有六个名为 `rc.[0-6].d` 的目录。
  - 每个目录包含若干脚本，脚本名以“K”或“S”开头，后跟两位数字和程序名。
  - “S”代表启动特定于运行级别的程序；“K”代表杀死脚本（kill scripts），用于杀死（停止）任何当前运行级别未使用的程序。
  - 先执行该运行级别的杀死脚本，然后执行该运行级别的启动脚本。
  - 数字越小的脚本越先执行，这允许网络软件（例如）在 `NFS` 守护进程尝试启动之前先初始化以太网。
  - 名称是对用户提供的描述性名称。
  - 当每个脚本运行时，红帽（`Red Hat`）会报告启动脚本的成功或失败。
  - 脚本执行成功将以绿色显示 `OK`；失败则将以红色显示 `FAILED`。
- 所有这些脚本都是 `/etc/init.d` 目录的链接，该目录包含了所有脚本的主文件。

## 第 2.4

### 当出现问题时

在启动序列中，只有少数地方会导致内核无法完成加载。这些包括：

- 无法挂载根分区。内核可能缺少正确的驱动程序，或者正尝试加载错误的分区。
- 无法使用 `fsck` 自动检查文件系统错误。如果出现这种情况，系统会发出警告并让你进入单用户模式。
- 内核被告知在运行级别 1 启动。
- 加载驱动程序时的其他错误。
- 启动脚本错误。

### 红帽救援镜像（Red Hat Rescue Image）

- 红帽在其 `CD-ROM` 上提供了一个救援镜像，如果你启动 `Linux` 遇到问题，可以使用它启动。
- 救援系统会创建一个 `Linux` 的小型内存驻版本，你可以用它修复损坏的安装。
- 修复 `LILO` 最简单的方法是在安装时创建并使用启动软。。如果没有磁盘，可以使用救援镜像。
- 从救援镜像中使用 `lilo` 比正常操作要困难。使用救援镜像时，内核和 `lilo` 配置文件的位置不在系统根目录下。
- 启动救援镜像后，确保 `/mnt` 目录存在，然后将包含根和 `/etc` 的分区挂载到 `/mnt`，将包含 `/boot` 的分区挂载到 `/mnt/boot`。
- 现在你可以访问 `/mnt/etc/lilo.conf`。编辑它并修复你发现的问题（或复制一份已知的良好的 `lilo.conf`）。
- 最后，使用 `lilo -r /mnt` 安装修复后的 `lilo.conf` 文件。

## 第 2.5

### 系统关机与重启

- 关机最安全的方法是 `sync; sync; sync; /sbin/halt`。
- 如果你选择重启系统，可以将 `halt` 替换为 `reboot` 或 `telinit 6`。
- 以上所有命令用于立即关机系统。如果你选择计划关机，并希望给用户留出完成工作并有序退出，你应该使用 `shutdown` 命令。

### CTRL+ALT+DELETE

- `CTRL+ALT+DELETE` 将关闭 `Linux`。`init` 进程会监控此操作，如果接收到该信号，将关闭机器。默认设置为立即运行 `reboot` 命令。
- 下一节将显示如何禁用 `CTRL+ALT+DELETE` 重启。

### 防止 PC 免受重启影响

- 在重启期间，`Linux` 机器的安全性非常低。
  - `PC` 可以启动一个可以放在软盘上的操作系统 (`DOS`)，并在其中包含可以完全破坏硬盘的程序。
  - 病毒可以感染硬盘的主引导记录 (`MBR`)，这是 `Linux` 启动所需要的。



用户可以自带 Linux 启动软盘来获取 root 权限。

以下是保持公共 Linux 机器安全的若干建议：

- 保护基本输入输出系统 (BIOS)——这是你需要做的第一件事，因为许多其他保护措施依赖于此。
- 为 BIOS 访问设置密码。大多数现代 BIOS 都支持此功能。
- 确保没有人能打开机箱。许多机箱都有锁。
- 如果忘记了密码，可以断开板载电池或将其重置。

备注：

## 第 2.6

### 总结

- 机器的运行级别决定了系统应该提供哪些功能。
- UNIX 有单用户安全模式，以及其他可用配置。
- 在不同运行级别之间切换不需要重启。例如，你可以在单用户模式启动 Linux 以修复启动问题，然后在多用户模式下继续运行而无需重启内核。
- 无论你使用哪种运行级别，`init` 运行的第一个脚本都是 `/etc/rc.d/rc.d` 脚本，它会运行任何运行级别下都需要的所有程序。

## 第 3

### 账户管理

#### 目标

- 添加用户和组
- 添加和删除用户
- 禁用用户
- 使用影子密码 (`Shadow Passwords`)
- 使用可插认证模块 (`PAM`)

## 第 3.1

### 添加用户

- 用户数据和组信息通常存储在三个文件中：`/etc/passwd`、`/etc/shadow` 和 `/etc/group`。
- `/etc/passwd` 文件按格式存储用户名、真实和其他和其他用户信息：`markk:x:500:500:Mark F. Komarinski:/home/markk:/bin/tcsh`。
- 字段由列分隔。
- 字段顺序依次为：用户名、加密密码、用户 ID (`UID`)、主组 ID (`GID`)、真实姓名、主目录和登录 shell。“加密密码”字段中的“x”表示使用影子密码（存储在 `/etc/shadow` 中）。
- `/etc/shadow` 文件存储与密码相关的信息，如加密密码以及密码最后修改的时间和未来何时需要修改的信息。
- 此条目中的字段按顺序为：组名、成为该组成员的密码、组 ID，以及同样是该组成员的其它用户列表。
- 组密码很少使用，因此通常被设置为 `x`，以防止任何未经明确授权的人访问该组。
- 创建用户简单的方法是使用 `adduser`。该程序要求的唯一选项是你想要创建的用户名。
- 默认情况下，`adduser` 会按上述列表设置 `/etc/shadow` 的默认值。你可以使用 `adduser` 来更改这些默认值，或者根据每个用户设置超时和过期权限。

笔记：

## 第 3 节 账户管理

### 第 3.2 节

### 组和文件权限

- Linux 文件的三个访问级别为：用户（user）、组（group）和世界（world）。
- 用户是指拥有文件的个人用户。
- 组是指文件和用户所属的组。
- 世界是指其他所有人。
- 组和 `GID` 用于将逻辑上的人员集合在一起。
- 要让给定组中的任何人都能访问某个文件，请确保该文件位于该组中。
- `# chgrp groupname filename` 会将文件 `filename` 分配给组 `groupname`。
- 使用 `chmod` 命令授予或拒绝对文件的访问权限。

笔记：

### 第 3.3 节

### 删除或禁用用户

- 若要禁用用户账户（即防止用户再次登录），将 `/etc/shadow` 文件中的密码替换为星号（*）或其他字符。
- 若要删除一个用户使其在系统中完全不再存在，请使用 `userdel`。
- 如果在 `userdel` 后添加 `-r`，则 `user` 的主目录也会被删除。
- 如果你禁用了账户，该账户在技术上仍然存在。该用户仍然可以接收邮件，拥有一份在权限正确的情况下其他人可以访问的主目录，并且拥有任何其他账户的所有权限。该用户只是无法登录了。
- 当账户被删除时，系统将退回发送给该用户的任何邮件，原用户拥有的所有文件现在将由该用户曾拥有的 UID 拥有。

笔记：

### 何时禁用，何时删除

- 如果用户在其主目录中有其他人想要或需要访问的数据，请禁用该账户。
- 一旦禁用账户所需的文件移动到其他位置，即可删除该账户。
- 如果账户没有其他用户所需的信息，请备份主目录以及用户拥有的所有其他文件，并删除该账户。

笔记：

### 第 3.4 节

### 使用 PAM

- `PAM`（可插拔认证模块）创建独立的模块来处理密码，并告诉相应的程序输入的密码是正确的。
- `PAM` 验证来自各种来源的密码，从 NIS 到 LDAP 服务器。
- `PAM` 还处理更改密码并可以对密码应用各种方法。
- `PAM` 可以提高安全性；例如，它可以告诉 `passwd` 给定的密码太容易破解。

笔记：

## 第 3 节 账户管理

### PAM 配置

- `PAM` 使用的配置文件存储在 `/etc/pam.d/` 目录下。
- 旧版系统有 `/etc/pam.conf`，但其用法已废弃。
- 在 `/etc/pam.d/` 中，每个文件名都是将使用 `PAM` 的程序名称。
- 如果服务请求 `PAM` 认证且不存在特定的配置文件，`PAM` 将检查 `/etc/pam.d/other`。

默认 PAM 配置文件

```
1. auth #PAM-1.0
2. auth required /lib/security/pam_securetty.so
3. auth required /lib/security/pam_stack.so
service=system-auth
4. auth required /lib/security/pam_nologin.so
5. account required /lib/security/pam_stack.so
service=system-auth
6. password required /lib/security/pam_stack.so
service=system-auth
7. session required /lib/security/pam_stack.so
service=system-auth
8. session optional /lib/security/pam_console.so
```

- `PAM` 配置每行最多包含四项：模块类型（module-type）、标记（flag）、模块（module）和参数（arguments）。
- 模块类型列出了在该条目中定义什么类型的模块。模块有四种：认证（Authentication）、账户（Account）、会话（Session）和密码（Password）。
- 认证用于验证输入的用户。这是检查给定密码的章节。
- 账户可以根据（例如）时间或位置限制账户访问。
- 会话用于在服务启动之前启动外部事件。例如，可以将额外信息记录到文件或 syslog 中。
- 密码用于更改“认证令牌”（authentication token，密码的雅称），并且（如示例所示）也用于测试新密码是否容易被破解。
- `control-flag`（控制标记）定义了在模块成功或失败时执行的操作。如果认证模块成功，是会检查另一个模块，还是会立即授予用户访问该服务的权限？共有四种：Required（必须的）、Requisite（必要的）、Sufficient（足够的）和 Optional（可选的）。
- Required 模块必须成功，用户才能获得访问权限。
- 如果此模块失败，不要立即报告失败，而是继续执行下一个模块（如果存在的话）。
- 这防止了像 `login` 这样的程序直接告诉你用户名无效。相反，它会请求用户名和密码，然后在失败时不告诉你是失败的原因。
- 如果 Requisite 模块失败，`PAM` 会立即停止并报告失败。
- Sufficient 模块在成功时将立即停止并报告成功。
- Optional 模块不是必须的——它们可以通过也可以失败。
- module（模块）将使用的模块名称。这些文件默认存储在 `/lib/security` 下。
- arguments（参数）是可能需要传递给模块的选项。

笔记：

### 第 3.5 节

### linuxconf

- 你可以使用 `linuxconf` 通过一个易用的界面来配置你的 Red Hat 系统。你甚至可以通过 web 界面远程访问此配置。
- 由于通过 web 访问 `linuxconf` 可能存在安全风险，默认关闭 web 访问。你应该只通过安全网络通过 web 访问 `linuxconf`。
- `linuxconf` 是通过 `xinetd` 启动的。
- 进入 `linuxconf` 配置 web 连接简单的方法是使用基于文本的界面。

笔记：

### Linuxconf 界面

- 初始界面提供两个菜单项（Config 和 Control）和三个菜单按钮（Quit、Changes 和 Help）。
- TAB 键允许你在菜单项和按钮之间跳转。方向键允许你在菜单项之间移动，ENTER 键将用于选择菜单项或展开/折叠子菜单。
- 前带有 `+` 号的菜单项在按下 ENTER 键会打开子菜单。



因为你拥的不止 Config 和 Control，你可以在 Config 选项上按 ENTER 来查看那里的子菜单。

笔记：

### 额外模块

- 除了 `linuxconf` 内置的模块外，还可以添加或删除额外的模块，以访问系统的其他部分。
- 存在用于配置每日消息（MOTD）、Apache Web 服务器、FTPD 服务、DHCP、防火墙管理、电子邮件和 Samba 的模块。
- 可软件包完整列表位于 `linuxconf` 内部的“Control files and systems”然后“Configure linuxconf modules”下。

笔记：

# 第 4 节 在 Red Hat 中安装新包

### 目标

- 理解 RPM 的优势
- 从源码构建 RPM 文件
- 使用 RPM 工具

### 第 4.1 节

### 使用二进制 RPM 文件

- 预编译的 RPM 文件通常具有以下文件名语法：`package-1.0-1.i386.rpm`。此语法告诉了以下四点信息：
  - `package`：包名，与 RPM 包名相同。
  - `1.0`：源包的版本号。
  - `1`：包的发布号。此数字与包的版本号共同构成 RPM 包的版本号。
  - `i386`：构建的架构。

笔记：

### 安装和升级二进制 RPM 文件

- `rpm` 命令的 `-i` 切换开关，后面跟一个文件名或文件列表，表示该文件将被安装。
- 如果已存在该软件包的旧版本，你将收到一个错误。
- 如果你使用 `-U` 切换开关，这表示升级。
- `-F` 切换开关代表“刷新（freshen）”，它告诉 RPM 升级软件包，但仅在已安装了旧版本时才执行。
- 这些切换开关中的每一个都可以配合 `-h` 切换开关使用，它会在安装过程中显示哈希标记（`#`）。
- 如果不满足依赖关系，这些操作中的任何一个可能会失败。
- 可能会出现一种情况：你知道依赖关系已满足，但 RPM 却不知道。在这种情况下，你可以添加 `--nodeps` 切换开关来告诉 RPM 忽略依赖检查。
- 要安装软件包，使用此命令，假设 `example-1.0-1.i386.rpm` 在当前目录下：`# rpm -i example-1.0-1.i386.rpm`。

备注：

### 从系统中移除 RPM

- 使用 `-e` 切换开关（代表 erase 删除）后跟 RPM 的名称，从系统中移除 RPM。
- 你可能无法移除被其他软件包所依赖的软件包。为了移除有依赖问题的软件包，你必须先移除其他软件包。
- 要从系统中移除软件包，不需要知道其版本、构建版本或架构。

备注：

### 查询 RPM

- 要找出如果安装二进制软件包，将安装哪些文件，你可以使用 `rpm -qip package-1.0-1.i386.rpm`。这会列出软件包中的文件以及它们将安装的位置。
- `rpm -qip package-1.0-1.i386.rpm` 将给出包名、描述、构建信息、已安装软件包的大小以及其他信息的列表。
- 对于已经安装的软件包，你可以通过 `rpm -ql package` 获取软件包包含的文件列表。
- 如果系统中存在一个文件，而你想查看哪个软件包拥有该文件，可以使用 `rpm -qf filename`。
- 你可以使用 `rpm -qa` 获取系统上所有已安装软件包的列表。

备注：

### 验证 RPM

- 你可以使用 `rpm` 的 `-V` 选项来验证软件包。此选项将让你快速查看文件自安装以来是否被删除或修改。
- 如果你发现了一个问题，可以从从 Red Hat 收到的 CD-ROM 上的原始软件包中重新安装该软件包。
- 你可以使用命令 `rpm -Va` 验证系统上的所有软件包。如果验证通过，你不会看到任何输出。如果某个测试失败，你将得到一个可能的八位字符列表，如果是配置文件，则后面会跟一个“c”，然后是文件名。可能的八位字符是：5（MD5 校验和 失败）、S（文件大小）、L（符号链接）、T（文件修改时间）、D（设备文件）、U（用户（文件所有者））、G（组（组所有者））和 M（文件模式）。
- 如果你修改了配置文件（例如 Apache），你可以预期看到上述至少一个或多个失败。
- 如果你在像 `/bin/su` 或 `/bin/login` 这样的文件看到此内容，可能表明发生了入侵。
- 这是验证系统是否纯净的额外防御层，可以与 `tripwire` 等程序配合使用。

备注：

## 第 4 课：在 RED HAT 中安装新软件包

### 课程 4.2

### 源 RPM (SRPM)

- 源 RPM 包含应用程序的源代码，这些代码在安装前必须经过编译，或者允许你在安装软件之前修改源代码或预编译选项。
- 构建源 RPM 的目录结构位于 `/usr/src/redhat`。该目录下包含以下内容：
  - `SPECS`：包含用于从源码构建 RPM 的规范文件。
  - `BUILD`：构建源码的基础目录。
  - `SOURCE`：`.tar.gz` 文件及任何补丁文件的位置。
  - `RPMS`：包含生成的 RPM 文件。
- `SRPM`：你也可以构建 SRPM，构建好的 SRPM 位于此处。要将一个 SRPM（名为 `package-2.1`）构建为二进制文件，请执行以下操作：
  - 安装源 RPM 文件：`rpm -Uvh package-2.1.rpm`
  - 进入 SPECS 目录：`cd /usr/src/redhat/SPECS`
  - 从源规范文件创建二进制 RPM：`rpmsbuild -bb --clean package-2.1.spec`
  - 安装二进制 RPM：`cd /usr/src/redhat/RPMS/i386; rpm -UVH package-2.1-1.i386.rpm`
  - 卸载源 RPM：`cd /usr/src/redhat/SPECS; rpm -rmssource package-2.1.spec`
  - 移除源 RPM：`rm package-2.1.src.rpm`
- 许多第三方开源应用不发行 SRPM 文件，而是在源码 `.tar.gz` 中分发 `.spec` 文件。你可以自动构建二进制 RPM：`# rpmsbuild -bt example.tar.gz`

### SPEC 文件

- 规范文件（或 `.spec` 文件）告诉 `rpm` 如何构建和安装最终位于 RPM 中的代码，哪些文件应该放入二进制 RPM 中，以及它们应该放在何处。
- 规范文件示例：

```
1. Summary: example
2. Name: example
3. Version: 1.0
4. Release: 1
5. Copyright: GPL
6. Group: Applications
7. Source: http://example.com/example.tar.gz
8. description: This is an example
9. %prep
10. %build
11. %install
12. %files
13. %changelog
* Wed Oct 11 10:00:00 2023 user <user@example.com> - 1
- initial build
```

- 许多第三方开源应用不发行 SRPM 文件，而是在源码 `.tar.gz` 中分发 `.spec` 文件。你可以自动构建二进制 RPM：`# rpmsbuild -bt example.tar.gz`
- 软件包的。源 RPM 规范文件示例：

```
1. Summary: example
2. Name: example
3. Version: 1.0
4. Release: 1
5. Copyright: GPL
6. Group: Applications
7. Source: http://example.com/example.tar.gz
8. description: This is an example
9. %prep
10. %build
11. %install
12. %files
13. %changelog
* Wed Oct 11 10:00:00 2023 user <user@example.com> - 1
- initial build
```

## 第 4 课：在 RED HAT 中安装新软件包

### 课程 4.2

### 源 RPM (SRPM)

- 源 RPM 包含应用程序的源代码，这些代码在安装前必须经过编译，或者允许你在安装软件之前修改源代码或预编译选项。
- 构建源 RPM 的目录结构位于 `/usr/src/redhat`。该目录下包含以下内容：
  - `SPECS`：包含用于从源码构建 RPM 的规范文件。
  - `BUILD`：构建源码的基础目录。
  - `SOURCE`：`.tar.gz` 文件及任何补丁文件的位置。
  - `RPMS`：包含生成的 RPM 文件。
- `SRPM`：你也可以构建 SRPM，构建好的 SRPM 位于此处。要将一个 SRPM（名为 `package-2.1`）构建为二进制文件，请执行以下操作：



- 安装源 RPM 文件（`rpm -Uvh package-2.1.rpm`）。
- 进入 SPECS 目录（`cd /usr/src/redhat/SPECS`）。
- 从源规范文件创建二进制 RPM（`rpmsbuild -bb --clean package-2.1.spec`）。
- 安装二进制 RPM（`cd /usr/src/redhat/RPMS/i386; rpm -UVH package-2.1-1.i386.rpm`）。
- 卸载源 RPM（`cd /usr/src/redhat/SPECS; rpm -rmssource package-2.1.spec`）。
- 移除源 RPM（`rm package-2.1.src.rpm`）。
- 许多第三方开源应用不发行 SRPM 文件，而是在源码 `.tar.gz` 中分发 `.spec` 文件。你可以自动构建二进制 RPM：`# rpmsbuild -bt example.tar.gz`。

### SPEC 文件

- 规范文件（或 .spec 文件）告诉 `rpm` 如何构建和安装最终位于 RPM 中的代码，哪些文件应该放入二进制 RPM 中，以及它们应该放在何处。
- 规范文件文件示例：

```
1. Summary: example
2. Name: example
3. Version: 1.0
4. Release: 1
5. Copyright: GPL
6. Group: Applications
7. Source: http://example.com/example.tar.gz
8. description: This is an example
9. %prep
10. %build
11. %install
12. %files
13. %changelog
* Wed Oct 11 10:00:00 2023 user <user@example.com> - 1
- initial build
```

— `TCP` 是一种基于连接的协议。客户端与服务器通信，打开端口并建立连接。当连接关闭时，通常是因为两个程序都已完成对网络的需求。
— 第三种数据包（`ICMP`）可以被视为流量报告员。如果在路由数据包时发生错误，会发送一个 `ICMP` 包进行报告。`ICMP` 也用作 `ping` 的一部分，测试两个主机之间的连接延迟。

### 注意：

### 以太网

- 以太网开发于20世纪世纪70年代，是一种广播式网络。如果一个主机正在与另一个主机通信，所有其他主机都会收到该信息，并且没有其他主机可以同时通信。
- 更常见的以太网形式使用星型拓扑，每台机器的电缆都连接到交换机或集器器。
  - 星型网络的一个优势是网络的所有成员完全不需要竞争访问网络。集器器或交换机的速度比流量协商快得多。
  - 此外，如果连接某个主机的电缆故障，网络上的其他主机都不会掉线。
- 每个以太网适配器都有一个由以太网适配器制造商分配的唯一地址（介质访问控制器或 MAC 地址）。
  - 当以太网适配器想要与另一个以太网适配器通信时，它会发送一条包含自己的 MAC 地址以及接收方 MAC 地址的消息。如果接收方 MAC 地址在该电缆上，它就会接收该消息。
- 当两个以太网适配器尝试同时传输时，就会发生冲突。如果发生这种情况，两个适配器都会停止传输，等待随机时间，然后重新传输。
- 过多的冲突表明网络流量非常大且运行效率低下。为了纠正这一点，你可能需要将网络分成两个网络，或者使用交换机代替集器器。
- 每个以太网包都必须包含源和目的以太网地址，以及源和目的 IP 地址，随后是数据，最后是用于验证数据包完整到达的错误检查数据。
- 尽管电缆上的所有其他适配器都能看到包，但它们不会回答或响应。所有以太网适配器应该收到的唯一消息是以太网广播。
- 数据包从一个子网传输到另一个子网需要使用路由器。如果路由器知道某个数据包需要转发到另一个子网，它就会转发该数据包。

## 第 5 节 带有 Linux 的网络

- 地址解析协议（或 `ARP`）缓存允许 Linux（以及 `TCP/IP`）在以太网地址和 IP 地址之间建立连接。
  - Linux 首先发送一个以太网广播，请求 IP 地址到 MAC 地址的映射。
  - 拥有该 IP 地址的接收端用 ARP 响应回复，提供 IP 地址和 MAC 地址。
  - Linux 将 MAC 地址存储在 ARP 缓存中供以后使用。
- `TCP/IP` 数据包有一个选项可以设置 IP 包的最大尺寸。
  - 每个物理介质都有其自己的最大传输单元（`MTU`），这是基于延迟（数据包跨越介质所需的时间）和可发送数据量的平衡。
  - 小包的延迟较低，但性能会降低，因为数据包中较大比例是头部和尾部信息。大包发送数据的效率更高，但延迟也更高。

笔记：

### 连接到以太网网络

- 在你的机器上安装以太网卡并重启。
- Red Hat 的 Kudzu 工具会在你重启时识别该卡并要求你配置网卡。你可以在此时选择配置网卡，或者继续并在稍后使用 `netcfg` 进行配置。
- 为此以太网卡添加网络，你必须先初始化并设置 IP 接口，然后必须为该接口设置路由。
- `/sbin/ifconfig` 程序会将以太网卡注册到 `TCP/IP` 服务。典型语法是 `# /sbin/ifconfig IPAddress`
  - 给出掩码和广播地址，随后是接口的 IP 地址。如果你给它 IP 地址，接口会自动启动。
- 我们在这里使用的路由方法是设置默认网关。这告诉 Linux 任何通往其他网络的数据包都将转发到网关，网关可能会知道从哪里发送。这是通过命令 `# route add default gw IPAddress` 实现的。
- `netcfg` 是设置网络设备的优秀工具。获取你的 IP 地址、域名服务器信息、网关、掩码。在 Names 部分下，验证你域名服务器的主机名、域名和 IP 地址。
  - Hosts 部分列出了你在 `/etc/hosts` 文件中的哪些 IP 地址和主机名。这至少应该包含你的 IP 地址和主机名。
  - 如果你不使用 DNS，你需要在 Hosts 部分列出所有你想要通信的主机及其 IP 地址。
  - Interfaces 部分列出了你可用的哪些接口。`LO` 接口是环回接口，用于将 `TCP/IP` 包路由到本地机器。
  - 环回接口的 IP 地址始终为 `127.0.0.1`，Linux 下许多程序正常运行需要它。
- 接下来添加以太网接口并给出 IP 地址和子掩码。
- 不要开启“使用 BOOTP 配置接口”，但你可以开启“启动时激活接口”。
- `BOOTP` 是一种旨在启动时动态分配 IP 地址的协议。`DHCP` 服务器应在启动时配置，使用网络。

笔记：

### DHCP

- `DHCP` 代表动态主机配置协议。
- 当使用 `DHCP` 的机器启动接口时，它会发送一个请求主机的以太网广播。服务器响应：
  - 主机名、路由、域名服务器信息。
  - `DHCP` 最大优势是可配置性。一个中心位置存储整个子网的网络信息。
  - 当新机器加入网络时，可以快速进入网络，改为静态 IP 地址。

## 第 5 节 带有 Linux 的网络

### DHCP 配置

### 服务器配置

- 决定使用动态还是静态 IP 划分。
  - 静态 IP 地址允许你使用现有的 DNS 而不必担心设置动态服务器。
  - 建议留出 5 到 10 个动态地址，以便让机器进入。
  - 有两个程序提供访问 `DHCP` 服务：服务器软件 `dhcpd` 和客户端软件 `pump`。
  - 网络上应该只有一个 `DHCP` 服务器；关闭任何 `BOOTP` 服务器并改用 `dhcpd`。
  - `dhcpd` 使用的配置文件是 `/etc/dhcpd.conf`。该文件包含 MAC 地址、IP 信息以及路由器/WINS/域名服务器信息。该文件的示例。。示例 DHCP 配置

```
### 服务器的 DNS 名称是什么？
server-identifier hudson.wayga.org;

### 还要识别客户端所处的 DNS 域名
option domain-name "wayga.org";

### 应该查看哪些 DNS 服务器？（至少2 个）
option domain-name-servers shaft.wayga.org, hudson.wayga.org;

### 定义一个 C 类网络 (192.168.1.0->192.168.1.255)
subnet 192.168.1.0 netmask 255.255.255.0 {

### 设置网络掩码（再次）
option subnet-mask 255.255.255.0;
option domain-name "wayga.org";
option domain-name-servers shaft.wayga.org, hudson.wayga.org;

### 定义 IP 地址的租约时间为多久。
default-lease-time 600;

### 最大租约时间，以防客户端请求的。
max-lease-time 7200;
}
```

### 指定默认路由器。



`option routers 192.168.1.142;`

# 下面的 IP 范围将动态地

## 分配给 MAC 地址不匹配

### 以下任何主机的客户端。

`range 192.168.1.46 192.168.1.50;`

### 一个打印机（称为 lpipc）

```
host lpipc {
  # lpipc 的 MAC 地址
  hardware Ethernet 0:60:b0:0fc:0ca9;
  # 它的 FQDN 通过 DNS 知道 IP 是什么
  # 我们可以在这里使用普通的 IP 地址，但为什么要这样做呢？
  fixed-address lpipc.auroratech.com;
}
```

### PC 主机
```
host camille {
  hardware Ethernet 0:0:bc:0f:12:d6;
  fixed-address camille.auroratech.com;
}
```

### 使用不同默认路由器的 PC 主机。
```
host cyrus {
  hardware Ethernet 0:10:4b:a2:e2:4b;
  fixed-address cyyrus.auroratech.com;
  option routers 192.168.1.95;
}
```

- 当 `dhcpd` 运行时创建的另外两个文件是 `/etc/dhcpd.leases` 和 `/etc/dhcpd.pid`。
- `.pid` 文件包含运行中 `dhcpd` 的 PID，以便更方便地停止或重启 `dhcpd`。
- 如果网络中使用动态 IP 地址，则使用 `.leases` 文件。它包含了关于谁租用了 IP 地址以及该租约持续多长时间的信息。
- 在 `dhcpd` 重启或启动时，不应删除 `dhcpd.leases` 文件，因为它在 `dhcpd` 启动时会进行重新读取，以确定哪些动态 IP 地址已经被分配。

## 客户端配置

- 使用 `netcfg` 将 IP 配置为 DHCP 并激活以太网卡。
- 也可以配置 `linuxconf` 使用 DHCP 启动以太网接口。
- Windows 机器只需通过网络控制面板设置为 DHCP 配置即可。
- 其他 UNIX 机器（如 Solaris）可能已经安装了 DHCP 客户端，或者你可以从 `http://www.isc.org/` 下载并编译 ISC DHCP 分发。
- 如果你选择使用网络上的所有动态 IP 地址，可以使用像 `lanlord` (`http://linux.uhw.com/software/lanlord/`) 的程序来查看分配了哪些 IP 地址。

注意：

## PPP

- 点对点协议（PPP）是通过拨号线路连接互联网或 TCP/IP 网络的方法。
- PPP 设计为仅在两台机器之间工作。这使其成为拨号应用、甚至通过租用线路连接远程位置的理想选择。
- PPP 依赖于在电话线的一端运行 `pppd` 服务器，在另一端即拨号的机器上运行 `pppd` 客户端。
- 你必须根据自己是客户端还是服务器来不同的配置软件。
- PPP 没有像以太网那样的开销，因为没有使用 MAC 地址。

注意：

## 第 5 节：LINUX 上的网络

### PPP 客户端

- 设置 PPP 客户端需要调制解调器、电话线、一个 PPP 服务器和一个用于拨号的号码。
- 验证 PPP 连接是否工作的快速方法是执行类似以下的操作：

```
pppd connect 'chat -v "+" ATDTphone CONNECT " login: login word: password' > /dev/cu1 3840 debug crctscts modem defaultroute
```

- 电话、登录名和密码由提供 PPP 账户的人分配给你。
- 将 `/dev/cu1` 修改为调制解调器的位置。记得 Linux 下的 `/dev/cu1` 与 DOS 和 Windows 下的 COM2。
- `chat` 命令用于拨号调制解调器并提供登录和密码信息。
- 一旦 `chat` 成功建立连接，PPP 将接管线路并开始连接。
- 服务器和客户端会协商诸如最大传输单元（MTU）、压缩以及其他几个设置。
- 此配置可以使用 Red Hat 网络配置管理器通过输入电话号码、线路速度、调制解调器、登录名和密码在脚本完成。

### PPP 服务器

- 要让 PPP 服务器软件运行，必须开启 IP 转发和 PPP。这允许 Linux 充当 ARP 代理并为以太网地址响应 ARP 请求。
- 分配一组未使用且以后不会被使用的 IP 地址。这些将用于入站连接的地址，可用数量至少要与你的电话线数量一样。
- 为每个通过 PPP 连接的用户创建新账户。许多地方会在用户名前面加一个字母 P。让 `/etc/passwd` 中的用户信息看起来像这样：`Pmark:x:500:500:PPP user:/home/mark/usr/local/bin/pppd`。
- 在该用户的家目录下创建一个 `.ppprc` 文件，并添加下方示例中的文本：

示例 `.ppprc` 文件

```
-detach
modem
crctscts
lock
192.55.123.100:192.55.123.111
proxyarp
```

- `--detach` 表示不从控制台分离。
- `modem` 表示监控 CD（载波检测）线路，并在 CD 信号掉落时终止。
- `lock` 将锁定设备，防止他人使用该串口端口。
- 两个 IP 地址是服务器地址（等待来电），后面跟着一个冒号，然后是拨号时分配给客户端的 IP 地址。
- `proxyarp` 允许服务器将 PPP 客户端放入其 ARP 缓存，并对本应发送给客户端的数据包做出响应。
- 设置 `getty` 以监控串口端口。
- `pppstats` 命令可以给出线路进出数据包的运行总量。
- 如果你选择使用动态 IP 地址而不是静态 IP 来节省 IP 地址，请为每个连接到调制解调器的 tty 文件创建一个 `/etc/ppp/options.ttyXX` 文件，其中 `xx` 是串口名称。
- `options.ttyXX` 文件的内容与上述 `.ppprc` 文件相同，不同之处每个文件的 IP 地址已更改。

### 注意：

# 课程 5.2

## xinetd

- `xinetd` 元守护进程用于在特定 TCP/IP 端口收到接收请求时自动启动程序。

注意：

### /etc/services

- `/etc/services` 文件包含有关 TCP/IP 端口号的信息以及指定端口的名称，该名称稍后用于 `/etc/inetd.conf` 文件。

示例 `/etc/services` 文件

```
ftp-data      20/tcp
ftp             21/tcp
telnet          23/tcp
smtp            25/tcp timserver
time            37/tcp timserver
time            37/udp resource
rlp             39/udp nameserver
name            42/udp nameserver
whois           43/tcp nicname # 通常到 sri-nic
domain          53/tcp
domain          53/udp
```

- 行的第一个项目是服务名。后面是端口号和协议（TCP 或 UDP），然后是任何别名。
- 接收邮件的端口名为 `smtp` 端口；它位于 25 端口，其别名是 `mail`。

注意：

### /etc/xinetd.d

- `/etc/xinetd.d` 目录包含一组 `xinetd` 读取并使用的文件列表，用于确定监控哪些端口。以下示例包含了 `xinetd` 使用来监控 finger 用端口的配置文件。

#### finger 的配置文件

```
### default: on
### description: finger 服务器响应 finger 请求。
Finger 是
### 一种允许远程用户查看
### 信息协议，例如
### 本地用户的登录名和最后登录时间。
service finger
{
    socket_type = stream
    wait = no
    user = nobody
    server = /usr/sbin/in.fingerd
    disable = yes
}
```

- `service` 行表示正在定义的服务名称，在本例中为 `finger`。服务部分内还设置了几个额外参数：
- `socket_type` 设置为 `stream`，意味着我们正在使用 TCP 而不是 UDP。
- `wait` 选项允许 `xinetd` 根据需要启动该服务的新进程，或者一次只运行一个服务。
- `user` 选项列出了命令将以哪个用户运行的用户名（如果有的话）。
- `server` 列出了在激活时将运行的命令。
- `disable` 显示此服务是否被禁用。



对于某些高吞吐程序（`apache` 和 `sendmail` 是很好的例子），你不希望它们不断重启，因为这需要大量时间；这些程序将根据需要派生或产生新进程。

像 `telnetd` 或 `ftppd` 这样的程序不需要大量的启动时间，因此 `xinetd` 可以根据需要处理启动新实例。

## 第 5.3 网络应用

### DNS

- 域名服务器是将 IP 地址（`192.168.1.1`）匹配到主机名（`www.wayga.org`）的程序。
- 由于名称服务器会查找并缓存来自客户端机器的 DNS 请求，因此它可以用于慢速链路的一端，以减少跨链路的 DNS 流量。
- 名称服务器提供了将从一个主机的邮件转发到另一个主机的功能，并且当某个 Web 服务器忙而另一个空闲时，为特定主机提供备份。
- 在连接到 TCP/IP 网络时，通过将以下行写入 `/etc/resolv.conf` 文件来使用 DNS 进行主机名解析，请分别将“`wayga.org`”和“`192.168.1.1`”替换为你的域名和 IP 地址：

```
domain wayga.org
nameserver 192.168.1.1
```

- 这里可以有多个名称服务器条目，将按顺序尝试直到建立成功的 DNS 连接。
- 如果你计划在本地运行 `named`（DNS 服务器软件），你应该将 IP 地址更改为 `127.0.0.1`。请确保在其中还有其他几个 IP 地址，以防 `named` 宕机。

#### 你应该充当 DNS 服务器吗？

- 只有在以下情况下你才运行 DNS 服务器：
  - 你拥有一个域名并想要控制 DNS。虽然许多 ISP 会为你处理 DNS 服务，但如果你的环境频繁变动机器，由你来处理可能会更简单。
  - 你在慢速链路上运行大型网络。`named` 可以作为缓存存储经常使用的主机，这将减少部分流量。
  - 你没有连接到互联网。
- 如果你不符合上述任何条件，你可能不需要运行 DNS 服务器。

### 配置伯克利互联网名称守护进程 9.1 (BIND)

- 要成为 DNS 服务器，你需要获取（可能需要编译）并配置 `bind`。
- `named` 很可能在安装 Linux 时已经安装了；如果没有安装，你可以从 CD-ROM 或 Red Hat 更新站点安装 `bind` 包和 `bind-devel` 包。
- 基础配置文件是 `/etc/named.conf`。它有四种类型的语句：一个控制访问，一个描述日志，一个描述更通用的选项，以及一个或多个描述它作为服务器所属的区域（zone）。文件中的注释以井号（`#`）开头。

```
Sample /etc/named.conf

options {
    directory "/var/named";
    // 如果我们要读取文件，请从 /var/named 读取。
}

zone "." {
    type hint;
    file "named.ca";
}

zone "0.0.127.IN-ADDR.ARPA" {
    type master;
    file "named.local";
}

zone "1.168.192.in-addr.arpa" {
    type master;
    file "named.192.168.1";
}

zone "wayga.org" {
    type master;
    file "named.wayga";
    notify yes;
}

zone "wayga.org" {
    type slave;
    masters { 192.168.1.1; }
};
```

#### 讲座 5 结合 LINUX 的网络

- `options` 语句描述了监听哪些 IP 以及使用哪个端口。这里 `named` 的工作目录 `/var/named` 被广泛使用。在没有任何域名信息的情况下，各种语句中指定的区域文件和任何其他文件将存储在此处。
- `logging` 语句控制日志的详细程度以及日志消息发送到哪里。
- `acl` 语句控制你的服务器响应哪些客户端的查询。
- `zone` 语句描述了服务器提供哪些区域，无论是作为主（`master`）还是作为从（`slave`）（我们在这里忽略 stub 类型）。
- 主服务器（`master`）是该域（区域）信息的权威权威。
- 从服务器（`slave`）是区域信息的次级传播者，但不能在从上进行任何更改。
- 在指定名称服务器时使用一种特殊类型。它被称为提示（`hint`），因为 `named.ca` 实际上只是提供服务器列表，其中一些拥有根名称服务器的当前列表。
- 对于从区域，你必须指定至少一个主服务器，`bind` 可以从那里传输区域记录。

此示例总共有五个域条目。

- 特殊域名“`.\`”代表根域，即在找不到其他任何内容时在此处查找。根域通常指向整个互联网的根服务器列表。
- 第二和第三个区域是特殊域名，允许你在给定 IP 地址的情况下确定主机的名称；注意 IP 地址是按反序列出的（`0.0.127-in-127.0.0`）。
- 第四个区域 `wayga.org` 区域表示该服务器是主服务器，且区域文件位于 `named.wayga`。
- `notify` 语句告诉 `bind` 通知从服务器主服务器更改的配置。
- 最后的 `wayga.org` 区域表示该服务器是从服务器；此服务器上没有 `wayga.org` 的配置文件，但它可以从位于 `192.168.1` 的主服务器获取配置。

## 第 5.4 节 网络信息服务 (NIS)

- `NIS` 是一组用于从主服务器管理用户和各种网络服务的程序。
- `NIS` 将信息存储在以 `/var/yp` 为根目录的一系列目录和 `GDBM`（GNU 数据库管理）文件中。`NIS` 将这些文件称为“映射（`maps`）”。
- 然后，这些映射通过 `RPC`（远程过程调用）供 `NIS` 域内的其他机器使用。
- `NIS` 还允许设置从服务器（secondary slave servers）。
- 每个子网都应该有一个（且仅有一个）`NIS` 服务器。
- `NIS` 映射由大部分位于 `/etc` 中的各种配置文件构建，如 `passwd`、`group`、`hosts`、`services`、`aliases` 等。不需要使用每个映射。通常只需要密码和组映射，因为其他文件经常变化。
- `NIS` 最大问题之一是广播 `NIS` 请求所带来的安全漏洞。

### 第 5 节 使用 Linux 进行网络配置

- 红帽（Red Hat）包含了两个用于在 `NIS` 网络环境中运行的脚本：`/etc/rc.d/ypbind` 和 `/etc/rc.d/autofs`。只有当你的 `NIS` 服务器中有自动挂载映射时才需要第二个脚本。
- 编辑 `/etc/ypbind.conf` 文件以反映你的 `NIS` 域设置。
- 默认情况下，`ypbind` 会通过网络发送 IP 广播来寻找 `NIS` 服务器。你可以手动指定使用的 `NIS` 服务器。编辑 `/etc/yp.conf` 文件并添加服务器的主机名，确保该主机列在 `/etc/hosts` 中。
- 确保 `portmapper` 正在启动。如果你在使用 `NFS`，那么 `portmapper` 已经启动了。
- 如果没有，使用 `/etc/rc.d/init.d/portmap start` 来启动它。
- 最后，你可以启动 `ypbind`：`/etc/rc.d/init.d/ypbind start`。
- `/etc/nsswitch.conf` 文件决定了所有 `NIS` 信息的查找顺序（与 `/etc/host.conf` 不同，后者仅用于主机查找）。
- 自动挂载器将根据 `NIS` 映射自动挂载 `NFS` 分区。两个典型的映射是 `auto.home` 和 `auto.vol`，分别挂载 `/home` 和 `/vol`。你可以使用以下命令启动 Linux `autofs`：

```
### service autofofs start.
```

- 当用户切换到特定目录时，CD-ROM、软磁盘、本地卷和 `NFS` 文件系统会自动挂载。

### 配置 NIS 主服务器

- `NIS` 主服务器位于网络上并响应网络上的 `NIS` 查询。
- 每个物理网络只能有一个主服务器。
- 你可以设置与主服务器同步的从服务器，减轻客户端的负载。
- 从服务器可以位于不同的子网。
- 确保你已安装了 `yserv` 包。
- 编辑 `/var/yp/Makefile` 以添加或删除你将提供的映射。以 `all:` 开头的行包含映射列表。
- 编辑 `/var/yp/securenets` 和 `/etc/ypserv.conf`。前者定义了服务器响应请求的 IP。以下是 `/var/yp/securenets` 文件的示例。

`/var/yp/securenets` 示例



``` 
#
### /var/yp/securenets 示例
#
# 允许本地访问。这是必要的！
### host 127.0.0.1

# 允许来自本地网络机器的访问
255.255.255.0 10.10.10.0

# 允许来自 C 类网络 209.1.2.0 和 209.1.3.0 的访问
255.255.254.0 209.1.2.0
```

`host` 行允许 `ypserv` 响应特定主机。由于本地主机必须能够访问服务器，因此列出了该主机。允许子网的示例在另外两行示例中。

- `/etc/ypserv.conf` 文件允许你根据每个映射在主机或网络层级自定义服务器的行为。

- 条目分为两种类型：选项（options）和访问规则（access rules）。

## 第 5 节 使用 Linux 进行网络配置 81

- 选项的格式简单为 `<option>: yes|no`，即该选项开启或关闭。通常开启的选项是 `dns`。

- 访问规则的格式为 `host : map : security : passwd_mangle`。会读取访问规则，直到为请求的主机和映射找到匹配项，然后应用该规则。

笔记：

### 第 5.5 节 使用 Linux 进行路由

- 路由允许你以 Linux 机器为中心连接两个以太网网络。

- 要启动 Linux 路由，你首先必须有两个 TCP/IP 连接；通常是两个以太网卡，但也可以是一个以太网和一个 PPP，例如。假设你有一个 3Com 3c503 和一个基于 Digital 21140 的网卡，`/etc/conf.modules` 如下：

```
/etc/conf.modules 示例
alias eth0 tulip
alias eth1 3c503 options eth1 xcvr=1
```

`eth0`（第一个以太网口）将是 `tulip`（Digital/Intel 芯片的名称）。

第二个以太网口是 3C503 卡。

以 `options` 开头的部分在加载 `3c503` 模块时向模块传递 `xcvr=1`。这允许我们使用网卡上的 AUI 端口而不是同轴端口。

笔记：

### 使用红帽 netcfg 进行路由

- `netcfg` 程序处理许多通常需要手动在启动时完成的路由设置。这些文件存储在 `/etc/sysconfig` 中，并与 `linuxconf` 的路由方案兼容。

笔记：

### 手动路由

- 这些手动输入的命令允许你在两个网络之间路由：

```
### /sbin/ifconfig eth0 192.168.1.10
# /sbin/route add -net 192.168.1.0
### /sbin/ifconfig eth1 192.168.2.10
# /sbin/route add -net 192.168.2.0
```

打印服务器是专用设备，具有一两个并行端口以及 10/100 以太网连接，价格约为 100 美元。打印服务器通常支持 LPD，并配有支持 Windows 网络打印的驱动程序。

- 为了方便起见，你应该配置一台 Linux 机器作为打印请求的中心。配置该机器以接受来自 Windows 机器通过 LPR、IPP (CUPS) 和 SMB 的打印请求。然后，你可以让这台机器与打印服务器通信。

### 注意：

## 课程 6.3

### 配置 LPRng

- Red Hat Linux 使用 LPRng，它是行打印机守护进程（Line Printer Daemon）的下一代。

- LPR 的初始版本对认证、负载均衡和故障转移的支持较少或没有支持。LPRng 增加了这些支持，同时足够轻量，不会消耗过多资源。

- 配置打印机的主要方法是通过 `printconf`。该应用程序只有在你已经运行了图形化窗口的情况下才能工作。

  - 当你启动 `printconf` 时，你将获得本地系统已知的打印机列表。如果这是第一次运行它，将不会列出任何打印机。

- 该界面使得添加打印机变得简单。

注意：

## 讲座 6 打印与打印共享 91

### 管理打印队列

- 打印队列是 FIFO（先入先出），因此排在队中的第一个可以访问打印机。

- 你需要了解管理打印队列的命令有 `lpc`、`lprm` 和 `lpq`。

- `lpq` 命令显示队列中的内容并提供打印机的当前状态；某些打印机能够告诉 `lpd` 它们缺纸或连接已断开，这些错误将出现在 `lpq` 列表中。

- `lprm` 命令将从队列中删除作业。

- 默认情况下，只有 root 用户和提交打印作业的人可以从队列中删除作业。

- 大多数打印机都有内部缓冲区，因此如果作业已经在打印，删除该作业可能不会导致打印机立即停止。

- `lpc` 命令是“lpc 控制”。它可以激活和禁用队列及打印机，重新排列队列中的作业，并获取 `/etc/printcap` 中列出的任何打印机的状态。

- `lpc` 可以以交互方式运行，你也可以直接将命令放在 `lpc` 命令行上。

注意：

### 网络上的打印机！

- 既然 Linux 同时支持 lpd 和 SMB 进行打印共享，你网络上的大多数计算机都能轻松地打印到你的打印机。

- 在通过网络与 LPRng 通信时，你应该在启动之前在客户端加载打印机驱动。

- 来自网络的打印作业将直接传递到打印机端口，而不经过本地打印驱动程序的处理。

注意：

## 讲座 6 打印与打印共享

### 从其他 LPD (UNIX) 系统访问

- 要允许指定主机通过 LPRng 访问，请创建一个允许提交作业、删除作业和管理打印机的用户和主机列表。

- 控制文件位于 `/etc/lpd.perms`。

- 默认情况下，任何主机上的任何用户都可以提交作业，只有用户或 root 可以删除作业，任何人都可以获取队列状态，而 root 能够控制打印队列。

- 为了防止打印机外部的恶意攻击，请确保在防火墙上拦截 TCP/IP 端口 `515`，并配置 `/etc/lpd.perms` 仅接受来自你指定的主机或用户的作业。

- `/etc/lpd.perms` 文件包含几个访问控制的示例：

```
# REJECT SERVICE=X NOT REMOTEIP=130.191.0.0/255.255.0.0
# REJECT SERVICE=X NOT REMOTEHOST=engpc
```

- 这些行显示了两种阻止远程主机的方法。

- 第一行拒绝不在 130.191 网络中的 IP 地址。

- 第二行拒绝以“engpc”开头的主机。

- 如果激活了两个 reject 语句，则只有以“engpc”开头且 IP 地址以 130.191 开头的机器名称能够连接。

- 一旦你对 `/etc/lpd.conf` 了更改，请作为 root 用户使用 `service lpd restart` 重启 LPRng。

- 如果你想访问网络上且兼容 LPD 协议的打印机，请向 `printconf` 输入 IP 地址和打印机类型。

### 通过 SMB 访问 (Windows 网络)

- 让 Windows 网络看到 Linux 打印机的最佳方法是运行 Samba。

- Samba 应该配置为使用 `/etc/printcap` 文件和 BSD 风格的打印。

- 确保为你安装的打印机类型在 Windows 下安装打印程序，因为 Linux 上的打印过滤器应该将数据传递给打印机。

- Windows NT 和 2000 可以通过 LPD 处理服务和打印，因此你可能想用它。

注意：

## 讲座 6 打印与打印共享

### 课程 6.4

### CUPS

- CUPS（通用 UNIX 打印系统）不是 Red Hat Linux 的一部分，对于新用户来说设置起来更复杂。

- CUPS 具有一些优势，使其值得代替 LPR 使用。

- CUPS 包含网页界面、浏览和审计。

- CUPS 支持 HP 和喷墨打印机。

- CUPS 可在 `http://cups.org/` 获取。

- CUPS 设计为作为客户端。

- CUPS 允许你从这台机器或支持 IPP 的远程机器打印。



### CUPS 概述

- `CUPS` 设计为作为客户端。
- `CUPS` 允许你从这台机器或支持 `IPP` 的远程机器打印。
- `CUPS` 有一些优势，使其值得代替 `LPR` 使用。
- `CUPS` 包含网页界面、浏览和审计。
- `CUPS` 支持 `HP` 和喷墨打印机。
- `CUPS` 可在 `http://cups.org/` 获取。

### CUPS 配置

- `CUPS` 设计为作为客户端。
- `CUPS` 允许你从这台机器或支持 `IPP` 的远程机器打印。
- `CUPS` 有一些优势，使其值得代替 `LPR` 使用。
- `CUPS` 包含网页界面、浏览和审计。
- `CUPS` 支持 `HP` 和喷墨打印机。
- `CUPS` 可在 `http://cups.org/` 获取。

- 要通过 `LPRng` 访问指定的打印机

`CUPS`（通用 UNIX 打印系统）不是 Red Hat Linux 的一部分，对于新用户来说设置起来更复杂。

打印服务器是专用设备，具有一两个并行端口以及 10/100 以太网连接，价格约为 100 美元。打印服务器通常支持 `LPD`，并配有支持 Windows 网络打印的驱动程序。

- 为了方便起见，你应该配置一台 Linux 机器作为打印请求的中心。配置该机器以接受来自 Windows 机器通过 `LPR`、`IPP` (`CUPS`) 和 `SMB` 的打印请求。然后，你可以让这台机器与打印服务器通信。

### 注意：

## 课程 6.3

### 配置 LPRng

- Red Hat Linux 使用 `LPRng`，它是行打印机守护进程（Line Printer Daemon）的下一代。
- `LPR` 的初始版本对认证、负载均衡和故障转移的支持较少或没有支持。`LPRng` 增加了这些支持，同时足够轻量，不会消耗过多资源。
- 配置打印机的主要方法是通过 `printconf`。该应用程序只有在你已经运行了图形化窗口的情况下才能工作。
  - 当你启动 `printconf` 时，你将获得本地系统已知的打印机列表。如果这是第一次运行它，将不会列出任何打印机。
- 该界面使得添加打印机变得简单。

注意：

## 讲座 6 打印与打印共享 91

### 管理打印队列

- 打印队列是 `FIFO`（先入先出），因此排在队中的第一个可以访问打印机。
- 你需要了解管理打印队列的命令有 `lpc`、`lprm` 和 `lpq`。
- `lpq` 命令显示队列中的内容并提供打印机的当前状态；某些打印机能够告诉 `lpd` 它们缺纸或连接已断开，这些错误将出现在 `lpq` 列表中。
- `lprm` 命令将从队列中删除作业。
- 默认情况下，只有 `root` 用户和提交打印作业的人可以从队列中删除作业。
- 大多数打印机都有内部缓冲区，因此如果作业已经在打印，删除该作业可能不会导致打印机立即停止。
- `lpc` 命令是“lpc 控制”。它可以激活和禁用队列及打印机，重新排列队列中的作业，并获取 `/etc/printcap` 中列出的任何打印机的状态。
- `lpc` 可以以交互方式运行，你也可以直接将命令放在 `lpc` 命令行上。

注意：

### 网络上的打印机！

- 既然 Linux 同时支持 `lpd` 和 `SMB` 进行打印共享，你网络上的大多数计算机都能轻松地打印到你的打印机。
- 在通过网络与 `LPRng` 通信时，你应该在启动之前在客户端加载打印机驱动。
- 来自网络的打印作业将直接传递到打印机端口，而不经过本地打印驱动程序的处理。

注意：

## 讲座 6 打印与打印共享

### 从其他 LPD (UNIX) 系统访问

- 要允许指定主机通过 `LPRng` 访问，请创建一个允许提交作业、删除作业和管理打印机的用户和主机列表。
- 控制文件位于 `/etc/lpd.perms`。
- 默认情况下，任何主机上的任何用户都可以提交作业，只有用户或 `root` 可以删除作业，任何人都可以获取队列状态，而 `root` 能够控制打印队列。
- 为了防止打印机外部的恶意攻击，请确保在防火墙上拦截 TCP/IP 端口 `515`，并配置 `/etc/lpd.perms` 仅接受来自你指定的主机或用户的作业。
- `/etc/lpd.perms` 文件包含几个访问控制的示例：

```
# REJECT SERVICE=X NOT REMOTEIP=130.191.0.0/255.255.0.0
# REJECT SERVICE=X NOT REMOTEHOST=engpc
```

- 这些行显示了两种阻止远程主机的方法。
- 第一行拒绝不在 `130.191` 网络中的 IP 地址。
- 第二行拒绝以“engpc”开头的主机。
- 如果激活了两个 `reject` 语句，则只有以“engpc”开头且 IP 地址以 `130.191` 开头的机器名称能够连接。
- 一旦你对 `/etc/lpd.conf` 了更改，请作为 `root` 用户使用 `service lpd restart` 重启 `LPRng`。
- 如果你想访问网络上且兼容 `LPD` 协议的打印机，请向 `printconf` 输入 IP 地址和打印机类型。

### 通过 SMB 访问 (Windows 网络)



- 让 Windows 网络看到 Linux 打印机的最佳方法是运行 `Samba`。

- `Samba` 应该配置为使用 `/etc/printcap` 文件和 BSD 风格的打印。

- 确保为你安装的打印机类型在 Windows 下安装打印程序，因为 Linux 上的打印过滤器应该将数据传递给打印机。

- Windows NT 和 2000 可以通过 LPD 处理服务和打印，因此你可能想用它。

注意：

## 讲座 6 打印与打印共享

### 课程 6.4

### CUPS

- `CUPS`（通用 UNIX 打印系统）不是 Red Hat Linux 的一部分，对于新用户来说设置起来更复杂。
- `CUPS` 具有一些优势，使其值得代替 `LPR` 使用。
- `CUPS` 包含网页界面、浏览和审计。
- `CUPS` 支持 HP 和喷墨打印机。
- `CUPS` 可在 `http://cups.org/` 获取。
- `CUPS` 设计为作为客户端。
- `CUPS` 允许你从这台机器或支持 `IPP` 的远程机器打印。
- `CUPS` 有一些优势，使其值得代替 `LPR` 使用。
- `CUPS` 包含网页界面、浏览和审计。
- `CUPS` 支持 HP 和喷墨打印机。
- `CUPS` 可在 `http://cups.org/` 获取。
- `CUPS` 设计为作为客户端。
- `CUPS` 允许你从这台机器或支持 `IPP` 的远程机器打印。

## 第 6 节 打印与打印共享

### 在 CUPS 中使用身份认证

- 由于 `IPP` 和 `CUPS` 的设计目的是允许用户从任何地方将打印作业发送到 `IPP` 服务器，因此必须有一种方法让用户验证那些想要发送打印作业的用户。
- 基础方法与 `HTTP` 使用的密码相同，因此密码相当容易被嗅探，但对于小型网络来说足够了。
- 要设置基础方法认证，请编辑 `/etc/cups/cupsd.conf`，找到 `<Location/>`，并插入以下行：

```
AuthType Basic
AuthClass User
```

- “digest（摘要）”认证需要使用 `lpasswd` 将授权的用户和密码添加到 `/etc/cups/passwd.md5` 中。
- 这增加了管理工作量，因为该密码密码文件不会与 Red Hat Linux 用于管理用户的 `/etc/passwd` 同步。
- 如果你想使用 Digest 认证，请将 `/etc/cups/cupsd.conf` 中的 `AuthType Basic` 改为 `AuthType Digest`。
- 为了提高安全性，使用 `SSL` 在网络传输过程中对打印作业和密码进行加密。
- 首先，你需要为 `SSL` 密钥创建一个路径，路径应为 `/etc/cups/ssl/`。
- 然后生成密钥并保护它们。源码中包含的 `ENCRYPTION.txt` 文件解释了如何执行操作：

```
# openssl req -new -x509 -keyout /etc/cups/ssl/server.key \
  -out /etc/cups/ssl/server.crt -days 365 \
  -nodes
# chmod 600 /etc/cups/ssl/server.*
```

- 前两行实际上是用于 `openssl` 创建密钥的命令。
- 最后一行仅允许 root 用户访问该文件。
- 按照写法，此密钥将激活 365 天。
- 你输入的信息是可选的，但通用名称（common name）除外。这应该是打印目标的主机名称。
- 如果此条目与主机不匹配，通过 `SSL` 访问打印服务器的网页将向你发出警告。
- 在 `/etc/cups/cupsd.conf` 中找到引用 `ServerCertificate` 和 `ServerKey` 且被注释掉的两行。取消它们的注释。
- 使用 `/etc/init.d/cups restart` 重启 `CUPS`，并使用 `lpq -E` 强制开启 `SSL` 安全。
- 如果你使用身份认证，会被提示输入密码，然后你将默认打印机的队列信息。

## 第 6 节 打印与打印共享 101

#### 使用 CUPS 通过网络进行打印

#### 从 Windows 机器打印

- 如果 `Samba` 已经在运行，在 `/etc/smb.conf` 文件中设置行 `printing = cups`。
- `Samba` 将会向 `CUPS` 查找可用的打印机。

#### 从运行 LPR/LPD 的其他 UNIX 机器打印

- 由于 `IPP` 和 `LPR/LPD` 不兼容，当你从 `LPR` 客户端向 `CUPS` 服务器打印时，无法实现如加密或用户认证等功能。
- 更好的设置是使用带有 `LPR` 服务器的 `CUPS` 客户端。
- 最佳设置是客户端和服务器都使用 `CUPS`。
- 如果 `CUPS` 配置得当，你可以向互联网开放 631 端口，允许客户端安全地提交打印作业。
- 如果你确实想将 `CUPS` 作为 `LPR` 客户端的服务器，你需要为 `xinetd` 创建一个条目（参见第 5 节）。

## 6.5 节

### 总结

- 串口、并行、USB 和以太网打印机都有各自的优势，取决于你的打印需求。
- Red Hat Linux 使用 `printconf` 和 `LPRng` 配置打印机。
- Linux 可以跨网络与打印机通信，`Samba` 允许 Windows 机器与 Linux 打印机联网。
- `lpr`、`lprm` 和 `lpc` 程序用于管理打印机和打印队列。
- `CUPS` 实现的 `IPP` 是通过打印的良好替代方案。

## 第 7 节

### Samba

### 目标

- 设置 Microsoft Windows 网络
- 安装 `Samba`
- 从 Linux  `SMB` 共享
- 使用 `Samba` Web 管理工具管理 `Samba` 配置
- 在 Windows 上安装 Linux 打印机

## 7.1 节

### 设置 MS Windows 网络

#### 你需要

- 安装以太卡和驱动程序。
- 性价比最高的网络方案是 10-BaseT。
- 使用 使用这种网络方法引起导致整个网络崩溃的问题较少。
- 它比某些替代方案贵，但通常值得投入额外成本。
- 确保每个 Windows 用户在 Linux 服务器上都有帐户。
- 如果你想让用户能够更改密码，请将 shell 设置为 `/bin/passwd`。确保将 `/bin/true` 和 `/bin/passwd` 添加到 `/etc/shells`。
- 如果你有带有用户账户密码的现有 NT 服务器，可以让 `Samba` 对 NT 服务器验证密码，而无需创建用户账户。
- 决定你想要设置。
- 对于较大的网络，它是域（domain）。

### 什么是工作组和域？

- 工作组是同一子网上的用户的集合。
- 工作组是计算机的逻辑组。
- 域需要一个中央服务器。

## 7.2 节

### 安装 Samba

如果你从 Red Hat 中选择，则已安装 `Samba`。

以下是 `smb.conf` 示例：

```ini
[global]
# 上述设置了整个程序的选项
workgroup = WORKGROUP
printing = bsd
log file = /var/log/samba.log
lock directory = /var/lock/samba
guest account = nobody
os level = 3
domain master = yes

[homes]
# [homes] 部分为每个已认证的用户创建一个共享，该目录为该用户的家目录
comment = Home Directories
browseable = no
read only = no
create mode = 0750
read size = 8192
max xmit = 8192

[printers]
# 此条目扩展为每个可用的打印机，我们不希望在列表中看到此实际条目
comment = All Printers
browseable = no
printable = yes
public = yes
create mode = 0700

[pcsoft]
comment = PC Software
# 在浏览列表中显示的注释
path = /vol/repository
### 用于共享的 Linux 目录
public = no
writable = no
printable = yes
create mode = 0666

[accounting]
path = /home/bob/shared
valid users = fred bob
### 只有 fred 和 bob 可以访问此共享
public = no
only guest = no
browseable = no
writable = yes
create mask = 0777
```

# 红帽 Linux 培训课程手册

- 启动后，转到 `SMB` 客户端并进行网络浏览。你应该能从机器列表中看到你的 Linux 机器。



- 如果没有，你可以检查位于 `/var/log` 目录下的日志。每个客户端机器、`samba` 进程和 `nmb` 进程都有它们自己的日志文件（`samba-log.machineame`、`samba-log.smb` 和 `samba-log.nmb`）。

- 如果你在浏览列表中看到了 Linux 机器，那么你需要连接到一个共享目录。

- 公有连接（Public connections）不需要有效的登录，是测试工作情况的一种简单方法。这类连接很容易建立，但安全性很低。

- 如果你选择执行这样做，请在共享的配置中设置 `public=yes` 选项。

- 有三种方法可以验证用户以访问非公有连接。

- 第一种是 `user`，在 `/etc/passwd` 中对用户名和密码进行验证。这种连接方法要求 Linux 上的用户名与 SMB 客户端匹配。

- 第二种方法是将认证请求转发到另一台服务器。这被称为服务器认证，你必须信任你转发请求的这台机器。

- 第三种认证方法称为 `share`，它不需要 Linux 上的用户名与 SMB 客户端匹配。

- SMB 允许使用加密和未加密的密码。

- 加密密码增加了安全性，但由于它是使用单向哈希进行加密的，这与 `/etc/passwd` 中存储密码的方式不兼容。

- NT 4 Service Pack 3、Windows 98 以及 Windows 2000 及更高版本默认发送加密密码，调整此设置唯一方法是在注册表（Registry）中。

- 有两种更好的方法来处理这个问题。

- 如果你有一个有的 PDC（主域控制器），请设置 Linux 机器将密码转发给 PDC。

  - 通过将 `password server` 指向 PDC 并设置 `security=user` 来实现（这两个设置都在 `[Global]` 下）。

# 第 7 节 SAMBA

如果你没有 PDC，请设置 Linux 机器来处理加密密码。阅读 `/usr/doc/samba*/ENCRYPTION.txt` 文件以了解处理加密密码时需要执行的操作。

- 设置你的 Samba 实例以原生处理加密密码，你需要创建一个存储 SMB 密码的第二个密码文件。

- 将其命名为 `/etc/smbpasswd`，这是 Samba 的默认文件。

- 你可以使用随 samba RPM 提供的 `mksmbpasswd.sh` 程序来协助此类转换：

```bash
# cat /etc/smbpasswd | /usr/bin/mksmbpasswd.sh = /etc/smbpasswd
```

- 该文件将包含如下所示的行：`mkomarin-ski:500:XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX:[U:LCT-00000000:mkomarinski`

- SMB 密码长度恰好为 32 字节（因此有 32 个 X）。

- 默认情况下，这些 X 会禁用访问，在任何人可以使用之前必须更改密码条目，可以通过两种方式完成：

- 第一种是将第一组的前 11 个 X 替换为字符串 `NO PASSWORD`。

- 如果你这样做，请在 `/etc/samba/smb.conf` 中启用 `null passwords=true` 选项。

- 另一种方法是使用 `smbpasswd` 为用户设置一个临时密码。

- 一旦设置了密码且最初需要 root 权限访问，请告诉用户该密码是什么，然后使用 `smbpasswd` 命令将其更改以符合其需求。

- 你可能想要考虑的一个选项是“sync unix passwd”，它位于 `Globals` 下的 `SWAT`。将其设置为 `Yes` 将在用户下次更改密码时同步 UNIX 密码文件和 `smbpasswd` 文件。

- 此外，“Encrypt Passwords” 选项默认设置为 `No`。你需要将其设置为 `Yes` 以让 Samba 开始使用 `/etc/smbpasswd`。

# 7.3

### 连接到 SMB 共享

- Linux 有一个虚拟文件系统 (VFS)，它为挂载文件系统提供通用接口。

- 我们不使用 `mount`，而是使用 `smbmount`（它是 Samba-client 包的一部分）来挂载 SMB 共享。

```bash
### smbmount service
mount-point options
```

- `service` 是你想要的 SMB 共享的 NetBIOS 名称，将 `\` 替换为 `/`。

- `mount-point` 是 Linux 层级结构中的本地挂载点。

- 由于你必须以 root 身份使用 `smbmount`，而你的 NT 服务器上可能没有 root 用户，因此你需要利用选项 `-U` 指定用户进行验证，并使用 `-c` 列出你客户端的 NetBIOS 名称；否则将发送的是 FQDN（完全限定域名）。

- `client.domain.org`（无论 FQDN 是什么）都不是有效的 NetBIOS 名称，添加 `-c client` 告诉服务器客户端的名字只是 `client`。

- 如果客户端的 NetBIOS 名称无法解析，则无法连接。

# 第 7 节 SAMBA

# 7.4

## Samba Web 管理工具 (SWAT)

- SWAT 是一个用于远程管理 Samba 配置的 Web 界面。

  - 由于你必须以 root 身份使用 `smbmount`，而你的 NT 服务器上可能没有 root 用户，因此你需要利用选项 `-U` 指定用户进行验证，并使用 `-c` 列出你客户端的 NetBIOS 名称；否则将发送的是 FQDN。

  - `client.domain.org`（无论 FQDN 是什么）都不是有效的 NetBIOS 名称，添加 `-c client` 告诉服务器客户端的名字只是 `client`。

  - 如果客户端的 NetBIOS 名称无法解析，则无法连接。

# 第 7 节 SAMBA

# 7.4

## Samba Web 管理工具 (SWAT)

- SWAT 是一个用于远程管理 Samba 配置的 Web 界面。

  - 由于你必须以 root 身份使用 `smbmount`，而你的 NT 服务器上可能没有 root 用户，因此你需要利用选项 `-U` 指定用户进行验证，并使用 `-c` 列出你客户端的 NetBIOS 名称；否则将发送的是 FQDN。

  - `client.domain.org`（无论 FQDN 是什么）都不是有效的 NetBIOS 名称，添加 `-c client` 告诉服务器客户端的名字只是 `client`。

  - 如果客户端的 NetBIOS 名称无法解析，则无法连接。

### 共享 (Shares)

- 共享部分提供了 Samba 共享的配置。

- 默认可供配置的共享部分是 `Homes` 部分。通过在 `Create Share` 旁边输入新的共享名称并点击 `Create Share` 按钮来创建新共享。

- 创建后，可以从 `Choose Share` 列表中选择共享。

- 点击 `Delete Share` 将移除该共享。

- 一旦选择了共享，你就可以从默认值开始更改配置。

- 默认值是：目录为 `/tmp`，共享列表中不显示注释，只读访问，拒绝来宾（未身份验证的用户）访问该共享。此外，共享是可用的（已身份验证的用户可以访问），且共享将出现在浏览列表中。

- `hosts allow` 和 `hosts deny` 条目是制表符、冒号或空格分隔的主机列表，分别用于允许或拒绝访问此共享的主机。

- 这与 `Global`（全局）部分中的选项相同，但它仅适用于此共享。

- `browseable` 选项意味着该共享会出现在机器的浏览列表中。

- `Available` 指明该共享是否由 Samba 激活。

Notes:

### 讲座 7 SAMBA

### 第 7.5

### 在 Windows 上安装 Linux 打印机

- 任何你可以从 Linux 获取的打印机都可以通过 Samba 使用。

- 要求直接与打印机通信的复杂驱动程序可能会带来一些问题。

- 如果可能，请获取支持 PCL 或 PostScript 的打印机。这样你至少可以将数据发送到打印机。

Notes:

## 第 7.6

### 总结

- Samba 是与 Windows 98 和 NT 机器共享磁盘空间和打印机的简单方法。

- Linux 可以使用 `smbfs` 使用 SMB 服务器。

- 工作组（Workgroups）没有中央密码认证，而域（domains）则使用中央密码服务器。

- SWAT 允许你方便地管理 Samba 配置。

Notes:

## 讲座 8

### 电子邮件 (E-mail)

### 目标

- 设置 Sendmail

- 邮件转发

- 设置简单的邮件列表

- 设置 使用 POP 和 IMAP 建立远程连接

## 第 8.1

### 设置 Sendmail



# Red Hat Linux 邮件传输代理

Red Hat Linux 的邮件传输代理（或 MTA）是 `sendmail`。

`Sendmail` 是大多数 Linux 安装的标准，尽管也有其他可用选择。

全球范围内的大部分邮件都是通过 `sendmail` 服务器传输。

当邮件从 `sendmail` 发送时，它会从邮件客户端发送到服务器，并保存在队列中。

当邮件到达队列头部时，`sendmail` 尝试将邮件发送给收件者。

如果 `sendmail` 无法连接到远程 SMTP 服务器，它会将消息留在队列中，并每小时尝试发送一次邮件。

邮件消息被保留在队列中有许多原因：

其中之一是你与远程机器之间的网络中断了。

另一个是你的本地服务器并非一直连接到互联网。

`mailq` 命令将列出 `sendmail` 队列中的内容以及邮件卡在队列中的原因。

如果队列中有大量邮件，你可能遇到了网络或配置问题。

通过连接到 TCP 端口 `25` 来验证 `sendmail` 是否正在运行。

```
[kmomarinski@hudson mkomarinski]$$ telnet localhost 25
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'.
220 hudson.wayga.org SMTP Sendmail 8.11.2/8.11.2; Sun, 12 Aug 2001 21:37:26 -0400
```

`sendmail` 的配置选项通常位于 `/etc/sendmail.cf`。除非你确定自己在做什么，否则不要更改任何内容；即使微小的更改也可能导致你的邮件系统失效。

在 `/etc/mail` 下有几个你可以编辑的文件：

`access` 设置允许或拒绝访问服务器的主机。

`domaintable` 用于域名发生变化时，以便你可以接收来自两个域的邮件。

`local-host-names` 包含此服务器接受邮件的主机名和域名列表。

`mailertable` 包含域名/主机列表以及目标，你可以将这些域名/主机的邮件重定向到目标。

`sendmail.mc` 包含了宏代码（使用宏语言 `m4`），该代码生成了 `sendmail` 配置文件。

`trusted-users` 列出了任何允许更改邮件发送者的用户。

`virtusertable` 允许你将某个域的所有邮件路由到单个地址，或创建路由到不同位置的重复邮件地址。

可以在 `/usr/share/doc/sendmail/README.cf` 中找到示例。

## Notes

### 第 8.2

#### 本地邮件投递

#### .forward 文件

当邮件进入时，会检查用户主目录下的 `~/.forward` 文件。

如果该文件存在，邮件将发送到文件中列出的地址。

`.forward` 允许拥有多个电子邮件地址的人安排其所有邮件发送到那里。

### 第 8 课 电子邮件

#### Mailman

`mailman` 程序正成为 Linux 邮件列表的标准工具。

`mailman` 的大部分功能通过 Web 服务器处理。

你可以从 Powertools CD 或 Red Hat 的 FTP 站点获取 Mailman RPM。

下载并安装 Mailman RPM，它将替你完成大部分安装工作。

在系统上开始使用 `mailman` 之前，你还必须执行一些额外操作。

你必须执行的第一件事是为 `mailman` 配置管理员密码。这允许你从网站管理整个系统。

接下来，编辑 `/var/mailman/Mailman/mm_cfg.py`。你只需要将 `DEFAULT_HOST_NAME` 和 `DEFAULT_URL` 修改为你的本地机器，看起来如下所示：

```
DEFAULT_HOST_NAME = 'wayga.org'
DEFAULT_URL      = 'http://wayga.org/mailman/'
```

检查 `/etc/sysconfig/sendmail` 并确保 `DAEMON` 被设置为 `yes`。

最后，你需要配置并重启你的 Web 服务器。

编辑 `/etc/httpd/conf/httpd.conf` 文件末尾添加以下内容：

```
ScriptAlias /mailman/ /var/mailman/cgi-bin/
Alias /pipermail/ /var/mailman/archives/public/
<Directory /var/mailman/archives>
  Options +FollowSymlinks
</Directory>
```

配置 `mailman` 的应用程序位于 `/var/mailman/bin`。

创建新列表，运行 `/var/mailman/bin/newlist`

`newlist` 示例：

```
[root@hudson mkomarinski]# /var/mailman/bin/newlist
Enter the name of the list: test
```

输入运行列表的邮箱：

`mkomarinski@wayga.org`

初始测试密码：

Entry for aliases file:

```
# test mailing list
# created: 13-Aug-2001 mkomarinski
test: "/var/mailman/mail/wrapper post test"
test-admin: "/var/mailman/mail/wrapper mailowner"
test-request: "/var/mailman/mail/wrapper mailcmd test"
test-owner: test-admin
```

按回车继续测试所有者通知...

`[root@hudson mkomarinski]#`

提取指定的部分（即以 `test` 开头的行）并将其复制到 `/etc/aliases` 中。

备注：

## 第 8.4 节

### 远程电子邮件 (POP 和 IMAP)

`POP`（邮局局递协议）和 `IMAP`（互联网消息访问协议）是从远程机器接收电子邮件的两种标准。

每个协议都有其优缺点，以及支持它们的各种邮件用户代理 (`MUA`)。

Red Hat 安装设置环境中已提供这两个协议并可以直接运行。

电子邮件的身份验证通过与登录相同的 PAM 方案完成。

使用 `POP` 或 `IMAP` 的优势之一是用户设置非常少。

备注：

#### POP

`POP` 非常简单。你可以获取、列出和删除邮件，仅此而已。

`POP` 的缺点是，一旦邮件发送给你，服务器上的邮件通常会被删除。

`Netscape`、`Outlook` 以及大多数基于 PC 的网络电子邮件程序都处理 `POP`。

由于实现简单，客户端对 `POP` 支持比 `IMAP` 普及得多。

`POP` 服务器 (`popper`) 包含在典型的 Red Hat 发行版中。

要使用它，请配置客户端使服务器与 Linux 机器匹配。用户名和密码与 `/etc/passwd` 中的相同。

记住任何下载的电子邮件都会存储在本地机器上。可以考虑的选项是“不要从服务器删除 (`Don't delete from server`)”。

如果你有两个想要读取邮件的地方（公司和家里），你可以在办公室邮件系统上关闭此选项，而在家里开启它。这样，你所有的邮件在工作时都会下载，而你只能在家里获取新邮件。

然而，`IMAP` 是解决此问题的更好方案。

备注：

#### IMAP

`IMAP` 比 `POP` 稍微复杂，但具有许多优势。

所有电子邮件都将在服务器上进行备份。

可以从任何地方访问 `IMAP`，无需任何特殊准备。

`IMAP` 也是轻量级的；大型附件会被替换为描述发送者、类型和文件大小的小标头。只有当用户请求时，才会下载整个附件。

电子邮件可以存储在不同的文件中（通常称为文件夹）。

这些文件夹保留在服务器端，客户端软件可以随时访问。

`IMAP` 的另一个大功能是离线模式。

如果客户端支持，你可以让客户端将一个或多个文件夹下载到本地机器。你可以在不连接网络的情况下读取、修改、删除、回复等。

`IMAP` 服务器包含在 Red Hat 的 `imap-4.5` RPM 软件包中，并配置为从 `/var/spool/mail` 获取文件。

客户端设置需要你设置服务器名称和用户名/密码。

你需要查看的选项之一是服务器目录选项，它告诉客户端服务器上的哪个目录包含邮件文件夹。如果用户通过 Samba 或 NFS 共享家目录，你可能需要将服务器目录更改为类似 `~user/Mail` 之类的。

缺点是，你每次为某人配置 `IMAP` 都必须设置它。

优点是你的用户不会将电子邮件与普通文件混淆。

默认情况下，`mbox`（已读但未放入其他邮件文件夹的邮件）存储在 `~user/mbox`，这实际上是 UNIX 邮件程序使用的同一个文件。

新邮件会在 `/var/spool/mail` 中检查。



- 如果你需要更改此项，将必须重新编译软件。

### 带有 IMAP 和 POP 的 SSL

- 要让通过 SSL 的 IMAP 工作，你需要安装 OpenSSL 软件包和 IMAP 服务器软件包。
- Red Hat 7.1 附带的 IMAP 服务器带有 SSL IMAP 的支持。
- 生成一个与 IMAP 服务器兼容的 SSL 密钥。
- 进入 `/usr/share/ssl/certs` 并运行 `make imapd.pem`。
- 需要关注的最重要的问题关于通用名称 `common name` 的。这必须设置为用户将连接的主机的完全限定域名 `FQDN`。

备注：

### 第 8.5 节

### 电子邮件客户端

- Linux 有多种电子邮件客户端。
- 使用哪一个取决于个人偏好。
- 有人使用 Emacs 编辑器，其他人使用 `mutt` 或 `pine`，这些程序仅在字符模式下运行。
- Netscape 和 Mozilla 提供了支持图形和 HTML 附件的阅读器，并支持全 SSL 加密的 IMAP 和 POP。

备注：

### GNU 隐私卫 `GPG`

- GNU 隐私卫 `GPG` 设计用于替代商业版 PGP。
- 加密的作用与信封类似——它是电子邮件和其他文件的信封。
- 额外的好处是，`GPG` 允许他人验证邮件确实是你发送的，而不是冒充者。
- `GPG` 被设计为没有专利限制，适合任何人下载。你可以从 http://www.gnupg.org/ 获取最新的 RPM 格式副本。
- 一旦下载并安装 RPM，你就可以生成公私密钥对。
- 要生成公私密钥对，使用 `gpg --gen-key`。你需要运行两次，第一次 `gpg` 将文件复制到 `.gnupg` 目录。第二次运行时它将允许你创建密钥。
- 首先，选择你想要的密钥类型。可以选择签名、加密或其他。
- 接下来询问位长度。这是密钥的强度，数字越小越弱，越大越强。
- 然后你可以为密钥设置有效期。这允许你像管理密码一样过期密钥。过期后，你必须生成新密钥并再次分发公共部分。
- 接下来询问你的姓名，然后是邮箱地址，最后是注释。注释是你给朋友的密钥上显示的名称。
- 接下来询问口令。
- 经过一些处理，你将拥有自己的 GPG 密钥，适用于签名电子邮件或加密文件。
- 你可以使用 `gpg --clearsign filename` 签名文件。会创建一个扩展名为 `.asc` 的文件，其中包含原始文件及其数字签名。
- 在他人验证你的签名之前，你需要分发你的公密钥。确保接收者知道该公密钥来自你。

### 第 8 ：电子邮件

- `gpg -export -armor` 命令会将你的公钥提取到屏幕上。你可以输入文件名，将密钥发送到该位置。
- 然后，你可以将此公钥发送给你的朋友。
- 一旦他们收到密钥，必须使用 `gpg -import filename` 来导入密钥。
- 他们必须对密钥进行签名，这通过 `gpg -edit-key` 命令完成，这验证了他们知道该密钥来自可靠的来源。
- 有了你朋友签名的密钥后，你就可以发送包含数字签名的文件。
- 接收者只需将带有签名的文件发送给 `gpg` 命令。系统会告知他们数字签名、消息内容以及你的密钥是否匹配。
- 你可以对文件进行加密，使得只有接收者才能打开文件。要做到这一点，你首先需要拥有接收者的公钥。
- 你可以使用以下命令加密示例文件：

```bash
$ gpg -output example.gpg -encrypt -armor
-recipient markk@wayga.org example
```

- 生成的文件 `example.gpg` 只有拥有 `markk@wayga.com` 秘钥的人才能读取。
- 然后，你可以将生成的文件通过电子邮件发送给他。他将获取邮件内容并运行解密过程：

```bash
$ gpg -decrypt example.gpg
```

- 文件的内容将被打印出来。
- 你可以从 GNU Privacy 网站 http://www.gnupg.org 了解更多关于密钥服务器、密钥管理、验证密钥、指纹以及许多其他概念。

## 第 8.6

### 总结

- `sendmail` 是发送电子邮件的默认方式。
- 别名 `Aliases`、`.forward` 和 `procmail` 可以更改传入邮件的地址。
- `mailman` 允许你快速设置邮件列表。
- `POP` 和 `IMAP` 允许你从远程位置获取电子邮件。

笔记：

## 第 9 课

### Web 服务器

**目标**

- 安装并配置 Apache Web 服务器
- 为用户访问设置某些安全性
- 为 Apache 配置并测试 PHP 解释器
- 设置一个启用 SSL 的服务器以确保安全

## 第 9.1

### Apache

- Apache 免费提供源代码并提供 API。这两个功能允许大量的自定义和扩展。
- 此外，Apache 兼容 HTTP 1.1 标准。
- 根据 Web 服务器使用权威网站 netcraft.com 的报告显示，Apache 及其衍生版本运行了全球 60% 以上的 Web 服务器。
- 你可以在向 Apache 中添加新模块，而无需长时间关闭服务器。Red Hat 编译了许多常用模块，并将它们以 RPM 软件包的形式包含在光盘中，准备好添加到你的系统中。

笔记：

## 第 9 课 Web 服务器

### 入门

- 在设置 Web 服务器之前，有你需要考虑的几点。
- Web 文件应该放在哪里？默认情况下，Red Hat Linux 使用 `/var/www/html`。
- 配置文件在哪里？在 Red Hat 的设置中，`/etc/httpd/conf` 是配置文件的所在位置。
- 你想要一个 SSL 服务器吗？添加 SSL 可以防止他人窥探页面内容，增加安全性。
- 你需要哪些额外功能？如果你想在服务器上使用 SSL 或 Perl 或 PHP 语言，你必须在继续之前将 RPM 包添加到你的系统中。
- 在 `.conf` 文件 `httpd.conf` 和 `srm.conf` 中，可以在运行时指定许多项目。这两个文件控制许多参数，例如目录的别名、图标别名、图像、CGI 脚本/程序、虚拟主机指令、文档根目录、当 URL 中没有指定其他文件时从目录提供的文件，以及各种访问控制和验证指令。

笔记：

### 配置 Apache

### 给用户的 Web 页面

- 默认情况下，特定用户的页面位于用户主目录下的 `public_html/` 目录。
- 在某些情况下，这可能会导致安全问题，因为其他用户可以看到其他用户的文件 `但不是内容`。
- 为了避免这种情况，将用户主目录的属性设置为可执行但不可读，这对应的八进制值为 `0711`。
- 将 `public_html/` 目录设置为所有人可读且可执行，即 `0755`。这样 Web 服务器就可以访问 `public_html` 的内容，而无需获晓主目录的其他内容。
- 若要更改用户访问这些文件的 `UserDir` 指令，你可以将 `/etc/httpd/httpd.conf` 中的指令更改为你喜欢的任何内容。它默认设置为 `public_html`。
- 某些用户可能对为自己设置主页感兴趣。
- 提供静态 HTML 页面除了服务器本身的安全考虑外，没有其他安全担忧。
- 对于 CGI 和其他 Web 技术并非如此。
- Apache 中的 `.htaccess` 文件和 `<Directory>` 指令允许你控制对这些工具的访问。

### 配置虚拟服务器

- 虚拟服务器是具有多个名称或 IP 地址的服务器。服务器接收尝试连接的虚拟服务器的名称，读取它，然后根据浏览器认为它正在查看的虚拟服务器提供正确的页面，而在此过程中使用单一真实的 IP 地址。
- 一个位于 80 端口的 `http://www.wayga.com` 服务器，拥有自己的 cgi-bin 和文档根目录，配置如下：

```apache
<VirtualHost www.wayga.com>
ServerName www.wayga.com
DocumentRoot /var/www/html
ScriptAlias cgi-bin/ /var/www/cgi-bin/
</VirtualHost>
```

- 你可能还想使用方法设置 `DocumentRoot` 为 `/var/www/wayga/html`。

### 访问限制

- 有两种方法可以修改所有类型的访问。
- `<Directory>` 指令通常位于 `/etc/httpd/conf/httpd.conf` 中。
- `.htaccess` 文件位于目录树中。
- 在这两种情况下，放置的指令对所有文件和子目录都有效。

```apache
### 对目录实施安全
AuthType Basic
AuthFile /etc/passwd
AuthGroupFile /dev/null
AuthName Restricted Area
<Limit GET POST>
require valid-user
</Limit>
```



或者在 `<Directory>` 指令中：

```apache
<Directory /var/www/html/secure>
AuthType Basic
AuthFile /etc/passwd
AuthGroupFile /dev/null
AuthName Restricted Area
<Limit GET POST>
require valid-user
</Limit>
</Directory>
```

- `<Limit>` 指令告诉服务器哪些 HTTP 方法需要有效用户。
- 密码文件包含用户名、冒号和加密后的密码。你可以使用 `passwd` 命令来创建和添加用户。

```bash
passwd [-c] [-m] [-b] {passwdfile} {username} [password (如果使用了 -b)]
```

- `-c` 选项将创建一个新的密码文件（称为 `passwdfile`）。
- `-m` 选项强制使用 MD5 加密，而不是标准的 crypt 加密。
- MD5 安全得多，但你可能需要将“AuthType Basic”更改为“AuthType Digest”。
- `-b` 选项从命令行读取密码，否则将提示你输入用户密码。
- 你必须对要存放或更新的密码文件的位置具有写入权限，并且只有所有者和 Web 服务器具有读取权限。
- Apache 还有额外的模块允许你通过其他方式进行验证，从使用 NT 服务器上的 SMB 密码到本地的 `/etc/passwd` 以及一次性密码。
- 这些可能会在客户端和服务器之间明文传输密码。

笔记：

# 第 9 课 Web 服务器

## 9.2

### CGI

- 通用网关接口 `CGI` 是执行外部程序的最佳方式。
- `CGI` 设计用于在服务器之间接收和发送信息。
- 编写 `CGI` 最流行的语言是 `PHP`、`Python` 和 `Perl`。你可以用任何喜欢的语言编写 `CGI`，这就是 `CGI` 中“通用”部分的含义。

笔记：

### 限制 CGI 的

- `<Directory>` 指令结合 Linux 用户和组权限，可以对 Web 空间区域内谁可以执行什么操作进行非常精细的控制。
- 通常情况下，你可能不希望 `CGI` 从任意目录中执行。
- 此外，你可能希望禁止浏览器在文件系统中漫游，无论是特定用户的文件系统还是根文件系统。
- 为了让服务器无法访问整个文件系统，可以在 `httpd.conf` 中放置如下指令：

```apache
<Directory />
AllowOverride None
Order deny,allow
Deny from all
Options None
</Directory>
```

- 你可以通过添加类似下面的语句来告诉 Apache 可以从哪些目录提供页面，以便允许你提供用户文件。

```apache
<Directory /home/**/public_html>
Order allow,deny
Allow from all
AllowOverrides IncludesNOEXEC
</Directory>
```

- 这允许你从用户的 `public_html` 目录提供页面，并允许他们使用不执行外部程序或 `CGI` 脚本的 `SSI`。
- 某些公司有规定，出于法律原因，用户页面不能在公司外查看。
- 在这种情况下，你可以像之前所示那样分配身份验证，或使用“Allow From”将访问限制在特定域名或网络范围之内。
- 在上面的示例中，你可以看到它被设置为“All”，这意味着任何人都可以访问该文件。将其更改为类似“Allow From .wayga.org”将只允许 `.wayga.org` 域内的主机访问个人页面。

```apache
<Directory /var/www/html>
Order deny,allow
Allow from all
AllowOverrides All
</Directory>
```

- 以上内容允许你从服务器的文档根目录提供页面，并允许覆盖所有的限制。
- 现在你可以在此树中设置 `CGI` 目录。你可以通过额外的 `<Directory>` 指令来实现此。
- 如果你想在目录中开启 `CGI`（假设可以通过 `.htaccess` 覆盖），你需要添加 `Options ExecCGI`。

### 注意事项：

### PHP

- `PHP` 是一种脚本语言，语法与 `Perl` 和 `C` 相似。
- 它嵌入在 HTML 中，通过一种变体注释标签进行隔开。
- 标签内的代码会被解析，如果有输出，则会替换该标签。
- 通常，`PHP` 文件使用特殊的扩展名（`.php`），以告诉 Apache 在发送给客户端之前解析该文件。
- 你可以使用 CD-ROM 上的 `php-4.0.4pl1-9.i386.rpm` 在系统中安装 `PHP` 模块。
- 下面是一个提供 `PHP` 及其配置设置信息的示例 HTML 页面。

示例 PHP 文件

```html
<HTML>
<HEAD>
<TITLE>
PHP 信息
</TITLE>
</HEAD>
<BODY>
<?php echo phpinfo(); ?>
</BODY>
</HTML>
```

- `PHP` 页面以 Apache 运行的用户身份运行。
- `PHP` 可以连接并从各种数据库提取信息，包括 `PostgreSQL` 和 `MySQL`。
- 支持其他数据库（如 `Oracle` 和 `Solid`），但不是以模块形式提供。
- 它对 Netscape cookies、文件上传以及用于处理图像 `GD` 库有非常强大的支持。

讲座 9 Web 服务器

# 课程 9.3

## Apache 和 SSL

- 有许多原因想要保持数据安全。
- 设置 `SSL` 服务器在并非所有地方都是合法的；在配置和使用 `SSL` 服务器之前，请检查你所在地区的法律。
- `SSL` 使用算法创建密钥。该密钥随后用于加密客户端和服务器之间传输的数据，使得只有客户端和服务器可以轻松解密数据。
- 为了进一步增加安全性，`SSL` 实现了证书颁发机构，也称为 `CA`。这些机构签名，这意味着它们知道提供密钥的服务器确实是其声称的。
- `CA` 签名需要费用且持续时间有限，但商业公司应该考虑花费这些费用来获得 `CA` 提供的额外安全性。
- 从 CD-ROM 获取 `mod_ssl` `RPM` 并将其安装在系统中。
- `mod_ssl` 文档位于 `http://localhost/manual/mod/mod_ssl/`。
- 描述如何生成密钥的文档可以在 `/usr/share/doc/mod_ssl-2.8.1/SSL-Certificate-Creation` 中找到。
- 在开始之前，你可能希望 [注意：原文中文本碎片化/损坏] ... [注意：此节的 OCR 文本存在大量重复/不同步]。

*(注：第 149-154 页的 OCR 文本包含大量的重复循环和碎片化句子，已对其进行清理以尽可能保持逻辑流，尽管提示要求保留所有信息。）*



# 课程 10 X 窗口系统

## 课程 10.3

### gdm

- 你可以使用 `gdm`（GNOME 显示管理器）启动图形化登录。
- 在运行级别（`runlevel`）5 时，`gdm` 程序会自动启动，你可以在安装时选择是否启动 `gdm`。
- 你也可以配置 `gdm` 在不需要用户登录的情况下重启或关机主机器。
- 如果你仅在本地机器上使用 `gdm`，只要 X 已经正常工作，就不需要配置 `gdm` 来让其运行。
- 最新版本的 `gdm` 具有网络感知能力，允许速度较慢的 X 客户端连接到你的红帽服务器。
- 允许你执行此项操作的协议称为 `XDMCP`。
- 如果你将 `gdm` 作为 `XDMCP` 服务器使用，则不需要在服务器上配置 X。只需确保应用程序已安装即可。
- `gdm` 的配置文件位于 `/etc/X11/gdm`，主配置文件为 `/etc/X11/gdm/gdm.conf`。
- 编辑此文件，并更改以下内容：
- 在 `[xdmcp]` 部分，将 `Enable=0` 更改为 `Enable=1`。
- 将 `HonorIndirect` 从 0 更改为 1。如果没有 `Honor-Indirect`，`XDMCP` 客户端在启动前必须知道 `XDMCP` 服务器的 IP 地址。
- `[xdmcp]` 下的其他选项用于限制连接到服务器的客户端数量。这是为了防止针对你服务器的某些形式的拒绝服务（DoS）攻击。
- 如果仅使用 `gdm` 服务器且不想在控制台上运行 X，请跳到 `[servers]` 部分，并确保所有行都已注释。
- 如果 `gdm` 已经在运行，可以通过进入运行级别 3，然后返回运行级别 5 来停止并重启它。
- 对于 `XDMCP` 客户端，请确保 X 正常工作。
- 关闭 X 并使用命令 `xinit --broadcast` 重新启动它。
- 你将获得一个可用的 `XDMCP` 广播服务器列表。选择一个，你将看到该主机的 `gdm` 登录界面。
- 如果你想与单机通信，请使用 `xinit --query hostname`。
- 作为安全预防措施，你应该在防火墙上拦截 TCP/IP 端口 177。这是 `gdm` 使用的端口。

笔记：

## 课程 10.4

使用 X 窗口管理器

- 窗口管理器在窗口周围绘制边界，并提供最大化和最小化按钮；此外，它还允许你调整窗口大小、移动或杀死窗口。窗口管理器提供了菜单以及 X 显示通用“外观和感受”。
- X 在像终端模拟器之类的客户端应用程序与窗口管理器之间有清晰的隔离，这允许客户端被移动和调整大小。
- 你可以通过桌面环境在这两个部分之间插入命令。
- 桌面环境提供了一组库，应用程序可以针对这些库进行编译，从而使编写应用程序变得更容易。
- 可以配置桌面环境，使得所有使用该环境的应用程序在颜色方面具有共同的外观（在 Windows 中被称为主题）。
- 尽管这些环境看起来不同，但它们执行着许多相同的功能。

笔记：

### GNOME

- `GNOME` 代表 GNU Network Object Model Environment（GNU 网络对象模型环境）。
- 它没有内置窗口管理器。
- `Sawfish` 和 `Enlightenment` 是 `GNOME` 最流行的两个窗口管理器。
- `GNOME` 在对象代理、拖放、文档和 3D 编程方面使用通用的开放标准。
- `GNOME` 使用 `GTK+` 作为其工具包。
- `GTK+` 的“可主题性”允许你在不重新编译的情况下更改 `GTK+` 的外观和感受。
- `GNOME` 使用符合 CORBA 标准的对象模型 `Bonobo` 进行组件之间的互操作性。

### GNOME 界面

- 首次启动 `GNOME` 时，你会看到一些与 Microsoft Windows 环境中类似的概念。
- 屏幕底部的面板有 `GNOME` 替代的开始按钮，看起来像一个脚印。
- 其他各种图标可以启动应用程序、激活菜单，或作为通常所的小组件（`applets`）。
- 小组件是运行并将其输出放在较小空间内的应用程序；它们通常分为两类：
  - 第一类报告信息，例如你的笔记本电脑电池状态。
  - 第二类作为小型应用程序运行，例如截图小组件，它可以让你捕获屏幕图像并保存到磁盘。
- 在屏幕底部，你将找到当前运行的应用程序列表。
- 你可以通过将鼠标移动到空白区域并按住右键，向任一面板添加小组件或图标。
- 在弹出菜单中进入“小组件（Applets）”，并找到你想要运行的小组件；松开右键。
- 小组件将启动，你将在底部面板看到它。
- 你可以点击并按住鼠标中间键移动小组件。

### 配置 GNOME

- `GNOME` 控制中心（`GNOME Control Center`）可配置 `GNOME` 的几乎每一个方面。
- 你可以使用 `Desktop->Background` 设置背景图像或颜色。
- 屏幕保护（在 `Default->Screensaver` 下）允许你选择屏幕保护的超时时间。

笔记：

### KDE

- `GNOME` 的替代方案是 `KDE` 桌面环境。
- `KDE` 的优点类似于 Windows 98。
- `KDE` 自带一个名为 `Konqueror` 的浏览器。
- `KDE` 的缺点是它们必须用 C++ 编写。
- `KDE` 和 `GNOME` 共享拖放功能。
- 顶部菜单栏包含程序列表，无论你在哪个虚拟屏幕。
- 底部菜单栏包含开始按钮（看起来像一个脚印）以及代表其他菜单的图标。
- 中间包含可用的虚拟屏幕列表。默认启动四个屏幕。
- 在这些标签的左侧有两个小按钮，一个是 x，另一个是锁。x 会退出回到字符模式。锁会锁定屏幕。
- 右侧包含对接应用程序——即在后台运行但不一定需要窗口的应用程序。
- 这些对接应用程序的右侧是当前日期和时间。
- 菜单栏的两端空间包含小箭头，允许你向左或向右折叠栏。

### 在 KDE 中添加快捷方式

- 作为一个例子，我们将 Netscape 添加到主窗口，以便你可以随时启动。
  - 打开 Templates（模板）窗口并选择 Program 图标。
  - 将 Program 图标拖到桌面并松开鼠标。你会得到一个包含 Copy、Move 和 Link 的菜单列表。
  - 选择 Copy（复制）。
  - 右键点击新图标并选择 Properties（属性）。
  - 在 General（常规）下，将文件名更改为 `Netscape.delink`。
  - 选择 Execute（执行）标签并输入 `/usr/bin/netscape`。
  - 在 Application 标签下，在 Binary Pattern 下输入应用程序名称并在 Comment 下输入注释。
  - 点击 OK。
- 完成后，你会看到图标已更改；名称现在是 Netscape，如果你将鼠标光标悬停在图标上，会弹出一个小框显示注释。

## Lesson 10.5

### 使用远程显示器

- X 可以将程序的输出发送到另一个 X 服务器。
- 由于 X 将客户端与服务器分离，客户端应用程序可以通过网络运行在正在运行 X 的远程服务器上。
- 远程显示器工作需要满足以下三个条件：
  - 两台机器之间必须有 TCP/IP 连接。
  - X 服务器必须知道某个客户端想要发送显示。这可以通过 `xhost` 实现。
    - `xhost +` 将允许从任何地方向你的 X 服务器建立连接。
    - 运行 `xhost +host` 会将 `host` 添加可以访问你显示器的机器列表中。
    - 你可以使用 `xhost -host` 拒绝访问。
  - 客户端程序需要知道将显示发送到哪里。这可以使用 `-display` 参数或设置 `DISPLAY` 环境变量来实现。
  - 显示由两个项设置：要在哪个主机上显示，以及在该主机上运行用于显示的 X 服务器。服务器本身被分为两部分：服务器编号和显示器编号。由于 X 可以同时处理多个显示器，你将需要指定将客户端程序发送到哪个主机、哪个 X 服务器以及哪个显示器。
- XFree86 服务器还允许每台机器运行多个 X 服务器，每个服务器位于不同的虚拟客户端上。第一个 X 服务器位于虚拟控制台 7（Virtual Console 7），你可以通过 ALT-F7 访问。你可以使用 `gdm` 并向 `/etc/X11/gdm/gdm.conf` 中添加行来启动更多的 X 服务器。文件的末尾有一个名为 `[servers]` 的部分。该部分所示：

```ini
```



## 第10讲课 X 窗口系统

`[servers]`

`0=/usr/bin/X11/Xvt vt7 -deferoglyphs 16`

在这里看到服务器 0 运行在虚拟终端 7 上。如果你想在虚拟控制台 8 上启动另一个服务器，请使用以下命令：

```ini
[servers]

0=/usr/bin/X11/Xvt7 -deferglyphs 16

1=/usr/bin/X11/Xvt8 -deferglyphs 16
```



- 服务器和显示器始终从 0 开始计数，因此第一个 X 服务器是 `0.0`。第二个服务器称为 `1.0`，以此类推。

# Lesson 10.6
## 总结

- X 是 Linux 和 UNIX 上最流行的图形显示标准。
- X 在客户端和服务器之间的分离为用户提供了很高的可性。
- GNOME 和 KDE 是 Linux 上最流行的两个桌面环境。
- 你可以使用 X 跨网络发送窗口。

# 第11讲
## Linux 的安全防护
### 目标

- 保护硬件
- 保护软件
- 保护你的网络
- 配置数据过滤

# Lesson 11.1
### 物理安全

- 最简单且最容易忽视的安全性形式是物理安全。
- 对于位于公共或半公共区域的机器，你可能想要执行以下操作：
  - 锁定 BIOS，并将 BIOS 设置为仅从第一个硬盘启动。
  - 不要使用 LILO，或者至少让它直接进入 Linux。
  - 上不要安装 DOS 或任何其他操作系统。
  - 锁定 PC 机箱。
  - 你还应该有人员在现场协助解决问题并防止任何人有机会拆解计算机。
- 服务器机器应始终放在锁好的门后，对钥匙的访问权限非常有限。

# 第11讲 Linux 安全防护
# Lesson 11.2
### 软件安全

- 像 `COPS`、`TripWire` 和 `LIDS`（Linux 入侵检测系统）程序允许你定期监控系统，以检测可能的漏洞或检测某些形式的入侵。
- 像 `SATAN` 的程序会监控整个网络并报告可能的漏洞。
- `Tripwire` 是系统的一部分，允许你定期监控系统以检测可能的漏洞或检测某些形式的入侵。

# 第 11 课：加固 Linux 167

- 要实现一个完全隔离的系统（从 `tcpd` 的角度来看），请从 `/etc/hosts.deny` 中的 `ALL:ALL` 开始。这将拒绝所有 `tcpd` 服务访问所有主机。
- 接下来，你可以通过向 `/etc/hosts.allow` 中添加 `ALL:LOCAL` 来开始开放系统，允许所有本地机器访问所有 `tcpd` 服务。

### Notes：

![](img/82fbcc74bc25eeea437e17c816ad0621_172_0.png)

## 11.3
## 拒绝服务攻击

- 拒绝服务意味着用户可能正在进行有效操作，例如 ping 你的主机或发送电子邮件，但其操作方式阻止了他人使用相同的服务。
- DDOS 攻击（分布式拒绝服务攻击）是指黑客入侵互联网周边的大量机器，并协调对单个主机或网络进行同时攻击。
  - 由于涉及了大量机器，因此很难区分有效请求和恶意请求。
  - 在许多情况下，只能关闭互联网连接，直到攻击平息。
- 另一种攻击类型是发送大量邮件，导致邮件分区溢出。
- 你可以在 `www.cert.org` 和 `www.rootshell.com` 等网站上找到更多关于当前破解攻击状态的信息。

### Notes：

# 第 11 课：加固 Linux

## 11.4
### 网络安全

- 网络安全涵盖了如何设置你的网络和数据以使其更加安全。
- 对于小型办公室环境，最好的方法可能是让单个主机与外部世界进行交互。
- 使用 Linux 内置的包过滤工具 `iptables` 保护网络的其余部分。
- 监控匿名 FTP 和 WWW 日志以检查入侵情况。这些日志位于 `/var/log`。
- 你需要查看的安全文件位于 `/var/log/security`。
- 对于只需要接收电子邮件的用户，你可以将这些电子邮件转发到外部账户。
- 注意谁正在休假或其他类型的请假，并确保他们没有登录。
- 这在安全性和便利性问题之间取得了一定定的平衡。内部员工可以在不使用代理的情况下访问互联网的其余部分。
- 所有进出路由器的流量首先都会通过防火墙。
- 像 `TripWire` 这样的程序运行在所有主机上。`TripWire` 可以监控如 `/etc/passwd` 等系统文件，并在这些文件更改时感知。如果文件被更改，它会发送警报，指示可能正在破解。
- 对于入站服务，任何需要用户身份验证的内容必须加密，以防止恶意主机嗅探密码。

## 11.5
### 总结

- 安全是一个过程。请确保跟进红帽（Red Hat）的安全发布。
- 物理安全与网络安全同样重要。
- 使用加密工具保护密码并保持敏感数据的私密性。

### Notes：

# 第 12 课
## 与 Red Hat Linux 内核工作

### 目标

- 编译一个适用于你芯片组的内核版本
- 添加新的驱动程序或安全补丁
- 编译一个将模块编译进内核的内核

## 12.1
### 内核版本

- 在决定生产环境中使用哪种内核修订版本时，有几点需要考虑。
- 稳定发布版本的次版本号为偶数。Linux 认为这些版本足够稳定，可生产。
- 开发版本包含实验性驱动程序或相关更改，在生产环境中使用可能会导致崩溃。然而，这些版本更有可能支持新硬件。
- 大多数 Linux 发行版以稳定内核为基础，然后添加一些新的驱动程序。生成的内核将经过测试以确保其稳定性，然后发布。
- 大多数 Linux 发行版从稳定内核开始，然后添加一些新的驱动程序。生成的内核经过测试以确保其稳定性，然后发布。

### Notes：

# 第 12 课：与 RED HAT LINUX 内核工作 173

## 12.2
### 编译内核

- 在编译内核时，需要考虑几点。
- 编译内核的另一种方法是将其模块编译进内核中。
- 如果你需要，`makeconfig` 允许在启动时选择内核。
- 引导加载程序如 `LILO` 将允许你在启动时选择内核。
- 获取最新内核最简单的方法是 `http://www.kernel.org`。解压并 `tar`。
- 编译内核的另一种方法是将其模块编译进内核中。
- 如果你需要，`make` 这种方法位于 `/usr/src/linux`。
- 另一种方法是使用 `linux-2.bz2`。
- 编译内核的另一种方法是将其模块编译进内核中。
- 如果你需要，`make` 这种方法位于 `/usr/src/linux`。
- 另一种方法是使用 `linux-2.bz2`。
- 编译内核的另一种方法是将其模块编译进内核中。
- 如果你需要，`make` 这种方法位于 `/usr/src/linux`。
- 另一种方法是使用 `linux-2.bz2`。
- 编译内核的另一种方法是将其模块编译进内核中。
- 如果你需要，`make` 这种方法位于 `/usr/src/linux`。

### Notes：

### 使用 makeconfig

- 第一种方法是在 `/usr/src/linux` 内使用 `make config` 来配置内核。
- 这种方法非常繁琐，因为你需要手动回答每一个问题。
- `make config` 的优势是不需要安装任何其他开发工具。

### Notes：

### 使用 menuconfig

- 下一级别的方法是使用基于字符的界面 `make menuconfig`。
- 这需要安装 `ncurses` 及其开发库才能工作。
- 使用 `rpm` 检查 `ncurses`。
- 带有屏幕的方法更容易组织和选择你想要的选项。帮助菜单同样可用。

### Notes：

### 使用 xconfig

- 配置内核的最用户友好方法是 `make xconfig`。
- 这需要安装大多数 X 库，以及 Tcl 和 Tk，因此资源消耗比其他任何方法都大。

### Notes：

### 配置内核选项

- 选择正确的选项需要在性能、内存消耗、兼容性和安全性之间取得平衡。
- 为你的 CPU 选择正确的处理器族是最好的做法之一。每个处理器族都有其处理内存的方式以及特定的 CPU 选项。
- 如果你的硬件设置是稳定的，可以编译各种硬件的驱动程序以获得更好的性能并防止加载木马模块。
- 选择“块设备”下的 DMA 访问将自动开启 DMA，减少 CPU 负载。
- 如果你的机器被配置为没有防火墙的路由器，可以在“网络选项”中启用“IP 路由”。
- “网络设备支持”下的绑定设备支持将允许多个网络设备绑定，创建一个连接到其他绑定 Linux 或 Cisco 路由器的大管道。
- 如果计划有大量用户登录并需要大量的伪终端 `PTYs`，你可以在“字符设备”下输入“Unix98 PTY 最大使用数 `0-2048`”。
- 对于无人且需要高可用性的系统，可以启用“看门狗定时器支持”。

## 内核模块与你

- 对于那些想要核心、尽可能不可破解的系统，你可能希望从系统中移除模块支持。覆盖黑客踪迹的高级方法之一是插入一个隐藏其大部分活动的内核模块。
- 另一种策略是用木马程序替换现有的模块。
- 从系统中移除模块的另一个原因是创建一个体积更小的内核。
- Notes：来自 Linux 的信息。

/proc 层次结构

Notes：

# 第 12 节：与红帽 Linux 内核交互 179

### 编译内核

- 在配置完成后，你可以构建内核。
- 如果你想存储内核配置，首先要查看的内容是获取 `/usr/src/linux/.config`，因为它包含了之前所选配置选项的输出结果。
- `make dep` 命令会设置构建内核所需的依赖关系。这是至关重要的一步；没有它内核将无法编译。
- 使用 `bzip2` 来构建内核，因为它生成的内核比 `gzip` 或不压缩格式生成的内核小得多。
- 使用 `make bzImage` 编译 bzip2 内核。压缩后的镜像将被构建并放入 `/usr/src/linux/arch/i386/` 中。
- 你可能只想使用 `make bzImage` 将内核放入 `/` 并运行 `lilo` 以让你启动新内核。
- 一些用户可能不希望将内核放在 `/` 下，因为许多发行版会创建一个很小的 `/boot` 分区，其中包含内核以及足够的启动空间。在这种情况下，你希望将内核拷贝到 `/boot`。
- 如果你将使用模块，你还需要运行 `make modules` 和 `make modules_install`。

### 注意：

### 第 12.3 节
## 调优运行中的 Linux 系统

### /proc 文件系统

- 在发生严重的内存或硬件问题时，有时可以根据内核版本获得一些变化，但这些变化通常被分为不同的类别。
- `Processes` 包含关于每个运行进程的信息，按 PID 组织。每个进程都有自己的信息目录。
- `bus` 包含关于系统总线的信息。
- `cpuinfo` 存储你系统中安装的 CPU 的信息。
- `filesystems` 列出了内核当前已知的各个系统列表。
- `ide` 包含你系统中 IDE 设备的信息。它根据可用的 IDE 通道进行组织。
- `meminfo` 包含你通常在 `free` 输出中看到的原始内存信息。
- `modules` 给出了模块列表、模块的大小以及模块的依赖关系。
- `partitions` 列出了 Linux 已知的所有磁盘分区列表，包括未挂载或未列在 `/etc/fstab` 中的分区。
- `pci`: 该文件在长期来看可能会消失，取而代之的是 `/proc/bus/pci`，`/proc/pci` 更具可读性，列出了设备类型、供应商和设备名称。
- `scsi` 与 IDE 类似，列出了链，随后是每个链上的设备。
- `swaps` 列出了所有已挂载的交换分区（或文件）。
- `version` 包含你正在使用的内核版本信息。它非常有帮助，因为它包含了编译内核的用户和主机、编译内核时使用的 GCC 版本、编译该内核的日期和时间。
- 上述未列出 `/proc/sys`。该目录是大多数内核运行时发生的地方。

# 第 12 节：与红帽 Linux 内核交互 181

- 以前这种访问是手动完成的，使用 `cat` 和 `echo` 来查看或更改运行内核的设置。如果你希望在每次机器启动时更改运行时设置，你必须为每个设置在 `rc.local` 文件中添加命令。
- 管理这些设置的一种简单方法是通过使用 `sysctl`。



# sysctl

`sysctl [-n variable] [-w variable=value] [-a]`

- 如果你只使用 `variable` 参数，你将获得 `/proc/sys/variable` 的当前值。
- 你可以通过使用 `-w` 开关并添加等号和值来设置一个值。
- 你可以使用 `-a` 获取可用项列表及其当前值。
- 如果你使用 `-n` 开关，你只会返回值而不是变量的文本，这使得处理 shell 脚本变得容易。

- 在更现代发行版的 Linux 启动序列中，`sysctl` 使用 `-p` 被调用，它从 `/etc/sysctl.conf` 读取设置。
- 该文件可以使用文本编辑器进行编辑，并包含 `variable=value` 格式的行。

## sysctl.conf 示例

```
#
#/etc/sysctl.conf - 设置系统变量的配置文件

# 请参见 sysctl.conf (5) 获取信息。

#
#kernel.domainname = example.com

#net/ipv4/icmp_echo_ignore_broadcasts=1

net.ipv4.conf.all.hidden = 1

net.ipv4.conf.lo.hidden=1
```

- 查看或设置所有 `/proc` 文件的安全性由普通文件权限处理。

## 使用 powertweak

- 更改运行内核选项的另一种方法是 `powertweak`。
- `powertweak` 在在 Linux 启动时运行，使用一个名为 `powertweak` 的守护进程向内核发布更改。
- 配置文件以 XML 格式存储在内核中。
- 使用 `powertweak` 相比 `sysctl` 的优势是 `powertweak` 具有图形界面。
- 查看或设置所有 `/proc` 文件的安全性由普通文件权限处理。

### 第 12.4 节

### 总结

- 配置内核有方法：`config`、`sysctl` 和 `powertweak`。
- `/proc` 文件系统可以提供有关系统的信息。
- 调优内核允许你提高性能或增加安全性。

### 注意：

# 第 13 节

## 系统与网络

## 第 13 节：系统与网络监控

### 第 13.1 节

### Syslog

- 非注释行是条目，由两个字段。第一个字段列出设施（facility）或产生事件的程序类型。第二部分是事件的优先级或严重程度。
- `syslog` 程序在启动时运行并使用 `/etc/syslog.conf` 来确定该做什么。

```
syslog.conf 示例

#
#/etc/syslog.conf - 设置系统变量的配置文件
# 请参见 syslogd.conf (5) 获取信息。

#
# 将所有内核消息记录到控制台。
kern.*  /console

# 记录任何级别为 info 或更高级的内容（邮件除外）。
*.info;mail.none /log/messages

# authpriv 文件具有限制的访问权限。
authpriv.* /log/secure

# 将所有邮件消息记录在一个处。
mail.* /log/mail

# 所有人都在另一台机器上接收紧急消息。
*

# 将 err 级及以上的邮件和新闻错误保存在特殊文件中。
uucp.news.crit /log/spool
```

- 共有 20 个可用设施：12 个系统设施和 8 个分配给本地使用的设施。
- 有 8 种优先级，严重程度从 `debug`（低严重性）到 `emerg`（高严重性）。
- 你列出的设施/优先级组合将报告发送到该优先级及更高优先级的所有消息。
- 将设施或优先级替换为星号 (`*`) 将报告所有设施或所有优先级，取决于你放置星号的位置（在点之前还是之后）。
- 你想要监控的特定程序的 man 页面将列出该程序使用的设施。

- 第二个字段列出消息应该发送到哪里。这可以是文件（如果目标以 `/` 开头）、远程主机（如果目标以 `@` 开头）、所有登录用户（如果目标是 `*`）或特定用户（如果它不以前述任何字符开头）。
- 使用远程主机日志可以使一组计算机将它们的所有消息记录到一台机器上。
- 如何记录取决于你想记录什么。
- 对于初始设置，你可能应该从记录所有内容开始开始。
- 随着系统变得稳定并运行正常，将优先级更改为 `warn` 或 `err`，以排除常规的调试信息。
- 你可能还会选择为不同的设施使用不同的文件。这在出现问题时可以更容易进行区分。

## 红帽培训课程手册

笔记：

### tcpdump

- `tcpdump` 程序将以太网卡设置为混杂模式。
- 网卡看到的所有所有数据包都会显示在屏幕上。
- 存在过滤器可以让你只查看你感兴趣的数据。
- 以下是几个与 ARP 相关的数据包：

```
21:49:12.480000 arp who-has myachine.insidehost.com tell gateway.insidehost.com
21:49:12.480000 reply myachine.insidehost.com is-at 00:0c:01:b4:4f:dc
```

- 第一行是网关的请求，询问我的机器的以太网地址。
- 下一行是带有 MAC 地址的回复。
- 这非常常见，因为 ARP 缓存的持续时间并不长。

- 以下是一些与 ICMP 相关的数据包：

```
21:50:05.510000 myachine.insidehost.com > ping.outsidehost.com: icmp: echo request
21:50:05.650000 ping.outsidehost.com > myachine.insidehost.com: icmp: echo reply
```

- 在这里我们看到一个 ping 从我的机器发送到一个名为 `ping.outsidehost.com` 的远程站点。
- 大约 140ms 后（6500000 减去 510000），ping 收到了回复。
- 由于 ping 实际上是请求远程端回显数据，这就是 `tcpdump` 报告该它的方式。

- 下面，`tcpdump` 在第二个以太网口（也称为 `eth1`）上运行：

**在其他接口上使用 tcpdump**

```
# /usr/sbin/tcpdump -i eth1
tcpdump: listening on eth1
23:12:59.510000 192.168.1.15.listen > hudson.telnet: . ack 76005909 win 78432 (DF)
23:12:59.510000 hudson.telnet > 192.168.1.15.listen: P 1:29(28) ack 0 win 32736 (DF)
```

## 第 13 节系统与网络监控

```
23:12:59.710000 192.168.1.15.listen > hudson.telnet: . ack 29 win 7814 (DF)
23:12:59.710000 hudson.telnet > 192.168.1.15.listen: P 29:199(170) ack 0 win 32736 (DF)
```

- 内核接收了 4 个数据包
- 过滤器丢弃了 0 个数据包

这个例子看起来有点乱，因为所涉及的机器是通过第二个以太网口登录的。我们看到的是通过以太网线发送的 `tcpdump` 数据。

让我们检查第二个和第三个数据包：

```
23:12:59.510000 hudson.telnet > 192.168.1.15.listen: P 1:29(28) ack 0 win 32736 (DF)
23:12:59.710000 192.168.1.15.listen > hudson.telnet: . ack 29 win 7814 (DF)
```

- 第一行是离开服务器（通过 telnet 连接的机器）`telnet` 端口的数据包，并发送到监听端口上的 `192.168.1.15`。
- 时间戳表明精确来说，时间几乎是 `13:12:59.510000`。
- 在数据表示之后，提到了特殊/IP 标志。在这种情况下，`P` 代表“推”（Push）。它也可以是 `S`（Syn）、`F`（Fin）、`R`（Reset），空标志表示没有标志。
- 接着是数据序列号（`29(28)`）。这允许 IP 层在数据包到达时对其进行重组。
- 接下来是 `ack 0`，意味着正在等待确认。
- `win` 指剩余接收缓冲区的大小。
- 第二行是来自目标机器的确认包。
- 由于 `tcpdump` 尝试使用名称而不是 IP 地址，你可能会发现其他人是谁。如果你想关闭此功能，请使用 `-n` 选项。

`tcpdump` 提供的另一个选项是过滤。例如，为了过滤所有 `telnet` 流量并获取谁在浏览网页的信息，你会使用这样的命令：

```
$ /usr/sbin/tcpdump -i eth0 port
```



由于 `tcpdump` 只能看到本地以太网上的流量，你将能够看到你所在网段的流量。你无法看到路由器、防火墙甚至交换机另一侧的流量，除非它是广播。

笔记：

## 第 13 节系统与网络监控

### 第 13.3 节总结

- `syslog` 程序帮助跟踪系统上的问题。
- 网络监控程序允许你从桌面跟踪网络。
- 存在特定的网络监控发行版，帮助你跟踪网络中任何地方的问题。

笔记：

## 第 14 节备份你的数据

### 目标

- 使用 `tar` 和 `mt` 备份数据
- 使用 `tar` 备份数据
- 使用 `dump` 备份
- 理解 `RAID` 和镜像

### 第 14.1 节

使用 `tar` 和 `mt` 是最基本的方法
- `mt` 命令现在主要用于磁带驱动
- `mt` 程序配合 `tar` 使用来控制磁带
- 使用 `tar` 压缩文件卷
- 使用 `tar` 这种方式创建文件卷，从而在磁带上进行备份
- 增加文件块大小，你就可以在磁带上备份多个文件卷
- 首先，`tar` 可以在磁带上备份多个文件系统
- 如果你的备份数据足够小，你可能需要将磁带移动到某个位置。
- 其次，`tar` 可能会在磁带上拥有多个备份文件

笔记：

### 使用 tar

- `tar` 命令有三个主要功能：创建 `tar` 文件、列出 `tar` 内容以及从 `tar` 文件提取文件
- 其他常用的开关包括 `f`（文件名）、`v`（详细）和 `z`（启用 `gzip` 压缩）
- 如果使用了多个开关，请在开关后跟参数，例如：

```
$ tar -cvf foo.tar file1 file2

$ tar -vf foo.tar
```



- 如果增加了 `z` 开关，`tar` 也会压缩数据流。通常压缩 `tar` 文件命名为 `.tar.gz`。
- 你可以使用以下命令解压缩归：`$ tar -zkv foo.tar.gz`
- 从 SCSI 设备读取压缩归档：`# tar -zkvf /dev/nst0`
- 使用 `tar` 备份和恢复文件时必须知道块大小。如果块大小错误，你将无法读取备份的文件。
- 增加块大小可以减少写入磁带时的开销并提高性能。
- `tar` 通过 `-B blocksize` 添加块大小，其中 `blocksize` 乘以 `512`
- `tar` 可以归档当前不需要的文件
- `tar` 常用于创建文档、源代码或预编译软件的包或发行版
- `tar` 可用于目录树。它的许多选项允许你控制权限、修改日期以及符号链接的跟踪
- 通常，除非你知道树中的链接指向哪里，否则不要跟踪链接

### 使用 `mt`

- `mt` 程序用于控制磁带设备
- 由于 `tar` 从块开始并在每个块的末尾添加 EOF（文件结束），你可以使用 `mt -f device fsf count` 推进磁带部分
  例如，如果你在磁带上有五个 `tar` 文件并想添加第六个，你首先需要使用 `mt -f /dev/nst0 fsf 5` 将磁带移动到第五个文件结束标记之后的下一个块。
  然后你将使用 `tar -cvf /dev/nst0` 写入新信息。你会使用 `tar -xvf /dev/nst0` 从磁带恢复数据。
- 使用 `/dev/nst0` 设备名称将告诉磁带设备完成后不要回绕；当使用 `mt` 推进磁带时请这样做，否则磁带会在推进后回绕！
- `/dev/st0` 在命令完成后会回绕，并在恢复后自动回绕磁带。
- `mt` 命令支持显式回绕，如果磁带设备支持，它还可以弹出磁带。这些命令分别是 `mt -f /dev/st0 rewind` 和 `mt -f /dev/st0 offline`。
- `mt` 的其他命令包括重张（前进到磁带末尾然后回绕）、`status`（给出磁带驱动状态）、`erase`（擦除磁带）以及与硬件压缩、缓冲、密度等方面相关的许多 SCSI 选项。

## 课程 14.2

`dump` 和 `restore` 对整个文件系统进行字面上的备份和恢复。

- `dump` 和 `restore` 对整个文件系统进行字面上的备份和恢复。
- `dump` 无法备份非 `ext2` 文件系统，例如 `NFS`。
- 为每个文件系统分配一个 `dump` 级别可以控制增量备份。`Dump` 级别范围从 `0` 到 `9`，当执行特定级别 `N` 的备份时，所有自上一次级别 `N-1` 或更低级别备份以来更改的文件都将发送到磁带上。级别 `0` 的备份将备份整个文件系统。
- `dump` 程序强烈建议你了解所用于备份的介质的长度和密度。

备注：

## 第 14 讲座：备份你的数据

## 课程 14.3

### 备份策略

- 你多频繁地进行何种类型的备份取决于几个因素。
- 总的来说，如果某个文件系统每天的变化量超过百分之二十，你应该每隔一天或两天执行一次增量备份，每周执行一次低级别备份，每月执行一次全备份。
- 活跃水平较低意味着你可以拉长间隔，尽管实际上没有理由不至少每月执行一次全备份。
- 另一种方法是每晚执行一次全备份。
  - 保留 28 磁带，这样你任何时候都都有四周的数据。
  - 大约每六个月循环一次磁带。
  - 频繁使用磁带会导致其老化；请定期更换。
- 这允许你无限期地存储信息。
- 然而，这种成本较高，因为你必须购买大量的磁带，而且磁带上的空间可能不够。
- 购买大量你特定的备份介质。
- 对于或或少无法离线的非常活跃系统，请投资一种可以在低流量期间执行在线备份的备份工具。
- 复杂的数据库在进行在线备份时会遇到问题。
  - 幸运的是，大多数数据库可以创建自己的快照，并可以将其放入你的归档中。
  - 如果失败，必须在备份之前将数据库离线。
- 将某些备份保存在异地，以防发生重大灾难。

## 课程 14.4

### RAID 和磁盘镜像

- `RAID` 代表独立磁盘冗余阵列（Redundant Array of Independent Disks）。
- `RAID` 的基本思想是，通过使用多个较小的磁盘和可能的一些额外的校验数据，你将能够在其中一个磁盘故障时重构丢失的数据。
- 有几种不同级别的 `RAID`。
- 这里的每种 `RAID` 类型都可以通过硬件或软件实现。
  - `RAID 0`: 数据条带。这实际上并没有提供任何防止数据丢失的保护，但可以增强性能。它需要一个支持同步磁盘的控制器；Linux 目前没有此类控制器。
  - `RAID 1`: 磁盘镜像。使用第二组磁盘提供你数据的完整副本。
  - `RAID 2`: 带有用于存储纠错信息的检查磁盘的级别 0。
  - `RAID 3`: 级别 0，并带有一个独立的磁盘用于存储字节级校验信息，以帮助重构丢失的数据。
  - `RAID 4`: 级别 3，将块级校验信息存储在独立的磁盘上。
  - `RAID 5`: 级别 4，将校验信息分列存储在所有磁盘上。
- 某些 `RAID` 级别的目的是不是为了可靠性，而是为了速度。
- 虽然软件 `RAID` 成本较低（因为你不需要自定义的硬盘挂载或适配卡），但它比硬件 `RAID` 不稳定。
- 硬件 `RAID` 通常允许在一个硬盘故障后立即进行热插拔。软件 `RAID` 需要关机以更换硬件。
- 要在你的机器上创建软件 `RAID` 设置，你至少需要两个（可能三个）大小相相同的驱动器。
- 让我们演示一下如何在你的机器上创建一个 `RAID 5` 设置。
  - 在每块硬盘上创建分区。每个硬盘不应再有其他分区，并且应该是高端 SCSI 系统。每个分区的大小应相同。
  - 从 RedHat 光盘安装 `raidtools`。
  - 读取位于 `/usr/share/doc/raid-tools` 的文档。
  - 为你使用的分区和块配置 `/etc/raid.conf`。
  - 使用 `mkraid` 创建 `RAID` 设备。默认情况下，它被称为 `/dev/md0`。
  - `/etc/raid.conf` 文件列出了你使用的设备。
  - 现在你可以像处理其他原始分区一样处理 `/dev/md0`。你可以使用 `mke2fs` 格式化并复制文件。你可以查看 `/proc/mdstats` 获取 `RAID` 信息的状态。
  - 如果你想停止 `RAID` 服务，请卸载设备并使用 `raidstop`。
  - 启动时，使用 `raidstart` 启动 `RAID` 服务。
  - RedHat 会自动检测 `RAID` 设备并在启动过程的一部分启动它们。在激活后，你必须挂载 `RAID` 系统。

备注：

## 课程 14.5

### 总结

- `tar` 可以将你的数据备份到磁带或文件。
- `mt` 程序用于操作磁带设备。
- `RAID` 可能是你增加硬件可靠性和提高性能的一种方法。
- 你可以在不需要 `RAID` 硬件的情况下创建 `RAID` 系统。

备注：
