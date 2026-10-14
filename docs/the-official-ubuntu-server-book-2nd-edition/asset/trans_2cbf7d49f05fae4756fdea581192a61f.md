
## rsync 微调

虽然对于大多数普通用户来说，默认的 rsync 选项应该已经足够，但根据你的环境，你可能还想启用一些额外的选项。

### 校验和种子

如果你的主机相对较新，那么它应该带有版本号大于或等于 2.6.3 的 rsync（如果你不确定自己的版本，可以输入 rsync --version 查看）。如果是这样，你可以利用 --checksum-seed 选项，它可以缓存 rsync 的校验和，从而整体上加快 rsync 进程。为此，你需要将该选项添加到 BackupPC 配置中的 RsyncArgs 和 RsyncRestoreArgs 选项中。

要通过 Web 添加此设置，请点击侧边栏中的 Web Config，然后点击 Xfer 链接。向下滚动到 RsyncArgs 选项，你可以看到每个选项单独占一行。在这些选项的末尾有一个 Add 按钮。点击该按钮并添加 --checksum-seed=32761。然后向下滚动，将相同的选项添加到 RsyncRestoreArgs 部分。

要在命令行上做同样的更改，请用文本编辑器打开 /etc/backuppc/config.pl，并找到包含 $Conf(RsyncArgs) 的那一行。每个 rsync 选项单独占一行，但如果你仍在使用随软件包附带的 config.pl，你会看到该选项被注释掉了：

```
#' --checksum-seed=32761' ,
```

只需将该选项开头的 # 去掉即可。如果你没有看到这个被注释掉的选项，只需在最后一个 RsyncArgs 选项下方添加一行，内容为：

```
' --checksum-seed=32761' ,
```

然后向下移动到 RsyncRestoreArgs 部分（通常它就是下一个选项），对该选项执行同样的操作。

### 单一文件系统

默认情况下，BackupPC 会遍历主机上的所有文件系统，并备份所有内容。在某些情况下，你可能不希望这是默认行为，尤其是在集群环境中，你可以通过重建主机来轻松替换主系统文件。在这种情况下，你真正想要做的是让 rsync 一次只处理一个文件系统，然后指定 BackupPC 应备份哪些挂载点。

第一步相对简单，因为这个选项与 `--checksum-seed` 选项位于同一位置。按照我上面描述的步骤，在 Web 界面或命令行中将 `--checksum-seed` 选项添加到 RsyncArgs 和 RsyncRestoreArgs。不过，这次你要添加的选项是：

```
--one-file-system
```

设置该选项后，你必须定义 BackupPC 将要备份的每个文件系统。在此示例中，假设你将 `/home` 和 `/var` 放在不同的分区上，并且只想备份它们。你要更改的选项称为 `rsyncShareName`。在 Web 界面中，返回到你用来将 `--one-file-system` 添加到 RsyncArgs 的 Xfer 配置界面。在该部分上方，你会看到名为 RsyncShareName 的部分。与 RsyncArgs 一样，每个共享独占一行。首先，将第一个选项从 `/` 改为 `/home`。然后点击 Add 按钮，添加一个名为 `/var` 的新共享。

要在命令行中更改同一选项，请打开 config.pl，找到类似于以下内容的行：

```
$Conf{RsyncShareName} = '/';
```

并将其改为：

```
$Conf{RsyncShareName} = ['/home', '/var'];
```

**排除目录**

你可能会发现，你通常想要备份主机上的所有文件，但有几个目录除外。例如，在上面的示例中，你可能想要备份 `/home` 和 `/var`，但也许你想跳过 `/var/spool/mail` 和 `/var/tmp`。要做到这一点，你可以回到 Web 界面的 Xfer 配置界面，向下滚动到 BackupFilesExclude 选项。然后在 New Key 字段中输入 `/var/tmp`，并点击 Add。刷新屏幕后，你可以向下滚动，以同样的方式添加 `/var/spool/mail`。

如果你想在命令行中更改此项，请在文件中搜索，直到看到类似这样的行：

```
$Conf{BackupFilesExclude} = undef;
```

默认情况下，不会排除任何文件。要添加这两个目录，请将该选项改为：

```
$Conf{BackupFilesExclude} = ['/var/tmp', '/var/spool/mail'];
```

与任何配置更改一样，完成所有更改后，不要忘记保存然后重新加载 BackupPC，以便更改生效。

### 主机特定的微调

虽然你可以设置一个适用于大多数主机的默认 BackupPC 配置，但你很可能会遇到一些需要与默认配置略有不同的机器。使用 BackupPC，从默认配置中分支出来并自定义选项尤其容易。例如，你可能只想在某台主机上应用 --one-file-system 选项或排除某些目录。

基本上，要为特定主机添加自定义选项，请将这些选项从 /etc/backuppc/config.pl 文件复制到 /etc/backuppc/hostname.pl 中，其中 hostname 是你要更改的主机的名称。因此，举例来说，如果你想在 BackupPC 主机上只备份 /home 和 /var，并且不遍历名为 web1 的主机上的文件系统，你需要将整个 RsyncArgs 和 RsyncRestoreArgs 以及 RsyncShareName 选项复制到名为 /etc/backuppc/web1.pl 的文件中。结果大致如下：

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
```

