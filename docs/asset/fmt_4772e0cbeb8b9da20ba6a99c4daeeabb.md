
Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42

Jan 06 07:20:58 testv1.both.org systemd[1]: sysstat-collect.service: Deactivated successfully

Jan 06 07:20:58 testv1.both.org systemd[1]: Finished sysstat-collect.service. activity accounting tool.

此输出显示了（其他内容外）针对 `Uid 1000` 的临时文件清理。与单个用户相关对于定位源自用户空间的问题根源可能很有帮助。我在这里发现了一些有趣的条目。在你的虚拟机上试一下，看看你会发现什么。

在实验一段时间后，将 root 的主目录设置为当前目录（`pwd`）。

# 添加你自己的日志条目

将你的条目添加到日志可能是很有用的。例如，你可能想在日志中记录程序到达的检查点。

（注：此处原文有重复或乱码，已按要求处理翻译）

这有助于解决问题。向日志中添加条目可以通过 `systemd-cat` 程序实现，它允许我们将命令或程序的标准输出（STDOUT）管道到日志中。

## 实验 9-5：向日志添加条目

此命令可以作为命令行管道的一部分或在脚本中使用。

```
# echo "Hello world" | systemd-cat -p info -t myprog
```

`-p` 选项指定优先级，"emerg"、"alert"、"crit"、"err"、"warning"、"notice"、"info"、"debug" 或代表每个命名级别的 0 到 7 之间的值。这些优先级值与 `syslog(3)` 定义相同。默认为 "info"。`-t` 选项是一个标识符，可以是任意字符串或脚本名称。此字符串可以使用 `journalctl` 命令进行搜索。

列出日志中最近的五个条目。

```
# journalctl -n 5
```

Jan 06 07:20:58 testv1.both.org systemd[1]: sysstat-collect.service: Deactivated successfully

Jan 06 07:20:58 testv1.both.org systemd[1]: Finished sysstat-collect.service. activity accounting tool.

Jan 06 07:20:58 testv1.both.org systemd[1]: SERVICE_START pid=1 uid=0 audit=42 ...（此处省略重复的日志输出，仅保留格式）

打开终端并将权限提升到 root。将 `/var/log/journal/<Your-Journal-directory>` 设置为当前目录，并查看 journal 目录下的文件。我的虚拟机上只有一个 journal 目录，但其中包含的文件可以追溯到三个月前。

```bash
# cd /var/log/journal/d1fbbe4122942289e5ed31a256200fb
```

```bash
[root@studentvm1 d1fbbe41229942289e5ed31a256200fb]# ls
```

```
system@0005f2b035b55c5c-a2dd8b6d3f7880~journal~
system@0005f2b0d45b1e40-35014cf9aedfbd8d0~journal~
system@0005f2b0d95f2a92364aadef5f5~journal~
system@0005f2b0fba23a6f4-376b000f61d8ac3~journal~
system@0005f2b13b6495c-2888d80cf01e173~journal~
system@0005f2b8d01f6b11-36122a575e54d385~journal~
system@0005f2b8eaf61ac9-309271fcecbcb11~journal~
system@0005f2b890329031c-d4bef84a7bdce922~journal~
system@0005f2ff9e4c5cdc-e12ef2f3a72fc765~journal~
system@0005f301c088bf9c-798178d0ef04a0fd~journal~
system@0005f327d35a4452f-45f91713c44c9cfd~journal~
system@0005f404e20611b09e4-608976ba4103dc2~journal~
system@0005f4a1e1e66b3d-cc6c841ae65f9351~journal~
system@0005f42ae53ef53c-65998ea6a38a3f~journal~
system@0005f431322b924b4-831c67531a6dd1~journal~
system@0005f4531130b09e4-6608463d876ae956~journal~
system@0005f4d7e9c1d4a-80c25a844c8aec6d~journal~
system@0005f56f5bd92641-f89a914425992ef~journal~
system@0005f5b08a16a1f8-309c5feb66b753c~journal~
system@0005f5b03b6e5881-a88dc053297c43197~journal~
system@0005f5fe836012c6-d66e03272713f47b~journal~
system@0005f637ce5e849a-330fd866eb58a62e~journal~
system@0005f692da4392-3e18a3f8e0bc69.journal~
system@0005f6c94576a2-f314d048307ac93.journal~
system@0005f6ca18260eb-8c7931d198593b6.journal~
system@0005f6ca2857111d-ea8996c255b04c5f.journal~
system@0005f7401797d2f2-5ec9901d0977a51.journal~
system@0005f768496af63c2-672a972fa95262ce.journal~
system@0005f8071a1af64-97ce4806260eed8.journal~
system@0005f3a336b92c29473851e3687ea888-00000000000-0005f69c1adc2.journal
system@0005f4a3f3f82e284a5b215fe84a1bb0-0000000000-0005fc6a24003fb.journal
system@0005f4e3e32982e45bd6572e1b692e-0000000000-0005f80712541.journal
user-1000@0005f43566e0a41-96c8a31073bc54.journal
user-1000@81e2499c0df450b25113e2d8800000000008aa3566e84c.journal
user-1000@81e2499c0df450b251bf3e2d88-0000000000006a0055f6b55da2.journal
user-1000@81e2499c0df450b251bf3e2d88-000000000000f1480005f73a7664013.journal
user-1000@1c165b49f11f4239380c5d447e7e-0000000000-151-0fc613990.journal
```

## 第 9 章 使用 system

归档日志和活动日志占用了 496.8M 空间。

```bash

# journalctl --disk-usage

[root@studentvm1 d1fbbe4122942289e5ed31a25620fb]# ls -l

```

对目录下的文件进行详细列出，以便与实验结果进行对比。

关闭虚拟机并创建一个 studentVM 快照。在“description”字段中添加以下文本：“taken at beginning of experiment 9”。通过恢复此快照来查看 journal 轮转（rotation）和清理（vacuum）的相同效果。在此实验期间多次恢复快照，然后启动虚拟机。

简单的日志管理方法是轮转。

```bash

# journalctl --rotate

```

列出 journal 目录下的文件。它们并没有发生太大变化——完全没有变。我不知道为什么，`journalctl` 说明。

## 第 9 章 使用 systemd 管理日志

由于操作没有像说明的那样生效，我在 Red Hat 的 Bugzilla 页面上报告了该问题。以下命令有效，它可以清理旧归档文件，只保留小于一个月的文件。可以使用“s”、“m”、“h”、“days”、“months”和“years”后缀。

```bash

# journalctl --vacuum-time=1month

```

已删除归档日志：`/var/log/journal/d1fbbe4122942289e5ed31a256200fb/system/0005f2b035b5ec5c-a8d2bbd3f7b880.journal` (16.0M)。
已删除归档日志：`/var/log/journal/d1fbbe4122942289e5ed31a256200fb/user-1000-0005f43566ce0a41-96c8a31073b4c54.journal` (8.0M)。已删除归档日志：`/var/log/journal/d1fbbe41229942289e5d31a25600fb/system@0005f2b04d5b1e40-350154cfaed8d0.journal` (8.0M)。

<省略>

清理完成，从 `/var/log/journal/d1fbbe41229942289e5ed31a256200fb` 释放了 488.8M 的归档日志。清理完成，从 `/var/log/journal` 释放了 0B 的归档日志。清理完成，从 `/var/log/journal` 释放了 0B 的归档日志。

检查磁盘占用情况。关闭虚拟机并恢复最后的快照。验证预期的文件是否存在。如果文件少于四个，将不会执行任何操作，文件数量保持不变。

```bash

# journalctl --vacuum-files=4
```
