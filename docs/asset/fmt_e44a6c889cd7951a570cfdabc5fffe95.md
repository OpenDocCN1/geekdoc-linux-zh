
# 6. Debian 系统管理

## 6.2 用户与身份验证

```
Adding user 'martin'...

Adding new group 'martin' (1003)

Adding new user 'martin' (1003) with group 'martin'.

Creating home directory '/home/martin'.

Copying files from '/etc/skel'

Enter new Unix password:

  # GECOS 是“通用电气综合操作系统”的遗留，并保留于当的 Unix 系统中，作为与登录账户相关的联系数据的格式规范。/etc/passwd 文件的第五个冒号分隔字段以逗号分隔字段持有 GECOS 数据：姓名、房间号、工作电话和家庭电话。最后一个字段可用于其他自由格式的数据。

重新输入新 Unix 密码：
密码更新成功
更改 martin 的用户信息
输入新值，或按回车使用默认值
全名 [] : Martin F. Krafft
...
信息是否正确？[y/N] y
正在从'template' 设置配额。
I: /usr/local/sbin/adduser.local called with arguments:
I: martin 1003 1003 /home/martin
```

### 删除用户

用户的删除受`/etc/deluser.conf`中设置的控制。该过程包含以下步骤：

-   `deluser` 移除 Unix 账户，而不触碰用户的任何数据（如主目录或邮件池）。
-   如果设置了 `$REMOVE_HOME` 或提供了命令行选项 `--remove-home`，则会清除用户的主目录（及其中的数据）。系统账户亦如此。
-   如果启用了 `$REMOVE_ALL_FILES` 或使用了选项 `--remove-all-files`，将扫描整个系统以属于该用户的文件并进行清除。此选项优于（并包含）`--remove-home` 选项。同样，系统用户账户以相同的方式处理。
-   启用 `$BACKUP` 或在调用 `deluser` 时传递 `--backup` 选项会导致工具将将在用户删除过程中删除的文件归档到 tar 包中。目标位置可以通过 `$BACKUP_TO` 或 `--backup` 命令行开关设置，默认是当前目录。
-   最后，`deluser` 执行 `/usr/local/sbin/deluser.local`（如果存在），并将账户名、用户 ID、主组 ID 和主目录路径作为参数传递。一个执行失败的退出码将返回给用户，否则将被忽略。

序列如下，并添加了文件删除和备份功能以供演示。此外，之前 `adduser` 示例中使用的相同钩子在这里也显示了作用：

```
# deluser --remove-all-files --backup martin

正在寻找需要备份/删除的文件...

正在将要删除的文件备份到 . .

/bin/tar: Removing leading './' from member names

正在删除文件...

Removing user 'martin'...

I: /usr/local/sbin/deluser.local called with arguments

I: martin 1003 1003 /home/martin

done.

# ls -F

martin.tar.bz2
```

### 组内存管理

本质上，Unix 系统上的组内存管理可以通过两种方式进行：作为 root，或者作为具有特定组权限的普通用户。Debian 对后者没有特殊规定，因此以下是你将看到的所有关于用户进行成员管理的内容。例如，假设有一个由 Alice 领导的编码组。系统管理员创建了该组并让 Alice 管理员：

```
# gpasswd -A alice coders
```

当 Bob 加入该组时，Alice 不需要咨询系统管理员，而是可以添加 Bob：

```
# gpasswd -A alice coders  # (注：此处原文示例代码似乎有重复，已按样翻译)
```

(注：此处原文中两次都是 `gpasswd -A alice coders`，翻译时保持一致)

缺失的环节现在是 `umask`，它决定了新文件的权限。为了让项目的其他成员可以使用新文件，组权限应为可读写。这可以通过将所有用户的 `umask` 设置为 007 来实现（例如在 `/etc/profile` 或用户特定的初始化脚本中）。如下例所示，coders 组的成员可以自由操作 `/coders/` 下的文件：

