
`passwd` 命令的常用用途是设置或修改用户密码；然而，你也可以使用此命令修改密码年龄属性，并锁定或解锁其账户。表 6-2 列出了短格式和长格式的一些关键选项。

| 选项 | 描述 |
| --- | --- |
| `-d` (`--delete`) | 删除用户密码，但不使账户过期。 |
| `-e` (`--expire`) | 强制用户在下次登录时更改密码。 |
| `-i` (`--inactive`) | 定义密码过期后账户锁定前的非活动天数。它对应于 `shadow` 文件中的第 7 字段。 |
| `-l` (`--lock`) | 锁定用户账户。 |
| `-n` (minimum) | 指定更改密码前必须经过的天数。它对应于 `shadow` 文件中的第 4 字段。 |
| `-S` (`--status`) | 显示用户的状态信息。 |
| `-u` (`--unlock`) | 解锁已锁定的账户。 |
| `-w` (`--warning`) | 指定用户在密码实际过期前接收更改提醒的持续数。它对应于 `shadow` 文件中的第 6 字段。 |
| `-x` (`--maximum`) | 表示用户密码过期前必须更改的最大有效数。它对应于 `shadow` 文件中的第 5 字段。 |

### 表 6-2 `passwd` 命令选项

这些标志中的大部分将在接下来的几次练习中使用。

# 练习 6-2：使用 `passwd` 设置并确认密码年龄

此练习应在 `server1` 上以 `root` 身份执行。

在本次练习中，你将使用 `passwd` 命令为 `user200` 配置密码年龄。你将 `mindays` 设置为 10，`maxdays` 设置为 90，`warndays` 设置为 14，并验证新设置。

接下来，你将非活动天数设置为 5，并确保用户在下次登录时被强制更改密码。你将通过另一个验证来完成练习。

- 1. 为 `user200` 设置密码年龄属性，分别为 `mindays` (`-n 10`)、`maxdays` (`-x`) 90 和 `warndays` (`-w`) 14：

```
[root@server1 ~]# passwd -n 10 -x 90 -w 14 user200
```

- 2. 确认新设置：

```
[root@server1 ~]# passwd -s user200
user200 PS 2019-09-14 10 90 14 (Password set, SHA512 crypt.)
```

输出确认了三个新设置（10, 90 和 14）。

- 3. 将非活动天数设置为 5：

```
[root@server1 ~]# passwd -i 5 user200
```

- 4. 确认新设置：

```
[root@server1 ~]# passwd -s user200
user200 PS 2019-09-14 10 90 15 (Password set, SHA512 crypt.)
```

输出验证了新设置（5）。

- 5. 确保用户在下次登录时强制更改密码：

```
[root@server1 ~]# passwd -e user200
```

- 6. 设置新设置进行确认：

```
[root@server1 ~]# passwd -s user200
user200 PS 1969-12-31 10 90 14 (Password set, SHA512 crypt.)
```

输出显示了一个在 UNIX 时间之前的日期。该用户在下次尝试登录时将会被提示更改密码。

## `usermod` 命令

`usermod` 命令的常用用途是修改用户的属性，但它也可以锁定或解锁其账户。表 6-3 解释了短格式和长格式的两个选项。

| 选项 | 描述 |
| --- | --- |
| `-L` (`--lock`) | 通过在哈希密码字符串之前的密码字段开头放置单个感叹号 (`!`) 来锁定用户账户。 |
| `-U` (`--unlock`) | 通过移除密码字段开头的感叹号 (`!`) 来解锁用户账户。 |

### 表 6-3 用于用户锁定/解锁的 `usermod` 命令选项

让我们在下次练习中应用这些选项。

# 练习 6-3：使用 `usermod` 和 `passwd` 锁定和解锁用户账户

此练习应在 `server1` 上以 `root` 身份执行。

在本次练习中，你将使用 `usermod` 和 `passwd` 命令禁用 `user200` 的登录能力。你将验证此更改并将其撤销。

