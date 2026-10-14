

## 重新配置你的内核

要在 Linux 上使用配额，你的内核必须配置为包含配额支持。这通常需要重新编译内核。我们说通常是因为如果你没有更改 SuSE Linux 安装的内核，它已经内置了配额支持。在这种情况下，你可以简单地跳过本节并继续。但如果你以任何方式更改了内核，你可能已关闭了配额支持。在这种情况下，你需要在配置为包含配额支持后重新编译内核。有关如何构建内核的详细说明，请参阅第 8 章“安装新内核”。要重新编译内核以包含配额支持，只需按照以下快速步骤操作：

- 1. 首先，以 root 身份登录。
- 2. 将当前路径更改为 /usr/src/linux：
  `#cd /usr/src/linux`
- 3. 要配置内核，请通过输入以下命令运行内核的配置模块：
  `#make menuconfig`
- 4. 会弹出一个菜单驱动的对话框。使用箭头键导航到 Filesystems 并按 Enter。
- 5. 会弹出一个新的对话框。该对话框中的第一个选项就是 Quota Support。如果该选项旁边没有星号，请按空格键将其标记为包含在内核中。星号表示此功能将被内置到内核中。如果你发现它已经被标记，则你的内核已经支持配额，你不需要做所有这些。在这种情况下，使用 Esc 退出内核配置对话框，然后跳到下一节。
- 6. 现在你已将配额标记为包含在内核中，使用 Esc 键退出内核配置模块。它会提示你保存新的设置；选择 Yes。
- 7. 你已配置了内核；现在需要编译它。要编译内核，请按此顺序输入以下命令：
  `# make dep`
  `# make clean`
  `# make bzImage`
- 8. 每个步骤完成执行需要一些时间。你会看到大量文本滚动，这很正常。所有步骤完成后，你需要重新启动以使更改生效。

就这样。你的内核现在应该已支持配额。如果你对之前的步骤遇到任何问题，请阅读第 8 章，了解有关编译新内核的完整详细信息。

## 安装软件

现在你需要确保你拥有使用配额所需的软件。要安装软件，请使用 YaST 安装来自系列 AP1 的名为 quota 的软件包。要安装它，请按照以下步骤操作：

- 1. 以 root 身份登录。
- 2. 确保你的 SuSE 安装 CD 已插入 CD-ROM 驱动器中。
- 3. 运行 YaST 并选择 Install。
- 4. 加载一个新的菜单。选择 Change/Create Configuration。
- 5. 选择系列 AP。
- 6. 查找名为 quota 的软件包。
- 7. 如果它旁边有一个 i，则说明没问题。如果没有，则按空格键将软件包标记为安装。
- 8. 按 F10 退出。
- 9. 按 Start Installation。
- 10. YaST 将开始为你安装软件包。
- 11. 完成后，只需退出 YaST 即可。

## 修改系统以运行配额支持

下一步是告诉 SuSE Linux 要监控哪些文件系统以使用配额。配额仅适用于第二扩展文件系统 ext2。这是 Linux 默认使用的文件系统。要将文件系统标记为由配额监控，你需要编辑 /etc/fstab。

/etc/fstab 是包含有关文件系统信息的文件。用任何编辑器打开该文件。它应该看起来像这样：

```
/dev/hda7   swap        swap        defaults    0
/dev/hda6   /           ext2        defaults    1
/dev/hda5   /boot       ext2        defaults    1
/dev/hdc    /cdrom      iso9660     ro,noauto,user 0
/dev/fd0    /floppy     auto        noauto,user 0
none        /proc       proc        defaults    0
# End of YaST-generated fstab lines
```

你的系统可能显示的内容与此不同，这没关系。你可以在这里看到你有两个 ext2 文件系统——根目录 / 和 /boot。你更感兴趣的是根目录 /，因为它包含 /home 目录。你想要控制包含用户主目录的文件系统。要在文件系统上启用配额支持，将选项 usrquota 添加到第四个字段，要启用组配额，将选项 grpquota 添加。例如：

```
/dev/hda7   swap        swap        defaults    0
/dev/hda6   /           ext2        defaults,usrquota,grpquota 1
/dev/hda5   /boot       ext2        defaults    1
/dev/hdc    /cdrom      iso9660     ro,noauto,user 0
/dev/fd0    /floppy     auto        noauto,user 0
none        /proc       proc        defaults    0
# End of YaST-generated fstab lines
```

