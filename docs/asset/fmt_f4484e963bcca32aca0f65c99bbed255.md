
### 7. Damn Small Linux
*http://www.damnsmalllinux.org/*

### 8. Tiny Core Linux
*http://tinycorelinux.net/*

### 9. antiX Linux
*https://antixlinux.com/*

### 10. Balena Etcher
*https://etcher.balena.io/*

### 11. Alpine Linux
*https://www.alpinelinux.org/*

### 12. VirtualBox
*https://www.virtualbox.org/*

### 13. Light
*https://sourceforge.net/projects/light/*

### 14. Ubuntu 变体
*https://ubuntu.com/flavours*

**图 8：你可以使用内置重制工具创建 `Puppy Linux` 或 `antiX Linux` 的修改版本；截图显示了 `antiX` 工具。**

### 信息

对于特殊任务，你需要一个特殊的工具。在那些伟大的通用型系统旁边，还有许多关注点非常窄的 Linux 发行版占据着特殊位置。

### `Daphile` 音频

如果你有一台旧电脑，为什么不把它变成 `Daphile` 音频服务器？

#### 轻量化 Linux 发行版

为了让你从其他位置通过 `Daphile` 硬盘播放音乐，该发行版启动了一个 `Samba` 服务器，你可以从任何 Linux、Windows 或 macOS 机器连接。

设置 `Daphile` 非常简单。网站提供了三个下载选项（64 位、32 位以及带有实时内核的 64 位），因此你可以使用现代电脑，但 `Daphile` 也能在非常老的机器上运行。对于我们的测试，我们选择了第一个选项，64 位镜像（`daphile-23.01-x86_64.iso`）。注意 `Daphile` 受限制的许可——网站上的免责声明写道：“`Daphile` 发行免费供非商业私人用途使用。任何形式的商业用途和重新分发都是禁止的。”

将 ISO 镜像写入 USB 闪盘，从该闪盘启动你的目标音频服务器，并检查屏幕上的输出：它将显示其 IP 地址。这也是你最后一次连接显示器，因为 `Daphile` 运行在无头模式下——你无法在电脑直接登录。通过浏览器连接并进入 `Settings` 选项页。你可以启动安装：选择一个将重新分区（并将丢失所有数据）的磁盘。`Daphile` 创建两个分区，一个名为 `DaphileBoot` 的小分区（存放软件）和一个名为 `DaphileData` 的大分区（你存储音乐的地方）。如果你不想使用电脑硬盘或只想尝试软件，你也可以安装到刚刚启动的 USB 闪盘上。从目标磁盘（或闪盘）重启并……

| 发行版 | 网站 | 版本 | Linux 内核 | 发布日期 | 大小 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `SystemRescue` | `https://www.system-rescue.org/` | `10.01` | `6.1.30` | `05/2023` | `737MB` |
| `Kali Linux` | `https://www.kali.org/` | `2023.2` | `6.1.27` | `05/2023` | `3.9GB` |
| `Daphile` | `https://www.daphile.com/` | `23.01` | `5.15.86` | `01/2023` | `276MB` |
| `Linux From Scratch` | `https://www.linuxfromscratch.org/` | `11.3` | `5.17.15` | `03/2023` | `–` |
| `Recalbox` | `https://recalbox.com/` | `9.1` | `6.1.11` | `06/2023` | `3GB` |

![](img/8db7a58bef2f490a3db3c4fd35de2457_22_0.png)

浏览器中的服务器。现在你可以开始添加音乐。

`Daphile` 包含一个 CD 刻录器，你可以用它将音乐添加到库中。你必须将 CD 插入连接到服务器的驱动器，而不是连接到显示 Web 应用界面的客户端。刻录效果良好，且刻录程序会自动查找专辑元数据（解释和标题）以及封面艺术。它将刻录的轨道转换为音频质量极佳的大 `FLAC` 文件。然而，刻录需要时间，而且你需要同时对服务器和客户端进行物理访问，这使得这种方法有点不利。如果你已经有一堆 `MP3` 或其他数字音频文件，可以通过 `Samba` 共享等方式复制到 `Music` 文件夹。在局域网上传输数 GB 的音乐也会花费大量时间，但你可以让它无人值。

## Linux From Scratch (从零开始构建 Linux)

`Linux From Scratch` 是一个非常特殊的发行版，自 1999 年以来一直存在并且仍然活跃：当前版本 `11.3` 已于 2023 年 3 月发布 [2]。当你进入下载目录时，你找不到 ISO 镜像——你得到的是一本书（370 页 PDF 或 HTML）、一组启动脚本以及一个指向 90 个源代码归档的下载列表。

使用 `Linux From Scratch` 意味着*从零开始*构建它。你将阅读这本书并完成所有必要的步骤，这些步骤最终让你能够启动操作系统并在上面运行一些基础程序。例如，你将获得 `Vim` 编辑器，但没有图形化桌面。

最终产品并不是真正的目标，重要的是引导你到达那里的旅程。你将学习如何构建和使用交叉编译工具链，以及程序和库是如何协同工作的。你将深入基于 System V 的

**图 1：通过浏览器控制 `Daphile`，或在其 `Samba` 共享上查找音乐。**

![](img/8db7a58bef2f490a3db3c4fd35de2457_23_0.png)

`Recalbox` 镜像包含了许多游戏，你可以立即开始游戏。浏览这些机器——当你选择一台电脑时，你将看到它能够运行的游戏列表 (roms)。选择一个游戏并在几秒钟内开始游戏（图 3）。

如果你想添加自己的游戏文件，可以通过 Secure Shell (SSH) 登录——root 密码为 `recalboxroot`。然后导航到 `/recalbox/share/roms/` 文件夹：你应该将文件放在这里，例如放在 `c64/` 子文件夹中的 C64 磁盘镜像。你也可以 `cd` 进入该目录并使用 `wget` 从 Internet Archive 下载游戏——以下是经典游戏 Q\*Bert 的命令：

```bash
cd /recalbox/share/roms/c64
wget https://archive.org/download/d64_Q-Bert_1983_Parker_Brothers/Q-Bert_1983_Parker_Brothers.d64
```
