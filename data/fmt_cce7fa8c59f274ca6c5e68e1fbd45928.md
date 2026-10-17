
虽然你可以设置一个适用于大多数主机的默认 BackupPC 配置，但你很可能会遇到一些需要与默认配置略有不同的机器。使用 BackupPC，从默认配置中分支出来并自定义选项尤其容易。例如，你可能只想在某台主机上应用`--one-file-system`选项或排除某些目录。

基本上，要为特定主机添加自定义选项，请将这些选项从`/etc/backuppc/config.pl`文件复制到`/etc/backuppc/hostname.pl`中，其中 hostname 是你要更改的主机的名称。因此，举例来说，如果你想在 BackupPC 主机上只备份`/home`和`/var`，并且不遍历名为 web1 的主机上的文件系统，你需要将整个`RsyncArgs`和`RsyncRestoreArgs`以及`RsyncShareName`选项复制到名为`/etc/backuppc/web1.pl`的文件中。结果大致如下：

```
$Conf{RsyncShareName} = ['/home', '/var'];
$Conf{RsyncArgs} = [
    #
    # Do not edit these!
    #
    '--numeric-ids',
    '--perms',
    '--owner',
    '--group',
    '-D',
    '--links',
    '--hard-links',

    '--times',

    '--block-size=2048',

    '--recursive',

    # my custom options

    '--one-file-system',

];

$Conf{RsyncRestoreArgs} = [

    # Do not edit these!

    #

    '--numeric-ids',

    '--perms',

    '--owner',

    '--group',

    '-D',

    '--links',

    '--hard-links',

    '--times',

    '--block-size=2048',

    '--recursive',

    # my custom options

    '--one-file-system',

];
```

## Change the Backup Schedule

默认情况下，BackupPC 每周进行一次完整备份，期间对每个主机进行增量备份。BackupPC 会保留一次完整备份和六次增量备份，然后才删除任何内容。最后，BackupPC 不会在工作日上午 7:00 至下午 7:30 之间为始终在线网络的主机启动新任务。这些默认值并不适合所有人。例如，你可能需要保留一个月的完整备份，或者大家可能在下午 6:00 就离开办公室，这样你就可以在那时开始备份。所有这些选项都可以在 BackupPC Web 界面中轻松更改。

首先，点击左侧边栏中的 Edit Config 链接，然后点击屏幕右上角的 Schedule 链接。你将看到如图 7-5 所示的计划编辑屏幕。第一组选项让你可以安排完整备份。每个选项都链接到手册页，以便你可以阅读它们所更改的内容。

`FullPeriod`选项定义了在安排新的完整备份之前应经过的时间（以天为单位）。此选项始终设置为略低于一个完整数字。以默认值 6.97 为例，完整备份将每七天安排一次。`FullKeepCnt`和`FullKeepCntMin`选项分别配置要保留的完整备份数量和要保留的最小数量，而`FullAgeMax`定义了在删除旧完整备份之前的最长天数。增量备份可以通过仅备份自上次完整备份以来发生更改的内容来节省备份资源。它们采用与完整备份大部分相同的选项，默认情况下每天运行并保存最后六个。

此页面的 Blackouts 部分让你可以定义 BackupPC 的黑名单时段。黑名单时段是在此期间 BackupPC 不会尝试备份始终在线网络的主机的范围。这样，如果你有在晚上可能关机的桌面电脑，BackupPC 会在白天备份它们，但对于始终在线的服务器，BackupPC 知道可以在晚上它们负载较低时再备份。当你向 BackupPC 添加新主机时，它会定期`ping`该主机以确定它是否始终在线网络。如果是，BackupPC 只会在黑名单时段内备份它。`hourBegin`选项定义黑名单时段开始的小时或小时的分数，而`hourEnd`选项设置其结束时间。`weekDays`选项设置黑名单时段生效的星期几。默认情况下，黑名单时段为周一至周五上午 7:00 至下午 7:30。

