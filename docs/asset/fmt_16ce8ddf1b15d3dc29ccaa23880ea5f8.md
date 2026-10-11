
# Interactive Backup and Recovery（交互式备份和恢复）

Interactive Backup and Recovery（交互式备份和恢复）子区域用于交互式执行备份，或恢复先前备份中包含的信息。当您进入此区域时，系统会提示您从生成的列表中选择备份设备，这与您首次进入 Automated Backups（自动备份）子区域时被提示选择备份设备的方式相同。

从列表中选择设备后，您可以选择之前提到的 Actions（操作）菜单中的某一项。如果您决定使用 Backup Files Interactively（交互式备份文件），系统会再次提供一个窗口，您可以从中指定要包含在备份中以及要从备份中排除的文件。系统会要求您 Select Backup Scope（选择备份范围）、Specify Tape Device Options（指定磁带设备选项）以及 Set Additional Parameters（设置额外参数）。但是，由于备份是交互进行的，因此系统不会要求您 Select Backup Time（选择备份时间）。

此区域的步骤会根据您选择的磁带设备而有所不同。

索引文件可以从 Actions（操作）菜单中查看。这些文件存储在 `/var/sam/log` 目录中。以下显示了一个交互式备份索引文件的最顶部和最底部内容：

```
#1 /
#1 /.profile
#1 /.rhosts
#1 /.sh_history
#1 /.sw
#1 /.sw/sessions
#1 /.sw/sessions/swinstall.last
# 1 /.sw/sessions/swlist.last
# 1 /.sw/sessions/swmodify.last
# 1 /.sw/sessions/swreg.last
# 1 /.dt
# 1 /.dt/Desktop
# 1 /.dt/Desktop/Two TOP
# 1 /.dt/Desktop/Four
# 1 /.dt/Desktop/One
# 1 /.dt/Desktop/Three
# 1 /var/uccp/.Log/uucico
# 1 /var/uccp/.Log/ucup
# 1 /var/uccp/.Log/uuxq
# 1 /var/uccp/.Log/uuxqt
# 1 /var/uccp/.Old
# 1 /var/uccp/.Status
# 1 /var/vrespool/sw
# 1 /var/vrespool/sw/catalog/dfiles
# 1 /var/vrespool/sw/catalog/swlock
# 1 /var/vrespool/sw/swagent.log
# 1 /var/yp
# 1 /var/yp/Makefile BOTTOM
# 1 /var/yp/binding
# 1 /var/yp/securenets
# 1 /var/yp/securereservers
# 1 /var/yp/updaters
# 1 /var/yp/ypmake
# 1 /var/yp/ypxfr_1perday
# 1 /var/yp/ypxfr_1perhour
# 1 /var/yp/ypxfr_2perday
```

## 执行恢复

然而，完整备份或增量备份的价值仅在于它所恢复的文件。要从备份磁带中检索文件，您需要指定一个备份设备，然后指定许多与备份相关的选项。图 11-24 显示了从连接到系统的四个 DLT 单元中选择一个设备：

![](img/eff8b9287a5f38c5adf538f24aacf29e_679_0.png)

图 11-24 从四个 DLT 单元中选择

选择设备后，您可以从许多选项中进行选择，其中包括图 11-25 中所示的选项：

![](img/eff8b9287a5f38c5adf538f24aacf29e_680_0.png)

图 11-25 Recover Files Interactively（交互式恢复文件）

在此窗口中，您需要提供三个区域的信息：Select Recovery Scope（选择恢复范围）、Specify Tape Device Options（指定磁带设备选项）以及 Set Additional Parameters（设置额外参数）。您指定的设备选项将取决于您正在使用的磁带设备。

Select Recovery Scope（选择恢复范围）允许您输入一个包含要恢复文件的文件名，或者手动列出要包含在恢复中的文件。您还可以选择列出要从恢复中排除的文件。

在 Specify Tape Device Options（指定磁带设备选项）中提供了磁带设备文件列表，您可以从中选择磁带设备。在此步骤中，您可以选择磁带设备文件；在其他情况下，您可能需要选择磁光盘表面，或者可能根本不需要选择任何内容。

在 Set Additional Parameters（设置额外参数）下，您可以选择以下任一选项：

- 覆盖较新的文件 (Overwrite Newer Files)
- 保留原始文件所有权 (Preserve Original File Ownership)
- 使用完整路径名恢复文件 (Recover Files Using Full Path Name)
- 将文件放入非根目录 (Place Files in Non-Root Directory)

完成所有所需的选择后，恢复操作将开始。如果一个文件被意外删除，您希望从恢复磁带上将其还原，那么您应选择 Preserve Original File Ownership（保留原始文件所有权）和 Recover Files Using Full Path Name（使用完整路径名恢复文件）选项。在恢复进行时，您将收到恢复状态信息；恢复完成后，您也可以从 Actions（操作）菜单中 View Recovery Log（查看恢复日志）。如果您选择 View Recovery Log（查看恢复日志），您将看到一个窗口，其中提供索引日志的名称以及已恢复文件的名称。

### 集群

可以通过 SAM 管理高可用性集群。诸如添加应用程序和添加应用程序组之类的任务可以使用 SAM 来完成。由于 高可用性（high availability）是计算环境中高度定制化的方面，我将不详细涵盖 SAM 的这部分内容。但是，如果您必须管理系统集群，建议您查看此 SAM 区域，看看它是否有助于您的集群相关工作。

### 磁盘和文件系统

Disks and File Systems（磁盘和文件系统）帮助您管理磁盘设备、文件系统、逻辑卷、交换区和卷组（如果您的系统中安装了其他 HP 磁盘设备，如 XP 和磁盘阵列，您也可以通过这些设备通过 SAM 进行管理。）没有必要手动操作这些设备，因为 SAM 在管理这些方面做得非常好。图 11-26 和 11-27 显示了 Disks and File Systems（磁盘和文件系统）的层次结构：

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_1.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_2.png)

- 操作：（还包括磁盘阵列维护）
    - 配置 (Configure)
        - 使用逻辑卷管理器 (Using Logical Volume Manager)
        - 不使用逻辑卷管理器 (Not Using Logical Volume Manager)
    - 诊断缺失磁盘 (Diagnose Missing Disk)
    - 查看更多信息 (View More Information)
    - 将磁盘标记为已使用 (Mark Disk As Used)
    - 取消配置 (Unconfigure)

![](img/eff8b9287a5f38c5adf538f24aacf29e_683_3.png)

- 操作：
    - 添加本地文件系统 (Add Local File System)
        - 使用逻辑卷管理器 (Using Logical Volume Manager)
        - 不使用逻辑卷管理器 (Not Using Logical Volume Manager)
    - 添加远程文件系统 (Add Remote File System)
        - 使用 NFS (Using NFS)
        - 使用 NFS - 自动挂载器 (Using NFS - Automounter)
        - 使用 NFS - 主机映射 (Using NFS - Hosts Map)
        - 导出自动挂载器 (Export Automounter)
    - 启用 NFS 客户端 (Enable NFS Client)
    - 启用自动挂载器 (Enable Automounter)
    - 查看更多信息 (View More Information)
    - 修改 (Modify)
    - 移除 (Remove)
