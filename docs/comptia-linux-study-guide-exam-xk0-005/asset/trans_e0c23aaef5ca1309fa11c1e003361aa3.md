

## 表 10.6 passwd 命令的常用选项

| 短选项 | 长选项 | 描述 |
| :--- | :--- | :--- |
| -d | --delete | 删除账户的密码。 |
| -e | --expire | 将账户密码设置为已过期。用户下次登录时必须修改账户密码。 |
| -i | --inactive | 设置密码过期后未更改的天数，超过此天数账户将被停用。 |
| -l | --lock | 在 /etc/shadow 文件中的账户密码前添加一个感叹号 (!)，从而有效防止用户通过该账户密码登录系统。 |
| -n | --minimum | 设置密码更改后允许再次更改密码的最小天数。 |
| -S | --status | 显示账户的密码状态。 |
| -u | --unlock | 移除 /etc/shadow 文件中账户密码前的感叹号 (!)。 |
| -w | --warning 或 --warndays | 设置在密码过期前向用户发出警告的天数。 |
| -x | --maximum 或 --maxdays | 设置要求更改密码的天数。这是密码的过期日期。 |

表 10.6 中的某个选项需要更多的解释，那就是 `–S` 选项。示例展示在列表 10.13 中。

**列表 10.13：** 使用 `passwd -S` 查看账户的密码状态

```
$ sudo passwd –S DAdams
DAdams PS 2021-10-01 0 99999 7 -1 (Password set, SHA512 crypt.)
$
```

在列表 10.13 中，显示了 DAdams 账户的密码状态。状态包含账户密码的状态，该状态可以是可用密码 (P)、无密码 (NP) 或锁定密码 (L)。在密码状态之后，显示最后一次密码更改日期，接着是密码的最小、最大、警告和停用设置。括号内显示额外的状态信息，包括密码是否已设置以及用于保护密码的哈希算法。

你还可以使用 `chage` 工具以更具可读性的格式显示类似的密码信息，如列表 10.14 所示。

**列表 10.14：** 使用 chage -l 查看账户的密码状态

```
$ sudo chage -l DAdams
Last password change : Oct 02, 2021
Password expires : never
Password inactive : never
Account expires : never
Minimum number of days between password change : 0
Maximum number of days between password change : 99999
Number of days of warning before password expires : 7
$
```

chage 程序也可以修改密码设置。你可以使用各种命令选项（详情见其 man 页面），或者如列表 10.15 所示，以交互方式使用 chage 工具。

**列表 10.15：** 使用 chage 更改账户密码的设置

```
$ sudo chage DAdams
Changing the aging information for DAdams
Enter the new value, or press ENTER for the default

Minimum Password Age [0]: 5
Maximum Password Age [99999]: 30
Last Password Change (YYYY-MM-DD) [2021-10-02]:
Password Expiration Warning [7]: 15
Password Inactive [-1]: 3
Account Expiration Date (YYYY-MM-DD) [-1]:
$
```

请注意列表 10.15 中，密码过期警告被设置为 15 天。如果你的公司允许两周的假期，这是一个很好的设置。

## 修改账户

用于修改账户的工具是 usermod 程序。与 passwd 命令类似，你可以锁定和解锁账户，如列表 10.16 所示。

**列表 10.16：** 使用 usermod 锁定账户

```
$ sudo usermod -L DAdams
$
$ sudo passwd -S DAdams
DAdams LK 2021-10-01 5 30 15 3 (Password locked.)
$
$ sudo getent shadow DAdams
DAdams: !$$6B/zCaNx[...]:17806:5:30:15:3::
$
$ sudo usermod -U DAdams
$
$ sudo passwd -S DAdams
DAdams PS 2021-10-01 5 30 15 3 (Password set, SHA512 crypt.)
$
```

请注意列表 10.16 中，使用 usermod -L 命令锁定 DAdams 账户。passwd -S 命令显示密码状态为 LK，表示已锁定。在列表 10.16 中，snipped getent 工具的输出显示在 DAdams 账户的密码前添加了一个感叹号 (!)，这就是导致账户被锁定的原因。然后通过 usermod -U 命令移除锁定，并重新检查状态。

你可以通过 usermod 工具的开关对多个用户账户进行修改。常用选项如表 10.7 所示。

## 表 10.7 usermod 命令的常用选项

