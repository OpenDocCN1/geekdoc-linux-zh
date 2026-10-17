
高级电源管理 (APM) BIOS 选项通常监控并控制系统电池。如果你想在工作站和服务器上实现新 PC 提供的 BIOS 待机和挂起模式，也可以使用它。

## 两分钟训练 265

- `inittab` 描述启动时应该启动哪些进程以及正常操作级别应该运行什么。`init(8)` 读取 `inittab` 以确定在什么运行级别运行什么。有效的运行级别范围从 0 到 6，以及 A 到 C。运行级别 A 到 C 被视为需求运行级别。

- 脚本 `/etc/rc.d/rc.sysinit` 执行了所有主要的系统设置和初始化。

- 当你编译内核时（参见第 6 章），你有选项将内核编译为模块。

- 为了动态加载和卸载内核模块，需要调用特殊的守护进程。你应该编辑 `/etc/conf.modules` 文件。

- 所有的内核模块都存在 `/lib/modules/...` 下，其中 `...` 是你的内核版本。

## 266 第5章：高级安装

## 自测

以下自测题将帮助你衡量对本章内容的理解。请仔细阅读选项，因为可能有多个正确答案。请为每个问题选择所有正确答案。

1. 你正在创建一个 NT/Linux 双系统。你已经安装了 NT 并计划使用 NTLDR 加载 Linux。你制作了一个可以正常启动的软盘。从 Linux 使用哪个命令来拷贝引导区？

- A. `dd if=bootsect.ln=/dev/0 bs=512 count=1`
- B. `dd if=/dev/0 of=bootsect.ln bs=512 count=1`
- C. `dd if=bootsect.ln=/dev/0 bs=512 count=1`
- D. `dd if=/dev/0 bs=512 count=1`

2. 你正在启动 NT/Linux 系统。你已成功将一个工作的引导区拷贝到 NT 分区并命名为 `bootsect.ln`。你需要做什么让 NTLDR 加载 Linux 系统？

- A. 在 NTLDR 文件中编辑 `C:\bootsect.lnx="Linux"`
- B. 在 BOOT.INI 文件中编辑 `"Linux"=C:\bootsect.lnx`。
- C. 在 BOOT.INI 文件中编辑 `C:\bootsect.lnx="Linux"`
- D. 无需操作；NTLR 会检测任何具有 `bootsect.xxx` 语法的引导区。

3. 你有一个三个驱动器的镜像 RAID 系统。前两个镜像，第三个应该是备用。当你查看 etc/raidtab 文件时，看到 spare-disk 0。这说明什么？

- A. raidtab 设置正确。
- B. 备用支持关闭。通过将 `spare-disks` 设置为 1 来开启它。
- C. 目前没有加载备用磁盘。
- D. 镜像失败并使用了备用磁盘。

4. 你需要在网上设置多个 Red Hat Linux 系统。你决定让软盘连接到你的 DHCP/BOOT 服务器，且 kickstart 文件位于 DHCP/BOOT 服务器上，使用以下语法：`<client_ip-kickstart>`。你计划从一个不在你不同服务器上的 FTP 服务器上 kickstart Linux。这样做有什么问题？

- A. 你不能将 FTP 服务器放在与你 DHCP/BOOT 服务器不同的服务器上。

## 自测题 267

- 7. ... B. kickstart 文件名错误。
- C. BOOTP 服务器只能用于加载内核，不会加载 kickstart 文件。
- D. 你无法从 FTP 服务器进行安装。

- 8. 你在笔记本电脑上运行 Linux。你 PCMCIA 卡的 `cardmgr` 守护进程占用了一个你想要保留的 IRQ。你使用哪个文件来告诉 `cardmgr` 从其列表中排除此 IRQ？

- A. `/etc/pcmciap/config.opts`
- B. `/etc/sysconfig/pcmciap`
- C. `/etc/pcmciap/rc.sysinit`
- D. `/etc/rc.d/config.exclude`

- 5. 你有一些需要安装 Linux 的远程分支。你决定此此操作的最佳方法是在 DHCP 服务器上的 kickstart 文件上预先配置所有答案，并从主分支的 NFS 服务器启动它。你计划分发一个包含 kickstart 文件的启动盘（bootdisk），但你担心网络上的某人会看到文件中的密码。你可以做什么？

