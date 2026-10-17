
`$ ls /bin/su`

`-rwxr-xr-x 2 root root 30092 Jan 30 07:11 su`

4. 将 `sales` 组分配给目录：
   `# chgrp sales /mnt/salestools`
5. 将目录更改为 `2775`。开启了设置组 ID 位 (`2`)、用户的完全 `rwx` (`7`)、组的 `rwx` (`7`) 以及其他的 `r-x` (`5`)：
   `# chmod 2775 /mnt/salestools`
6. 通过 `su - mary` 变成 `mary`。作为 `mary`，在共享目录中创建一个文件并查看权限。当你列出权限时，你可以看到目录是一个 set GID 目录，在组执行权限应该的地方有一个小写的 `s` (`drwxrws-x`)：

```bash
$ su - mary

[mary]$ touch /mnt/salestools/test.txt

[mary]$ ls -d /mnt/salestools /mnt/salestools/test.txt

drwxrws-x 2 mary sales 4096 Jan 24 14:32 /mnt/salestools/test.txt

-rw-r-- 1 mary 0 Jan 22 14:32 /mnt/salestools/test.txt
```

通常，由 `mary` 创建的文件将分配给组 `mary`。因为 `test.txt` 是在 set GID 组目录中创建的，该文件被分配给 `sales` 组。现在，任何属于 `sales` 组的人都可以根据组权限读取或写入文件。

## 创建限制删除目录（粘滞位）

通过开启目录的粘滞位来创建一个限制删除目录。限制删除目录与其他目录的区别在于？如果一个用户对文件或目录有写权限，该用户就能删除该文件或目录。但在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。

通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。

### 集中用户账户

虽然我将只讨论集中认证的概念，但我想介绍如何删除用户文件。通常，限制删除目录被用作用户创建文件的地方。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

在限制删除目录中，除非你是 `root` 用户或目录的所有者，否则你永远无法删除其他用户的文件。例如，`/tmp` 目录：

```bash
ls -ld /tmp

drwxrwxrwt 12 root root 4096 Oct 12 10 /0
```

## 使用配置窗口

在 Fedora 和 Red Hat Enterprise Linux 中，有一个用于配置集中认证的图形窗口，称为身份验证窗口。通过该窗口，你可以配置系统从哪里获取账户信息以及使用何种类型的认证来验证用户。支持的集中式数据库类型包括：

- `LDAP`—轻级目录协议 (`LDAP`) 是一种提供目录服务（如电话簿、地址和用户账户）的热门协议。它是一个在许多计算环境中配置的开放标准。
- `NIS`—网络信息服务 `NIS` 起初由 Sun Microsystems 创建，用于将用户账户、主机配置和其他类型的系统信息传播到许多 UNIX 系统中。由于 `NIS` 以明文形式传递信息，大多数企业现在都使用更安全的 `LDAP` 或 `Winbind` 协议进行集中式认证。
- `Winbind`—从身份验证窗口进行绑定可以允许你针对 Microsoft Active Directory (`AD`) 服务器验证你的用户。许多大公司将其桌面设置扩展到包含服务器配置以及使用 `AD` 服务器。

对于该配置集中式服务器的介绍，你将使用身份验证窗口配置 Linux 系统向 `LDAP` 服务器进行认证。

开始之前，你需要收集你所在地 `LDAP` 服务器的信息。这包括关于账户数据库和认证方法的信息：

- `LDAP` 服务器—`LDAP` 服务器的主机。例如，`ldap://ldap.example.com`。
- 搜索基 (`Search Base`)—这是用于识别用户账户记录位置的 `LDAP` 数据库的区分名称。通常该名称由公司的 DNS 域名构建。
选择此项后，你还必须选择标识证书机构 (`CA`) 证书的位置，该证书将被下载到本地系统，以验证并加密与 `LDAP` 服务器的通信。传输层安全 (`TLS`) 组织证书从证书机构处获得。或者你可以创建自签名证书。
- 认证方法—与其使用普通的 `MD5` 密码，不如选择 `LDAP` 密码或 `Kerberos` 作为 `LDAP` 的认证方法。对于 `Kerberos`，你还必须提供有关 `Kerberos` 服务器的信息，包括 `Kerberos` 领域 (`Realm`)、`KDC` 和管理服务器。所有这些信息应该由管理公司 `Kerberos` 服务器的管理员提供。

# 第三部分：成为 Linux 系统管理员

要在 Red Hat Enterprise Linux 6 桌面启动身份配置窗口，选择 System（系统） ➤ Administration（管理） ➤ Authentication（认证）。对于仅进行本地（`passwd`/`shadow`）认证的默认系统，会出现该窗口。

要添加 `LDAP` 认证，选择 User Account Database（用户帐户数据库）框并选择 `LDAP`。然后填写项目符号中描述的信息。

如果新认证方法配置得当，你应该能够进入 shell 并使用以下 `get` 命令验证从 `LDAP` 服务器获取的用户账户是否可用：

```bash
# passwd jsmith

smith:13599:13600:John Smith:/home/jsmith:/bin/bash
```

如果你看到了该账户，说明你的系统能够从 `LDAP` 服务器检索到它。下一个需要检查的是认证方法是否也正常工作。为此，你可以尝试从控制台或使用 `ssh` 命令以该用户身份登录。

```bash
$ ssh jsmith@localhost
```
