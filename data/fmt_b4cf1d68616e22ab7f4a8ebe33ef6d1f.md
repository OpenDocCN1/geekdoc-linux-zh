
2. 如有必要，使用`su --`命令切换到你的 root 用户账户。

3. 在 shell 提示符下输入`cd /RandD`更改到`/RandD`目录。

4. 你需要在`RandD`目录中创建几个研发（Research and Development）文档。然而，你需要确保这些文档免受窥视者的查看。回想一下前一个练习，当你创建文件时，其他人（Others）会自动被授予读访问权限。你不希望这种情况发生。你需要让其他人对创建的文档完全没有访问权限。执行以下操作：

   a. 在 shell 提示符下输入`umask 027`更改默认权限。

   b. 在 shell 提示符下输入`umask`验证`umask`的值。它应显示`0027`。

   c. 在 shell 提示符下输入`touch schedule.odt`创建一个名为`schedule.odt`的新文件。

   d. 在 shell 提示符下输入`ls -l`。验证所有者有`rw-`权限，组有`r--`权限，其他人有`--`权限。

5. 在一个之前的练习中，我们授予了所有者和组对`RandD`目录的`rwx`权限。然而，目录的写权限允许研发组中的任何人删除目录中的任何文件。我们希望配置目录，使得研发组中的用户只能删除他们实际拥有的文件。执行以下操作：

   a. 在 shell 提示符下输入`cd .`。

   b. 在 shell 提示符下，通过输入`chmod 1770 RandD`为`RandD`目录添加粘滞位 (Sticky Bit) 权限。

   c. 在 shell 提示符下输入`ls -l`。注意，`RandD`目录模式中其他人部分的最后一位数字中已添加了`T`。这表明已设置了粘滞位：

```
wsl:/ # ls -l
total 105
drwxrwx--T  2 tux    research    4096 Mar 18 11:25 RandD
...
```

6. 通过以系统中不同的用户身份登录并测试这些权限允许你做什么以及不允许你做什么，来实验你刚刚添加的新权限。

7. 在一个之前的练习中，我们创建了一个名为`dtracy`的用户。然而，由于我们在创建他时没有使用`-m`选项，他没有主目录。利用你学到的知识，执行以下操作：

   a. 在`/home`下为`dtracy`创建相应的主目录。

   b. 查看其他主目录并确定应分配的所有权和权限。

   c. 使用命令行实用工具设置`dtracy`主目录的所有权和权限。

   d. 完成后运行`pwck`以验证账户是否配置正确。

让我们通过讨论磁盘配额来结束本章。

### 实现磁盘配额

磁盘配额是管理 Linux 系统时非常有价值的管理工具。这里的问题是，由于 Linux 是一个多用户系统，一个或两个用户完全独占文件系统中所有可用磁盘空间的情况是有可能发生的。在当今的网络世界中，这尤其是一个问题，因为用户正在从互联网下载大型音乐文件甚至更大的电影文件。你如何防止这些用户消耗超过他们公平份额的磁盘空间？你使用磁盘配额。

简而言之，磁盘配额为系统上的用户建立了空间限制。你可以指定每个用户只允许使用一定量的磁盘空间或 inode（配额）。用户不允许超过此配额。

要在你的 Linux 文件系统中实现配额，你首先需要在系统上安装`quota`软件包。某些发行版，特别是服务器发行版，会将此软件包作为基础安装的一部分进行安装。然而，大多数发行版会要求你在系统设置后单独安装它。要查看你的系统上是否已安装`quota`，请在 shell 提示符下输入`rpm -qi quota`。如果未安装，请使用`rpm`或其他适当的包管理实用工具进行安装。

安装完软件包后，请完成以下操作以建立配额：

- 打开终端会话，并使用`su`切换到根用户账户。

- 通过执行以下操作来配置已挂载的文件系统以使用配额：

  - 使用文本编辑器打开`/etc/fstab`文件。

  - 为您要建立配额的文件系统的挂载选项添加`usrquota`和`grpquota`参数。在以下示例中，已为`/`文件系统建立了配额：

