
你应该会听到 Zip 驱动器短暂激活的声音。然后你可以使用 `dmesg` 命令查看发生了什么：

```
# dmesg
```

```
ppa: Version 2.03 (for Linux 2.2.x)
ppa: Found device at ID 6, Attempting to use EPP 32 bit
ppa: Communication established with ID 6 using EPP 32 bit
scsi0 : Imagen VPD0 (ppa) interface
scsi : 1 host.
  Vendor: IBM       Model: ZIP 100        Rev: D.17
  Type:   Direct-Access                     ANSI SCSI revision: 02
Detected scsi removable disk sda at scsi0, channel 0, id 6, lun 0
SCSI device sda: hwr sector= 512 bytes. Sectors= 196608 [96 MB] [0.1 GB]
sda: Write Protect is off
  rda: sda4
```

正如你所见，Linux 将该驱动器识别为一个 SCSI 设备（连接到你笔记本的并行端口上）。识别出的 SCSI 设备是 /dev/sda4。然后你可以使用 `mount` 命令将 Zip 磁盘挂载到指定的挂载点（例如 /mnt/zip）：

```
# mount -t vfat /dev/sda4 /mnt/zip
```

你可以使用 `df` 命令验证磁盘状态：

```
# df /mnt/zip
```

| 文件系统 | 大小 | 已用 | 可用 | 使用率 | 挂载点 |
|---|---|---|---|---|---|
| /dev/sda4 | 96M | 84M | 11M | 88% | /mnt/zip |

如你所见，这块特定的磁盘（使用 vfat 文件系统）几乎已满。如果你使用 `umount` 命令卸载 Zip 磁盘，然后可以使用 Linux 工具，如 `mke2fs`，将 Zip 磁盘重新格式化为原生 Linux 分区。这些磁盘是一种经济实惠的方式来存储归档、备份或其他信息，并且当挂载时，可以像其他任何硬盘一样使用。Linux 还附带了 `mzip` 命令，可用于查询、弹出或设置密码/写保护你的 Zip 磁盘。你还可以使用 X11 的 jaZip 客户端（如图 12.5 所示）来查询、挂载、卸载、锁定和解锁 Zip 磁盘。下载该程序，构建软件，然后使用以下命令启动程序：

```
# jazip &
```

便捷按钮用于控制你的 Zip 磁盘，滚动显示屏提供状态消息。

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_315_0.png)

图 12.5 jaZip X11 客户端可用于挂载、卸载、查询、锁定和解锁 Linux 下的 Iomega Zip 磁盘。

## 资源信息

