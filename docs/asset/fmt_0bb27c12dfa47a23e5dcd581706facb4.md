
```bash
SIZE=1000000  # 1兆字节
head -c $SIZE < /dev/zero file  # 创建指定大小的文件。
losetup /dev/loop0             # 将其设为回环设备。
mke2fs /dev/loop0               # 创建文件系统。
mount -o loop /dev/loop0 /mnt   # 挂载它。

# Thanks S.C.
```

`mkswap` 创建交换分区。交换区域必须通过 `swapon` 启用。

`swapon` 启用/禁用交换分区或文件。这些命令通常在启动和关机时生效。

`mke2fs` 创建 Linux ext2 文件系统。此命令必须以 root 身份调用。

### 示例 17-9 添加新硬盘

```bash
#!/bin/bash
# 为系统添加第二块硬盘。
# 软件配置。假设硬件已挂载。
# 来源于 ABS 指南作者的一篇文章。
# 来源于 _linuxgazette 第 38 期，http://www.linuxgazette.com。
ROOT_UID=0      # 此脚本必须以 root 运行。
E_NOTROOT=67  # 非 root 退出错误。
```

第 17 章 系统与管理命令

```bash
if [ "$UID" -ne "$ROOT_UID" ]
then
  echo "必须是 root 才能运行此脚本。"
  exit $E_NOTROOT
fi
```

```bash
# 请极其谨慎使用！
# 如果出现问题，你可能会抹除当前的文件系统。
```

```bash
NEWDISK=/dev/hdb # 假设 /dev/hdb 是空闲的。检查！
MOUNTPOINT=/mnt  # 或者选择另一个挂载点。
```

```bash
fdisk $NEWDISK
mk2fs -cv $NEWDISK
# 注意：检查坏块（详细输出）。
# /dev/hdb1，*不是* /dev/hdb
mkdir $MOUNTPOINT
chmod 777 $MOUNTPOINT # 让新硬盘对所有用户可访问。
```

```bash
# 现在，测试...
# mount -t ext2 /dev/hdb1 /mnt/newdisk
# 尝试创建一个目录。
# 如果成功，卸载它并继续。
```

```bash
# 最后一步：
# 将以下行添加到 /etc/fstab。
/dev/hdb1 /mnt/newdisk ext2 defaults 1 1
```

```bash
exit
```

参见示例 17-8 和示例 31-3。

## mkdosfs

创建 DOS 文件系统。

## tune2fs

调整 ext2 文件系统可用于更改文件系统参数，例如最大挂载次数。这必须以 root 身份调用。

> 这是一个极其危险的命令。请自担风险，因为你可能会无意中破坏你的文件系统。

## dumpe2fs

列出（到标准输出）详细信息。这必须以 root 身份调用。

```bash
dumpe2fs
```

## hdparm

列出（到标准输出）详细信息。这必须以 root 身份调用。

```bash
dumpe2fs
```

# 高级 Bash 脚本指南

某些进程用于检查该进程是否正在运行。请注意，如果进程已经存在，脚本可能会挂起。

通常情况下，应用程序会在 `/var/lock` 目录下创建并检查锁文件。脚本可以通过类似下面的方式测试锁文件是否存在。

```
appname=xyzzip
# 应用程序 "xyzzip" 创建了锁文件 "/var/lock/xyzzip.lock"

if [ -e /var/lock/$appname.lock ];
then
    # 防止其他程序和脚本
    # 访问 xyzzip 使用的文件/资源。
```

比 `lockfile` 命令有用得多的是 `flock`。它在文件上设置一个“建议性”锁，并在持有锁期间执行某个命令。这是为了防止任何其他进程在指定的命令完成之前对该文件设置锁。

```
flock $0 > lockfile_$
# 在脚本所在的行设置一个锁，
# 同时等待脚本输出到标准输出。
```

> 与 `lockfile` 不同，`flock` 会自动创建锁文件。

创建或删除设备文件（在系统上安装新硬件时可能是必要的）。`MAKEDEV` 工具具有 `mknod` 的所有功能，并且易于使用。

# MAKEDEV

用于创建设备文件的工具。它必须以 `root` 身份并在 `/dev` 目录下运行。它是 `mknod` 的一种高级版本。

# tmpwatch

自动删除在指定时间范围内未被访问的文件。通常由 `cron` 调用以移除日志文件。

# Backup

`dump, restore`

`dump` 命令是一个复杂的备份工具，通常用于规模较大的安装环境和网络。它读取原始磁盘分区并以二进制格式写入备份文件。要备份的文件可以保存到各种存储介质，包括磁盘和磁带驱动器。`restore` 命令使用 `dump` 恢复备份。

# fdformat

对软磁盘 (`/dev/fd0*`) 进行低级格式化。

# System Resources

# ulimit