你现在已在 / 文件系统上同时启用了用户和组配额。

## 创建记录文件

对于每个你要使用配额支持的文件系统，你需要在其根目录上创建记录文件。

使用前面的示例，你需要在 / 上创建这些文件。你需要创建一个名为 quota.user 的文件（用于用户配额）和另一个名为 quota.group 的文件（用于组配额）。要创建这些文件，使用 touch 命令：

```
# touch /quota.user
# touch /quota.group
```

你必须使这些文件仅对用户 root 可读/写：

```
# chmod 600 /quota.user
# chmod 600 /quota.group
```

如果你的 /home 是独立的分区，并且你想对其设置配额，你将在 /home 下创建这些文件。现在是时候重新启动以使所有这些更改生效了。

## 为用户分配配额

要开始为用户分配配额，使用 edquota 命令。在开始使用此命令之前，你可能希望将 $EDITOR 变量设置为你选择的编辑器，例如 pico。这是个好主意，因为默认编辑器是 vi，对大多数人来说很难使用。输入以下内容：

```
# export EDITOR=pico
```

假设你想为用户 John 设置配额。你这样运行 edquota：

```
# edquota -u john
```

这将打开编辑器并显示有关 John 配额的信息：

```
Quotas for user john:
/dev/hda6: blocks in use: 1325, limits (soft = 5000, hard = 6500)
inodes in use: 156, limits (soft = 1000, hard = 1500)
```

使用配额你可以限制用户使用的空间，即 blocks，以及用户可以拥有的文件数，即 inodes。此特定用户已使用 1325 KB 空间，允许的软限制为 5000 KB，硬限制为 5000 KB。至于文件数，他有 156 个文件，软限制为 1,000，硬限制为 1,500。

设置用户的配额时，你可以同时设置硬限制和软限制。如果用户超过软限制，系统会警告她，如果她尝试超过硬限制，系统将不允许她。

要为 John 设置配额，只需按需编辑数字，保存并退出。就这样，完成了。

## 为多个用户分配配额

你已学会如何为一个用户设置配额，但你会为系统上的每个用户都这样做吗？这并不实用。你可以通过使用脚本来自动化此操作。你所要做的就是为一个用户设置配额，然后让系统将设置复制到所有其他用户。要做到这一点，输入以下命令：

```
# edquota -p john `awk -F: '$3 > 499 {print $1}' /etc/passwd`
```

此命令将用户 John 的设置复制到系统中 ID 大于 99 的所有用户。在大多数系统上，组用户 ID 从 500 开始，但请检查你的系统。awk 命令从密码文件 /etc/passwd 读取这些用户名。就这样，你已为所有用户设置了配额。

## 为组分配配额

要为组设置配额，你使用与单个用户相同的程序。如果你想为组 students 设置配额，请将 $EDITOR 设置为你喜欢的编辑器（如果你尚未设置）：

```
# export EDITOR=pico
# edquota -g students
```

pico 将打开并显示有关组 students 的相关信息：

```
Quotas for group games:
/dev/hda6: blocks in use: 6325, limits (soft = 10000, hard = 30000)
inodes in use: 2114, limits (soft = 5000, hard = 7000)
```

编辑限制值，保存并退出。

## 设置宽限期

你已看到你可以拥有两个限制，软限制和硬限制。我们说当用户超过软限制时，系统会警告他。但如果用户持续超过限制会怎样？这就是宽限期。在这里你设置系统允许用户超过软限制的时间，然后再强制执行。这可以以秒、分钟、小时或天为单位设置。

要设置宽限期，使用 edquota 命令：

```
# edquota -t
```

```
Time units may be: days, hours, minutes, or seconds
Grace period before enforcing soft limits for users:
/dev/hda6: block grace period: 7 days, file grace period: 7 days
```

在此示例中，我们已将宽限期设置为文件和块软限制均为七天。你可以将其设置为你想要的任何值。

## 更新你的设置

现在你已更改了许多配额设置，你需要更新配额系统。只需运行命令 quotacheck -a。

此命令在启动时会自动运行。但是，如果你不想重新启动系统以使更改生效，只需手动运行此命令，或使用 cron 设置为每周定期运行。

![](img/659f91d9da7b29976c0625e2e9628511_128_0.png)

