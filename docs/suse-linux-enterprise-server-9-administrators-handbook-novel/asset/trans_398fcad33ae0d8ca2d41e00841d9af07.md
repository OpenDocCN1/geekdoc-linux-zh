
它所知道的所有可执行文件并生成一份冗长的发现报告。以下是该报告的部分内容。

```
Athena: ~ # ./chkrootkit
ROOTDIR is '/'
Checking `amd'... not found
Checking `basename'... not infected
Checking `biff'... not found
Checking `chfn'... not infected
Checking `chsh'... not infected
Checking `cron'... not infected
Checking `date'... not infected
Checking `du'... not infected
Checking `dirname'... not infected
Checking `echo'... not infected
.
.
.
Searching for Hidrootkit's default dir... nothing found
Searching for t0rn's default files and dirs... nothing found
Searching for t0rn's v8 defaults... nothing found
Searching for Lion worm default files and dirs... nothing found
Searching for RSHA's default files and dirs... nothing found
Searching for RH-Sharpe's default files... nothing found
.
.
.
Searching for LPD Worm files and dirs... nothing found
Searching for Ramen worm files and dirs... nothing found
Searching for Maniac files and dirs... nothing found
Searching for RK17 files and dirs... nothing found
Searching for Ducrootkit... nothing found
Searching for Adore Worm... nothing found
.
.
.
Checking `lkm'... chkproc: nothing detected
Checking `rexecd'... not infected
Checking `sniffer'... eth0: PF_PACKET(/usr/bin/snort)
Checking `w55808'... not infected
Checking `wted'... chkwtmp: nothing deleted
Checking `scalper'... not infected
Checking `slapper'... not infected
Checking `z2'... chklastlog: nothing deleted
Checking `chkutmp'... chkutmp: nothing deleted
```

在 Athena 上生成的报告中，产生了超过 100 行输出。正如从此列表中可以看到的那样，机器是干净的。正如预期的那样，嗅探器检查发现 eth0 处于混杂模式，并且负责的二进制文件是 `/usr/bin/snort`。由于我们知道 Snort 正在运行，因此这不是问题。如果我们发现了意外的东西，这可能表明发生了入侵。

chkrootkit 实用程序在检测许多已知后门方面非常有用。它还可以查找本节中所示嗅探器示例等后门的已知行为。然而，它无法保证超出其设计范围的其他修改的保护。

## 高级入侵检测环境（AIDE）

诸如 chkrootkit 之类的工具在检测它们被设计为检查的应用程序中的更改方面非常出色。然而，由于新的后门技术不断被开发，这类对策永远在追赶。

检测系统未经授权更改的一种方法是定期对其内容进行快照。随着时间的推移比较这些快照可以提供更改的时间推移重建。诸如高级入侵检测环境（AIDE）之类的应用程序采用了这种方法。

## Tripwire

Linux 上可用的第一个 HIDS 产品之一称为 Tripwire。有免费和商业版本可用。此工具的免费版本包含在 SLES 发行版中。

该产品基本上提供了与 AIDE 相同的功能。然而，它是跨平台的。根据您站点的架构，您可能会决定想要一个适用于所有平台的通用工具。在这种情况下，Tripwire 将是一个理想的候选者。有关 Tripwire 工具的更多信息可从网站 `http://www.tripwire.org` 获得。

AIDE 实用程序是一个文件完整性检查器。它不知道不同的攻击算法或后门如何植入系统。然而，它确实知道如何跟踪文件并注意到是否进行了更改。

诸如 AIDE 之类的工具的主要优势在于它们检测模式变化的能力。当系统从已知、可信的媒体构建时，可以认为它是安全且未被利用的。一旦机器连接到网络，它就可能容易受到利用。在公开系统之前，您必须记录文件的选定特征。因此，您将知道它们在 pristine 状态下是什么样子的。定期，您可以将实时系统的相同特征与时间零快照进行比较。属性的变化可能反映了机器被入侵。

