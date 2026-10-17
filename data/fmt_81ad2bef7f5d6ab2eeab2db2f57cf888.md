
```
root@ubuntu:~# who
agonzalez tty1
2022-07-23 12:21
agonzalez pts/0
2022-07-23 12:21 (192.168.122.1)
```

图 4.8：`who` 命令的输出示例。

命令 `w` 不仅显示登录到系统的用户信息，还显示他们正在执行的主命令，如图 4.9 所示：

```
root@ubuntu:~# w
13:15:56 up 58 min,  2 users,  load average: 0.01, 0.11, 0.07
USER     TTY      FROM             LOGIN@  IDLE   JCPU   PCPU  WHAT
agonzalez tty1       -              12:21   54:57  0.05s  0.03s  -bash
agonzalez pts/0  192.168.122.1     12:21   0.00s  0.10s  0.02s  sshd: agonzalez
```

图 4.9：`w` 命令的输出示例。

#### `userdel` 命令

该命令用于从系统中删除本地用户。它需要一个参数来指定要删除的用户。该命令最常用的选项显示在表 4.9 中：

| 选项 | 描述 |
| --- | --- |
| `-f, --force` | 此选项强制删除用户账户，即使该用户仍处于登录状态。 |
| `-r, --remove` | 删除用户主目录中的文件。 |

表 4.9：`userdel` 命令的常用选项

在图 4.10 中，删除了用户 `testuser2` 及其文件：

```
root@ubuntu:~# userdel -r testuser2
userdel: testuser2 mail spool (/var/mail/testuser2) not found
```

图 4.10：删除用户 `testuser2` 及其主目录的示例。

#### `passwd` 命令

此命令用于操作本地用户的密码和密码过期日期。使用 `useradd` 命令创建用户后，必须运行此命令来设置该用户的密码。管理员或普通用户可以在不带参数的情况下运行此命令来更改自己的密码。最常用的选项显示在表 4.10 中：

| 选项 | 描述 |
| --- | --- |
| `-l, --lock` | 锁定用户密码，仅 `root` 可用。 |
| `-u, --unlock` | 解锁用户密码。 |
| `-e, --expire` | 用户将在下次登录时被迫更改密码。 |
| `-n, --minimum DAYS` | 最小密码有效期，以天为单位。 |
| `-x, --maximum DAYS` | 最大密码有效期。 |
| `-w, --warning DAYS` | 提前多少天，用户将收到密码即将过期的警告。 |
| `-l, --inactive DAYS` | 密码过期后经过多少天账户将变为非活动状态并应被禁用。 |
| `-S, --status` | 输出关于密码状态的简短信息。 |

表 4.10：`passwd` 命令的常用选项

在图 4.11 中，展示了如何为某个用户设置密码以及如何锁定账户（命令 `passwd -S` 显示字母 `L` 表示已锁定）：

![](img/863afa537de4eed7deb11978bfbfa90e_119_0.png)

图 4.11：`passwd` 命令使用的输出示例。

#### `chage` 命令

此命令用于更改用户密码过期信息。常用选项显示在表 4.11 中：

| 选项 | 描述 |
|---|---|
| `-d, --lastday LAST_DAY` | 设置密码上次更改的日期。 |
| `-E, --expiredate EXPIRE_DATE` | 设置用户账户不再可访问的日期。 |
| `-I, --inactive INACTIVE` | 设置密码过期后账户被锁定前的非活动天数。 |
| `-l, --list` | 显示账户老化信息。 |
| `-m, --mindays MIN_DAYS` | 设置密码更改之间的最小天数为 `MIN_DAYS`。 |
| `-M, --maxdays MAX_DAYS` | 设置密码有效期的最大天数。 |
| `---, --warndays WARN_DAYS` | 设置更改密码前的警告天数。 |

表 4.11：`chage` 命令的常用选项

在图 4.12 中，用户 `testuser` 被迫在下次登录时更改密码，并显示了关于账户的信息：

```
root@ubuntu:~# chage -d 0 testuser
root@ubuntu:~# chage -l testuser
Last password change                  : password must be changed
Password expires                      : password must be changed
Password inactive                     : password must be changed
Account expires                       : never
Minimum number of days between password change  : 0
Maximum number of days between password change  : 99999
Number of days of warning before password expires : 7
```

图 4.12：使用 `chage` 命令的示例。

#### `last` 命令

此命令将显示登录系统的用户列表。可以使用表 4.12 中所示的一些选项来过滤输出：

| 选项 | 描述 |
| --- | --- |
| `-n, --limit number` | 告诉 `last` 显示多少行。 |
| `-p, --present time` | 显示在指定时间在线的用户。 |
| `-R, --nohostname` | 抑制显示主机名字段。 |
| `-s, --since time` | 显示自指定时间以来的登录状态。 |
| `-t, --until time` | 显示截至指定时间的登录状态。 |

表 4.12：`last` 命令的常用选项

在图 4.13 中，我们仅看到用户日志的最后三条条目：

```
root@ubuntu:~# last -n 3
agonzalez pts/0  192.168.122.1  Sat Jul 23 12:21  still logged in
agonzalez tty1    Sat Jul 23 12:21  still logged in
reboot  system boot  5.15.0-40-generic Sat Jul 23 12:17  still running

wtmp begins Sun Jun 26 20:41:10 2022
```

图 4.13：使用 `last` 命令的示例

### 用于操作组的命令

#### `groupadd` 命令

该命令将向系统添加一个本地组。表 4.13 展示了两个常用选项：

| 选项 | 描述 |
| :-- | :-- |
| `-g, --gid GID` | 组 ID 的数值。在迁移时很有用。 |
| `-r, --system` | 创建一个系统组。 |

表 4.13：`groupadd` 命令的常用选项

如图 4.14 所示，创建了一个名为 `example` 的新组：

```
root@ubuntu:~# groupadd example
```

图 4.14：使用 `groupadd` 命令的示例。

#### `groups` 命令

此简单命令显示调用该命令的用户所属的组。指定参数将显示该用户所在的组。图 4.15 展示了两种场景：

```
root@ubuntu:~# groups
root
root@ubuntu:~# groups agonzalez
agonzalez : agonzalez adm cdrom sudo dip plugdev lxd
```

图 4.15：使用 `groups` 命令的示例。

#### `groupmod` 命令

`groupmod` 命令允许修改指定组的某些参数。表 4.14 展示了常用选项：

| 选项 | 描述 |
| :-- | :-- |
| `-g, --gid GID` | 组的新组 ID。 |
| `-n, --new-name NAME` | 组的新名称。 |

表 4.14：`groupmod` 命令的常用选项

如图 4.16 所示，之前创建的组 `example` 被重命名为 `writers`：

```
root@ubuntu:~# groupmod -n writes example
```

图 4.16：使用 `groupmod` 命令的示例。

#### `groupdel` 命令
