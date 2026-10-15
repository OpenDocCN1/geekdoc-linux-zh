
# 对象摘要

`Unix 文件系统`

正如你可以看到，发现了三个策略违规：

- 修改：`/root`
- 规则名称: `root` 配置文件 (`/root`)
- 严重性级别: 100
- 修改：`/.vmininfo`
- 规则名称: `Tripwire` 数据文件 (`/var/lib/tripwire`)
- 严重性级别: 100
- 添加：`/var/lib/tripwire/polo.twd`

# 错误报告

保持安全 481

`Unix 文件系统`

+ 文件系统错误。
文件名: `/usr/sbin/fixrmatab`
无此类文件或目录

`*** 报告结束 ***` `Tripwire` 2.3 版本 copyright 2000 `Tripwire`, Inc. `Tripwire` 是 `Tripwire`, Inc. 的注册商标。本软件不提供任何保证；详情见 `COPYING`。保留所有权利。完整性检查完成。

正如你看到的，发现了三个策略违规：`/var/lib/tripwire/polo.twd`（`Tripwire` 数据库）被添加，`/.vmininfo`（`Vim` 编辑器使用）被修改。作为结果，`/root` 目录也被修改，`Tripwire` 也报告了这一点。

# 更新数据库

在之前的示例中，你可以通过将 `.vmininfo` 设置为动态，或简单地忽略它来停止该警告：

如果你以后需要更新策略，明显的方法是编辑策略并重新运行 `twinstall.sh`。但是，这种方法并不高效（这意味着要重建整个数据库），`Tripwire` 提供了另一种方法，可以使用以下语法调用：

```bash
# tripwire --update policy.txt
```

# 结语

你可能注意到 `Tripwire` 与第 9 章涵盖的 ACL（访问控制列表）之间的强烈相似之处：两者都使用列出对象及其模式的数据库，但仍然存在根本区别。ACL 会主动阻止用户更改文件，而 `Tripwire` 仅在更改发生时发出警告。即使如此，如果管理员不执行完整性检查并查看生成的报告，他也不会发现任何违规。

# chrootkit

尽管很少这样描述，`chrootkit` (`http://www.chrootkit.org/`) 本质上是一个针对 rootkit 的病毒扫描器。正如我们在第 2 章讨论中提到的，病毒、蠕虫和 rootkit 之间的区别（尽管每个都有明确定义）在实践中可能会变得模糊，某些程序显示出三者的特征。因此，尽管 `chrootkit` 自称为 rootkit 扫描器，但你会发现它也能检测我们通常描述为蠕虫或病毒的程序。

截至目前，`chrootkit` 最新版本扫描 50 多个恶意程序，包括

- `LRK` (`Linux Rootkit`)
- `Törn`（见第 2 章）
- `Adore LKM`（见第 2 章）
- `Slapper` 蠕虫
- `Adore` 蠕虫（与 `Adore` rootkit 无关）

# 安装与用法

安装 `chrootkit` 非常简单。从 `http://www.chrootkit.org/` 获取最新的源码压缩包，解压并执行 `make` 和 `make install`。要扫描系统，只需启动 `chrootkit` 二进制文件即可：

484 `Linux` 网络安全

```bash
# chkrootkit

ROOTDIR = '/'

Checking `amd`... not found
Checking `basename`... not infected
Checking `biff`... not infected
Checking `chfn`... not infected
....
```

几分钟后，扫描将完成，你可以回溯输出内容寻找警告信息。与所有工具一样，误报是不可避免的；最好的解决办法是在安装操作系统后立即运行 `chkrootkit`。假设你信任该发行版没有后门——现在你将获得一个任何针对你系统特有的误报的列表。在随后的扫描中，你将能够区分误报和真正的 rootkit（根内核程序）。

# 专家模式

虽然 `chkrootkit` 是一个非常有用的工具，但它仅限于扫描其具有特征码的 rootkit，这意味着——和普通病毒扫描器一样——它总是落后检测器一步。为了应对这个问题，`chkrootkit` 提供了一个专家模式（使用 `-x` 标志），在此期间，会创建一个更详细的报告——包括对系统二进制文件运行 `strings` 命令的输出。你可能希望将输出重定向到文件中，以便稍后检查：

```bash
# chkrootkit -x > /root/scan.log
```

# 对可疑系统使用 Chkrootkit

`Chkrootkit` 使用了 `ps` 和 `netstat` 等常用系统工具，但许多 rootkit 会二进制文件替换为带有木马的副本；如果你在怀疑已被攻破的机器上运行 `chkrootkit`，这种技术是不准确的。

解决方案是在软盘、CD-ROM 或只读介质上制作此类实用程序的备份副本。然后你可以使用 `-p` 选项将此位置指定给 `chkrootkit`：

```bash
# chkrootkit -p /mnt/cdrom/bin
```

你需要复制给 `chkrootkit` 的二进制文件有 `awk`, `cut`, `echo`, `egrep`, `find`, `head`, `id`, `ls`, `netstat`, `ps`, `strings`, `sed` 和 `uname`；如果你发现自己试图调查被攻破的机器，可能会发现复制其他程序供自己使用很有用。考虑到 `/bin`、`/sbin`、`/usr/sbin` 和 `/usr/bin` 的体积较小，你应该能够轻松地将所有四个目录都放入一张 CD-ROM 中。

# 入侵检测

前述的工具检查本地文件系统的完整性，而入侵检测系统（IDS）则监控网络，寻找可能指示正在进行攻击的数据包序列。大多数 IDS 使用基于特征码的检测（监控已知漏洞利用的特征码）和异常检测（系统“学习”网络上的典型流量模式，然后记录任何偏离该模式的差异）的结合。需要注意的是，虽然许多 IDS 提供了阻止可疑数据包的功能，但这种行为并不是蕴含在定义之中的——在它的真正意义上，IDS 仅仅是检测，而不是防御。

最流行的 IDS 之一是 `LIDS`，你在第 9 章中读到过它。`LIDS` 已经不仅仅是一个 IDS 了，那时我们讨论了使用它来强制 ACL（访问控制列表）；然而，它提供了传统意义上的 IDS 功能。你只需要在配置了 IDS 补丁的内核时选择“内核端口扫描检测器”（`Port Scanner Detector in Kernel`），即可让 `LIDS` 检测并记录端口扫描。

# Snort

`Snort` 被亲切地称为“猪”（`pig`），是一个灵活的 IDS，也可以用作数据包嗅探器和记录器。`Snort` 可以从 `http://www.snort.org` 获取，随附的 CD-ROM 中可以版本 2.2.0。

### 安装

安装遵循通常的 `./configure;make;make install;`；如果你想记录日志到数据库（如 `MySQL`），输入 `./configure --help` 查看配置选项列表。安装后，创建 `/etc/snort` 目录，并将其复制到 `Snort` 源码中 `/etc` 目录下的 `Snort` 文件中。你还需要创建 `/var/snort` 目录供 `Snort` 存储：

```bash
# mkdir /etc/snort
# cp /home/peter/snort-2.2.0/* /etc/snort
# mkdir /var/snort
```
