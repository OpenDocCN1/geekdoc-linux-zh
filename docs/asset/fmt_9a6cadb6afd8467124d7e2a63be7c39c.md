
USER PID %CPU MEM VSZ RTT STAT TIME COMMAND

...output omitted...

root 2983 100 0.22860 1744 ? R 21:08

      0.23 mdsum /dev/zero

root 2967 101 0.22860 1732 ? RN 21:08

      0.23 shaisum /dev/zero

[serverb ~]$

```
2.2. 识别每个最高 CPU 消耗者的当前 `nice` 值。
```

[serverb ~]$ ps -o pid,pcpu,nice,comm $(pgrep shaisum;pgrep mdsum)

PID %CPU NI COMMAND

2967 99.6 2 shaisum

2983 99.7 -2 mdsum
```

2.3. 使用 `sudo renice -n 10 2967 2983` 命令将每个进程的 `nice` 值调整为 10。使用在前述命令输出中识别出的 PID 值。

```
[serverb ~]$ sudo renice -n 10 2967 2983
[sudo] password for student: student
2967 (process ID) old priority 2, new priority 10
2983 (process ID) old priority -2, new priority 10
```

2.4. 验证每个进程的当前 `nice` 值为 10。

```
[serverb ~]$ ps -o pid,pcpu,nice,comm $(pgrep shaisum;pgrep mdsum)

PID %CPU NI COMMAND

2967 99.6 10 shaisum

2983 99.7 10 mdsum
```

2.5. 退出 serverb。

```
[serverb ~]$ exit
logout
Connection to serverb closed.
[student@workstation ~]
```

## 评估

在 `workstation` 上，运行 `lab tuning-review grade` 命令以确认本次实验成功。

```
[student@workstation ~]$ lab tuning-review grade
```

## 结束

在 `workstation` 上，运行 `lab tuning-review finish` 脚本完成本次练习。

```
[student@workstation ~]$ lab tuning-review finish
```

本实验结束。

## 总结

在本章中，你学习了：

- `tuned` 服务通过特定的配置来满足需求并修改设置。
- 回滚由 `tuned` 服务所做的更改。
- `nice` 命令在进程启动时分配设置设置，以满足访问的优先级。
- `renice` 命令在进程运行时修改以满足访问的优先级。

# 第 4 章

# 使用 ACL 控制文件访问

## 目标

解释并设置文件的访问控制列表 (`ACLs`)，以处理复杂的用户和组访问情况。

## 目标

- 描述 `ACL` 的用例，识别设置了 `ACL` 的文件，并通过 `ls` 和 `getfacl` 查看并解释 `ACL`。
- 描述 `ACL` 掩码和权限优先级。

## 章节

- 解释文件 `ACL`（引导实验）
- 使用 `ACL` 安全文件（引导实验）

## 实验

使用 `ACL` 控制文件访问

![](img/3c5df78dee32860001366607c8aa7b_110_0.png)

## 解析文件 ACL

## 访问控制列表概念

标准文件权限在适用于单个所有者和单个指定组时是足够的。某些用例需要为命名用户和组设置文件权限。访问控制列表（`ACL`）提供了这种功能。

通过 `ACL`，你可以根据用户名、组名、UID 或 GID 使用与文件权限相同的标志（读、写、执行）来授予权限。这些文件所有者和组之外的用户和组分别被称为命名用户和命名组，因为它们不在长列表中，而是在 `ACL` 中。

用户可以对其拥有的文件和目录设置 `ACL`。拥有 `CAP_OWNER` 能力的特权用户可以对任何文件或目录设置 `ACL`。新文件和子目录会自动从父目录的默认 `ACL` 继承（如果已设置）。与普通文件访问规则类似，父目录层次结构至少需要设置搜索（执行）权限以允许用户和组访问。

## 文件系统 ACL 支持

文件系统必须带有 `ACL` 支持才能挂载。`XFS` 文件系统内置了 `ACL` 支持。其他文件系统，例如 Red Hat Enterprise Linux 8 上的 `ext3` 或 `ext4`，默认启用了 `acl`，在旧版本中你应该确认是否启用了 `ACL` 支持。要启用文件系统 `ACL` 支持，请在 `mount` 命令中使用 `acl` 选项，或在 `/etc/fstab` 配置文件的文件系统条目中使用。

## 查看和解释 ACL 权限

`ls -l [host content] ls -l reports.txt` 显示 `ACL` 设置：

```
[user@host content] ls -l reports.txt
-rw-r--+ 1 user operators 30 Mar 19 23:56 reports.txt
```

10 位权限字符串末尾加号 (`+`) 表示该文件存在带有条目的扩展 `ACL` 结构。

## 第 4 章 | 使用 ACL 控制文件访问

user:
显示用户的 `ACL` 设置，与标准用户文件设置相同；**rwx**。

group:
显示当前的 `ACL` 掩码（mask）设置，而不是组所有者设置；**rw-**。

other:
显示其他的 `ACL` 设置，与标准其他文件设置相同；无访问。

> **重要**
使用 `chmod` 修改带有 `ACL` 的文件的组权限不会更改组组权限，但会更改 `ACL` 掩码。如果目的是更新文件的组所有者权限，请使用 `setfacl -m g:perms file`。

## 查看文件 ACL

要显示文件上的 `ACL`，请使用 `getfacl file`：

```
[user@host content]$ getfacl reports.txt
# file: reports.txt
# owner: user
# group: operators
user:rwx
user:consultant3::-
user:1005:rwx #effective:rw-
group::rwx #effective:rw-
group:consultant1:r-
group:2210:rwx #effective:rw-
mask:rw-
other::---
```

检查上述示例的每个部分：

注释项：

```
# file: reports.txt
# owner: user
# group: operators
```

前三行是注释，用于标识文件名、所有者（**user**）和组所有者（**operators**）。如果有任何额外的文件标记位（例如 `setuid` 或 `setgid`），则会出现第四行注释，显示设置了哪些标记位。

用户项：

```
user::rwx
user:consultant3::-
user:1005:rwx #effective:rw-
```

文件所有者权限。**user** 拥有 **rwx**。

命名用户权限。每个与此文件关联的命名用户有一个条目。`consultant3` 没有权限。

命名用户权限。UID `1005` 拥有 `rwx`，但掩码将有效权限限制为 `rw`。

组项：

```
group::rwx          #effective:rw-
group:consultant1:r----
group:2210:rwx      #effective:rw-
```

- 组所有者权限。`operators` 拥有 `rwx`，但掩码将有效权限限制为 `rw`。
- 命名组权限。每个与此文件关联的命名组有一个条目。`consultant1` 只有 `r`。
- 命名组权限。GID `2210` 拥有 `rwx`，但掩码将有效权限限制为 `rw`。

掩码项：

```
mask::rw-
```

掩码设置显示了所有命名用户、组所有者和命名组可能的最大权限。UID `1005` 和 GID `2210` 无法执行此文件，尽管每个条目都具有执行权限。

其他项：

```
other::---
```

其他或“世界”权限。所有其他 UID 和 GID 没有任何权限。

## 查看目录 ACL

要显示目录上的 `ACL` 设置，请使用 `getfacl` 目录命令：

```
[user@host]$ getfacl
# file:
# owner: user
# group: operators
# flags: -s-
user::rwx
user:consultant3::-
user:1005:rwx
group::rwx
group:consultant1:r-x
```