这基本上就是 AIDE 允许您执行的操作。AIDE 的行为通过其配置文件 aide.conf 控制，其中包含三种不同类型的指令。

第一种行类型可用于设置多个配置选项。通过这些选项，您可以设置 database、database_new 和 report_url 的路径值。将这些值定义在配置文件中意味着它们不必在命令行上定义。

宏行允许您指定简写形式，以定义将为每个文件记录哪些特征。诸如权限、inode、所有权、时间戳和文件哈希值等属性可以注册到 AIDE 数据库中。

最后一种行类型包含有关哪些目录结构部分将存在于 AIDE 数据库中的指令。目录使用正则表达式包含在列表中。这些表达式可以允许忽略目录的部分甚至特定文件。

以下是随 SLES 提供的位于 /etc 目录中的默认 aide.conf 文件的一部分：

```text
#
#  AIDE _Example_ Configuration
#
# Configuration parameters
#
database=file:/var/lib/aide/aide.db
database_out=file:/var/lib/aide/aide.db.new
verbose=1
report_url=stdout
warn_dead_symlinks=yes

#
# Custom rules
#
Binlib        = p+i+n+u+g+s+b+m+c+md5+sha1
ConfFiles     = p+i+n+u+g+s+b+m+c+md5+sha1
```

```text
#
# Directories and files
#
# Kernel, system map, etc.
/boot                              Binlib

# watch config files, but exclude, what changes at boot time,
#... /etc/mtab
/etc/vm*                           ConfFiles

# Binaries
/bin                               Binlib
/sbin                              Binlib

# Libraries
/lib                               Binlib

# Complete /usr and /opt
/usr                               Binlib
/opt                               Binlib
```

在此示例中，您可以清楚地看到预定义了许多命令行参数的位置。此外，还创建了 Binlib 宏以标识我们希望 AIDE 跟踪的文件属性。AIDE 能够跟踪的属性列表显示在表 12.3 中。

**表 12.3**  
跟踪 AIDE 属性

| 属性 | 描述 |
|---|---|
| P | 权限 |
| I | 索引节点 |
| N | 链接数 |
| U | 用户 |
| G | 组 |
| S | 大小 |
| B | 块计数 |
| M | 修改时间（mtime） |
| A | 访问时间戳 |
| C | 创建时间（Ctime） |

**表 12.3**  
**跟踪 AIDE 属性（续）**

| 属性 | 描述 |
|---|---|
| `md5` | 为文件创建 MD5 校验和 |
| `sha1` | 为文件创建 sha1 校验和 |
| `rmd160` | 为文件创建 rmd160 校验和 |
| `tiger` | 为文件创建 tiger 校验和 |
| `R` | p+i+n+u+g+s+t+m+c+md5 组合的简写形式 |
| `r` | p+i+n+u+g 组合的简写形式 |
| `E` | 检查空组 |
| `>` | p+u+g+i+n+s 组合的简写形式 |
| `crc32` | 创建 crc32 校验和（如果启用了 mhash） |
| `haval` | 创建 haval 校验和（如果启用了 mhash） |
| `gost` | 创建 gost 校验和（如果启用了 mhash） |

AIDE 可以以四种不同的模式调用，如表 12.4 所列。

**表 12.4**  
**AIDE 运行时模式**

| 模式 | 描述 |
|---|---|
| `--check` | 对 AIDE 数据库执行完整性检查 |
| `--init` | 基于 aide.conf 配置创建初始数据库 |
| `--update` | 允许将对系统内容的批准更改接受到数据库中 |
| `--compare` | 检查由配置文件中 database_new 和 database 参数指向的数据库之间的差异 |

`--init` 版本的 AIDE 只需运行一次。它创建初始数据库。随后对 AIDE 的调用应使用 `--check` 选项。例如，在配置 AIDE 并初始化数据库后，我们手动更改了系统中的一个文件。当我们运行检查阶段时，AIDE 生成了以下内容：

```
Athena:/var/lib/aide # aide -C
AIDE found differences between database and filesystem!!
```