为了演示如何更改这些选项，我定义了一种可能在组织中使用的不同备份策略。在该组织中，我们希望每周进行完整备份并每天进行增量备份，但我们希望在丢弃之前保存长达一个月的完整备份。我们还希望保留最近两周的增量备份。最后，办公室里每个人都在下午 6:00 离开，所以我们希望在那时开始备份。要进行这些更改，我只需要更改以下值：

```
FullKeepCnt = 4
IncrKeepCnt = 12
hourEnd = 18
```

## Restore Files

备份文件固然好，但如果不能恢复它们就没什么用。我认为 BackupPC 最好的功能之一就是其易于使用的基于 Web 的恢复。如果你为`backuppc`设置了额外的 Web 账户（使用`htpasswd -c /etc/backuppc/htpasswd username`），你可以将这些账户添加到`/etc/backuppc/hosts.conf`中的特定主机（或在 Web 界面中），然后这些用户可以登录 BackupPC 并恢复自己的文件。

要恢复主机上的文件或目录，首先转到 BackupPC 上该主机的主页（在左侧边栏的下拉菜单中选择主机）。在主机的主页面上，你会看到一个已完成的备份列表的表格，其中列出了备份是完整还是增量、备份开始时间、耗时以及这些文件存储在文件系统中的位置。点击某一行开头的超链接备份编号以从该备份恢复。然后你将看到主机在页面上的整个目录结构，文件和目录旁边有复选框（图 7-6）。该界面类似于大多数文件管理器，你可以点击单个目录将其展开。选择好要恢复的所有文件后，点击页面顶部或底部的“Restore selected files”按钮。

![](img/304f637afcecc491b152ee8ac5afadee_318_0.png)

## Figure 7-6 BackupPC restore file browser

BackupPC 为您提供了三种不同的恢复选项：

- Direct restore

在直接恢复中，BackupPC 将文件或目录直接恢复到一台主机。您实际上可以选择恢复到哪台主机，因为 BackupPC 允许您选择其配置的任何主机。默认情况下 BackupPC 会恢复到文件原本所在的共享以及共享下的目录，因此如果您想覆盖或替换当前的内容，只需点击 Start Restore 按钮即可。您甚至可以在需要时用完整备份完全覆盖远程主机上的整个`/`目录。您也可以不将文件恢复到原始目录，而是恢复到不同的目录，以便比较两个文件。

- Download zip archive

当您备份 Windows 桌面并允许用户自行恢复其文件时，此选项非常有用。与直接将文件恢复到主机不同，您可以生成一个包含所有恢复文件和目录的 .zip 文件并将其下载到当前计算机。

- **Download tar archive**

此选项与 zip 归档选项本质上相同，只是这种情况下您获得的是 tar 归档，这对 Linux 桌面更有用。

## Ubuntu BackupPC Conventions

- `/etc/backuppc`：此目录包含 BackupPC 的所有配置文件，包括其 Apache 配置和任何主机特定的配置文件。

- `/etc/backuppc/config.pl`：所有默认的 BackupPC 选项都设置在`config.pl`文件中。随软件包默认提供的`config.pl`版本充满了文档，解释每个选项并给出示例。任何主机特定的配置都进入一个以主机命名并以`.pl`结尾的单独文件。

- `/etc/backuppc/hosts`：BackupPC 将备份的所有主机都在此处定义。

- `/etc/backuppc/htpasswd`：Web 用户及其密码默认设置在此文件中。这是标准的 Apache 密码文件，因此您可以使用`htpasswd`命令进行更改（输入`man htpasswd`以了解如何使用该程序）。

- `/etc/backuppc/apache.conf`：此文件定义了 BackupPC Web 管理页面的所有虚拟主机设置。BackupPC 从`/etc/apache2/conf.d/backuppc.conf`创建到此文件的符号链接，尽管如今它更适合放在`/etc/apache2/sites-available`下。

- `/etc/init.d/backuppc`：这是 BackupPC 的 init 脚本。BackupPC 在安装后默认启动服务，并在启动时自动启动。

- `/var/lib/backuppc`
