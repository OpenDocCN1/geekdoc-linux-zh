
### 50. 在 Debian 机器上，`/etc/passwd` 和 `/etc/shadow` 文件的正确权限分别是什么？

- A. 644 和 440
- B. 644 和 600
- C. 644 和 400
- D. 644 和 640

注：类似于 Red Hat，但 Debian 通常使用 `shadow` 组来读取 shadow 文件。因此 640（所有者 rw，组 r，其他人无权限）是常见的，其中组是 `shadow`。选项 D 很可能是 Debian 的正确答案。

### 51. 你需要在繁忙的服务器上节省备份的时间和空间，因此你决定不备份两个特定的目录树。以下哪项*最不可能*定期变化？（选择两项。）

- A. `/usr`
- B. `/etc`
- C. `/home`
- D. `/dev`
- E. `/root`

注：与 `/home`、`/etc` 和 `/root` 相比，`/usr` 和 `/dev` 相对静态。`/dev` 通常在启动时或由 `udev`/`hwdb` 填充，就用户数据而言，不会“定期”变化。`/usr` 包含系统二进制文件/应用程序，仅在更新时变化。`/home` 和 `/etc` 经常变化。

### 52. 你需要让一组用户创建文件，这些文件的所有者和组具有读和写权限，但其他任何用户都没有任何权限。你应该在 `~/.bash_profile` 文件中为这些用户中的每一个设置什么值？

- A. `umask 007`
- B. `umask 022`
- C. `umask 027`
- D. `umask 054`

注：期望权限：所有者 rw，组 rw，其他人 0。

标准文件创建模式是 666。

我们需要掩码掉其他人（写和读）和组（无？不，组需要 rw）。

等等。“所有者和组具有读和写权限”。

所有者：rw (6)

组：rw (6)

其他人：0 (0)

所以我们想要 660。

`umask` 是我们*移除*的部分。

666 - `umask` = 660。

`umask` = 006？ 不。

如果我们设置 `umask 007`：

666 - 007 = 660。

所有者：6 (rw)

组：6 (rw)

其他人：0 (0)

这匹配。

选项 A 是 `umask 007`。

### 53. 作为普通用户，你发现无法创建超过特定大小的文件。当你联系系统管理员时，她告诉你已经设置了 __________，从而有效限制了你创建大文件的能力。从下列选项中选择缺失的单词：

- A. `umask`
- B. `unalias`
- C. `noclobber`
- D. `ulimit`
- E. `unset`

注：`ulimit` 控制如文件大小等资源限制。

### 54. 在将大量小文件移动到系统后，你需要确定 inode 的空闲和已用百分比。哪个命令最能实现这一点？

- A. `du`
- B. `fsck`
- C. `df`
- D. `tree`
- E. `dumpe2fs`

注：`df -i` 显示 inode 使用情况。 `df` 是通用命令。 `dumpe2fs` 是低级别的。 `df` 是磁盘使用摘要的标准工具（包括带 `-i` 标志的 inode），但即使没有它，它也是这些选项中“空闲和已用百分比”摘要的主要候选者。具体而言，`df` 报告 inode 使用情况。

### 55. 要查看 /home 目录树的空间使用摘要，你会使用以下哪个命令？

- A. `df -h`
- B. `du -sh /home/`
- C. `freespace /home`
- D. `dirs /home`

注：`du`（磁盘使用量）计算目录树大小。`-s` 摘要，`-h` 人类可读。

### 56. 选择需要在给定文件系统上启用用户配额所必须执行的步骤。列表不必包含每个动作——只需列出必须执行的那些。

- A. 将字符串 `usrquota` 添加到 `/etc/fstab` 的第四列。
- B. 运行 `edquota` 命令。
- C. 运行 `quotacheck` 命令。
- D. 重新挂载文件系统。
- E. 运行 `quota` 命令。

注：步骤通常是：1. `fstab` 选项。 2. 重新挂载。 3. `quotacheck`。 4. 使用 `edquota` 设置配额。

因此 A、D、C、B 是步骤。

问题要求“选择步骤...”。它暗示多项选择。

