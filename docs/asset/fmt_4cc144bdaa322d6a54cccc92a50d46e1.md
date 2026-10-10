
# 第 10 章 管理用户和组

```
$ sudo ls -a /home/JKirk/
.. .bash_logout .bashrc .desktop .profile
$

$ sudo ls -a /etc/skel
.. .bash_logout .bashrc .desktop .profile
```

在列表 10.10 中，注意`useradd`命令使用了三个选项。因为该系统没有设置`CREATE_HOME`指令，所以需要`-m`选项强制`useradd`为账户创建主目录。`-d`指定目录名为`/home/JKirk`。该系统的`SHELL`指令设置为`/bin/sh`，因此需要`-s`选项将账户的默认 shell 设置为`/bin/bash`。注意`/etc/passwd`和`/etc/shadow`文件中存在新用户账户的记录。此外，还创建了目录`/home/JKirk`，其中包含了来自`/etc/skel/`目录的文件。记住，`JKirk`账户尚未添加密码，它在`/etc/shadow`文件中的记录密码字段显示为`!`。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_342_0.png)

Ubuntu 和 Debian 发行版推荐使用`adduser`程序而非`useradd`工具。它们的主页将`useradd`命令称为“低级工具”。其他一些名为`adduser`的符号链接，这可能有帮助。`adduser`的配置信息通常存储在`/etc/adduser.conf`中。

另一种查看`/etc/passwd`和`/etc/shadow`文件中记录的方法是使用`getent`工具。对于此程序，只需传递文件名，加上想要查看的账户名。列表 10.11 使用该命令查看列表 10.10 中创建的账户。

## 列表 10.11：在 Ubuntu Desktop 上使用 getent 查看用户账户

```
$ getent passwd JKirk
JKirk:x:1002:1002::/home/JKirk:/bin/bash
$

$ getent shadow JKirk
JKirk::17806:0:99999:7::
```

在列表 10.11 中注意，当对 shadow 文件使用`getent`时没有使用超级权限，没有任何返回。这是因为`getent`尊重`/etc/shadow`上的安全设置。

> 如果你需要修改`/etc/default/useradd`的指令设置，而不是使用文本编辑器，可以使用`useradd -D`命令。只需加上所需的参数。例如，要将`SHELL`指令指向 Bash，请使用超级权限并执行`useradd -D -s /bin/bash`命令。

在创建账户时，可以使用`crypt`工具创建密码，然后在通过`useradd`工具的`-p`选项创建账户时添加它。然而，这不仅麻烦而且被认为是一个坏做法。在下一节中，我们将正确地创建和管理账户密码。

## 维护密码

当你创建一个交互式账户时，应该立即使用`passwd`工具为该账户创建密码。在列表 10.12 中，为 Fedora Workstation 系统上的新`DAdams`账户创建了密码。

### 列表 10.12：在 Fedora Workstation 上为新账户使用 passwd

```
$ sudo passwd DAdams
Changing password for user DAdams.
New password:
Retype password:
passwd: all authentication tokens updated successfully.
$
```

你可以使用`passwd`工具为特定用户更新密码，并将用户的账户名作为参数，类似于列表 10.12 所示。如果你需要更新你的账户密码，只需输入`passwd`而无需额外命令。

> `passwd`工具与可插认证模块（PAMs）协同工作。例如，当你通过`passwd`工具设置或更改密码时，`pam-cracklib` PAM 会检查密码以标记易猜密码或使用字典中单词的密码。PAM 在第 16 章中有更详细的介绍。

使用`passwd`工具不仅仅是设置和修改密码。你还可以锁定或解锁账户、设置账户密码过期、删除账户。

密码，等等。表 10.6 显示了更常用的`passwd`选项；所有这些选项都需要超级用户权限。

### 表 10.6 passwd 命令常用的选项

| 简写 | 完整选项 | 描述 |
| :--- | :--- | :--- |
| `-d` | `--delete` | 删除账户密码并设置为已过期。 |
| `-e` | `--expire` | 设置账户密码为已过期。用户在下次登录时需要更改账户密码。 |
| `-i` | `--inactive` | 设置密码过期后未更改的天数，直到账户被停用。 |
| `-l` | `--lock` | 在`/etc/shadow`文件中的账户密码前放置一个感叹号 (`!`)，从而有效地防止用户通过账户密码登录系统。 |
| `-n` | `--minimum` | 设置从密码密码到可以再次更改密码之前所需的天数。 |
| `-S` | `--status` | 显示账户的密码状态。 |
| `-u` | `--unlock` | 移除`/etc/shadow`文件中账户密码前放置的感叹号 (`!`)。 |
| `-w` | `--warning` 或 `--maxwarndays` | 设置密码过期前向用户发出警告的天数。 |
| `-x` | `--maximum` 或 `--maxdays` | 设置需要更改密码的天数。这是密码的过期日期。 |

表 10.6 中的一个选项需要更详细的解释，那就是`-S`选项。列表 10.13 显示了一个示例。

