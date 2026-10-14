
```
# 用于 ARGO
sh:12345:powerfail:/sbin/shutdown -h THE POWER IS FAILING
```

```
# 用于正常运行级别的 getty
<id>:<runlevels>:<action>:<process>
# "id" 字段必须与设备
# 字符（"tty" 之后）相同
1:123:respawn:tty1
2:123:respawn:tty2
3:123:respawn:tty3
4:123:respawn:tty4
5:123:respawn:tty5
6:123:respawn:tty6
7:123:respawn:tty7
8:123:respawn:tty8
9:123:respawn:tty9
```

## `/sbin/init.d` 目录

`/sbin/init.d` 子目录用于存储所有运行级别（run levels）所需的所有脚本。

> 请注意，`/etc/rc.d` 目录链接到 `/sbin/init.d` 目录。软链接是 Linux 中让一个目录或文件出现并像另一个文件一样工作的方法。SuSE 创建该链接是为了使其文件系统结构看起来更像传统的 UNIX 文件系统。

将所有脚本保留在一个位置便于管理它们。每个脚本都用于启动/停止特定的服务——例如，域名系统（DNS）、Web 服务或类似的服务。所有这些脚本都遵循特殊的命令行参数语法。例如，要启动网络文件系统（NFS）服务，你可以运行以下脚本：

```
/etc/rc.d/nfs start
```

要停止同一个服务，你可以如下所示运行相同的脚本：

```
/etc/rc.d/nfs stop
```

如你所见，`nfs` 脚本接受 `start` 和 `stop` 作为参数。该目录中的所有脚本都是如此，它们根据需要符号链接到 `rc[0-6]` 目录。

## `/etc/rc.d/rc` 脚本

当 `init` 将运行级别更改为七种可能的级别之一时，它会运行 `/etc/inittab` 文件中以下行之一指定的脚本：

```
10:0:wait:/etc/rc.d/rc 0
11:1:wait:/etc/rc.d/rc 1
12:2:wait:/etc/rc.d/rc 2
13:3:wait:/etc/rc.d/rc 3
14:4:wait:/etc/rc.d/rc 4
15:5:wait:/etc/rc.d/rc 5
16:6:wait:/etc/rc.d/rc 6
```

对于每个运行级别（0–6），都会运行一个名为 `/etc/rc.d/rc` 的脚本，并将运行级别作为脚本的参数。该脚本负责启动和停止目标运行级别的所有服务。例如，假设 `init` 被告知将运行级别更改为 3。它将在一个类似于下面的命令行中带有参数 `3` 运行 `/etc/rc.d/rc` 脚本：

```
/etc/rc.d/rc 3
```

`/etc/rc.d/rc` 脚本显示在列表 2-3 中。

列表 2-3：脚本 `/etc/rc.d/rc`

```
## /bin/bash
# Copyright (c) 1996-98 SuSE GmbH Nuremberg, Germany. All rights reserved.

# Author: Florian La Roche <florian@suse.de>, 1996
# Werner Fink <werner@suse.de>, 1994,96,98,99

# /sbin/init/rc -- 主资源控制脚本
# 此文件负责在运行级别更改时
# 启动/停止服务。如果新运行级别中某个特定
# 功能的操作与上一个运行级别中的操作相同，则此脚本既不启动
# 也停止该功能。

# 避免被子进程或键盘中断
trap "echo" SIGINT

# 获取系统控制台标准输入的大小
test -z "$CONSOLE" && CONSOLE=/dev/console
set -- $(stty < $CONSOLE)
LINES=$1
COLUMNS=$2
export LINES COLUMNS

# Configuration

## /etc/rc.config

# 如果之前的运行级别与当前运行级别相同
# 不要重新检查当前运行级别。
# # test "$PREVLEVEL" = "$RUNLEVEL" && exit 0

# # 这在重启和停止期间将所有 rc 消息
# 重定向到 tty1，如果系统控制台绑定在 VGA (tty0) 上。
if test $COLUMNS -gt 0 ; then
 # VGA
if test "$RUNLEVEL" = "0" -o "$RUNLEVEL" = "6"; then
 CONSOLE=/dev/tty
test -x /usr/bin/chvt &/usr/bin/chvt 1
fi
else
 # 串口：未定义列和行
LINES=24
COLUMNS=80
fi
# # 重定向此脚本及其子进程的输入输出
exec 0< $CONSOLE 1>&2

# # 设置 oncr 以避免阶梯效应且锁定滚动
stty oncr -ixon 0

# # \033[1m 切换粗体
# # \033[31m 切换红色
# # \033[32m 切换绿色
# # \033[33m 切换黄色
# # \033[m 切换颜色/关闭粗体
extd="\033[1m"
warn="\033[1m"
norm="\033[1m"
stat=7

echo -n "Master Resource Control: "
echo -n "previous runlevel: $PREVLEVEL. "
echo -e "switching to runlevel: ${extd}${norm}"

curdir=/sbin/init.d/rc$RUNLEVEL.d
prevdir=/sbin/init.d/rc$RUNLEVEL.d
rex="0-9]"
failed=""

# 运行对应运行级别的 KILL 脚本
for i in $prevdir/K*; do
    test -x "$i" || continue
    # 如果新级别有启动脚本，则不运行停止脚本
    start=$(ls $curdir/S* | cut -d/ -f- | head -n 1) # 注意：OCR 逻辑匹配
    start=$(*/K$rex)
    set -- $curdir/Srex$start
    test -n "$2" -e "$0: more one start -- @"
    test -f $1 && continue
    $i stop || failed=${start}
done
echo -e "$rc_reset"

# 运行当前运行级别的 START 脚本
for i in $curdir/S*; do
    test -x "$i" || continue
    # 如果上一个级别有停止脚本，则不运行启动脚本
    start=$(*/S$rex)
    set -- $prevdir/Krex$start
    test -n "$2" -e "$0: more one kill -- @"
    test -f $1 && continue
    $i start || failed=${start}
done
echo -e "$rc_reset"

echo -n "Master Resource Control: "
if test "$failed"; then
    echo
    echo -n "Failed services in runlevel $(RUNLEVEL)${norm}"
    echo -e "${extd}${failed}${norm}"
else
    echo -e "runlevel $(RUNLEVEL) has ${stat}${norm}"
fi

test -e /etc/issue-SuSE-first-run && (
    cat /etc/issue-SuSE-first-run
rm -f /etc/issue-SuSE-first-run
exit 0
```

## 第一部分：安装并启动 SuSE Linux

此脚本主要执行以下操作：

1. 检查是否存在指定运行级别的子目录。也就是说，如果带参数 3 运行脚本，它将检查 `/etc/rc3.d/` 目录是否存在。如果目录存在，脚本将继续。

2. 确定新级别要运行的任何程序或服务是否已经在运行。如果某个服务正在运行，脚本将其杀死并在下一步中重启它。要停止正在运行的服务，脚本将运行带有 `stop` 参数的脚本。

3. 运行所有带有 `start` 参数的脚本。

## `/etc/rc.d/rc[0-6].d` 目录

`rc0.d` 到 `rc6.d` 子目录用于运行级别 0 到 6。这些目录包含指向 `/etc/rc.d/init.d` 中脚本的符号链接。查看 `rc3.d` 目录。该目录列出了列表 2-4 所示的符号链接。

列表 2-4：`/etc/rc.d/rc3.d` 目录部分列表

| 权限 | 所有者 | 组 | 日期 | 目标 |
