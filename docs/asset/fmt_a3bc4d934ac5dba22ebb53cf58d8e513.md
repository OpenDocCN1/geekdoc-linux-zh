
可以使用相同的 `exit`、`logout` 和 `ctrl-d` 命令退出用户 `donna` 账户。当然，用户也可以在 GUI 中登录和注销。步骤根据桌面环境略有不同，但与任何其他操作系统的登录和注销步骤一样简单。

# 第 6 章 用户管理

## 认证目标 6.04

### 特殊组

过去，许多 Linux 发行版通常会将所有用户分配到同一个主组，以便他们更容易共享文件。然而，这种方法存在安全方面的缺陷：如果权限没有配置妥当，该主组的所有成员都可以访问彼此的文件和目录。这通常是不希望的，因为用户可能不想与组内的所有人共享他们的数据。红帽通过为每个用户分配唯一的组 ID `GID` 编号解决了这个问题，增强了安全性和用户隐私。
如之前提到的，这被称为私有组方案。用户对自己的主组拥有独占访问权限，而不必担心其他用户读取其目录中的文件。

### 标准组和红帽组

在 RHEL 中，每个用户默认都拥有一个自己的私有组。如前所述，`UID` 和 `GID` 通常从 `1000` 开始，分配匹配的数字并按升序排列。此外，你还可以为专用用户设置特殊组，理想情况下具有较高的 GID。例如，管理员可能会为财务部门配置一个组， GID 可能为 `7000`。

### 共享目录

大多数人以小组形式工作，他们可能想要共享文件。然而，这些组中的人员可能有充分理由防止他人获取他们的信息。为了支持小组，你可以设置一个共享目录，并将访问权限限制为组内成员。

假设你想为一组会计师设置共享目录 `/home/accshared`。要完成，你可以按照以下基本步骤设置共享目录：

- 创建共享目录：

```
# chmod /home/accshared
```

- 在 `/etc/logindefs` 文件中，更改 `UMASK` 指令并将其更改为 `077`。此 `umask` 值由登录 shell 评求的。
- 登录一个普通非特权用户。使用 `touch` 命令创建一个新的空文件。使用 `ls -l` 验证该文件的权限。
- 打开一个非登录 shell（即输入 `bash`）。再次使用 `touch` 命令创建一个新的空文件，并使用 `ls -l` 验证该新文件的权限。
- 从步骤 1 创建的备份中恢复 `/etc/bashrc` 和 `/etc/profile` 的原始版本。

### 特殊组 243

- 6. 运行 `/home/testshared` 命令。发生了什么？
- 7. 现在以 root 用户身份，为 `testshared` 目录设置组写权限：

```
# chmod 770 /home/testshared
```

- 8. 以 `user1` 用户身份，返回到 `/home/testshared` 目录，然后尝试在新目录中创建一个文件。到目前为止，一切正常。

```
$ cd /home/testshared
$ date >> test.txt
$ ls -l test.txt
```

- 9. 以 root 用户身份，移除 `/home/testshared` 目录中新文件的其他用户权限：

```
# chmod o-rwx /home/testshared/*
```

- 10. 现在使用以下命令检查新文件的所有者。你认为 `tgl` 组中的其他用户可以访问此文件吗？如果有怀疑，请以 `test2` 用户身份登录并亲自尝试。

```
$ ls -l
```

- 11. 从 root 账户，为目录设置 SGID 位：

```
# chmod g+s /home/testshared
```

（如果你注重效率，你可能知道 `chmod 2770 /home/testshared` 命令结合了此命令和之前的 `chmod` 命令的效果。）
- 12. 回 `test1` 账户，返回 `/home/testshared` 目录并创建另一个文件。移除新创建文件的其他用户权限。检查新创建文件的所有者。你认为现在 `test2` 用户可以访问此文件吗？（如需亲自验证，请从 `test2` 账户尝试。）

```
$ date >> test.txt
$ chmod o-rw /home/testshared/testb.txt
$ ls -l
```

- 13. 以 `test2` 账户登录。创建一个不同的文件，并再次使用 `ls -l` 检查权限和所有者。（为了确认操作生效，请尝试从 `test1` 账户访问此文件。）
- 14. 切换到 `test3` 账户，检查该用户是否可以在此目录中创建文件，以及该用户是否可以查看此目录下的文件。正如预期的，该用户无法访问 `/home/testshared` 目录，因为它不在 `tgl` 组。