A 是必要的。

D 是必要的（为了应用 `fstab` 更改或在已挂载的 FS 上启用配额）。

C 是必要的（以建立配额数据库）。

B 用于设置实际的配额限制。

E 用于检查。

通常，启用*功能*需要 A、D、C。设置*限制*需要 B。

如果问题暗示“启用用户配额”是指开启该功能，A、C、D 是关键。

让我们看看提示结构中提供的选项。这是一个“选择步骤”的问题。

可能的答案：A、C、D。或者 A、B、C、D。

我将列出有效的步骤。

- A. 将字符串 `usrquota` 添加到 `/etc/fstab` 的第四列。
- C. 运行 `quotacheck` 命令。
- D. 重新挂载文件系统。
- B. 运行 `edquota` 命令。

### 57. 你的系统有两个并行端口，你已将设备连接到系统后面板列表中列出的第二个端口。请在下方空白处填写代表此端口的设备文件的完整路径和文件名：

`/dev/lp1`

### 58. 你已将调制解调器连接到现有的第三个串行端口，并希望配置它。请在下方空白处填写指向所提及串行端口的设备文件的完整路径和文件名：

`/dev/ttyS2`

注：Linux 串行端口是 `ttyS0` (COM1)、`ttyS1` (COM2)、`ttyS2` (COM3) 等。第三个端口是 `ttyS2`。

### 59. 你正在使用一台工作站作为主站，以部署实验室中的相同工作站。哪个命令会按块复制 `/dev/hda` 磁盘到作为设备 `/dev/hdb` 存在的相同磁盘？请在下方空白处填写实现此目的的最简单字符串：

`dd if=/dev/hda of=/dev/hdb bs=4M status=progress`

注：提示要求“最简单字符串”。 `dd if=/dev/hda of=/dev/hdb` 是核心。添加 `bs=...` 是优化。我将提供标准的 `dd` 命令。

```
dd if=/dev/hda of=/dev/hdb
```

### 60. 你需要配置 `xscreensaver` 在 30 秒后超时。你可以编辑哪个文件名来实现此功能？（选择两项。）

- A. `/etc/ssaver.conf`
- B. `/etc/X11/xinit/screensaver.conf`
- C. `.xscreensaver`
- D. `.Xdefaults`
- E. `.xssaverrc`

注：`xscreensaver` 使用 `~/.xscreensaver` 或系统范围的 `/etc/X11/xscreensaver`。它还可以通过 X 资源在 `~/.Xdefaults` 或 `~/.Xresources` 中控制。

选项 C `.xscreensaver` 是正确的用户配置文件。

选项 D `.Xdefaults` 可以包含 `xscreensaver.timeOut: 30`。

因此 C 和 D 可能是答案。

### 61. 哪个文件用于存储用户会话期间的程序自定义设置？

- A. `Xresources`
- B. `Xdefaults`
- C. `.Xsession`
- D. `xrdb`

注：这个问题有点模糊。 `Xresources` 是一种文件类型。 `Xdefaults` 是传统的用户级 X 资源文件。 `.Xsession` 是在登录时运行的脚本。 `xrdb` 是加载资源的程序。

如果询问存储自定义设置的*文件*，它通常被称为 `~/.Xdefaults` 或 `~/.Xresources`。

在 A 和 B 之间，B 在许多 X 配置中是用户默认资源文件的常见名称，尽管 `~/.Xresources` 也非常常见。

然而，查看典型的考题，“`Xdefaults`”（B）通常是用户资源文件的预期答案，或者“`Xresources`”（A）。

让我们看措辞：“存储程序自定义设置”。

如果我必须选择一个，`~/.Xdefaults` 或 `~/.Xresources`。

让我们假设问题指的是文件 `~/.Xdefaults` 或 `~/.Xresources`。

实际上，`xrdb` 加载该文件。文件本身是 `Xresources` 或 `Xdefaults`。

我选择 **B. `Xdefaults`**，因为它是旧系统中用户 X 资源的非常常见的文件名，或者 **A. `Xresources`**。

让我们检查上下文。“在用户会话期间”。
