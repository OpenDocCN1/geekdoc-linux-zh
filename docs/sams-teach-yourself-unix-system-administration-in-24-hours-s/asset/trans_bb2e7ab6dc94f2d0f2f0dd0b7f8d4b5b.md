
以我这位老手的眼光来看，其中很多都可疑地像是垃圾邮件，尤其是 liberty4success.com、poorrichardsenterprises.com 和 chequemail.com。由于你作为系统管理员，需要对你的用户社区负责，并确保人们遵守可接受使用政策（AUP），你最好还是调查一下这些邮件。

一种调查方式就是直接查找与这些邮件关联的收件人和发件人。这可以通过 grep 完成，特别是使用 `-B n` 标志，它表示你希望在每次匹配之前显示 n 行上下文。由于延迟查询总是针对收件人的，因此这很可能揭示我们需要的信息：

```
# mailq | grep -B1 -A1 liberty4
QAA17284      4657 Tue Mar 26 16:36 <lori@salesinminutes.net>
    (host map: lookup (Liberty4Success.com): deferred)
<Karen@Liberty4Success.com>
..
QAA15045      4657 Tue Mar 26 16:30 <lori@salesinminutes.net>
    (host map: lookup (Liberty4Success.com): deferred)
<Karen@Liberty4Success.com>
..
AAA18116      269 Tue Mar 26 00:06 ximinute
    (host map: lookup (Liberty4Success.com): deferred)
Karen@Liberty4Success.com
..
AAA27255      269 Mon Mar 25 00:04 ximinute
    (host map: lookup (Liberty4Success.com): deferred)
Karen@Liberty4Success.com
..
AAA27203      269 Sun Mar 24 00:04 ximinute
    (host map: lookup (Liberty4Success.com): deferred)
Karen@Liberty4Success.com
..
AAA00798      269 Sat Mar 23 00:05 ximinute
    (host map: lookup (Liberty4Success.com): deferred)
Karen@Liberty4Success.com
..
AAA20693      269 Fri Mar 22 00:04 ximinute
    (host map: lookup (Liberty4Success.com): deferred)
Karen@Liberty4Success.com
```

正如所料，这些消息中几乎每一封都是从 ximinute 发往 Karen@liberty4success.com。注意这些消息的时间：几乎都在午夜，分别是 3 月 22 日、3 月 23 日、3 月 24 日、3 月 25 日和 3 月 26 日。我怀疑是某个 cron 作业或类似的自动化邮件系统，并怀疑是某种垃圾邮件。如果我是这台机器的主要系统管理员，我会和这个用户谈谈，问问到底是怎么回事。

5. 另一种你可以采用的策略是进入实际的邮件排队区域，通常是 /var/spool/mqueue。那里会有大量文件，包括每个排队消息所对应的一堆配置和数据文件，如表 20.1 所述。

**表 20.1：mqueue 目录中常见的文件**

| 前缀 | 内容 |
| --- | --- |
| df | 消息正文 |
| Qf | 在消息被退回且无法返回时创建 |
| qf | 消息的头（控制文件） |
| tf | 尝试投递期间 qf 文件的临时版本 |
| Tf | 如果 52 次或更多次锁定尝试失败，则创建 |
| xf | 来自远程服务器的特定错误消息的文本记录 |

让我们创建一条简单消息，并仔细查看这些可能的文件：

```
# sendmail -O DeliveryMode=d -t
From: ximinute
To: Karen@Liberty4Success.com
Subject: fabulous offer

You are authorized to receive a fabulous offer...
#
```

这会立即将消息排队（这正是 DeliveryMode=d 的作用），然后我们就可以用 mailq 查看它在队列中的样子；在它的大量输出中，会显示：

```
g2R8OWC14928   50 Wed Mar 27 00:24 ximinute
Karen@Liberty4Success.com
```

默认情况下创建的两个文件是 df\* 和 qf\* 文件：

```
# cat df*
You are authorized to receive a fabulous offer...
# cat qf*
V4
T1017217472
K0
N0
P120
I8/18/26706
Fb
$_ximinute@localhost
Sximinute
Aximinute@staging.intuitive.com
RPD:Karen@Liberty4Success.com
H?P?Return-Path: <7g>
H?D?Date: Wed, 27 Mar 2002 00:24:32 -0800
H?M?Message-Id: <20020327...>
H??From: ximinute
H??To: Karen@Liberty4Success.com
H??Subject: fabulous offer
.
```

无需逐行详细说明 qf\* 文件中的每一行，只说它包含了所有消息头以及相当多的排队信息就够了。当投递尝试正在进行时，会创建一个空的 xfg2R8OWC14928 文件。

邮件队列目录 /var/spool/mqueue 中的实际文件可以揭示一些有趣的信息，并帮助你识别哪些用户可能在发送垃圾邮件，以及你是否存在开放中继或其他潜在问题。密切关注其内容是值得的。

![](img/5ced0c78d748bd190e9027e5549a3622_420_0.png)

> 不过，再次提醒你注意隐私问题：读取离开系统的每封电子邮件的内容是很容易的。然而，如果用户发现了，他们可能不会太高兴。

