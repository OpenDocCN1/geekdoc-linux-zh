
在 `RedHat/` 目录之外，除了 `dosutils`、`file` 以及 Red Hat 软件的 GPG 签名（在 `RPM-GPG-KEY` 目录），你可能不需要访问此 CD 上的大部分内容（安装程序代表你处理了大部分工作）。

## 关于 CD2

CD2 主要由 Red Hat Linux 7、额外的 RPM 和源码包组成。你是在安装过程中被提示安装这些内容，还是选择安装它们。CD2 还包含一份来自 Red Hat 的 README 文件，详细说明了你在 CD 上发现的内容。目录结构如下（当然，缺少了我们方便的注释）：

```
/mnt/redhat
  ---> RedHat -- 额外的二进制包，包括：
      ---> RPMS -- 游戏、工具和实用程序
      ---> instimage -- NFS 安装树
  ---> SRPMS -- 源包，包括：
                               -- 第三方的 RPM 包
                               -- 工具和实用程序
                               -- alpha & beta 包
                               -- 仅供冒险用户使用的
                               -- （源码与二进制文件）
  ---> preview -- 版权信息
  ---> COPYING -- CD 2 readme 文件
  ---> README
  ---> RPMS-GPG-KEY -- Red Hat 软件包的 GPG 签名
```

在 `RedHat/RPM` 目录、`SRPMS` 目录以及 Red Hat 软件的 GPG 签名（在 `RPM-GPG-KEY` 目录）之外，你可能不需要访问此 CD 上的大部分内容（Red Hat 软件包管理器代表你处理了大部分工作）。

两个包都包含 GPG 签名，因为安装程序可以使用存储的签名检查其尝试安装的文件内容，以确保文件没有被更改过（假设所有更改都是向更坏的方向发展，例如木马或病毒），因为它们是被写入 CD 的。因此，签名提供了一种确保你的电脑一切安全且健康的方法！

![](img/4e9f259b21147d1fb7569159ef49ec31_391_0.png)

## 关于 CD3

CD3 包含 Red Hat 7 的文档文件。这些包括《官方 Red Hat Linux 入门指南》、《官方 Red Hat Linux 安装指南》和《官方 Red Hat Linux 参考指南》。此外，你还会发现许多 FAQ 和 HOWTO，它们可以帮助你学习更多或为你使用 Linux 系统提供分步说明，以及来自 Red Hat 官方的描述 CD 内容的 README 文件（该 README 仅名为 "README"，而此处的则名为 "IDGB_README"）。你可以将指南安装在电脑的硬盘上，也可以在 CD 上查看。无论哪种方式，请随手保留——你可能会多次参考它们。

在 CD3 的 `/linux_for_dummies` 目录下，你还会找到一个 README 文件，其中包含了本附录的文本和四个额外附录（名为 `BonusApp.pdf` 到 `BonusAppD.pdf`），以及一个指向书中所有 URL 的链接页面（名为 `links.html`）。

## 如果你遇到了问题（CD 类的故障）

我们尽力寻找可以在具有最低系统要求的多数电脑上运行的程序，Red Hat 对其操作系统也是如此。遗憾的是，你的电脑可能有所不同，某些程序由于某些原因无法正常工作。

两个最可能的问题是你为想要使用的程序没有足够的内存（RAM），或者你有其他程序正在运行，影响了它们的安装或运行。

两个 两个最可能的问题是你为想要使用的程序没有足够的内存（RAM），或者你有其他程序正在运行，影响了它们的安装或运行。

- 两个最可能的问题是你为想要使用的程序没有足够的内存（RAM），或者你有其他程序正在运行，影响了它们的安装或运行。

 两个最可能的问题是你为想要使用的程序没有足够的内存（RAM），或者你有其他程序正在运行，影响了它们的安装或运行。

# Linux傻傻指南，第3版

```
/usr/bin subdirectory, 228
/usr/etc directory, 55
/usr/games subdirectory, 228
/usr/include subdirectory, 228
/usr/lib subdirectory, 228
/usr/local subdirectory, 228
/usr/src subdirectory, 228
/usr/bin subdirectory, 228
/usr/share subdirectory, 228
/usr/X11R subdirectory, 228
/var directory, 227, 235
/var/log directory, 305
```

- 命令, 326

- tarball 包文件, 357

- 星号 (`*`), 121, 160

- 非对称数字用户线路 (`ADSL`), 349

- `at` 命令, 331

- `ATAPI` 标准, 22

- `atq` 命令, 331

- 自动分区, 42

# ● B ●

- `b` 文件类型, 140

- 备份, 312

- `badblocks` 命令, 331

- `basename` 命令, 331

- shell 环境

  - 修改环境, 182–186

  - 内置软件, 326

  - 命令语法, 180–182

  - 配置文件, 60

  - 描述, 60, 179, 349

  - 文件名/名称补全, 161

  - 登录会, 180

  - 管道, 182

  - 重定向, 181–182

- 批命令, 331

- 铃声动作, 293

- 贝尔实验室, 14

- 最佳 Linux, 299

- `bg` 命令, 331

- 二进制, 15

- `bind` 软件包, 114

- `BIOS` (基本输入/输出系统)

  - 启动, 75

  - 描述, 75, 349

  - 屏幕, 24

  - 设置, 24–25, 28

  - 另见 emacs text

- 臃肿软件, 194.

- 书签功能, Netscape, 131

- 启动盘, 51–52, 76–77, 360

- [方括号], 160

- `~` 目录, 55

- `~/.xsession` 文件, 60

- `~/.bash_profile` 文件, 61

# ● A ●

- `adduser` 命令, 85

- `ADSL` (非对称数字用户线路), 349

- `alias` 别命令, 331

- `alt.ext.sighting` 新闻组, 322

- `Amanda` 备份程序, 312

- 反病毒软件, 224, 364

- `Apache` Web 服务器, 210, 349, 55

- `APM` (高级电源管理), 304

- `AppleTalk` 协议, 216

- 小程序, 167, 170, 173–175, 349

- 应用

  - 手动添加, 97–99

  - 在 GNOME 中管理, 171, 175–176

  - 移除, 287–288

  - 故障排除, 99–100

- `Applizix` 套件, 201

- `Applizix Words`, 201

- `apropos` 命令, 331

- `ar` 程序, 331

- `arch` 命令, 331

- 归档

# 索引 369

- 启动分区, 81

- 启动提示符, 76–80, 303

- 启动脚本, 315

- `boot=device` 选项, 79

- 启动

  - 从 CD, 20, 25, 361

  - 从软盘, 20, 26, 28, 361

  - Linux, 73–74

  - 问题, 76–83

- Bourne Again shell. 另见 `bash` shell

- Bourne shell (`sh`), 179, 349

- `brousers`. 另见 Web browsers

- `bzip2` 工具, 331

- `cfdisk` 命令, 269–271, 273

- `chage` 命令, 332

- `chattr` 命令, 332

- `checkalias` 命令, 332

- `cfhn` 命令, 332

- `chgrp` 命令, 332

- `chmod` 命令, 149, 332

- `chown` 命令, 148, 332

- `chsh` 命令, 255, 332

- `clear` 命令, 332

- 客户端, 352

- `cmp` 命令, 333

- `code`. 另见 source code

- `col` 命令, 333

- `column` 命令, 333

- 命令提示符

  - 添加设备驱动程序, 94–97

  - 定义, 350

  - 与 GUI 对比, 163

  - Linux 工具, 66

  - 使用, 173

- 命令. 另见

  - 归档, 326

  - `bash` 内置, 326