```
# install --directory --mode=2770 --group=coders coders

# cd coders

/coders# umask 007

/coders# touch hello.c

# ls -la

drwxrwxrwx 2 alice 4096 Dec 21 20:40 ./

drwxr-xr-x 3 alice 4096 Dec 21 20:39 ..

-rw-r--r-- 1 alice 0 Dec 21 20:40 hello.c
```

当经典的 Unix 情况下所有用户默认属于 `users` 组时，会出现问题。由于 `umask` 是针对整个会话的（如果在初始化脚本中设置，则对每个会话生效），当随后撰写一封私信时，`users` 组的所有其他成员都可以读取并编辑该信，该信创建时将具有组读写权限。为了防止这种情况，每个用户默认都会获得一个显式的组。

同样，`deluser` 可用于从组中删除用户（“从组中删除用户 bob”）：

```
# deluser bob coders

Removing user 'bob' from group 'coders'...

Done.
```

### LDAP 用户管理

遗憾的是，`adduser` 目前不支持 `/etc/passwd` 以外的其他用户数据库。如果你的用户存储并针对 LDAP 访问的目录服务中，你将需要采用其他方法。`cpu` 包提供了一个前景良好的框架，可以通过 LDAP 执行大多数用户管理操作。此外，`ldap` 包提供了 `ldapvi`，适用于通过 LDAP 批量编辑用户数据。

### 6.2.3 PAM — 大多数软件包安装软件组件的可扩展功能

Debian 并不一定将身份验证、账户和会话初始化以及密码更改功能放在 PAM 库中安装软件组件。PAM 是一种插件架构，允许对单个程序或一组程序使用自由形式的身份验证方法组合。它可能是过去十年最重要的发明之一。

Debian 的 PAM 与上游库相比没有显著区别。然而，它允许使用 `include` 指令。因此，Debian 为四个 PAM 设施（facilities）中的每一个在 `/etc/pam.d` 下引入了一组通用文件：`common-account` 用于账户管理，`common-auth` 用于身份验证，`common-password` 用于密码管理，以及 `common-session` 用于会话管理。各个服务通常只添加特定于该服务的设施，而所有服务都会共同使用（并强制执行通用文件中定义的设施。

取决于 PAM 配置的性质，修改将位于通用文件中。两个标准的示例是：一致地使用 LDAP 进行身份验证，或者使用如 `libpam-pwquality` 等密码检查器来选择强密码。由于这些模块（应该）适用于机器提供的每个服务，因此最好将它们添加到相应的 `common-*` 文件，而不是单独的服务控制文件中。当安装新服务时，特定配置将自动生成，这在某些情况下很方便，而在另一些情况下则不然。

#### 将设备限制为本地用户

有一个特殊的 PAM 模块值得特别提及，尽管它不是官方 PAM 发行版的一部分：`pam_console`。它的目的是根据本地登录的用户来更改设备权限（类似的操作）。由于这种方法无法适用于多个本地用户，并且已知会暴露安全漏洞和不一致问题，因此它在 Debian 系统上不可用。相反，Debian 使用组来处理特定的设备类。通过 `pam_group`，可以限制例如音频设备仅供本地登录使用。

```bash
# echo auth pam_group.so >> /etc/pam.d/common-auth

# echo *ttytty*:root;A10000-2400:audio' >> /etc/security/group.conf
```

同样的概念也可以用于保护例如 CD-ROM 设备。在 6.2.1 中，Debian 系统上常用的定义的组如下。请注意，该方法不能防止恶意用户。为了规避该规则，用户可以创建一个重复的 shell 并使用 `setgid` 将其设置为音频组，从而导致使用 `pam_group` 选择性添加音频组变得毫无用处。

#### 前置环境变量

在许多情况下，系统管理员倾向于为系统上的所有用户（以及可能的进程）将环境变量设置为某些默认值。实现这一结果的一种方法是修改相应 shell 的全局初始化文件。例如，为了确保你的用户搜索路径中包含 `/bin`，你可以更改 `/etc/bash.bashrc`：

```bash

```