https://t.me/CCNA_SECURITY
https://t.me/CCNPSECURITY

## 认证摘要

你可以使用 shadow 密码套件的文件管理用户和组。这些文件可以在 `useradd` 和 `groupadd` 等命令或 Cockpit Web 控制台的帮助下直接修改。用户的配置基于 `/etc/login.defs` 文件。任何变量或系统级设置定义在 `/etc/bashrc`、`/etc/profile` 以及 `/etc/profile.d/` 中的文件里。它们可以通过用户目录下的 `.bashrc` 和 `.bash_profile` 文件进行修改。

有多种方法可以限制管理权限的使用。登录能力可以通过 `/etc/security/access.conf` 文件进行规范。可以借助 PAM 帮助来限制对 `su` 命令的访问。可以在 `/etc/sudoers` 文件中为 `sudo` 命令配置部分和完整的管理权限。

默认情况下，Red Hat Enterprise Linux 为每个新用户分配唯一的用户 ID 和组 ID 编号。这种私有组方案支持为特定用户组配置特殊组。得益于 SGID 位，组内的用户可以更改和修改专用目录中的他人的文件。

## 两分钟训练

这里是第 6 章认证目标中的一些关键点。

### 用户账户管理

- 安装后，系统可能只有一个登录账户：`root`。对于日常操作，最好创建一个或多个普通账户。
- shadow 密码套件的配置在 `/etc/passwd`、`/etc/shadow`、`/etc/group` 和 `/etc/gshadow` 文件中。
- 管理员可以使用 `useradd` 和 `groupadd` 命令或 Cockpit Web 控制台直接添加用户和组。用户的配置方式基于 `/etc/login.defs` 文件。任何变量或系统级设置定义在 `/etc/bashrc`、`/etc/profile` 以及 `/etc/profile.d/` 中的文件中。它们可以通过用户目录下的 `.bashrc` 和 `.bash_profile` 文件进行修改。

有多种方法可以限制管理权限的使用。登录能力可以通过 `/etc/security/access.conf` 文件进行规范。可以借助 PAM 限制对 `su` 命令的访问。可以在 `/etc/sudoers` 文件中为 `sudo` 命令配置部分和完整的管理权限。

默认情况下，Red Hat Enterprise Linux 为每个新用户分配唯一的用户 ID 和组 ID 编号。这种私有组方案支持为特定用户组配置特殊组。得益于 SGID 位，组内的用户可以更改和修改专用目录中的他人的文件。

### 用户账户管理

- 安装后，系统可能只有一个登录账户：`root`。对于日常操作，最好创建一个或多个普通账户。
- shadow 密码套件的配置在 `/etc/passwd`、`/etc/shadow`、`/etc/group` 和 `/etc/gshadow` 文件中。
- 管理员可以使用 `useradd` 和 `groupadd` 命令或 Cockpit Web 控制台直接添加用户和组。用户的配置方式基于 `/etc/login.defs` 文件。

### 访问控制

- 登录能力可以通过 `/etc/security/access.conf` 文件进行规范。
- 可以借助 PAM 限制对 `su` 命令的访问。
- 可以在 `/etc/sudoers` 文件中为 `sudo` 命令配置部分和完整的管理权限。

### Shell 配置

- 用户的环境源自 `/etc/skel` 目录。
- 任何变量或系统级设置定义在 `/etc/bashrc`、`/etc/profile` 以及 `/etc/profile.d/` 中的文件中。
- 它们可以通过用户目录下的 `.bashrc` 和 `.bash_profile` 文件进行修改。

### 特殊组

- 这种私有组方案支持为特定用户组配置特殊组。
- 得益于 SGID 位，组内的用户可以更改和修改专用目录中的他人的文件。

## 248 第6章 用户管理

注意使用 `usermod` 命令时的 `-a` 选项。这是因为 `newguy` 是 `users` 组的成员。如果不传递 `-a`（追加）选项，`newguy` 将从 `users` 组中移除。或者，你可以指定 `newguy` 的所有组：

```bash
```
