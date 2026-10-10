
- `siggen` (8) - Tripwire 签名收集程序

- `tripwire` (8) - Unix 系统文件完整性检查器

- `twadmin` (8) - Tripwire 管理实用工具

- `twconfig` (4) - Tripwire 配置参考

- `twfiles` (5) - Tripwire 和备份过程使用的文件概述

- `twintro` (8) - Tripwire 软件介绍

- `twpolicy` (4) - Tripwire 策略参考

- `twprint` (8) - Tripwire 数据库和报告打印机

关于本页面的意见和建议请邮件至 `gmourani@videotron.ca`

# 运行完整性检查

完整性检查（Integrity Check）模式会将当前文件系统对象与 Tripwire 数据库中记录的属性进行比较。违规项将打印到标准输出（`stdout`）；报告文件将被保存，之后可以通过 `triprint` 访问。

完整性检查模式的语法为：

```
[root]@deep]# tripwire --check
```

- 要运行完整性检查模式，请使用命令：

```
[root]@deep]# tripwire --check
```

你可以在交互检查模式（Interactive Check mode）下运行 Tripwire。在交互模式下，你可以通过终端自动更新更改。添加 `-interactive` 语法后生成的报告将在编辑器中打开以更新数据库。

- 要以交互检查模式运行，请使用命令：

```
[root]@deep]# tripwire --check--interactive
```

邮件选项允许你发送电子邮件。使用 `[-email-report]` 选项运行 Tripwire，可以指定将报告发送给策略文件中列出的接收者，并使用默认配置文件中的选项。

- 要运行完整性检查模式并向接收者发送邮件，请使用命令：

```
[root]@deep]# tripwire --check--email-report
```

# 在完整性检查后更新数据库

数据库更新模式（Database Update mode）允许你在完整性检查后更新 Tripwire 数据库，前提是发现的违规项是有效的。此过程通过允许你在无需重新生成的情况下更新数据库来节省时间；更重要的是，它允许进行选择性更新，这种更新可以通过重新生成来实现。在我们的 `tripwire` 配置中，配置文件使用基于时间的变量指定报告文件名，因此报告不会处于常规模式。这是因为 `$(DATE)` 变量已经发生变化以反映当前时间。为了解决这个问题，必须在命令行上使用 `-r` 或 `-twistle` 参数指定报告文件。

数据库更新模式的语法为：

```
[root]@deep]# tripwire --update -r
```

- 要更新数据库，请使用命令：

```
[root]@deep]# tripwire --update -r /usr/TSS/report/deep.openarch.com-200001-021854
```

其中 "r" 指定报告文件（`deep.openarch.com-200001-021854.twr`）。该选项是配置文件中 `REQUIRED_REPORT` 变量 `$(DATE)` 所要求的。

注意：在数据库更新模式或交互检查模式下，Tripwire 显示报告时会在每个策略违规项旁边显示一个选择框。你可以通过在每个策略违规项旁保留 "x" 来批准对系统的更改。如果你删除了选择框中的 "x"，数据库将不会更新该对象的新值。在你退出编辑器并提供本地口令后，Tripwire 软件将更新并保存数据库。

关于本页面的意见和建议请邮件至 `gmouraoui@videotron.ca`

# 更新策略文件

你可以更改策略文件中的规则，这将改变 Tripwire 软件扫描系统的方式，并在无需完全重新初始化的情况下更新数据库。这可以节省大量时间；更重要的是，它通过保持策略文件与数据库同步来维护安全性。

策略更新模式的语法为：

```
[root@deep]# tripwire --update-policy /path/to/new/policy/file
```

- 要更新策略文件，请使用命令：

```
[root]@deep]# tripwire --update-policy /usr/TSS/policy/newtripwpol.txt
```

