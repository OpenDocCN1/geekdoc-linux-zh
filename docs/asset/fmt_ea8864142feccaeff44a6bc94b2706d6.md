
C. `mount /floppy`

D. `mount ext2`

- 2. **文件系统层次结构标准 (FHS) 已被大多数 Linux发行版采用。** 尽管各个发行版遵循 FHS，但它不能保证文件系统的结构在每个发行版之间保持相对一致。

A. 正确

B. 错误

## 450 道练习题

- A. 系统管理员希望在其系统的硬盘上存储文件，并使其对所有其他用户（包括 root）隐藏。尽管他无法手动隐藏它们，但以下什么方法可以防止这些敏感文件在 `find` 命令中出现，而不对其产生不利影响？

- B. 修改权限，使无人对文件具有读取或执行权限。

- C. 将任何敏感文件移动到 `/proc` 目录。

- D. 将文件移动到一个目录并在其挂载某些文件系统。

- E. 使用 `chmod` 对文件设置隐藏位。

- 4. 大多数在 Linux 上运行的程序都需要链接库才能正常运行。使用的链接方法可以决定程序在库丢失或位置错误的情况下如何反应。以下哪些共享库的有效类型？（选择所有适用）

- A. 静态链接 (Static-linked)

- B. 简单页共享 (Simple page shared)

- C. 动态页共享 (Dynamic page shared)

- D. 内联链接 (Inline-linked)

- 5. 以下哪些守护进程允许用户在特定时间甚至定期间隔自动执行常规任务？

- A. `specJob`

- B. `kerneld`

- C. `cron`

- D. `init`

- 6. Linux 系统的所有用户都可以使用 `cron` 程序调度任务。

A. 正确

B. 错误

- 7. 备份可以在系统崩溃或其他重大灾难后恢复系统提供许多资源。通常认为有三种基本的备份策略。选择有效的备份策略。（选择所有适用）

- A. 全量 (Epoch)

- B. 分段 (Fractional)

- C. 增量 (Incremental)

- D. 差异 (Differential)

- 8. 一个大型网络的系统管理员计划使用磁带备份系统备份邮件服务器硬盘。磁带驱动存储在远程系统中，因此他计划使用命令：

```
tar cf - | rsh remotehost 'cat > /dev/rmt0' 
```

由于可能网络延迟，他可以使用什么程序来替换 `cat` 命令，以确保磁带接收到连续的数据流？

- A. `archiver`

- B. `cpio`

- C. `buffer`

- D. `ar`

- 9. 熟设备（cooked device）是指设备驱动程序将所有原始数据转换为某种预期或“规范”格式的设备。熟设备的反面是原始设备（raw device），它对数据不进行任何特殊解释。所有 Linux 设备都可以被视为熟设备或原始设备，取决于传递给应用程序的应用和参数。

A. 正确

B. 错误

- 10. 用户必须设置某些参数来配置网络接口。她将使用哪种方法？

- A. 传递内核 (Pass the kernel)

- B. `insmod`

- C. `ifconfig`

- D. 以上所有

- 11. 根据习惯，哪个目录包含内核并在启动期间使用？

- A. `/boot`

- B. `/sbin`

- C. `/var`

- D. `/usr`

- 12. 系统管理员 John 希望安装一个新的打印机。他列需要编辑以下哪些文件？

- A. `/etc/print`

- B. `/var`

- C. `/etc/lilo`

- D. `/printcap`

- 13. 通过执行命令可以将最大打开文件数从默认的 1024 更改为 4096：

```
echo 4096 > /proc/file-max
```

A. 正确

B. 错误

- 14. 假设目标设备是 `/dev/hda`，如何防止 Linux 跟踪访问时间？

- A. 在 `/fstab` 中为 `/dev/hda` 添加 "noatime" 选项

- B. `tune2fs --atime /dev/hda`

- C. `mkfs -t ext2 noatime /dev/hda`

- D. `echo 0 > /proc/fs/options`

- 15. 哪些说明可以解释启动过程中 LILO 仅显示 LI？（选择所有适用）

