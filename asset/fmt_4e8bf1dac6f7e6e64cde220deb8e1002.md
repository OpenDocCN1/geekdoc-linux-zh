
## 设置默认 Linux 文本编辑器

Ubuntu 的默认文本编辑器是 `nano`。它是一个易于使用的编辑器。在编辑的文件中输入和删除文本不需要特殊命令。`nano` 编辑器提供了一个直观的界面，如图 6-3 所示。

然而，`vi` 编辑器仍然非常流行，而且它是某些救援系统中唯一的编辑器。此外，有些用户更偏于 `emacs` 编辑器。某些 Unix 用户可能更偏于 `ed` 编辑器。

![](img/fadb0f527b947cf4d02cbbbb791a6562_177_0.png)

图 6-3. `nano` 编辑器

以下命令提供了修订 Ubuntu 默认编辑器的选项：

```
$ sudo update-alternatives --config editor
```

有 4 个备选方案提供 `editor`。

| 选择 | 备选项 |
| :--- | :--- |
| 1 | `/usr/bin/vim.tiny` |
| 2 | `/bin/ed` |
| *3 | `/bin/nano` |
| 4 | `/usr/bin/emacs22` |

按回车保留默认值 [*]，或输入选择数字：

结果反映在 `/etc/default/editor` 二进制配置文件。如菜单所示，Ubuntu 系统使用 `vi` 编辑器的简化版本，即 `vim.tiny`。我将我的系统改为使用 `vi`，因为它最了解我。

> 注意 `vi` 命令有几种专门的变体。三种变体是 `vipw`、`vig` 和 `visudo`，它们分别编辑

## 第 6 章：命令行工具与 Shell 管理

注意 `vi` 命令有几种专门的变体。三种变体是 `vipw`、`vig` 和 `visudo`，它们分别编辑 `/etc/passwd`、`/etc/group` 和 `/etc/sudoers`。

## 优化 Shell

对于 Ubuntu 用户来说。在本节中，你可以在 `/etc/cron.daily` 目录中找到一些 Ubuntu shell 程序。如果你对 shell 命令和编程表达式熟悉，你可以在 `/etc/cron.daily` 目录中找到一些。

### /etc/bashrc

`/etc/bashrc` 文件用于系统级。以下是 Ubuntu 的版本。例如，我稍后在本节中解释这些。

### /etc/bashrc

`/etc/bashrc` 文件用于系统级。以下是 Ubuntu 的版本。首先，它查找 `/etc/profile.d` 中的其他配置文件。它设置了

### /etc/profile

```
# /etc/profile: system-wide .profile file for the Bourne (sh1) and Bourne compatible shells (bash(1), ksh(1), ash(1), ...)
if [ -d /etc/profile.d ]; then
  for i in /etc/profile.d/*.sh; do
    if [ -r $i ]; then
      $i
    fi
  done
unset i
fi
if [ "$PS1" ]; then
  if [ "$BASH" ]; then
    PS1='\u@\h:\w\'
    if [ -f /etc/bash.bashrc ]; then
      /etc/bash.bashrc
    fi
  else
    if [ "`id -u`" -eq 0 ]; then
      PS1='#'
    else
      PS1='$'
    fi
  fi
fi
```

## 脚本入门

“真正的”Linux 管理员会编写自己的脚本。他们创建脚本是因为他们不想一直坐在电脑前。脚本允许 Linux 在办公室没人时自动备份目录。脚本帮助 Linux 在人们使用较少时处理数据库。

如果你不是程序员，不要担心，这听起来没有那么复杂。例如，与 `crontab` 命令相关的工具可以创建许多不同的脚本。`cron` 系统将在第 7 章进行详细讨论。

## 变量及更多

变量是可以更改的。`bash` shell 包含许多标准环境变量。它们的默认值显示在 `env` 命令的输出中。一个关键的变量是 `PATH` 的值，你可以通过命令行使用 `echo $PATH` 命令来检查它。当你尝试运行一个命令时，系统会自动搜索 `PATH` 中的目录。例如，如果你想运行 `/sbin` 目录下的 `fdisk` 命令，可以使用以下命令：

```
$ /sbin/fdisk
```

