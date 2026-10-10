
# `amanda.conf` 配置文件说明

```
# Specify tape device and/or tape changer. If you don't have a tape
# changer, and you don't want to use more than one tape per run of
# amdump, just comment out the definition of tpchanger.

runtapes 1 # number of tapes to be used in a single
# run of amdump
tapedev "/dev/nrft0" # the no-rewind tape device to be used
rawtapedev "/dev/rft0" # the raw device to be used (ftape only)

tapetype HP-DAT # what kind of tape it is
# (see tapes below)
labelstr "*DailySet[0-9]*" # label constraint all
# tapes must match

# Specify holding disks. These are used as a temporary
# staging area for dumps before they are written to tape and
# are recommended for most sites.

holdingdisk hdl {
# *.*
comment "main holding disk"
directory "/home/amanda" # where the holding disk is
use 290 Mb # how much space can we use on it
chunksize -1 # size of chunk
}

# Note that, although the keyword below is infofile, it is
# so only for historic reasons, since now it is supposed to
# be a directory (unless you have selected some database
# format other than the 'text' default)

infile "/usr/adm/amanda/normal/curinfo" # database DIRECTORY
logdir "/usr/adm/amanda*" # log directory
indexdir "/usr/adm/amanda/normal/index" # index directory

# tapetypes

# Define the type of tape you use, and use it in "tapetype"
# above. Some typical types of tapes are included here. The
# tapetype tells amanda how many MB will fit on the tape device, how
# big the filemarks are, and how fast the tape device is.

define type HP-DAT {
comment "DAT tape drives"
# data provided by Rob Browning <rlb@cs.utexas.edu>
length 1930 mbytes
filemark 111 kbytes
speed 468 kbytes
}

# dumptypes
# These are referred to by the disklist file.

define dump global {
comment "Global definitions"
# This is quite useful for setting global parameters, so you
# don't have to type them everywhere.
}

define dump always-full {
global
comment "Full dump of this filesystem always"
compress none
priority high
dumpcycle 0
}
```

# 第三部分 管理 OpenLinux

## 第14章 备份和恢复文件

这个示例 `amanda.conf` 是从 `Amanda` 源代码发行版 `examples` 中较大的示例精简而来的。与其从头开始输入配置文件，我建议你以该 `amanda.conf` 为起点并根据需要进行修改。

### 交叉引用

目录中的 `amanda.conf` 文件提供了有关可用配置选项的额外信息。此外，`Amanda` 的在线手册页也应该有所帮助。（输入 `man amanda` 来阅读它。）你可以在 `Amanda` 源代码目录的 `docs` 子目录中找到更多说明。

通常，你需要执行以下操作来修改 `amanda.conf` 文件：

- 修改报告的组织名称。

- 将为 `tapedev` 和 `rawtapedev` 指定的设备名称更改为与你的磁带设备相匹配。

- 选择适合你的磁带驱动器的磁带类型条目。

- 将 holding disk（`holdingdisk`）部分中指定的目录名称更改为你之前创建的目录。

### 创建 `disklist` 文件

你必须在 `/usr/local/etc/amanda/normal` 目录为 `Amanda` 创建一个 `disklist` 配置文件。该文件仅包含要备份的系统和磁盘分区的列表。限定符 `always-full` 包含在每个条目中，以告诉 `Amanda` 执行哪种类型的备份。它表示使用完整备份而不是增量备份。

```
# sample Amanda2 disklist file
# File format is:
# hostname diskdev dumptype [spindle][interface]
#
# where the dumptypes are defined by you in amanda.conf.

dexter hda5 always-full
dexter hda6 always-full
dexter hda7 always-full
dexter hda8 always-full

daffy hda5 always-full
daffy hda6 always-full
daffy hda7 always-full
daffy hdb1 always-full
daffy hdb2 always-full
```

此示例文件备份了两个系统，`dexter` 和 `daffy`。系统和分区的顺序是这样选择的，以便最重要的数据最先被备份。这样，如果磁带驱动器已满，你仍然设法备份了最重要的數據。

### `Amanda` 网络服务

`Amanda` 设计用于通过网络执行备份。因此，你需要在 `/etc/services` 和 `/etc/inetd.conf` 文件中添加一些新服务。在备份服务器和客户端系统上，都将以下行添加到 `/etc/services` 文件中：

| `amanda` | `10080/udp` |
|---|---|
| `amandaix` | `10082/tcp` |
| `amidxtape` | `10083/tcp` |

此外，在每个客户端工作站上，将以下行添加到 `/etc/inetd.conf` 中：

```
amanda dgram udp nowait root /usr/local/libexec/amandad amandad
```

这使 `Amanda` 能够连接到客户端系统并在无需用户干预的情况下启动备份过程。你需要在此更改生效前通知 `inetd` 守护进程重新加载 `inetd.conf` 文件。你可以通过 `kill` 命令向其发送 `HUP` 信号来实现。使用 `ps` 命令确定 `inetd` 的进程号，然后执行 `kill -HUP` 后跟进程号。