设置系统资源使用的上限限制。通常配合 `-f` 选项调用，该选项设置了文件大小限制（`ulimit -f 1000` 文件最大限制为 1MB）。`-t` 选项限制核心转储大小（`ulimit -c` 消除核心转储）。`ulimit` 的值应设置在 `/etc/profile` 和 `~/.bash_profile` 中（见附录 H）。

第 17 章 系统与管理命令

# 高级 Bash 脚本指南

审慎使用 `ulimit` 可以保护系统免受可怕的 fork 炸弹攻击。

```bash
#!/bin/bash
# 此脚本仅用于说明目的。
# 请自担风险 - 它将会冻结你的系统。

while true; do
# 无限循环。
  $0 & \
    # 此脚本调用自身 . . .
    # 产生无限次 fork \
    # 直到所有资源耗尽导致系统冻结。
    # 这是臭名的“巫师的学徒”场景。

  exit 0
# 不会在此退出，此脚本永远不会终止。
```

在 `/etc/profile` 中设置 `limit -XX`（其中 `XX` 是用户进程限制）会在脚本超过预设限制时中止该脚本。

`quota`

显示用户或组的配额。

`setquota`

从命令行设置用户或组的磁盘配额。

`umask` 用户权限掩码。限制特定用户的默认属性。该用户创建的所有文件都具有 `umask` 指定的属性。`umask` 的（八进制）值定义了禁用的权限。例如，`umask 022` 确保新文件最多具有 `755` 权限（`777 AND 022`）。当然，用户可以使用 `chmod` 更改特定文件的属性。通常做法是在 `/etc/profile` 和/or `~/.bash_profile` 中使用 `umask`（见附录 H）。

# 示例 1 使用 umask 设置权限

```bash
#!/bin/bash
# 此脚本仅用于说明目的。
# 显示 umask 如何影响文件权限。

umask 022
touch testfile
ls -l testfile
# 输出应类似于：-rw-r--r-- 1 user group ... testfile
```

# 示例 2 设置文件限制

```bash
#!/bin/bash
# 此脚本仅用于说明目的。
# 显示 ulimit 如何限制文件大小。

ulimit -f 100
dd if=/dev/zero of=largefile bs=1k count=200
# 失败，因为超过了限制。
```

# 高级 Bash 脚本指南

```bash
bright=1      # 如果没有命令行参数，将亮度设置为 1.0（默认）。
else
if [ "$1" = "+" ];
then
    bright=$(echo "scale=2; $old_brightness + $INCR | bc) # +.05
else
if [ "$1" = "-" ];
then
    bright=$(echo "scale=2; $old_brightness - $INCR | bc) # -.05
else
if [ "$1" = "#" ];      # 打印亮度；不改变亮度。
then
    bright=$old_brightness
else
if [ "$1" = "H" ] || [ "$1" = "h" ];
then
    echo "用法:          设置/重置亮度为默认值 (1.0)。"
    echo "[无参数]      增加 0.5 亮度"
    echo "$0 -          减少 0.5 亮度"
    echo "$0 +          显示当前亮度而不更改。"
    echo "$0 N (数字) 将亮度设置为 N (可用范围 .7 - 1.2)"
    echo "$0 h [H]      显示此帮助信息。"
    echo "$0 any-other  提供 xrandr 使用信息。"
    bright=$old_brightness
else
    bright="$1"
fi
fi
fi
```

```bash
xrandr --output "$OUTPUT" --brightness "$bright"      # 查看 xrandr 手页。
E_CHANGE=$?                                              # 使用 root 权限！
echo "Current brightness = $bright"
```

```bash
exit $E_CHANGE
```

```bash
# ========== 或者，或者使用 . ==========================

#!/bin/bash
# backlight2.sh
# reldate 20jun2012

# Pedora Core 16 中的一个 bug 破坏了键盘背光控制。
# 这是一个快速且粗略的解决方案，是 backlight 的替代方案。
target_dir=/sys/devices/pci0000:00/0000.00:0001.0/0100.00.0/backlight/acpi_video0
# 硬件目录。
```

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

```bash
actual_brightness=$(cat $target_dir/actual_brightness)
max_brightness=$(cat $target_dir/max_brightness)
Brightness=$target_dir/brightness

let "req_brightness = actual_brightness" # 请求的亮度
if [ "$1" = "-" ];
then
    # 降低亮度 1 个档位。
    let "req_brightness = $actual_brightness - 1"
else
    if [ "$1" = "+" ];
then
        # 增加亮度 1 个档位。
        let "req_brightness = $actual_brightness + 1"
    fi
fi

if [ $req_brightness -gt $max_brightness ];
then
    req_brightness=$max_brightness
fi # 不要超过硬件设计的最大亮度。

echo

echo "Old brightness = $actual_brightness"
echo "Max brightness = $max_brightness"
echo "Requested brightness = $req_brightness"
echo

################################################====
echo req_brightness > $Brightness
# 必须是 root 才能生效。
E_CHANGE1=$? # 成功？
################################################====

if [ "$?" -eq 0 ];
then
    echo "Changed brightness!"
else
    echo "Failed to change brightness!"
fi

act_brightness=$(cat $Brightness)
echo "Actual brightness = $act_brightness"

scale=0
sf=100 # 缩放因子；$actual_brightness / $max_brightness * $sf | bc
pct=$(echo "scale=$scale;$0 / $pct%")
echo "Percentage brightness = $pct"

exit $E_CHANGE1
```

