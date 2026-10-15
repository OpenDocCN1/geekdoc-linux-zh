
如你所见，文件左侧消失了 `x`，这意味着 `script` 不再由文件所有者 `mj` 或 `project` 组的任何成员执行。

### Linux 所有权

权限定义了用户、组和网络上的每个其他用户对文件可以做什么。你可以更改拥有该文件的用户和组。`chown` 命令将文件的所有权从一个用户转移到另一个用户。考虑共享目录上的 `script` 情况。用户 `mj` 和 `nc` 都在处理它。如果你运行以下命令，用户 `nc` 将获得 `script` 的所有权：

```
chown nc /home/script
```

如下输出显示了这一点：

```
-rw-r--r-- 1 nc project 46528 May 14 19:24
```

假设有人决定将 `script` 的所有权从 `project` 重新分配给 `mfg` 组。你可以通过以下命令进行设置：

```
chgrp mfg /home/script
ls -l /home/script
```

输出结果：

```
-rw-r--r-- 1 nc mfg 46528 May 14
```

## 访问控制列表的有限支持

访问控制列表 (ACL) 是指定用户、组对文件可以做什么的权限的细节。在 `Samba 2.7` 中，它对 `ACL` 的支持是改进的。

在 `Linux 9` 版本中，`Samba` 对 `ACL` 的支持是改进的。

> `Samba` 不支持使用仅位于 `Windows` 或 `Linux PDC` 上的账户登录 `Linux`。

随后，我将向你展示如何设置 `Samba` 密码，这些用户在登录到 `Domain` 上的工作站时会输入这些密码。在未来的发行版中，这种情况将会改变。

### Linux 组

`Windows` 默认包含了一系列组，如备份操作员、高级用户等。

### Linux 的私有组

在某些情况下，每个 `Linux` 用户都属于自己的私有组。通过查看 `/etc/passwd` 和 `/etc/group` 文件可以发现这一点。其他 `Linux` 发行版通常对所有用户具有某些访问权限。

### 创建特殊组

经常，网络会将需要对单个目录中的文件具有访问权限的用户聚集在一起。在 `Linux` 中进行这种设置并不困难。

假设你想为飞机座椅工程师 `Gabe`、`Wayman`、`Padma` 和 `Diane` 设置一个私有目录。首席工程师是 `Gabe`。为了使之工作，请按照以下步骤操作：

1. 登录 `PDC`。在 `Red Hat` 用户 `Manager` 中点击主菜单 | 系统设置 | 用户和组。点击添加用户打开图 2 所示的新用户窗口。为工程师创建一个账户。或者，你可以使用以下命令为座椅工程师创建用户账户：

```
/usr/sbin/useradd gabe
/usr/sbin/useradd wayman
/usr/sbin/useradd padma
/usr/sbin/useradd diane
```

2. 如果你的座椅工程师想直接登录 `Linux` 工作站，请使用 `passwd username` 命令为该工作站上的每个用户创建一个密码。如果他们只是使用 `Windows` 工作站，你不需要为每个用户创建 `Linux` 密码。稍后，我将向你展示如何设置 `Samba` 密码。

3. 为座椅工程师设置组。在 `Red Hat` 用户 `Manager` 中，点击添加组。在图 5 所示的创建新组窗口中，设置一个适当的组名称。最好也手动设置组 ID，使其位于普通用户 ID 范围之外，正如之前解释的那样。

![](img/6ee4859e736a0839007ea9afb576c195_144_0.png)

## 第 4 章：设置文件服务器用户 125

![](img/6ee4859e736a0839007ea9afb576c195_145_0.png)

**图 5。** 创建一个特殊组。

4. 为座椅工程师创建一个特殊目录。将用户所有权分配给首席工程师 (`Gabe`)，将组所有权分配给座椅工程师组。允许用户和组在该目录中拥有完全权限。

5. 配置该目录，使其文件属于该特殊组。防止其他用户读取此目录（`Linux` 管理员用户 `root` 仍然具有访问权限）。在命令行界面执行此操作最为简单：

```bash
mkdir /home/seatengr
chown gabe /home/seatengr
chgrp seatengr /home/seatengr
chmod 770 /home/seatengr
chmod g+s /home/seatengr
```

> `chmod g+s /home/seatengr` 命令会在 `/home/seatengr` 目录中复制或创建的任何文件上设置组 ID 位，使其继承该目录的组所有。换句话说，`seatengr` 组成员对 `/home/seatengr` 目录下的所有文件具有完全的默认权限。

6. 在 `Red Hat` 用户管理器中，点击“组”选项卡。选中你的 `seatengr` 组并点击“属性”。在属性窗口中，点击图 6 所示的“组”选项卡。从列表中选择你的座椅工程师，然后点击“确定”。如果你有一个特殊目录 `/home/seatengr`，访问将仅限于你的座椅工程师。

7. 为每个用户设置 `Windows` 登录。你可以通过两种方式实现。如果你想使用 `Red Hat Samba` 配置器，点击“主菜单 | 系统设置 | 服务器设置 | Samba 服务器”。在 `Samba` 服务器工具中，点击“首选项 | Samba 用户”。在 `Samba` 窗口中，为每个座椅工程师点击“将用户添加到 Samba 数据库条目”。图 7 展示了 `Waymon` 的 `Windows` 用户名为 `waymonww`。

## 126 面向 Windows 网络管理员的 Linux 传输

![](img/6ee4859e736a0839007ea9afb576c195_146_0.png)

**图 6。** 为组选择用户。

![](img/6ee4859e736a0839007ea9afb576c195_146_1.png)

**图 7。** 为 `Windows` 域登录创建 `Samba` 用户。

8. 此外，你可以在命令行中使用 `smbadduser` 命令执行此操作。对于图 7 所示的情况，运行以下命令：

```bash
smbadduser waymon:waymonww
```

系统会提示你输入 `Waymon` 从微软工作站登录时将使用的密码。

9. 向 `Samba` 文件中添加共享。将访问权限限制为座椅工程师组的成员。根据第 3 章的讨论，你可以通过在 `Samba` 配置文件的末尾添加以下命令来实现这一点：

```ini
[seatengr]
comment = 座椅工程师目录
path = /home/seatengr
valid users = @seatengr
public = no
writable = yes
printable = no
create mask = 0770
```

10. 使用 `testparam` 命令检查更改的语法。解决 `testparam` 指出的任何问题。使用以下命令重启 `Samba` 守护进程：

```
/etc/rc.d/init.d/smb restart
```
