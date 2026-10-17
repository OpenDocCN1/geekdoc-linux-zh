
一种解决方案是创建三个空时间文件，每个每日、每周和每月任务一个，然后在 `/etc/daily`、`/etc/weekly` 和 `/etc/monthly` 目录中添加新条目以更新每个时间文件的修改日期。这解决了一部分问题：`cron` 可以检查该任务上次调用的时间，如果通过的时间不足以再次运行该任务，则退出。

该解决方案无法处理的情况是：在每月任务上次运行六周后，管理员调用了每月任务。四天后，有人忘记关闭电脑，结果每月 `cron` 被调用了。该任务如何知道实际上没有必要运行每月任务？

可以在相应的目录中添加两个脚本。一个脚本必须从 `run-script` 或 `periodic`（调用 `cron` 任务的标准方式）运行，然后打开目录中所有其他脚本的可执行权限，这在 `run-script` 或 `periodic` 扫描并确认无事可做后会将可执行权限重新打开：目录中的没有任何文件看起来都是可执行的，因此 `cron` 不会运行它们。然而，这并不是一个很好的解决方案，因为无法保证脚本的评估顺序，如果我们无法保证新脚本的运行顺序，整个解决方案就会失效。

实际上，这个困境可能没有完美的解决方案。或者，它可能涉及为 `run-script` 或 `periodic` 编写封装器，让它知道如何管理时间戳以确保任务执行得不会太频繁。或者，我们可能在担心某些在大全局中其实并不那么重要的事情。🙂

# 50 日志轮滚动（Rotating Log Files）

对 Linux 经验并不丰富的用户会对大量的命令、实用程序和守护进程将事件记录到系统日志文件中感到非常惊讶。即使在具有磁盘空间的计算机上，密切这些这些的大小——当然，还有它们的内容——也是关重要的。

因此，许多系统管理员有一组指令，将它们放置在日志文件分析工具的顶部，类似于这里显示的命令：

```
mv $log.2 $log.3
mv $log.1 $log.2
mv $log $log.1
touch $log
```

如果每周运行一次，这将产生一个为期一个月的日志文件信息滚动存档，分为按周划分的数据。然而，很容易创建一个脚本，一次性完成 `/var/log` 目录下的所有日志文件的操作，从而减轻任何日志文件分析脚本的负担，并在管理员没有进行任何分析的月份管理日志。

列表 6-12 中的脚本遍历了 `/var/log` 目录中匹配特定标准的每个文件，检查每个匹配文件的滚动计划和最后修改日期，以查看是否是时候对文件进行滚动了。该脚本仅仅就是这一点。

## 代码

```
#!/bin/bash
# rotatools--对 /var/log 中的日志文件进行滚动以便存档，并确保
# 文件不会变得到无法管理的程度。此脚本使用一个配置文件
# 来允许自定义每个日志轮滚的频率。
# 配置文件格式为 filename=duration，其中 duration 单位为
# 天。如果配置文件中缺少特定文件名的条目，
# rotatools 滚动该文件的频率不会高于每七一次。
# 如果 duration 设置为零，脚本将忽略那组特定的
 日志文件。

logdir="/var/log" # 你的日志文件目录可能会不同。
config="$logdir/rotatlogs.conf"
m="/bin/mv"
```

162 第 6 章

```
default_duration=7 # 我们默认采用 7 天的滚动计划。
count=0
duration=$default_duration
```

```
if [ ! -f $config ]; then
# 此脚本没有配置文件？那我们没戏。你也可以安全地删除
# 此测试，并在配置文件缺失时直接忽略自定义。
echo "echo $0: no config file found. Can't proceed." >&2
exit 1
```

```
if [ ! -w $logdir -o -x $logdir ]; then
# -w 是写权限，-x 是执行权限。你需要两者才能在 Unix 或 Linux 目录
# 创建新文件。如果你没有它们，我们就失败了。
echo "echo $0: you don't have the appropriate permissions in $logdir" >&2
exit 1
```

```
cd $logdir
```

```
# 虽然我们想在 find 中使用像 :digit: 这样的标准集合符号，
# 但许多版本的 find 不支持 POSIX 字符类
# 标识符--[0-9]
```

```
# 这是一个相当复杂的 find 语句，在后文的正文中
# 有了解释。如果你好奇，请继续阅读！
```

```
for name in $config; find maxdepth 1 -type f -size +0 -name '*[0-9]*' \
! -name '*.*' -name '*conf' -print | sed 's/\\/\\/'
done
```

```
count=$((count + 1))
# 从配置文件中获取该特定文件的匹配条目。
```

```
duration=$(grep "${name}" $config -d= -f2)
if [ -z "$duration" ]; then
duration=$default_duration # 如果没有匹配，我们使用默认值。
elif [ "$duration" = "" ]; then
echo "duration set to zero: skipping $name"
continue
fi
```

```
# 设置文件名。足够简单：
back1="${name}.1"; back2="${name}.2";
back3="${name}.3"; back4="${name}.4";
```

```
# 如果最近滚过的文件 (back1) 在特定的
# 时间段内被修改过，那么还没到滚动它的时候。这
# 通过 -mtime 修改测试找到。
```

```
if [ -f "$back1" ]; then
if [ -z "$(find "$back1" -mtime +$duration -print > /dev/null)" ]
then
echo -n "$name's most recent backup is more recent than $duration "
echo "days: skipping"; continue
fi
echo "Rotating log $name (using a $duration day schedule)"
# 滚动，从最旧的日志开始，但要小心，可能
# 一个或多个文件尚不存在。
```

```
if [ -f "$back3" ]; then
echo "... -> $back4"; mv "$back3" "$back4"
fi
```

```
if [ -f "$back2" ]; then
echo "... -> $back3"; mv -f "$back2" "$back3"
fi
```

```
if [ -f "$back1" ]; then
echo "... -> $back2"; mv -f "$back1" "$back2"
fi
```

```
if [ -f "$name" ]; then
echo "... -> $back1"; mv -f "$name" "$back1"
fi
```

```
if [ $count -eq 0 ]; then
echo "Nothing to do: no log files big enough or old enough to rotate"
fi
```

列表 6-12: `rotatools` 脚本

为了具有最大的实用性，脚本与一个位于 `/var/log` 的配置文件一起工作，允许管理员为不同的文件指定不同的滚动计划。典型配置文件的内容在列表 6-13 中。

# 滚动脚本的配置文件：格式为 name=$duration，

# 其中 name 可以是 `/var/log` 中任何文件名。

# 持续时间以天计算。

```
ftp.log=30
lastlog=14
lpr.log=7
mail.log=7
```

```
netinfo.log=7
secure.log=7
statistics=7
system.log=14
# 如果持续时间为零，不滚动
tmp=0
```

列表 6-13: 滚动脚本的示例，在 `var/log`

## 工作原理

脚本与一个存在于 `/var/log` 的配置文件工作，允许管理员为不同的文件指定不同的滚动计划。该脚本的核心是那个复杂的 `find` 语句，它返回了 `/var/log` 中所有符合特定条件的、大于 0、不包含点、不以 `.conf` 结尾且文件名包含数字的文件。它不会进入子目录，因为它使用了 `maxdepth 1`。它通过 `sed` 移除了任何前导斜杠。

注意是好的！该脚本展示了 shell 编程的一个基本概念：避免重复工作。

## 运行脚本

脚本不接受任何参数，但它会打印正在滚动的日志

## 结果

`rotatools` 脚本易于使用，如列表 6-14 所示，但要小心权限，它可能需要以 `root` 运行。