- A. LILO 能够读取你系统上的主引导代码。

- B. 四个启动阶段中只有两个成功通过。

- C. 第二阶段引导加载程序读取正确，但未找到启动镜像。

- D. 磁盘可能需要线性寻址而非标准的扇区/头部/柱道方法。

- 16. 以下哪个命令将我们的新内核镜像以原始格式写入 `/dev/fd0`？

- A. `rawrite /vmlinuz.floppy /dev/fd0`

- B. `cp /boot/vmlinuz.floppy /dev/fd0`

- C. `dd if=/boot/vmlinuz.floppy of=/dev/fd0`

- D. `cat /boot/vmlinuz.floppy /dev/fd0`

# 第 2 章：基础系统

1. 考虑以下 `/etc/passwd` 文件的摘录：

`firewall:*9fJ7AsjgT8kUpS5:41:31:firewall account:/tmp/bin/false`

密码字段中星号（`*`）的作用是什么？

A. 强制 root 用户在下次登录时更改密码。

B. 禁用此账户。

C. 告诉系统在 `/etc/shadow` 文件中查找加密密码。

D. 它没有作用；它只是另一个加密字符。

2. `useradd` 命令（或 `adduser`）用于添加或更新用户账户。

关于此用户管理命令，以下哪些描述也是正确的？（请选择所有适用项。）

A. 超级用户使用 `useradd`（或 `adduser`）命令创建的新账户在用 `passwd` 程序分配密码之前将一直保持禁用状态。

B. 该命令可以为账户创建一个家目录，该目录包含来自 `/etc/skel` 的默认文件。

C. `useradd` 可用于设置密码的最小长度。

D. 在将用户添加到 NIS 组时，必须在 NIS 服务器上运行 `useradd` 命令。

3. 超级用户可以通过编辑 `/etc/passwd` 文件来设置新用户账户。

在影子系统（shadowed system）在使用此方法创建账户后，建议运行 `pwconv` 命令。关于该命令，以下哪是正确的？

A. `pwconv` 将加密密码从密码文件移动到影子密码文件 (`/etc/shadow`)。

B. 如果影子文件不存在，`pwconv` 将不会创建它。

C. `pwconv` 命令仅对 `/etc/shadow` 文件进行操作。

4. 在创建用户账户时，`/etc/skel` 目录的内容会被复制到新用户的家目录。由于这个原因，该目录将是每个用户存储其个人文件的好去地方。

A. 正确

B. 错误

5. `suid(S)` 和 `guid(s)` 定义了允许权限位中执行位开启特殊访问模式的进程。以以下文件为例：

```
$ls -la tzsoccer
rwxr-xr-- 1 steve users 19 Sep 19 00:11 tzsoccer
```

这个特定示例演示了文件 `tzsoccer` 的 sgid 位。找到一个设置了 suid 的示例。

A. `-rwsr--r-- 1 steve users 19 Sep 19 00:11 tzsoccer`

B. `-rwxr-xr-s 1 steve users 19 Sep 19 00:11 tzsoccer`

C. `-rwxr--s-- 1 steve users 19 Sep 19 00:11 tzsoccer`

6. 选择允许管理员创建一个名为 "power" 组 ID 为 218 的组命令。

A. `addgroup -g 218 power`

B. `grouppadd -g 218 power`

C. `newgroup power --gid=218`

D. `addgg power 218`

7. Mike 想要访问 Zach 刚刚完成的项目文件。以下哪个语句赋予了 Zach 将文件所有权更改为 Mike 的？

A. `chown Zach:Mike project`

B. `chown Mike project`

C. `chown project Mike`

D. `chown` 无法执行此任务

8. Ashley 想要处理属于 Heather 的文件 SPORTS。什么让系统管理员能够赋予 Ashley 该文件的所有权？

A. `chown Ashley SPORTS`

B. `chmod u+rx SPORTS`

C. 只有 Heather 可以给 Ashley 正确的权限

D. `chown Ashley SPORTS`