#### 列表 10.13：使用 passwd -S 查看账户的密码状态

```
$ sudo passwd -S DAdams
DAdams PS 2018-10-01 0 99999 -1 (Password set, SHA512 crypt.)
$
```

在列表 10.13 中，显示了`DAdams`账户的密码状态。该状态包含账户密码的状态，状态可以是可用的密码 (`P`)、无密码 (`NP`) 或锁定的密码 (`L`)。在密码状态之后，显示了最后更改密码的日期，随后是密码的最小、最大、警告和非活动设置。

括号内还显示了额外的状态，包括密码是否过期以及用于保护密码的哈希算法。

你也可以使用`chage`实用工具显示类似的密码信息，但格式更符合人类阅读习惯，如列表 10.14 所示。

#### 列表 10.14：使用 chage -l 查看账户的密码状态

```
$ sudo chage -l DAdams
Last password change               : Oct 02, 2018
Password expires                   : never
Password inactive                  : never
Account expires                    : never
Minimum number of days between password change : 0
Maximum number of days between password change : 99999
Number of days of warning before password expires : 7
```

`chage`程序也可以修改密码设置。你可以使用各种命令选项（详情请参阅其 man 页），或者像列表 10.15 所示交互式地使用`chage`实用工具。

#### 列表 10.15：使用 chage 更改账户密码设置

```
$ sudo chage DAdams
Changing the aging information for DAdams
Enter the new value, or press ENTER for the default

Minimum Password Age [0]: 5
Maximum Password Age [99999]: 30
Last Password Change (YYYY-MM-DD) [2018-10-02]:
Password Expiration Warning [7]: 15
Password Inactive [-1]: 3
Account Expiration Date (YYYY-MM-DD) [-1]:
$
```

注意列表 10.15 中的密码过期警告被设置为 15 天。如果你的公司允许两周的休假，这是一个很好的设置。

## 修改账户

用于修改账户的实用工具是`usermod`程序。与`passwd`命令类似，你可以锁定和解锁账户，如列表 10.16 所示。

### 列表 10.16：使用 usermod 锁定账户

```
$ sudo usermod -L DAdams
$
$ sudo passwd -S DAdams
DAdams LK 2018-10-01 5 30 15 3 (Password locked)
$
$ sudo getent shadow DAdams
DAdams:$6$B/zCaNx[=:]:17806:5:30:15:3::
$
$ sudo usermod -U DAdams
$
$ sudo passwd -S DAdams
DAdams PS 2018-10-01 5 30 15 3 (Password set, SHA512 crypt.)
```

注意列表 10.16，使用`usermod -L`命令来锁定`DAdams`账户。`passwd -S`命令显示密码状态为`LK`，表示它已锁定。在列表 10.16 中，`getent`实用工具的输出片段显示`DAdams`账户密码前放置了一个感叹号 (`!`)，这就是导致账户被锁定的原因。然后通过`usermod -U`命令移除锁定，并重新检查状态。

你可以通过`usermod`实用工具对用户账户进行许多修改。常用的选项如表 10.7 所示。

### 表 10.7 usermod 命令常用的选项

| 简写 | 完整选项 | 描述 |
| :--- | :--- | :--- |
| `-c` | `--comment` | 修改注释。 |
| `-d` | `--home` | 修改主目录。 |
| `-e` | `--expire` | 设置账户过期日期。 |
| `-f` | `--inactive` | 设置密码过期后未更改的天数。 |
| `-g` | `--gid` | 修改默认组。 |
| `-G` | `--groups` | 修改附加组。 |
| `-l` | `--login` | 禁用登录能力。 |
| `-L` | `--lock` | 在`/etc/shadow`文件中的账户密码前放置一个感叹号 (`!`)。 |
| `-m` | `--move` | 主目录。 |
| `-n` | `--name` | 修改用户名。 |
| `-U` | `--unlock` | 移除`/etc/shadow`文件中账户密码前放置的感叹号 (`!`)。 |
| `-u` | `--uid` | 修改 UID。 |
| `-x` | `--maximum` | 设置需要更改密码的天数。 |

`usermod`命令还有许多其他选项。更多信息请参阅其 man 页。

在许多情况下，你需要在创建账户后对其进行修改。列表 10.17 显示了此类示例。

### 列表 10.17：使用 usermod 修改账户

```
$ sudo useradd -md /home/DAdams DAdams
$ sudo getent passwd DAdams
DAdams:x:1003::1:/home/DAdams:/bin/sh
$ sudo usermod -s /bin/bash DAdams
$ sudo getent passwd DAdams
DAdams:x:1003::1:/home/DAdams:/bin/bash
```

在列表 10.17 中，创建了用户`DAdams`，但使用`getent`检查账户时，显示使用的是`/bin/sh` shell。为了解决这个问题，使用了`usermod`命令的`-s`选项将其修改为 bash。

## 删除账户