接下来你需要在 `/root` 目录中创建一个 `.amandosts` 文件。该文件应包含将连接到此客户端的任何备份服务器的完全限定主机和域名。例如，要在系统 `dexter.glaci.com` 上创建 `.amandosts` 文件以允许备份服务器 `ratbert.glaci.com` 连接，请执行以下操作：

```
echo ratbert.glaci.com > /root/.amandosts
chmod 600 /root/.amandosts
```

我使用 `chmod` 来更改文件的访问权限。这确保只有 `root` 可以读取或修改此文件。

### 执行 `Amanda` 备份

现在一切都已配置好，你可以执行 `Amanda` 备份了。以 `root` 身份登录后，输入以下命令：

`/usr/local/sbin/amdump normal`

这会运行 `amdump` 命令并指示它读取在 `/usr/local/etc/amanda/normal` 目录中找到的配置文件。它按 `disklist` 文件中系统和分区的列表顺序进行，备份每个分区。`amdump` 的结果写入 `/usr/adm/amanda/normal` 目录。阅读你在那里找到的文件以检查备份结果。（参见前面关于如何创建 `disklist` 文件的部分，以了解 `amdump` 所经历的过程。）

当然，你可以用 `cron` 来自动化此操作。要创建一个与前面章节中讨论的常规 `dump` 计划类似的 `amdump` 计划，请执行以下操作。以 `root` 登录，输入带 `-e` 选项的 `crontab` 命令：

```
crontab -e
```

这会在编辑器中打开 `root` 的 `crontab` 文件。将以下行添加到文件末尾：

```
0 22 * * 1 /usr/local/sbin/amdump normal
0 22 * * 2 /usr/local/sbin/amdump incremental
0 22 * * 3 /usr/local/sbin/amdump incremental
0 22 * * 4 /usr/local/sbin/amdump incremental
0 22 * * 5 /usr/local/sbin/amdump incremental
0 22 * * 6 /usr/local/sbin/amdump incremental
```

保存并退出文件。`cron` 守护进程现在将在每周每天的晚上 `10:00`（军用时间 `22:00`）运行 `amdump`。此示例假定已创建第二个增量配置。你可以通过在 `/usr/local/etc/amanda` 下创建 `incremental` 子目录并用适当修改的 `amanda.conf` 和 `disklist` 文件填充它来实现。

> 你还需要在 `/usr/adm/amanda` 下创建一个 `incremental` 子目录，以便 `Amanda` 有地方写入此配置的日志文件。

将其全部设置好可能需要一些工作，但一旦完成，`Amanda` 可以使你的网络备份更易于管理。对于小型办公室来说这可能有点过头，但在大型企业网络环境中，它使 `OpenLinux` 能够充当强大的备份服务器。

![](img/f0f494d795c6ea03cd25d687dd72914c_502_0.png)

### 摘要

建立一个适当的备份计划需要一些工作，但这项努力非常值得。希望你永远不会遇到主要的硬盘崩溃，但如果发生了，备份所付出的努力将得到数倍回报。把它当作一份保险政策。你希望永远用不到它，但在灾难发生时你会庆幸拥有它。

有多种低成本的备份硬件可与你的 `OpenLinux` 系统一起使用。传统的磁带驱动器是备份大量数据的绝佳选择。如果需要长期归档数据，可写 `CD` 驱动器是不错的选择。如果你的主要关注点是最小化停机时间，将数据镜像到第二块硬盘是另一个明智的选择。无论你选择哪种备份策略与 `OpenLinux` 系统一起使用，请确保选择一种并坚持使用。你已投入大量时间创建数据。再多投入一点来保护它安全。

## 第15章 计算机安全问题

随着互联网的增长，计算机和网络安全变得比以往任何时候都更重要。我们越来越多地听到恶意个人入侵世界各地企业和政府计算机系统的消息。媒体称这些人为黑客。这种描述并不完全准确。在业余爱好者和软件爱好者的亚文化中，黑客一词通常指的是某种特定的程序员。另一方面，破解者是指入侵计算机的人，通常是为了做恶意的事情。

本章描述了保护你的 `OpenLinux` 系统免受可能损坏你计算机的破解者侵害的方法。讨论的主题包括密码保护、网络过滤和安全审计。

### 定义黑客和破解者

简而言之，黑客是指富有创造性地编程并且通常纯粹为享受而编程的人。（大多数在 `Linux` 上工作的程序员在这个意义上都是黑客。）入侵计算机系统的人的正确术语是破解者。（请参阅本章后面“什么是黑客？”侧边栏。）

黑客和破解者之间的区别可能看起来是毫无意义的语义，但事实并非如此。如果你打算使用 `OpenLinux` 操作系统，你不可避免地会与 `Linux` 和 `OpenSource` 社区互动。如果你希望避免尴尬的社交失误甚至冒犯某人，了解这些术语的正确含义非常重要。

