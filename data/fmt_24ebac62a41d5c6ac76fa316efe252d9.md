
ext2 系统的其他有趣的特性（例如删除删除属性）尚未实现，但在未来的 ext2 文件系统版本中将可用。如果你开始使用 `chattr` 命令，有时你会发现无法修改或删除某个文件，尽管你有权限。这是因为你忘记了使用 `chattr` 设置了文件的不可变属性，该属性不会显示在 `ls` 输出中。要查看哪些文件具有 ext2 属性，你可以使用 `lsattr` 程序。

不幸的是，你关于文件和文件系统安全的知识可能也被知情的坏人所知。使用像 `chattr` 这样的工具让你

# 第六部分：安全与监控

对于坏人来说，这变得稍微困难了，但并没有让破坏你的文件或文件系统变得不可能。事实上，如果坏人获得了 root 级权限，ext2 属性将变成一个简单的“躲迷猫”游戏。入侵后，一个主要问题是确定你是否还能信任你的文件。你可能会怀疑坏人是否安装了木马程序，或嵌入了病毒来感染新文件，并提供访问你使用的其他计算机的权限。我提到的关于这类安全问题的解决方法都没有解决它。不过，解决方案是运行像 Tripwire 这样的文件完整性检查程序。

## 使用 Tripwire 确保文件完整性

简单来说，Tripwire 是一个文件和目录完整性检查工具，它为所有文件和目录创建一个签名数据库并将其存储在单个文件中。当再次运行 Tripwire 时，它为当前的文件和目录计算新签名，并与存储在数据库中的原始签名进行比较。如果存在差异，将报告该文件或目录名称以及有关差异的信息。

现在你可以看到为什么 Tripwire 可以成为帮助你判断入侵期间哪些文件被修改过的绝佳工具了。当然，你必须确保应用程序所需的数据库的安全。在设置新服务器系统时，许多经验丰富的系统管理员会执行以下操作：

- 1. 确保新系统未连接到任何网络，以保证没有人已经安装木马程序、病毒程序或类似东西。
- 2. 运行 Tripwire 为所有重要的系统文件创建签名数据库，包括所有系统二进制文件和配置文件。
- 3. 将数据库写入可刻录的 CD-ROM。这确保了高级坏人无法修改 Tripwire 数据库来隐藏木马和被修改的文件，以免被应用程序发现。监控文件较少的管理员通常使用软磁盘存储数据库。将数据库写入软磁盘后，管理员会对磁盘进行写保护，并在 BIOS 允许的情况下，将驱动器配置为只读设备。
- 4. 设置一个 `cron` 作业（定时任务）定期（每日、每周、、每月）运行 Tripwire，以便应用程序使用 CD-ROM 版本的数据库。

现在你可以使用 Tripwire 获得同级别的安全保障。方法如下：

安装 TRIPWIRE 由 Red Hat 销售的官方发行版（盒装版）包含一个应用程序 CD，其中包含一个版本的 Tripwire。该版本适用于单 CPU 终端用户设置。该软件以

# 第 18 章：安全基础

两个独立的 RPM 包提供——一个包含二进制发行版，另一个包含源码发行版。除非你对编译自己的副本感兴趣，否则可以使用二进制发行版。通常，如果可以，我会编译安全软件，因为 Red Hat 在其产品中封装了该软件，我对他们的专业性有一定程度，我将在这里讨论二进制安装。

和通常一样，二进制安装非常简单；你只需要按照如下方式运行 `rpm` 命令：

```
rpm -ivh tripwire_package.rpm
```

请将 `tripwire_package.rpm` 替换为适用于你系统架构的 RPM 包。一旦安装了 Tripwire，你可以运行 `-ql tripwire_package.rpm` 来查找文件的安装位置。Tripwire 1.3 版本的默认安装路径为 `/usr/local/bin/tw`。