| 短选项 | 长选项 | 描述 |
| :--- | :--- | :--- |
| `-c` | `--comment` | 修改注释字段的内容。 |
| `-d` | `--home` | 设置新的用户主目录规范。与 `-m` 选项一起使用可将当前目录的文件移动到新位置。 |
| `-e` | `--expiredate` | 修改账户的过期日期。使用 `YYYY-MM-DD` 格式。 |
| `-f` | `--inactive` | 修改密码过期后未更改且账户将被停用的天数。`-1` 表示账户永远不会被停用。 |
| `-g` | `--gid` | 更改账户的默认组成员身份。 |
| `-G` | `--groups` | 更新账户的附加组成员身份。如果仅指定新的组成员身份，请使用 `-a` 选项以避免移除其他组成员身份。 |
| `-l` | `--login` | 将账户的用户名修改为指定的名称。不修改主目录。 |
| `-L` | `--lock` | 通过在账户的 `/etc/shadow` 文件记录中的密码前添加感叹号来锁定账户。 |
| `-s` | `--shell` | 更改账户的 shell。 |
| `-u` | `--uid` | 修改账户的用户标识 (UID) 编号。 |
| `-U` | `--unlock` | 通过移除账户的 `/etc/shadow` 文件记录中密码前的感叹号来解锁账户。 |

请注意，你可以更改账户的默认组，并为账户提供附加组成员身份。账户组将在本章后面详细讲解。

**usermod** 真正方便的地方在于一种情况：你创建了账户但忘记检查发行版的账户创建配置设置。列表 10.17 展示了在 Ubuntu Desktop 发行版上这种情况的一个示例。

**列表 10.17：** 使用 usermod 修改账户

```
$ sudo useradd -md /home/DBowman DBowman
$ 
$ sudo getent passwd DBowman
DBowman:x:1003:1003::/home/DBowman:/bin/sh
$ 
$ sudo usermod -s /bin/bash DBowman
$ 
$ sudo getent passwd DBowman
DBowman:x:1003:1003::/home/DBowman:/bin/bash
$ 
```

在列表 10.17 中，创建用户账户 **DBowman**，但当使用 **getent** 工具检查账户记录时，显示使用的是 `/bin/sh` shell 而不是 Bash shell。为了修复此问题，使用带有 `-s` 选项的 **usermod** 命令，将账户的 shell 修改为 `/bin/bash` shell。

## 删除账户

在 Linux 上删除账户相当简单。**userdel** 工具是完成此任务的关键工具。最常用的选项是 `-r` 开关。此选项将删除账户的主目录树及其内的任何文件。列表 10.18 展示了删除账户的一个示例。

**列表 10.18：** 使用 userdel 删除账户

```
$ sudo ls -a /home/DBowman
. .. .bash_logout .bashrc examples.desktop .profile
$ 
$ sudo getent passwd DBowman
DBowman:x:1003:1003::/home/DBowman:/bin/bash
$ 
$ sudo userdel -r DBowman
userdel: DBowman mail spool (/var/mail/DBowman) not found
$ 
$ sudo ls -a /home/DBowman
ls: cannot access ‘/home/DBowman’: No such file or directory
$
$ sudo getent passwd DBowman
$
```

列表 10.18 中的前两个命令显示 /home/DBowman 目录存在且其中包含文件，并且该账户在 /etc/passwd 文件中确实有记录。第三个命令包含 userdel -r 命令，用于删除账户以及主目录。请注意生成了一条错误消息，指出未找到 /var/mail/DBowman 文件。这不是问题。它仅表示在创建账户时未创建此文件。最后，最后两个命令显示 /home/DBowman 目录及其文件已被移除，并且 /etc/passwd 文件不再包含 DBowman 账户的记录。

![](img/c0a399aca0d18f8822d714ad0a173123_374_0.png)

## 实际场景

### 账户删除策略

在删除系统上的任何账户之前，请与你的雇主的人力资源部门 staff 和/或法律部门或法律顾问核实。可能存在关于已离职或退休员工以及已离开公司跳槽的个人的文件保留策略。你可能需要在从系统中删除文件之前备份文件，和/或执行其他类型的文档记录。如果你的雇主没有此类策略，建议制定一个策略是个好主意。

## 管理组

组是 Linux 自主访问控制 (DAC) 的一部分，是一种组织结构。DAC 是传统的 Linux 安全控制机制，其中对文件或任何对象的访问基于用户的身份和当前的组成员身份。当创建用户账户时，会将其分配到一个特定的组，称为该账户的默认组。虽然用户账户可以拥有许多组成员身份，但其进程一次只能有一个指定的当前组。默认组是用户首次登录系统时账户的当前组。

组由其名称及其组标识号 (GID) 识别。这类似于用户通过 UUID 识别的方式，即 Linux 使用 GID 来识别特定的组，而人类使用组名称。

如果在创建用户账户时未指定默认组，则会创建一个新组。这个新组与用户账户名称相同，并被分配一个新的 GID。要查看账户的默认组，可以使用 getent 命令进行查看

