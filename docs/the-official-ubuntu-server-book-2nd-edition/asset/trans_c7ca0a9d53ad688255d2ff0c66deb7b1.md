

![](img/304f637afcecc491b152ee8ac5afadee_318_0.png)

## Figure 7-6 BackupPC restore file browser

BackupPC 为您提供了三种不同的恢复选项：

- Direct restore
在直接恢复中，BackupPC 将文件或目录直接恢复到一台主机。您实际上可以选择恢复到哪台主机，因为 BackupPC 允许您选择其配置的任何主机。默认情况下 BackupPC 会恢复到文件原本所在的共享以及共享下的目录，因此如果您想覆盖或替换当前的内容，只需点击 Start Restore 按钮即可。您甚至可以在需要时用完整备份完全覆盖远程主机上的整个 / 目录。您也可以不将文件恢复到原始目录，而是恢复到不同的目录，以便比较两个文件。

- Download zip archive
当您备份 Windows 桌面并允许用户自行恢复其文件时，此选项非常有用。与直接将文件恢复到主机不同，您可以生成一个包含所有恢复文件和目录的 .zip 文件并将其下载到当前计算机。

- **Download tar archive**
此选项与 zip 归档选项本质上相同，只是这种情况下您获得的是 tar 归档，这对 Linux 桌面更有用。

## Ubuntu BackupPC Conventions

- **/etc/backuppc**
此目录包含 BackupPC 的所有配置文件，包括其 Apache 配置和任何主机特定的配置文件。

- **/etc/backuppc/config.pl**
所有默认的 BackupPC 选项都设置在 config.pl 文件中。随软件包默认提供的 config.pl 版本充满了文档，解释每个选项并给出示例。任何主机特定的配置都进入一个以主机命名并以 .pl 结尾的单独文件。

- **/etc/backuppc/hosts**
BackupPC 将备份的所有主机都在此处定义。

- **/etc/backuppc/htpasswd**
Web 用户及其密码默认设置在此文件中。这是标准的 Apache 密码文件，因此您可以使用 htpasswd 命令进行更改（输入 man htpasswd 以了解如何使用该程序）。

- **/etc/backuppc/apache.conf**
此文件定义了 BackupPC Web 管理页面的所有虚拟主机设置。BackupPC 从 /etc/apache2/conf.d/backuppc.conf 创建到此文件的符号链接，尽管如今它更适合放在 /etc/apache2/sites-available 下。

- **/etc/init.d/backuppc**
这是 BackupPC 的 init 脚本。BackupPC 在安装后默认启动服务，并在启动时自动启动。

- **/var/lib/backuppc**
此目录包含 BackupPC 备份的所有文件，因此您应考虑将此目录放在单独的大型挂载点上，或至少确保其有足够的可用空间。

- **/var/lib/backuppc/log**
每个备份的日志都可以在此目录下找到。您也可以从 Web 界面访问日志。

- **/var/lib/backuppc/pc**
每个主机在此都有自己的目录，包含其最新的文件集。BackupPC 使用硬链接将多个主机的相同文件合并在一起，但如果您已从 BackupPC 中删除一台主机并且也想删除其文件，请先删除此处的该主机目录。

## CHAPTER 8

## Monitoring

![](img/304f637afcecc491b152ee8ac5afadee_321_0.png)

工具，然而，它能够扫描您的硬盘以查找故障，并在故障实际发生前发出警告。

第一步是安装 smartmontools 软件包：

```
$ sudo apt-get install smartmontools
```

该软件包包含一个名为 smartd 的守护进程，可以在系统启动时启动并开始监控您的驱动器。默认情况下 smartd 不会启动，因此您需要编辑 /etc/default/smartmontools 并取消注释读取为

```
# start_smartd=yes
```

的行

现在 smartd 将在启动时启动，但您也希望手动启动它，以便它现在可用：

```
$ sudo /etc/init.d/smartmontools start
```

默认情况下 smartd 会扫描所有驱动器以查找启用了 SMART 的驱动器并对其进行监控，因此您此时无需执行任何特殊配置。当 smartd 检测到错误时，它会运行在 /etc/smartmontools/run.d/ 下找到的任何脚本。默认情况下该目录下只有一个名为 10mail 的脚本，它会向 root 用户发送电子邮件以便其了解问题，但您也可以向此目录添加任意数量的自定义脚本，并且它们将按字母顺序运行。当 smartd 发现问题时，它会执行您的脚本并将错误文件的完整路径作为参数传递，因此在您的脚本中您可以通过 $1 变量访问它，例如。查看 /etc/smartmontools/run.d/10mail 脚本以获取一个简单的示例，您可以基于此创建自己的脚本。

## sysstat

让我们面对现实吧，您可能没有使用像 top 这样的工具登录到您管理的每个系统的终端。即使您这样做了，您在睡觉时仍然不会知道系统负载或 RAM 统计信息。现在一些管理员通过 cron 作业运行 top 来解决这个问题，但 Ubuntu 通过 sysstat 提供了更好的系统。sysstat 软件包提供了一个