- 8. 你在工作期间经常将笔记本电脑作为服务器使用。许多用户每天来这里处理特殊项目文件。你担心可能会断电，并希望在电池即将耗尽时通知其他用户。处理此情况的最佳方法是什么？

- A. 加密存储在 DHCP/BOOTP 服务器上的 kickstart 文件。
- B. 在 kickstart 文件中使用 `linux ks--encrypted` 启动磁盘。
- A. 告诉每个用户尽可能运行 `apm` 以检查电池电量。
- B. 设置用户策略，指示所有用户提前五分钟保存。
- C. 在 kickstart 文件中使用 `rootpw--encrypted`。
- C. 使用 `/etc/sysconfig/apmd` 文件中的 `wall` 选项。
- D. 编辑在级别 0 运行的关机脚本。
- D. 你无能为力。

- 6. 当尝试加载声音模块时，你收到设备错误信息。你觉得那是你的 ISA 即插即用卡。你想查看即插即用配置选项，以便编辑它们为非冲突值。你会使用哪个命令创建一个包含所有 ISA 即插即用设备的文件？

- 9. 为了在启动时自动运行 X11，你应该切换到哪个运行级别？

- A. 1
- A. `dumppasswd >isapnp.conf`
- B. 2
- B. `nppasswd >isapnp.conf`
- C. 3
- C. `displaypasswd >isapnp.conf`
- D. 5
- D. `showpasswd >isapnp.conf`

## 268 第 5 章：高级安装

- 10. 加载单用户模式需要哪个运行级别？

- A. 1
- B. 2
- C. 3
- D. 5

- 11. 如果你将 `/etc/initittab` 文件中的 `initdefault` 条目修改如下所示：`id=5:initdefault:/usr/games/fortune`，会发生什么？

- A. 它会在你每次登录时显示一条幸运言（fortune）。
- B. 它将启动到 X11 并显示一条幸运言。
- C. 它只在启动时显示一条幸运言。
- D. 幸运言行将被忽略。

- 12. 哪个启动文件加载模块？

- A. `/etc/rc.d/rc.modules`
- B. `/etc/init.d/S10modules`
- C. `/etc/rc.d/rc.sysinit`
- D. 以上均非

- 13. 下列哪项**不**描述内核模块？

- A. 它们让内核尺寸更小。
- B. 它们增加了你的内核速度。
- C. 你可以从内存中动态卸载模块。
- D. 模块具有 dll 扩展名。

- 14. 你有一张网卡，在加载模块时需要在命令行中指定选项。你只是偶尔需要这张网卡，所以想让它作为一个模块。你可以做什么来简化模块的加载？

- A. 在 `conf.modules` 文件中添加 `bind` 命令。
- B. 在 `conf.modules` 文件的末尾添加 `options` 命令。
- C. 在 `conf.modules` 文件的 `alias` 的末尾添加 `options`。

- 15. 模块在移除时会自动在 `/tmp` 目录中保存它自己的文件。

- A. 模块未被在使用，应该被移除
- C. `kerneld` 将自动处理将其从内存中移除
- D. `modprobe` 命令已设置为 `autoclean`。

- 16. 你在一个异国，不确定里面是什么种网卡。你已经检查了 `dmesg`，没有列出任何网卡。你有一堆编译好的网络模块，但目前没有加载的。你可以做什么来快速加载网络设备？

- A. 尝试手动加载每个模块。
- B. `modprobe *`
- C. 内核将在访问网卡时加载该模块。
- D. `modprobe -t net`

- 19. 在默认的 Red Hat 安装中，在系统上运行的第一个脚本名称是什么？

- 17. 你想尽可能节省内存。在进行一些检查时，你注意到有些模块加载了但没有使用。你可以使用哪个命令来移除这些模块？（选择所有适用项）

- A. `/etc/rc.d/rc.sysinit`
- B. `/etc/init.d/S10modules`
- C. `/etc/rc.d/rc.sysinit`
- D. 以上均非

- 17. 你想尽可能节省内存。在进行一些检查时，你注意到有些模块加载了但没有使用。你可以使用哪个命令来移除这些模块？（选择所有适用项）

- A. `/etc/rc.d/rc.sysinit`
- B. `/etc/init.d/S10modules`
- C. `/etc/rc.d/rc.sysinit`
- D. 以上均非