```
/dev/sda2 swap swap defaults 0 0
/dev/sda3 / ext4 acl,user_xattr,usrquota,grpquota 1 1
/dev/sda4 /boot ext4 acl,user_xattr 1 2
/dev/sda4 /var ext4 acl,user_xattr 1 2
proc /proc proc defaults 0 0
sysfs /sys sysfs noauto 0 0
debugfs /sys/kernel/debug debugfs noauto 0 0
devpts /dev/pts devpts mode=0620,gid=5 0 0
/dev/sdb1 /mnt/newdisk ext4 acl,user_xattr 1 2
```

  - 保存您对文件的更改并退出编辑器。

  - 重新启动系统以使更改生效。

- 系统重启后，通过执行以下操作来创建您的配额文件：

  - 打开终端会话并使用`su`切换到根用户账户。

  - 在 shell 提示符下，输入`quotacheck -amug`。

`quotacheck`实用程序用于扫描文件系统的磁盘使用情况以及创建配额文件。与`quotacheck`一起使用的上述选项执行以下操作：

- `-a` 检查所有已挂载的文件系统。

- `-m` 强制检查已挂载的文件系统。

- `-u` 检查用户。

- `-g` 检查组。

- `-v` 以详细模式操作。

当`quotacheck`完成后，应在已挂载文件系统的挂载点中创建两个名为`aquota.user`和`aquota.group`的文件，如下所示：

```
ws1:# ls
RandD bin etc lib64 mnt root srv usr
aquota.group boot home lost+found opt sbin sys var
aquota.user dev lib media proc selinux tmp
ws1:#
```

- 在 shell 提示符下输入`quotaon -av`在文件系统中启用配额。

- 在 shell 提示符下输入`repquota -av`查看当前用户使用的磁盘空间。屏幕上会显示一份报告，展示每个用户消耗了多少空间，如下所示：

```
ws1:/ # repquota -av
*** Report for user quotas on device /dev/sda3
Block grace time: 7days; Inode grace time: 7days
User used soft hard grace used soft hard grace
games -- 416 0 0 3 0 0
sdm -- 12 0 0 32 0 0
lp -- 12 0 0 3 0 0
man -- 208 0 0 2 0 0
news -- 4 0 0 1 0 0
polkituser -- 24 0 0 2 0 0
root -- 4236032 0 0 154678 0 0
uucp -- 4 0 0 1 0 0
ksanders -- 680 0 0 505 0 0
tux -- 108844 0 0 742 0 0
jsanders -- 52 0 0 14 0 0
tracy -- 52 0 0 14 0 0
#10000 -- 2688 0 0 211 0 0
Statistics:
Total blocks: 8
Data blocks: 1
Entries: 13
Used average: 13.000000
```

请注意，在此报告中未为任何用户配置限制。

- 通过执行以下操作为您的用户创建磁盘配额：

  - 在 shell 提示符下，输入`edquota -u username`。将显示一个类似于下方为`tracy`用户所示的屏幕：

```
Disk quotas for user tracy (uid 1004):
Filesystem blocks soft hard inodes soft hard
/dev/sda3 52 0 0 14 0 0
```

在此示例中，正在为`tracy`设置配额。请注意，配额文件已在`vi`编辑器中打开。此外请注意，您可以为块和 inode 设置硬配额和软配额。软配额是可以暂时超过的。硬配额不能超过。块配额指定用户可以在磁盘上消耗多少个块。inode 配额指定用户可以拥有多少个文件。

  - 使用`vi`编辑器设置块和/或 inode 的软配额和硬配额。

  - 保存您的更改并退出编辑器。

  - 对每个用户重复此过程。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_462_0.png)

- 通过执行以下操作为您的组创建磁盘配额：

  - 在 shell 提示符下，输入`edquota -g groupname`。

  - 使用`vi`编辑器设置块和/或 inode 的软配额和硬配额。