然而，由于 `/sbin` 目录在第一个用户的默认 `PATH` 中，你不需要前面的 `/sbin` 即可调用该命令；如下所示：

```
$ fdisk
```

但对于普通用户，`PATH` 变量并不包含 `/sbin`。如果你想将 `/sbin` 添加到 `PATH` 中，只需运行：

```
export PATH=$PATH:/sbin
```

如果你想将用户的 `PATH` 设置为包含 `/sbin` 目录，适当的位置位于 `.profile` 配置文件。你只需要在该文件的末尾添加以下行即可：

```
PATH=$PATH:/sbin
```

当该用户下次打开控制台时，`/sbin` 目录将作为该用户 `PATH` 的一部分被激活。

## 管理权限

Linux 的基础安全性与读、写、执行权限相关。默认权限通过 `umask` 变量设置。所有权基于创建文件的用户 ID 和组 ID。管理权限和所有权的命令（如 `chmod`、`chown` 和 `chgrp`）允许用户访问特殊文件。

### 基本文件权限

Linux 文件权限非常直观。考虑来自 `ls -l /sbin/fdisk` 的输出：

```
-rw-r-x-- 1 root root 856 2008-03-06 20:24 /sbin/fdisk
```

权限显示在列表的左侧。第一个字符决定了这是一个普通文件还是特殊文件。其余字符每三个一组，分别适用于文件所有者（用户）、组所有者以及系统上的所有用户。在这种情况下，用户所有者和组所有者都是 `root`，如第三和第四列所示。这些字符非常直观：`r` = 读，`w` = 写，`x` = 执行。字符位置在表 6-2 中描述。

### 修改权限和所有权的命令

默认权限取决于 `umask` 的值。此时，`umask` 只能更改标准的读、写、执行权限。帮助你管理文件权限和所有权的键是 `chmod`、`chown` 和 `chgrp`。`chmod` 命令特别强大，它可以自定义文件的权限。`chattr` 命令在管理文件属性方面提供了不同的方式。

### 使用 chmod 修改权限

`chmod` 命令使用与所有者和其他人相关的权限数值。在 Linux 中，权限被赋予以下数值：`r` = 4，`w` = 2，且 `x` = 1。例如，如果你疯狂到给所有用户 `fdisk` 赋予读、写、执行权限，你将运行 `sudo chmod 777 /sbin/fdisk`。如果你想给管理员用户 Samba 配置文件提供读写权限，并给所有其他人只读权限，你将运行 `sudo chmod 644 /etc/samba/smb.conf`。请注意，这些数字与表 6-2 中描述的位置不同。

| 字符位置 |  |
| --- | --- |
| 1 | 类型：- = 普通文件，b = 块设备，c = 硬件设备，d = 目录，l = 链接文件 |
| 234 | 授予文件所有者的权限 |
| 567 | 授予文件组所有者的权限 |
| 890 | 授予 Linux 系统上所有其他用户的权限 |

**表 6-2. 文件权限说明**

## Ubuntu 服务器管理

另一种，可以使用 `chmod` 命令进行细微的更改。首先，查看以下命令的输出：

```
$ ls -l /usr/games/newgame
15972 2007-12-12 05:59 /usr/games/newgame
-rw-r--r 1 dickens
```

输出揭示了 `/usr/games` 目录下脚本 `newgame` 的权限和所有权。它的用户所有者是 `dickens`，组所有者是 `coolcats`。换句话说，`dickens` 拥有读写权限，`coolcats` 组的成员拥有读权限而所有其他用户对该脚本没有权限。

接下来，使用以下命令为用户所有者 `dickens` 启用脚本的执行权限：

```
$ chmod u+x /usr/games/newgame
```

分析此命令中的开关。`u` 代表用户所有者，`+` 添加所请求的权限——在这里是 `x`，即执行权限。其他示例包括以下，它为 `coolcats` 组的成员激活新脚本的写权限：

```
$ chmod g+w /usr/games/newgame
```

当然，这可以反过来。以下命令移除 `coolcats` 组成员的权限：

```
$ chmod g-w /usr/games/newgame
```

然后你可以通过以下命令允许 `coolcats` 成员执行脚本：

```
$ chmod g+x /usr/games/newgame
```