默认情况下，策略更新模式以 'secure-mode high' 运行。如果自上次数据库更新以来文件系统发生了变化，且这些更改仍导致策略中的违规，则在 във安全模式下运行时可能会遇到错误。例如，如果在策略更新过程中有另一个进程正在修改文件，就可能发生这种情况。为了适应这种情况，在确定高安全模式下报告的所有违规都是授权的后，你可以在低安全模式下更新策略文件：

- 要加载低安全模式下更新策略文件，请使用命令：

```
[root]@deep]# tripwire --update-policy --secure-mode /usr/TSS/policy/newtripwtxt
```

# 安装文件

| 路径 A | 路径 B |
| :--- | :--- |
| `/usr/TSS` | `/usr/TSS/key/deep.openarch.com.key` |
| `/usr/bin` | `/usr/man` |
| `/usr/bin/siggen` | `/usr/man/man4` |
| `/usr/bin/twprint` | `/usr/man/man4/twconfig.4` |
| `/usr/bin/tadmin` | `/usr/man/man4/twpolicy.4` |
| `/usr/bin/tripwire` | `/usr/man/man5` |
| `/usr/bin/twcg.txt` | `/usr/man/man5/twifiles.5` |
| `/usr/bin/tw.cfg` | `/usr/man/man6` |
| `/usr/policy` | `/usr/man/man8/siggen.8` |
| `/usr/TSS/policyguide.txt` | `/usr/man/man8/tripwire.8` |
| `/usr/TSS/policywpol.txt` | `/usr/man/man8/twintro.8` |
| `/usr/TSS/policywtpol.bak` | `/usr/man/man8/tripprint.8` |
| `/usr/report` | `/usr/README` |
| `/usr/TSS/db` | `/usr/Release_Notes` |
| `/usr/TSS/key` | `/usr/License.txt` |
| `/usr/TSS/key/site.key` |  |

# Linux Tripwire ASR 1.3.1

### 概述

随着日益复杂和微妙的攻击出现，需要工具辅助检测文件未经授权的修改变得变得非常明确。Tripwire 是一种帮助系统管理员和用户监控指定文件集任何变化的工具。通过对系统文件进行定期（例如每日）使用，Tripwire 可以通知管理员已损坏或被篡改的文件，以便及时采取控制措施。

© Copyright 1999 Open Network Architecture ®

819

关于本页的意见和建议请邮寄至 `gmouriani@videotron.ca`

`chmod` 命令将 "tripwire" 目录的默认模式更改为 700 (`drwx------`)，仅允许超级用户 "root" 读取、写入和执行。它将使二进制文件 `/usr/bin/tripwire` 仅允许超级用户 "root" 读取和执行 (`-r-x--`)，并最终使 `/usr/bin` 目录下的 "sigen" 程序允许被 "root" 执行和读取。

`rm` 命令将删除 `/usr/sbin` 下的 "tw.config" 文件。我们不再需要这个文件，因为我们在 `/etc` 目录下已经创建了一个新的。

# 工作后的清理

```
[root@deep]# cd /var/tmp
[root@deep]# rm -rf tw_AS_VERSION/ Tripwire-version.tar.gz
```

`rm` 命令将删除我们用于编译和安装 Tripwire 的所有源文件。它还将删除来自 "var/tmp" 目录的 Tripwire 压缩包。

# 配置

我们在书籍"Linuxos.pdf"中描述的所有软件都将在名为 "floppy.tgz" 的压缩包中拥有特定的目录和子目录，其中包含特定程序的的配置文件。如果你使用此文件，你就不需要手动重现配置文件的差异，或将它们剪切粘贴到你的配置文件中。无论你决定复制配置文件，还是从压缩文件中根据你的方便进行其他更改，修改、根据你的需求进行调整并将文件放置到 Tripwire 软件在服务器机器上的适当位置将是你的责任，如下所示。服务器配置文件归包位于以下互联网地址：http://pages.infinit.net/lotus/doc/opt/floppy.tgz

- 运行 Tripwire 需要以下文件，必须将它们复制或拷贝到服务器适当的目录。

- 将 `tw.config` 文件复制到 "etc" 目录。