## 创建 sendmail 别名

我想，在深入探讨了 sendmail 程序的一些内部机制之后，你的脑袋可能已经有点晕了，所以我们来换一个更轻松的话题歇一歇：邮件别名。

这个概念相当直接——邮件别名不只是接受发往你系统上特定登录名的邮件，而是让你接受电子邮件并将其转发给另一台系统上的某个人、一组人、一个列有若干邮件地址的文件，甚至某个特定程序或文件。

![](img/5ced0c78d748bd190e9027e5549a3622_420_1.png)

> Mac OS X 有一种完全不同的邮件别名管理方式，通过 NetInfo 机制实现。这将在本课时的最后一节中介绍。

### 任务 20.3：邮件别名

最初的 sendmail 程序允许你设置指向多种不同目标的别名，包括文件、程序、远程地址，甚至电子邮件地址列表。最近几年，电子邮件领域在安全方面投入了更多精力，这最直接地影响了 sendmail——标准系统配置上可用的别名受到了更多限制。

在最后一节中，我们会快速了解一些更高级的别名；但如果你发现你的 Unix 操作系统默认阻止它们，并常常附带一条晦涩难懂的错误消息，也不要感到惊讶。

1. 最基本的别名是让一个不同的名称指向现有邮箱。这看起来似乎有点傻，但对于确保用户能收到发给他们的邮件却非常有用，无论发件人是否知道他们的具体登录名。

   例如，在我的服务器上，我的账户是 taylor，但如果你把邮件发给 dave 会怎样？默认情况下它会被退回。不过，这很容易修复，只需在 /etc/aliases 中添加以下内容：

   ```
   dave:  taylor
   ```

   我们要做的就这些；一旦用 newaliases 命令重建了别名文件，发往 dave 的邮件就会被正确投递到 taylor 的邮箱中。

   因此，许多站点会自动为给定名称添加常见的替代拼写作为别名，以确保退信尽可能少。如果新用户 Susan McGill 加入公司，可能会创建下面这一组别名：

   ```
   mcgill:    susan
   macgill:   susan
   smcgill:   susan
   susanm:    susan
   susan.mcgill: susan
   susan_mcgill: susan
   ```

   尤其注意第二个别名：因为我们预料到有些人会把 Susan 的姓氏拼错，所以很容易添加一个别名来确保发往 macgill@ourserver 的邮件能够正常工作。

2. 第二种别名是系统外的重定向：

   ```
   john:    john@aol.com
   ```

   在这种情况下，任何在本地系统上发送给 john 的邮件，无论他是否设置了账户，都会自动重定向到他的 AOL 邮箱。

3. 不过，有一种更好的方式来管理地址列表，那就是使用文件包含别名。这些别名看起来有点古怪，但事实证明它们极其有用：

   ```
   writers: :include:/home/taylor/writers.list
   ```

   在这种情况下，任何发送给 writers 的邮件都会被发送到指定文件中的每个电子邮件地址。每次发送消息时，文件内容都会被按需读取，因此如果在两次 newaliases 运行之间文件发生了变化，这些变化会立即生效。

   :include: 记法的真正优势在于，你的用户可以管理他们自己的邮件列表，而你不必去修改（也不用让他们修改！）实际的 /etc/aliases 文件。这可以大大简化你日常的系统管理任务！

4. 要重定向到文件，别名可以写成：

   ```
   archive: /private/mail/archive
   ```

   然而，由于安全问题，现在大多数 sendmail 配置都会禁用直接保存到文件的功能（尽管我实在想不出直接写入文件会有什么安全问题，除非你把类似 /etc/passwd 的文件当作归档文件——那样的话，你可以通过电子邮件发送一行类似 root::0:0::: 的内容，立刻获得超级用户登录权限）。

5. 另一种在 sendmail 安装中曾经广泛使用、但现在受到很大限制的机制，是让别名直接指向服务器上的某个程序。为了解决安全问题，现代 sendmail 安装现在包含一个特殊程序 smrsh，即 sendmail 受限 shell，它被明确用作一个安全的“沙盒”，用于运行作为别名一部分的程序。这个别名看起来像这样：

   ```
   ps: "|/bin/ps"
   ```

   如果你的安装带有良好的错误消息，那么向 ps 别名发送邮件的尝试会作为退回测试消息的一部分，产生以下信息：

   ```
   .... The following addresses had permanent fatal errors ....
   "|/bin/ps"
   (reason: service unavailable)
   (expanded from: toprog)
   .... Transcript of session follows ....
   smrsh: ps not available for sendmail programs
   554 5.0.0 "|/bin/ps"... Service unavailable
   ```

   注意倒数第二行中对 smrsh 的引用：我们原以为指定的是 /bin/ps，但 smrsh 自动去掉了路径部分，并在它自己的已知程序列表中查找 ps。

要了解如何配置 smrsh，以允许访问流行的 vacation 程序、filter、procmail 以及其他复杂的电子邮件过滤程序，请阅读 smrsh 手册页。

