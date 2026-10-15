

```
# 我们假设 root 的 cron 中已有针对“daily”、“weekly”和
# “monthly”任务的条目。如果找不到与指定项匹配的内容，那么，
# 这就是一个错误。但首先，我们会尝试获取命令（如果存在
# 匹配项，这也是我们所预期的）。

job="$(awk "NF > 6 && $1/ { for (i=7;i<=NF;i++) print $i }" $rootcron)"

if [ -z "$job" ] ; then  # 没有任务？奇怪。好吧，这是一个错误。
 echo "所以：错误：在 $rootcron 中未找到 $1 任务" >&2
 exit 1
fi

SHELL=$(which sh)      # 与 cron 的默认设置保持一致

eval $job              # 任务完成后我们将退出。
```

清单 6-11：docron 脚本

## 工作原理

位于 /etc/daily、/etc/weekly 和 /etc/monthly（或 /etc/cron.daily、/etc/cron.weekly 和 /etc/cron.monthly）中的 cron 任务与用户 crontab 文件的设置方式完全不同：每个都是一个目录，包含一组脚本，每个任务一个脚本，由 cron 设施按照 /etc/crontab 文件中的指定运行。更让人困惑的是，/etc/crontab 文件的格式也不同，因为它增加了一个额外的字段，用于指明应该以哪个有效用户 ID 来运行任务。

/etc/crontab 文件指定了一天中的小时（在下面输出的第二列中），以完全不同于你作为普通 Linux 用户所见的格式来运行 daily、weekly 和 monthly 任务，如下所示：

```
$ egrep '(daily|weekly|monthly)' /etc/crontab
# 运行 daily/weekly/monthly 任务。
15   3   *   *   *   root    periodic daily
30   4   *   *   6   root    periodic weekly
30   5   1   *   *   root    periodic monthly
```

如果系统在每天凌晨 3:15、周六早上 4:30 以及每月 1 日早上 5:30 没有运行，那么 daily、weekly 和 monthly 任务会怎样？什么也不会发生。它们就是不会运行。

我们没有尝试强制 cron 运行这些任务，而是编写了脚本来识别此文件中的任务①，并在最后一行用 eval 直接运行它们②。从该脚本调用任务与作为 cron 任务的一部分调用它们之间的唯一区别是：当任务从 cron 运行时，其输出流会自动转换为电子邮件消息，而此脚本将输出流显示在屏幕上。

当然，你也可以通过如下方式调用脚本来复制 cron 的电子邮件行为：

```
./docron weekly | mail -E -s "weekly cron job" admin
```

## 运行脚本

此脚本必须以 root 身份运行，并且有一个参数——要么是 daily、weekly 或 monthly——用于指明你想运行哪一组系统 cron 任务。与往常一样，我们强烈建议使用 sudo 以 root 身份运行任何脚本。

## 结果

除非在脚本内部或 cron 脚本派生的某个任务中遇到错误，否则此脚本基本上没有直接输出，只显示从 crontab 中运行的脚本的结果。

## 修改脚本

有些任务不应该每周或每月运行多次，因此确实应该有某种检查来确保它们不会更频繁地运行。此外，有时重复的系统任务可能已经由 cron 运行了，所以我们不能一概而论地认为如果 docron 没有运行，这些任务就没有运行。

一种解决方案是创建三个空的时间戳文件，分别用于 daily、weekly 和 monthly 任务，然后向 /etc/daily、/etc/weekly 和 /etc/monthly 目录中添加新条目，用 touch 更新每个时间戳文件的最后修改日期。这可以解决一半的问题：docron 随后可以检查重复 cron 任务上次被调用的时间，如果距离上次运行时间不足以证明需要再次运行，则退出。

这个解决方案无法处理的情况是：在 monthly cron 任务上次运行六周后，管理员运行 docron 来调用 monthly 任务。然后四天后，有人忘记关机，monthly cron 任务又被调用了。那个任务怎么知道最终没有必要运行 monthly 任务呢？

可以向适当的目录添加两个脚本。一个脚本必须先从 run-script 或 periodic（调用 cron 任务的标准方式）运行，然后可以关闭目录中所有其他脚本的可执行位，但其伙伴脚本除外；伙伴脚本会在 run-script 或 periodic 扫描并确认无事可做之后重新打开可执行位：目录中的所有文件看起来都不可执行，因此 cron 不会运行它们。然而，这并不是一个好解决方案，因为无法保证脚本的求值顺序，如果我们无法保证新脚本的运行顺序，整个解决方案就会失败。