远程发行客户端：同步、克隆或备份远程服务器上的文件系统。

# 17.1. 分析系统脚本

利用我们对管理命令的知识，让我们检查一个系统脚本。最短且最易理解的脚本之一是 `"killall"`，用于在系统关闭时挂起运行进程。

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

示例 17-12. killall，来自 `/etc/rc.d/init.d`

```bash
#!/bin/sh

# 由文档作者添加的注释，标记为 "--"

# --> 这是 'rc' 脚本包的一部分
# --> 由 Miquel van Smorenberg, miquels@drinkinkel.nl.mugnet.org 提供。

# --> 这个特定的脚本似乎是 Red Hat / FC 特有的
# --> (可能在发行发行中不存在)

# 关闭所有仍在运行的不需要的服务
# --> (不应该有任何，所以这是一种完整性检查)

for i in /var/lock/subsys/; do
    # --> 标准的 for/in 循环，但 "do" 在某些同一行，
    # --> 有必要添加 ""
    # 检查脚本是否存在。
    [ -f $i ] || continue
    # --> 这是对“列表”的巧妙用法，等同于：
    # --> if [ ! -f "$i" ]; then continue

    # 获取子系统名称。
    subsys=$(ls /var/lock/subsys/)
    # --> 变量名，在这种情况下，它是文件名。
    # --> 这与 babys=`basename $i` 完全等同。

    # --> 它从锁文件名称中获取
    # --+ (如果存在锁文件，
    # --+ 那证明进程一直在运行)。
    # --> 参见上方的 "lockfile" 条目。

    # 关闭子系统。
    if [ -f /etc/rc.d/init.d/$subsys.init ]; then
        /etc/rc.d/init.d/$subsys.init stop
    else
        /etc/rc.d/init.d/$subsys stop
        # --> 注意 "stop" 是一个位置参数，
        # --> 不是 shell 内置命令。
    fi
done
```

这还不糟。除了在变量匹配上有点花哨外，没有新内容。

`练习 1。` 在 `/etc/rc.d/init.d` 中，分析 `halt` 脚本。它比 `killall` 长一点，但概念相似。在你的主目录某处复制此脚本并执行它（不要以 `root` 身份运行）。

`练习 2。` 在 `/etc/rc.d/init.d` 中，分析 `halt` 脚本。它比 `killall` 长一点，但概念相似。在你的主目录某处复制此脚本并执行它（不要以 `root` 身份运行）。

第 17 章。系统与管理命令

# 高级 Bash 脚本指南

# 第 5 部分。高级主题

此时，我们准备好深入探讨某些主题。

## 目录

- 18. 正则表达式

- 18.1. 正则表达式简介

- 19. Here Documents

- 20. I/O 重定向

- 21. 子 Shell

- 22. 受限 Shell

- 23. 替换

- 24. 函数

- 25. 别名

- 26. 列表

- 27. 数组

- 28. 引用

- 29. dev 和 proc

- 30. 编程

- 31. 空值

- 32. 调试

- 33. 选项

- 34. 脚本编写

- 35. 风格

- 36. 其他

- 37. 版本

# 18. 表达式

# 正则表达式

与软件开发相关的智力活动很大程度上取决于洞察力。为了充分利用脚本编写的力量，你需要精通正则表达式。某些命令和工具，如 `grep`；`sed` 和 `awk`，解释并使用正则表达式。从版本 3 开始，Bash 获得了自己的正则运算符：`=~`

## 18.1. 正则表达式简介

表达式是字符字符串。那些具有字面意思之外解释的字符被称为元字符。例如，引号符号可能表示人的说话。正则表达式是字符和/或元字符的集合，用于匹配或指定模式。

正则表达式包含一个或多个：

- 字符集。这些是保留字面意义的字符。简单的正则表达式仅由字符集组成，没有元字符。

- 锚点。这些指定正则表达式匹配的行位置。例如，`^` 和 `$`。

- 修饰。这些扩展或缩小正则表达式匹配的文本范围。修饰包括星号、括号。正则表达式的主要用途是文本搜索和字符串处理。正则表达式匹配单个字符或字符集——字符串或字符串的一部分。

- 星号 `*` 匹配前面的字符字符串或正则表达式的任意数量重复，

  `1133*` 匹配 `11` + 一个或多个 `3`：`113`, `1133`, `11333` 等。

- 点 `.` 匹配任何字符，换行符除外。

  `13.` 匹配 `13` + 至少一个任意字符（包括空格）：`1133`，但不是 `13`（缺少额外字符）。

- 参见 16-18 查看单字符匹配的演示。