我注意到包含 Tripwire 二进制版的 RPM 包没有包含任何帮助页（man pages）。然而，我在源码发行版中找到了帮助页。你应该安装 Tripwire 的源码 RPM 发行版，它也包含在 Red Hat 附带的应用程序 CD 中。使用 `rpm` 安装源码后，你可以将 `/usr/src/redhat/SOURCES` 中的源码提取到适当的位置以访问帮助页。如果你想安装帮助页，请遵循以下步骤：

- 1. 在目录中解压源码发行版 tar 文件，并进入 `man` 子目录。
- 2. 编辑 `man` 目录下的 `Makefile`，在顶部的注释行之后添加 `AND MANDIR = /usr/man`。
- 3. 执行 `make` 将帮助页安装到系统中相应的帮助页位置。

一旦完成这些步骤，你就可以访问 `siggen (8)`、`tripwire (8)` 和 `tw.config (5)` 帮助页了，在继续使用 Tripwire 之前你应该阅读它们。

现在让我们看看如何为你的系统配置 Tripwire。

## 创建 TRIPWIRE 数据库

要让 Tripwire 运行起来的首要任务是为你想要比较的所有文件和目录创建一个签名数据库。为此，你必须在名为 `tw.config` 的配置文件中指定文件和目录，该文件也存储在 `/usr/local/bin/tw` 目录下。RPM 版本的配置文件是为 Linux 系统定制的。在阅读 `tw.config` 帮助页并理解其语法后，你应该对其进行修改。示例 18-6 显示了我在 Red Hat Web 服务器系统使用的 `tw.config`。

### 582 第六部分：安全与监控

#### 列表 18-6：tw.config 文件示例

```
# $Id: tw.conf.linux,v 1.1 1994/04/04 00:34:03 gkim Exp $

#

# last updated: 1998/04/17 genek

# tripwire.config for linux mahcines

# 首先，root 的 "home"

/root R

 / R

# 关键启动资源

/boot R

# 关键目录和文件

/etc R

/etc/config R

/etc/inetd R

/etc/group R

/etc/motd R

/etc/passwd R

/etc/rc.d R

/etc/exports R

# 关键启动资源

/boot R

# 关键目录和文件

/etc R

/etc/config R

/etc/inetd R

/etc/group R

/etc/motd R

/etc/passwd R

/etc/rc.d R

/etc/exports R

# 关键目录和文件

/etc R

/etc/config R

/etc/inetd R

/etc/group R

/etc/motd R

/etc/passwd R

/etc/rc.d R

/etc/exports R

# 关键启动资源

/boot R

# 关键目录和文件

/usr/local/bin R

/usr/local/usr/local/sbin R

/usr/local/bin R

/var/log R

/var/spool/cron R

/var/spool/queue R

/var/spool/mail R

/var/spool/lock R

/var/spool/tripwire R
```

（后续重复内容已省略）

## 第 18 章：安全基础

来自 Xerox 的 Snefru、循环冗余校验（CRC-32）、CRC-16、MD4、MD2、安全哈希算法（SHA）以及 Haval。

在大型文件系统中，对每个文件执行所有这些算法将消耗大量的 CPU 资源并花费很长时间。为了减少系统负载并加快检查过程，你可以告诉 Tripwire 忽略一个或多个此类算法。例如：

```
./tripwire -i 1
```

这里 Tripwire 被告知要忽略第一种算法 MD5。只要你知道算法对应的数字，就可以使用 `-i` 命令行选项来忽略任何算法。数字与算法的映射如表 18-9 所示。

表 18-9 TRIPWIRE 算法

| -i 选项 | 签名算法 |
|---|---|
| -i 0 | 空签名 |
| -i 1 | MD5 |
| -i 2 | Snefru |
| -i 3 | CRC-32 |
| -i 4 | CRC-16 |
| -i 5 | MD4 |
| -i 6 | MD2 |
| -i 7 | SHA |
| -i 8 | Haval |
| -i 9 | 空签名（预留未来） |

要在不进行任何签名完整性检查的情况下定位新文件或缺失文件，运行：

```
./tripwire -i all
```