- [http://samba.anu.edu.au/rsync/](http://samba.anu.edu.au/rsync/)
    - rsync 主页，你可以在这里找到最新版本以及示例。
- [ftp://trycham.ce.ryerson.ca/pub/PalmOS/](ftp://trycham.ce.ryerson.ca/pub/PalmOS/)
    - pilot-xfer 软件最新版本（包含在 pilot-link 包中）的存储库，以及用于构建 Linux 下 Palm PDA 客户端所需的 Linux m68k 交叉编译器和相关信息。
- [http://www.s1ac.com/pilone/kpilot_home/mainpage.html](http://www.s1ac.com/pilone/kpilot_home/mainpage.html)
    - KDE 和 Palm PDA 用户使用的 KPilot 软件主页。浏览以下载最新版本或获取有关该程序的更多信息。
- [http://www.torque.net/~/campbell/](http://www.torque.net/~/campbell/)
    - Dave Campbell 的 Zip 驱动器网页，包含大量关于在 Linux 上使用旧版和新版 Zip 驱动器的信息，以及下载最新驱动器的链接。
- [http://www.linuxdoc.org/HOWTO/mini/ZIP-Drive.html](http://www.linuxdoc.org/HOWTO/mini/ZIP-Drive.html)
    - Kyle Dantis 的 Zip 驱动器迷你指南。这是在 Linux 上使用 Zip 驱动器的必读材料。
- [http://www.scripps.edu/~-jsmith/jazip/](http://www.scripps.edu/~-jsmith/jazip/)
    - jaZip 图形化 Zip 和 Jaz 驱动器软件的主页。

即使你远离办公室，遇到麻烦时也不意味着你被困住了。学习如何进行一些预防性维护，并优雅地从那些会让其他用户束手无策或陷入困境的错误或问题中恢复过来。你将看到如何恢复数据、绕过打印问题、在旅途中连接互联网、跟踪时间以及节省电池电量。你还将对离线或空闲时间的一些优雅和经典消遣进行介绍。

- 13 崩溃预防与恢复
- 14 路上的打印
- 15 路上的网络连接
- 16 时区和区域设置
- 17 电池电量
- 18 路上的娱乐
- 19 必备旅行工具包

# 第三部分

在路上——问题与解决方案

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_316_0.png)

# 第 13 章：崩溃预防与恢复

- 1. 预防性提示
- 2. 备份策略
- 3. 备份设备
- 4. 备份软件
- 5. 替代备份方法
- 6. 随机硬盘维护
- 7. 恢复你的硬盘
- 8. 资源信息

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_318_0.png)

确保数据安全的最佳方法是在悲剧发生之前采取预防措施。这意味着你应该始终预料到灾难会降临。硬盘崩溃和数据丢失可能由于多种原因发生，移动 Linux 用户还面临额外的危险。以下是一些可能发生的情况：

- 你的笔记本被偷（每年有数十万台被盗）。
- 你摔倒了你的笔记本。
- 软饮料洒在你的笔记本键盘上。
- 某人黑进你的笔记本并更改 BIOS 启动和硬盘密码。
- 你的笔记本保持在线，某人侵入你的系统。
- 关键组件，如显示器、键盘或硬盘，发生故障。
- 你意外删除了关键文件或整个文件系统。
- 软件安装导致你的 LILO 引导加载器无法运行，无法引导 Linux。

我相信还有许多关于笔记本（或其他设备，例如变成酥脆狗玩具的朋友的 Palm PDA；谢天谢地 Palm LCD 覆盖有塑料涂层）可能发生的恐怖故事。本章概述了一些你可以采取的基本步骤，以防止数据灾难性丢失或笔记本的使用。其中一些技术只是常识，其他一些可能帮助你在安装、更新或升级 Linux 或其他软件时从问题中恢复。

### 预防性提示

当你第一次获得笔记本时，记下其序列号并将其存放在安全的地方。许多在线或邮寄订购的运输公司和制造商也在销售收据或运输箱上注明笔记本的序列号。你通常会在笔记本的底部找到序列号，很可能是在 FCC 铭牌上。

确保你的笔记本有保险。如果你住在公寓里，请购买重置成本保险。你的家庭财产保险可能涵盖你的笔记本，但如果用于商业目的，你可能需要特别附加险。如果你的公司为你提供笔记本，请检查关于盗窃或误用的政策。如果你在工作和工作中使用自己的笔记本，请检查关于更换个人设备政策。

你可以用雕刻笔或带有个人信息的环氧树脂贴纸永久破坏你的笔记本，以阻止小偷或不道德的当铺。

### 使用 BIOS

你应该做的第一件事之一是设置 BIOS 密码、系统密码或硬盘密码。重新启动你的计算机，然后按下所需的 *F1* 或其他组合键以调出 BIOS 配置屏幕。大多数 BIOS 菜单提供启动、从挂起返回和 BIOS 更改密码设置的选择。使用所有密码设置，并为不同的设置使用不同的密码。

设置 BIOS 密码会使大多数笔记本对普通窃贼或潜在买家无用。然而，有方法可以绕过已设置的 BIOS 密码。一些制造商甚至在网络上提供技术和硬件手册，其中包含如何击败已设置密码的详细信息。例如，要重置 IBM ThinkPad 1400 系列的 BIOS 密码，你需要执行以下操作：

1. 关闭并拔掉笔记本的电源，并移除电池。
2. 拆下键盘。
3. 拆下散热板。
4. 将 SW2（开关 2），密码开关，从关闭移动到开启。
5. 插上交流适配器，并引导笔记本。
6. 按 F1 进入 BIOS（蜂鸣声后）。
7. 选择系统安全，然后将开机密码设置为无。
8. 保存 BIOS 设置。
9. 关闭并拔掉笔记本的电源。
10. 将密码开关从开启移动到关闭。
11. 重新组装笔记本。

在 390 或 1700 系列 ThinkPads 上禁用 BIOS 开机密码更容易：

1. 拔掉笔记本的电源，并移除其电池。
2. 将笔记本的备用电池移除 20 分钟。
3. 或者，短接备用电池一秒。