### 本章内容

- 定义黑客和破解者
- 使用密码保护
- 防范入侵
- 通过过滤网络访问保护你的计算机
- 使用防火墙保护你的网络
- 防范 `NFS` 漏洞
- 使用 `Tiger` 运行安全审计
- 从日志文件检测入侵
- 使用 `Tripwire` 检测被篡改的文件
- 使用加密技术
- 防范拒绝服务攻击
- 获取有关安全问题的更多信息

存在许多类型的 `cracker`，从专业的计算机罪犯到为寻求刺激而为之的业余爱好者。`cracker` 问题的发展与互联网的发展保持同步。一种新一代、年轻的 `cracker` 正在出现。这些青少年伪 `cracker` 并没有真正 `cracker` 那样的全部知识和技能，但他们可以访问日益增多的能够自动化破坏系统安全性的 `cracker` 工具。

通过使用真正有才华的 `cracker` 创建的程序和脚本，年轻人往往可以在不真正了解其工作原理的情况下入侵系统。由于他们通常年轻且主要依赖他人提供的工具，因此有时被称为 `script kiddies`。不要弄错了，如果你的系统没有得到妥善保护，`script kiddies` 造成的破坏与任何其他 `cracker` 一样严重。

### 什么是黑客？

《`Jargon File`》(`http://www.tuxedo.org/~usr/jargon/`) 将 `hacker` 定义如下：

`hacker` `n.`

[最初，指用斧头制作家具的人]

- 1. 一个喜欢探索可编程系统的细节以及如何发挥其能力的人，而大多数用户则只愿意学习必要的最低限度内容。

- 2. 一个热爱编程（甚至痴迷）的人，或是喜欢编程而不是仅仅空谈编程的人。

- 3. 一个能够欣赏 `hack` 价值的人。

- 4. 一个编程速度很快的人。

- 5. 对特定程序很精通的人

- 6. 任何领域的专家或爱好者。例如，可能是一名天文学黑客。

- 7. 一个喜欢在智力上创造性地克服或规避限制的挑战的人。

- 8. [已弃用] 一个恶意窥探者，试图通过四处探查来发现敏感信息。因此有密码黑客、网络黑客。这一含义的正确术语是 `cracker`。

无论你怎么称呼他们，`crackers` 对任何将计算机连接到互联网的人都构成严重风险。他们入侵系统的动机各不相同：有些人希望窃取财务信息，而另一些人则希望在同行中获得炫耀的资本。经常，一个系统只是被攻破，以便用作发起对其他系统进一步攻击的跳板。有时 `cracker` 会向网站发送大量请求，使其无法处理（这种做法被称为拒绝服务攻击，迅速关闭了多个主要电子商务网站）。在某些情况下，造成的损害可能只是被篡改的网页，相当于互联网上的涂鸦。在其他情况下，`cracker` 可能会抹去你的整个硬盘以掩盖她的或他的踪迹。幸运的是，有办法保护自己。本章将向你展示其中的一些方法。

### 使用密码保护

密码是任何现代操作系统的最基本安全工具，因此也是最常被攻击的安全特性。选择容易记住的密码很自然，但这通常意味着选择也容易猜到的密码。`Cracker` 知道在任何拥有不到一百名用户的系统上，至少有一人很可能拥有容易猜到的密码。

通过使用“暴力”方法尝试登录系统上的每个账户并在每个账户上尝试最常见的密码，坚持不懈的 `cracker` 有很大的机会找到进入的方法。记住，`cracker` 会自动化这种攻击，因此数千次登录尝试并非不可能。显然，选择良好的密码是你拥有安全系统的第一步，也是最重要的一步。

以下是选择密码时应牢记的一些规则：

- 不要使用登录名或全名的任何变体。即使你使用大小写变化，附加或前置数字或标点符号，或将其倒写，这仍然是一个容易猜到的密码。

- 不要使用字典单词，即使你向其中添加数字或标点符号。

- 不要使用任何类型的专有名词。

- 不要使用键盘上任何连续的一行字母或数字（例如 `qwerty` 或 `asdfg`）。

### 选择良好的密码

选择强密码的一个好方法是取一个容易记住的句子的每个单词的首字母。密码可以通过添加数字、标点符号和大小写变化变得更好。你选择的句子对你有意义，并且不应公开可用。（在你的个人网页上选择句子是个坏主意。）表 15-1 列出了强密码的示例以及记住它们的技巧。

不要使用下面所示的任何字面密码。一旦密码被发布，它通常会被添加到密码破解字典中。最好选择对你有意义的密码。

### 表 15-1 良好密码的思路

| 密码 | 如何记住它 |
|---|---|
| `Mrci7yo!` | My rusty car is 7 years old! |
| `2EmBp1lb` | 2 elements make BAD pets, 1 is better |
| `ITMc7Gib` | Is that MY coat? Give it back |