在 Linux 上删除账户非常简单。`userdel`实用工具是执行此任务的关键。最常用的选项是`-r`。该选项将删除主目录及其内部文件。列表 10.18 显示了一个示例。

### 列表 10.18：使用 userdel 删除账户

```
$ sudo ls -a /home/DAdams
.. .bash_logout .profile
$ sudo getent passwd DAdams
DAdams:x:1003::1:/home/DAdams:/bin/bash
$
$ sudo userdel -r DAdams
userdel: DAdams mail spool (/var/mail/DAdams) not found
$
$ sudo ls -a /home/DAdams
ls: cannot access '/home/DAdams': No such file or directory
$
```

列表 10.18 中的前两个命令显示`/home/DAdams`目录存在且包含文件，并且该账户在`/etc/passwd`文件中有记录。第三条命令包含了`userdel -r`命令来删除账户以及主目录。注意生成了一条错误信息，说明未找到`/var/mail/DAdams`文件。这不是问题，这只是意味着在创建账户时没有创建该文件。

## 管理组

组是 Linux 任意访问控制 (DAC) 的组成部分组织结构。DAC 是传统的 Linux 安全控制机制，其中对文件或任何对象的访问是基于用户身份和当前组成员身份的。当创建用户账户时，它会被分配到一个特定的组，称为该账户的默认组。虽然一个用户账户可以拥有许多组成员身份，但其进程在同一时间只能有一个指定的当前组。当用户首次登录系统时，默认组就是该账户的当前组。

组通过名称及其组标识符 (GID) 来识别。这与通过 UID 识别用户的方式相似。Linux 使用 GID 来识别特定组，而人类则使用组名。

如果在创建用户账户时没有指定默认组，则会创建一个组。该新组的名称与用户名称相同，并被分配一个新的 GID。要查看账户的默认组，可以使用`getent`命令查看该账户的`/etc/passwd`记录。请记住，记录中的第四字段是账户的 GID，即默认组。如果你需要复习各种`/etc/passwd`记录字段的含义，请复阅表 10.3。列表 10.19 显示了查看在 Fedora Workstation 发行版上创建的`DAdams`默认组信息的示例。

### 列表 10.19：查看账户的组成员身份

```
$ getent passwd DAdams
DAdams:x:1002::/home/DAdams:/bin/bash
```

```
$ sudo groups DAdams
DAdams : DAdams
```

```
$ getent group DAdams
DAdams:x:1002::
```

```
$ grep 1002 /etc/group
DAdams:x:1002::
```

列表 10.19 中的第一个命令显示`DAdams`默认组的 GID 为 1002，但它没有提供组名。`groups`命令显示了组名，该组名与用户账户名`DAdams`相同。这在创建账户时没有指定默认组的情况下是典型的。第三个命令显示组`DAdams`确实映射到 GID 1002。第四个命令确认了这一信息。

## 管理组

要将用户添加到新组中或更改账户的默认组，该组必须预先存在。此任务通过`groupadd`工具完成。该组的 GID 将由系统自动分配，但你可以使用`-g`选项覆盖此默认行为。创建新组的示例在列表 10.20 中。

### 列表 10.20：使用 groupadd 工具创建新组

```
$ sudo groupadd -g 1042 Project42
$
```

```
$ getent group Project42
Project42:x:1042:
$
```

```
$ grep Project42 /etc/group
Project42:x:1042:
$
```

注意列表 10.20，创建新组需要超级用户权限。`groupadd`工具以及`grep`命令被用于显示`/etc/group`文件中的新组记录。`/etc/group`文件中的字段由冒号 (`:`) 分隔，如下所示：

- 组名
- 组密码：`x`表示如果存在组密码，它存储在`/etc/gshadow`文件中。
- GID
- 组员：属于该组的用户账户，用逗号分隔。

![](img/0c1e7d2699b9d354c8d2f84669d18d73_350_0.png)

> Ubuntu 和 Debian 发行版推荐使用`addgroup`程序代替`groupadd`程序。他们认为`groupadd`是一个低级工具。

新创建的组没有为其创建组密码。然而，`/etc/group`文件中`Project42`组记录中的`x`并不能证明这一点。列表 10.21 检查了存储组密码的地方以确保没有组密码。

### 列表 10.21：检查组密码

```
$ sudo getent gshadow Project42
Project42::::
$
```

列表 10.21 中的命令显示了`/etc/gshadow`文件中的`Project42`组记录。第二个字段包含一个感叹号 (`!`)，表示该组未设置密码。

组密码如果设置了，将允许用户账户访问他们所属的组。如果使用了组密码，该密码通常在需要访问该组的各种用户之间共享。这是一种糟糕的安全实践。密码绝不应该共享。每个账户都需要自己的密码，并且应该通过组成员身份允许访问组，而不是组密码。

一旦创建了新组，你就可以设置组成员身份，这只需将用户账户添加到组。列表 10.22 显示了使用`usermod`命令执行此操作的示例。
