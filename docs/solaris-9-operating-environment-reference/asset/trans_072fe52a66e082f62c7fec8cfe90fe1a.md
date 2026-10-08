

# 1530

# view

# 摘要

# 另请

ctags(1), ed(1), edit(1), ex(1), intro(1), attributes(5), environ(5),
largefile(5), standards(5)
Solaris 高级用户指南

# 作者

vi 和 ex 是由加利福尼亚大学伯克利分校计算机科学系、电气工程与计算机科学系开发的。

# view — 基于 ex 的面向屏幕的视觉化显示编辑器

```
/usr/bin/view [- -s] [-L] [-R [filename] [-S] [-t tag] [-v]
[-V] [-x] [-wn] [-C]
/usr/xpg4/bin/view [- -s] [-1] [-L] [-R [filename] [-t tag]
[-V] [-x] [-wn] [-C] [+command |c command] filename...
/usr/bin/view [- -s] [-1] [-L] [-R [filename] [-t tag] [-v]
[-x] [-wn] [-C] [+command |c command] filename...
/usr/xpg4/bin/view [- -s] [-1] [-L] [-R [filename] [-t tag] [-v]
[-V] [-x] [-wn] [-C] [+command |c command] filename.
```

# 描述

参见 vi(1)。

# vipw — 编辑密码文件

# 摘要

```
/usr/ucb/vipw
```

# 描述

vipw 在编辑密码文件时设置相应的锁，并在密码文件解锁后进行任何必要的处理。如果密码文件正在被编辑，系统会提示你稍后再试。除非环境变量 VISUAL 或 EDITOR 指明了替代编辑器，否则将使用 vi(1) 编辑器。
vip 对 root 密码条目进行多次一致性检查，不允许安装带有“损坏”root 条目的密码文件。它还会检查 /etc/shells 文件以验证 root 的登录 shell。

# 文件

```
/etc/passwd
/etc/shells *
```

# volcancel

# 属性

有关以下属性的描述请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNWscpu |

# 另请

passwd(1), vi(1), passwd(4), attributes(5)

# volcancel — 取消当前不在驱动器中的可移除介质请求

# 摘要

```
/usr/lib/vold/volcancel [-n] [volume]
```

# 描述

volcancel 取消访问特定软磁盘或 CD-ROM 文件系统的请求。当包含文件系统的可移除介质不在驱动器中时，此命令非常有用。

使用路径 /vol/rdsk/name_of_volume 来指定卷。如果调用时不指定卷名，volcancel 将检查卷管理（Volume Management）是否正在运行。

# 选项

- -n 显示到到设备名称翻译表中的别名。

# 示例

以下示例取消了访问未命名 CD-ROM 的请求。
castle@ /usr/lib/vold/volcancel vol/rdsk/unnamed_cdrom

你可以使用 volcancel 命令检查卷管理是否正在运行。在接下来的示例中，卷管理正在运行。

```
castle@ /usr/lib/vold/volcancel
castle@
```

在接下来的示例中，卷管理未运行，并显示消息 volume management is not running。

```
castle@ /usr/lib/vold/volcancel
usr/lib/vold/volcancel: volume management is not running
castle@
```

# 1532

# volcheck

# 属性

有关以下属性的描述请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUM+volume |

# 另请

- volcheck(1), volmissing(1), rmount(1M), void(1M), rmount.conf(4),
vold.conf(4), attributes(5), volfs(7FS)

# volcheck — 检查驱动器中的介质

# 摘要

/usr/bin/volcheck [-v] [-i secs] [-t secs] pathname

# 描述

volcheck 命令告诉卷管理按顺序查看每个 dev/pathname，并确定驱动器是否插入了新介质。

默认操作是让 volcheck 在所有由卷管理管理的的可检查介质上运行。

> 警告 — 由于许多软磁盘驱动器的硬件限制，检查介质会导致软磁盘驱动器的机械动作。持续轮询软磁盘驱动器会磨损驱动器。建议仅在高频使用期间对软磁盘进行轮询。

# 选项

- -i secs 将设备检查频率设置为 secs 秒。默认为 2 秒。最小频率为 1 秒。

- -t secs 在接下来的 secs 秒内检查指定的设备。允许的最大秒数为 28800 秒，即 8 小时。

-v 详细模式。

# 参数

- pathname 指定的设备路径。

# 示例

以下示例让 volcheck 查看驱动器以检查是否有新介质。

```
castle$ volcheck -v /dev/diskette
```

# volcheck — 检查介质 1533

以下示例让卷管理每隔 2 秒检查一次，在过去的 600 秒内检查新介质。
```
castle$ volcheck -i 2 -t 600 /dev/diskette
```

# 描述

volcheck 命令告诉卷管理按顺序查看每个 dev/pathname，并确定驱动器是否插入了新介质。

默认操作是让 volcheck 在所有由卷管理管理的的可检查介质上运行。

> 警告 — 由于许多软磁盘驱动器的硬件限制，检查介质会导致软磁盘驱动器的机械动作。持续轮询软磁盘驱动器会磨损驱动器。建议仅在高频使用期间对软磁盘进行轮询。

# 选项

- -i secs 将设备检查频率设置为 secs 秒。默认为 2 秒。最小频率为 1 秒。

- -t secs 在接下来的 secs 秒内检查指定的设备。允许的最大秒数为 28800 秒，即 8 小时。

-v 详细模式。

# 参数

- pathname 指定的设备路径。

# 示例

以下示例让 volcheck 查看驱动器以检查是否有新介质。

```
castle$ volcheck -v /dev/diskette
```

# volctl — 卷控制

# 属性

有关以下属性的描述请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUM |

# 另请

volcheck(1), volmissing(1), attributes(5)

# volctl — 卷控制 1534

# 描述

volctl 控制卷。

# 属性

参见 attributes(5) 关于以下属性：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUM |

# 另请

volcheck(1), volmissing(1), attributes(5)

# volctl — 卷控制 1535

# 描述

volctl 控制卷。

