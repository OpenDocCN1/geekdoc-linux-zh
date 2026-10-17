
```bash
case "$1" in
start)
  echo -n "Starting power management daemon: "
  start-stop-daemon --start --quiet --exec /usr/sbin/apmd \
  -s 'run-parts /etc/suspend.d'
  -r 'run-parts /etc/resume.d' $APMD
  echo "apmd."
  ;;
stop)
  echo -n "Stopping power management daemon: "
  start-stop-daemon --stop --quiet --exec /usr/sbin/apmd
  echo "apmd."
  ;;
restart|force-reload)
  echo -n "Stopping power management daemon:"
  start-stop-daemon --stop --quiet --exec /usr/sbin/apmd
  echo "apmd."
  echo -n "Starting power management daemon:"
  start-stop-daemon --start --quiet --exec /usr/sbin/apmd \
  -s 'run-parts /etc/suspend.d'
  -r 'run-parts /etc/resume.d' $APMD
  echo "apmd."
  ;;
*)
  echo "Usage: /etc/init.d/apmd {start|stop|restart|force-reload}"
  exit 1
  ;;
esac
```

假设一切顺利，脚本现在可以以状态 0 退出。

`exit 0`

## autofs

此文件控制自动挂载器（automounter），它控制文件系统的自动挂载。注意，此脚本使用了一些本书范围之外的元素。特别是，它使用了网络信息服务（NIS，以 "`yp`" 开头的命令属于该服务）以及 `sed` 程序，它是一个文本字符串处理器。我们在这里给出这里的大致情况，而不深入细节。你可能根本没有在使用 NIS，而且有整本书都在介绍 `sed` 的工作原理。

```bash
#! /bin/sh -e
#
# 使用 Sun 风格“主映射”自动挂载 rc 文件
# 我们首先查找本地 /etc/auto.master，然后查找同名的 YP
# 映射。在大多数发行版中，此文件应名为：
# /etc/rc.d/init.d/autofs 或 /etc/init.d/autofs
#
# NIS 映射中要忽略的选项列表。你可以利用此过滤掉 Linux
# （尚未）理解的选项，如果你的挂载点
# 理解 -s（松散）标志。请用空格分隔选项！
#
PRUNE_OPTIONS="quota"
```

```bash
#
# 我们可以在这里添加本地选项
# 例如：localoptions='rsize=8192,wsize=8192'
#
localoptions='
```

```bash
#
# 传递给 autofs 守护进程命令行参数
daemonargs="--setuser"
```

```bash
#
# 守护进程的名字和位置
DAEMON=/usr/sbin/automount
```

```bash
# 检查 automount 是否存在
test -f $DAEMON || exit 0
```

与之前显示的脚本一样，第一部分通过定义某些变量来打开脚本。然后它测试以确保 `automount` 守护程序确实存在。然而，与之前的脚本不同，此脚本的作者对每个变量进行了注释，这非常有帮助。这些注释并不是严格必要的，你会在大多数脚本中找不到这种对细节的关注，但它确实有助于理解脚本中每个变量的作用。

```bash
# 检查系统上是否可用 autofs
if ! grep -q autofs /proc/filesystems; then
if [ -e /lib/modules/$(uname -r)/fs/autofs.o ]; then
  echo "Error: autofs support not available."
  exit 0
fi
fi
```

前面的部分是一段扩展的检查。脚本检查了两个元素：首先，检查 `autofs` 文件系统在 `/proc/filesystems` 目录中是否有条目；其次，检查内核模块 `calofs` 是否可用。如果不可，脚本将打印错误消息并退出。

```bash
PATH=/sbin:/usr/sbin:/bin:/usr/bin
export PATH
```

在前面的几行中，脚本定义了 `PATH` 变量并将其导出，使其成为一个环境变量。

```bash
# 从 PRUNEOPTIONS 创建一个正则表达式
test ! -z "$PRUNEOPTIONS" && \
PRUNEREGEX=$(echo "\$PRUNEOPTIONS" | \
sed -e 's/\/\\/' -e 's/\/\\#/g' -e 's/\/\\\\\\#')
```

前面的代码块将 `PRUNEOPTIONS` 变量包含的字符串调整为正则表达式。正则表达式是泛化文本字符串的一种方式，使其能够匹配多个可能的特定字符串。

```bash
#
# 此函数将构建一个要执行的 automount 命令列表，
# 以激活所有挂载点。它用于在
# 重载时确定 automount 挂载点的差异
```

```bash
getmounts() {

cat /etc/auto.master | sed -e '^\#/d' -e '^$/d' | (
	while read dir map options
	do
	if [ -z "$dir" -a -z "$map" -a -z "$(echo "$map" | cut -d'=' -f1)" ];
	then
		map=$(echo "/etc/$map" | sed -e 's/:/etc://:')
		# 特殊：处理或 --timeout（或任何合理的变体）
		# 特殊处理，因为不能变成普通的挂载选项。
		mountoptions=""
		if echo $options | grep '-t' >/dev/null 2>&1; then
		mountoptions="--timeout $(echo $options | \"
```

这种结构表示正在定义一个函数。因此，随后的所有代码（直到遇到匹配的右大括号）在此时都不会执行，而是在调用 `getmounts` 函数时才会执行。该函数本身使用 `sed` 从某些系统文件中提取若干参数。这些参数将用于配置挂载点。

```bash
#
# 检查是否有需要加载的本地 map
[ -f /etc/auto.master ]
```

```bash
sed 's/.*-t(timeout)\*[ \t]*(([0-9][0-9]*).*/\2/g'
fi
options=$(echo "options" | sed -e \
s/--t[ \t]*[0-9][0-9]*//g\
s/\([ \t]*)-\1/g')
```

```bash
if [ -x map ]; then
echo "$DAEMON $mountoptions $dir program $map $options"
localoptions
elif [ -f map ]; then
echo "$DAEMON $mountoptions $dir file $map $options"
localoptions
else
echo "$DAEMON $mountoptions $dir `basename $map`"
localoptions
fi
done
) sed 's/ / /g'
```
