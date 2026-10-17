
root tty6 Tue 16 13:01-13:01 (00:00)

root tty6 Tue 16 13:01-13:01 (00:00)

root tty6 Tue 16 13:02-13:02 (00:00)

root tty6 Tue 16 13:02-13:02 (00:00)

root tty6 Tue 16 13:03-13:03 (00:00)

root tty6 Tue 16 13:03-13:03 (00:00)

使用 `pwck` 检查 `/etc/passwd` 文件，查找所有类型的问题。该命令对 `passwd` 文件进行健康检查，虽然它不是日志文件，但它是应该密切监控的文件。以下是运行 `pwck` 命令发现的 `passwd` 文件中的两个错误：第一个用户有 `passwd` 条目但在系统中没有文件；第二个用户的家目录名称错误。

![](img/6969df54e516231f8e64fd1177ac1127_1046_0.png)

denise - 系统未找到登录名
jlance:hadsf4353hadsfa:10:20:Joe Lance:/net/sys1/net/home/jlance:/usr/bin/sh
未找到目录

使用 `grpck` 检查 `/etc/group` 文件，查找所有类型的问题。该命令对组文件进行检查，该文件也必须仔细监控。以下示例显示了一个没有用户的组条目，以及一个包含在 `passwd` 文件中没有条目的用户的组：

![](img/6969df54e516231f8e64fd1177ac1127_1046_1.png)

```
database:10:
```
此组没有用户

```
development1*:200:nadmin,charles,william
```
william - 密码文件中未找到登录名

## 逻辑卷审查

检查 `/etc/lvmtab` 文件的完整性。一种方法是将 `strings lvmtab` 与 `vgscan -v -p` 进行比较。在示例中，将 `strings lvmtab` 的输出作为 `vgscan` 的输入，产生了一个未使用的卷组：

```
# vgscan -v -p
/dev/vgsys
/dev/dsk/c2d0s2
/dev/dsk/c3d0s2
/dev/vgtext
/dev/dsk/c4d0s2
/dev/dsk/c5d0s2
/dev/vgroot
/dev/dsk/c4d0s2
/dev/dsk/c5d0s2
```

卷组 `/dev/vg00` 未匹配到任何物理卷。

```
strings lvmtab
```
作为 `vgscan` 的输入，产生了一个未使用的卷组：

```
/dev/vgsys
/dev/dsk/c2d0s2
/dev/dsk/c3d0s2
/dev/vgtext
/dev/dsk/c4d0s2
/dev/dsk/c5d0s2
/dev/vgroot
/dev/dsk/c4d0s2
/dev/dsk/c5d0s2
```

以下是未识别为卷组一部分的磁盘结果：

```
pvsplay: Couldn't query physical volume "/dev/dsk/c0d0s2":
```

指定的路径未对应连接到任何卷组的物理卷。这一事实意味着磁盘在物理上已连接到系统，但不在卷组中。

## 性能

性能是一门独立的学科。你不会在系统审计中进行详细的性能分析。然而，你可以获取系统的快照，稍后可以坐下来进行审查，这可能会提供一些有趣的结果。

作为审计的一部分，你应该运行以下性能相关的命令：`vmstat`、`iostat`、`uptime`、`sar -u` 和 `sar -b`。以下是运行 `sar -u` 和 `sar -b` 的示例：

```
# sar -u 5 5
```

HP-UX system 9000/819

| time | usr | sys | wio | idle |
| :--- | :--- | :--- | :--- | :--- |
| 19:08:02 | | | | |
| 19:08:07 | 1 | 2 | 1 | 96 |

## 系统审计简介

```
19:08:12    1    0    99
19:08:17    0    1    99
19:08:22    1    2    98
19:08:27    1    0    99
Average     1    1    0    98
```

等待，上一个块是命令输出的一部分：

```
# sar -b 5 10
```

```
HP-UX system1  9000/819
```
fi
done