- 1. 从 `shadow` 文件获取 `user200` 的当前密码信息：

```
[root@server1 ~]# grep user200 /etc/shadow
user200:$6$gnv93VTOeNU94s.$6PEdcB31g1IULxbbEAKPMwW8SPXnyston.3nif/kc15Aw8Kt2
TnHI000ug/rNBs9Bower132rzVmp1:01:90:14:5::
```

未锁定的用户账户密码字段以感叹号 (`!`) 开头。上面的输出表明账户目前处于锁定状态。

- 2. 锁定账户：

```
[root@server1 ~]# usermod -L user200
```

- 3. 确认更改：

```
[root@server1 ~]# grep user200 /etc/shadow
user200:$6$gnv93VTOeNU94s.$6PEdcB31g1IULxbbEAKPMwW8SPXnyston.3nif/kc15Aw8Kt2
TnHI000ug/rNBs9Bower132rzVmp1:01:90:14:5::
```

- 4. 解锁账户：

```
[root@server1 ~]# usermod -U user200
```

- 5. 确认撤销：

```
[root@server1 ~]# grep user200 /etc/shadow
user200:$6$gnv93VTOeNU94s.$6PEdcB31g1IULxbbEAKPMwW8SPXnyston.3nif/kc15Aw8Kt2
TnHI000ug/rNBs9Bower132rzVmp1:01:90:14:5::
```

# Linux 组及其管理

Linux 组是用户集合，允许对文件进行协作。组信息存储在 `/etc/group` 文件。

## `groupadd`, `groupmod` 和 `groupdel` 命令

这组管理命令用于添加、修改和删除组。`groupadd` 命令添加项。表 6-4 列出了 `groupadd` 的选项。

| 选项 | 描述 |
| --- | --- |
| `-g` (`--gid`) | 指定给组的 GID |
| `-o` (`--unique`) | 创建具有相同 GID 的组 |
| `-r` | 创建小于 1000 的系统组 |
| `group` | 指定组名 |

### 表 6-4 `groupadd` 选项

`groupadd` 命令从 `login.defs` 文件获取默认值。

你可以使用 `groupmod` 命令修改组属性。该命令的语法与 `groupadd` 非常相似，大部分选项相同。唯一的标志是 `-n`，它可以更改现有组的。

`groupdel` 命令非常直接。它从组文件和 `shadow` 文件移除指定的组。

# 练习 6-4：创建组并添加成员

此练习应在 `server1` 上以 `root` 身份执行。在本次练习中，你将创建一个 GID 为 5000 的 `linuxadm` 以及另一个共享 GID 5000 的 `dba` 组。你将 `user1` 作为次要成员添加到 `groupadm`。

- 1. 创建 GID 为 5000 的组 `linuxadm`：

```
[root@server1 ~]# groupadd -g 5000 linuxadm
```

- 2. 创建一个与 `groupadm` GID 相同的 `dba` 组：

```
[root@server1 ~]# groupadd -o -g 5000 dba
```

- 3. 确认组的创建：

```
[root@server1 ~]# grep linuxadm /etc/group
linuxadm:x:5000:
[root@server1 ~]# grep dba /etc/group
dba:x:5000:
```

组的 GID 是相同的。

- 4. 使用 `usermod` 命令将 `user1` 作为次要成员添加到 `dba`。用户现有的成员关系必须保持完整。

```
[root@server1 ~]# usermod -aG dba user1
```

- 5. 通过从组文件中提取项并运行 `id` 和 `groups` 命令验证 `user1` 更新的组成员信息：

```bash
[root@server1 ~]# grep dba /etc/group
dba:x:5000:user1
[root@server1 ~]# id user1
uid=1000(user1) groups=1000(user1),5000(dba)
[root@server1 ~]# groups user1
user1 : user1 dba
```

输出确认了 `user1` 的主组（`user1`）和辅助组（`dba`）成员关系。
