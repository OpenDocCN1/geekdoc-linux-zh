
现在让我们使用以下命令在 KDC 上创建主机密钥、主机密钥表文件和一个用户：

```bash
# kinit admin/admin  <------------------ 以 admin 账户进行身份验证
# kadmin              <---- 启动 kadmin 交互 shell
kadmin:  list_principals
kadmin:  add_principal -randkey -clearpolicy host/kdcsrv.osborne.com
kadmin:  ktadd host/kdcsrv.osborne.com
kadmin:  add_principal UserName
kadmin:  exit
```

现在从客户端和 KDC 服务器测试你新的 UserName 主体。

```bash
# kinit UserName  <-------------------- 以新的 UserName 主体进行身份验证
# klist            <------ 列出你的新 Kerberos 票据
```

## 附加信息

前面的章节仅简要介绍了网络认证服务的部署。实现 Kerberos 需要大量的规划和资源，以确保系统的安全性、可靠性和可扩展性。幸运的是，IBM 提供了广泛的文档，格式包括 PDF 和 HTML，位于文件集 krb5.doc.en_US 中，也可以在扩展包 CD-ROM 中找到。另一个出色的信息源是 M.I.T. Kerberos 网站，位于 http://web.mit.edu/kerberos/www/。

## 控制超级用户访问

必须谨慎对待 root 密码、其使用方式以及谁可以访问它。通常，root 不应直接登录到系统；拥有超级用户账户访问权限的用户应先登录自己的账户，然后使用 su 命令变为 root。这样，所有尝试变为 root 的操作，无论成功或失败，都会被记录到 /var/adm/sulog。为了阻止通过直接网络登录 root 账户，请运行以下命令

```bash
# chuser rlogin='false' root
```

AIX 通过定义可以使用 su 命令切换到特定账户的组，以及拒绝允许使用 su 切换到特定账户，从而提供额外的保护。这些控制在 /etc/security/user 文件中按每个用户设置：

```yaml
root:
    sgroups = system,security
```

前面的片段说明，只有通过 **su** 命令切换到 root 的 system 或 security 组成员才允许。

## 保护网络访问

保护网络访问或许是确保安全受保护的计算环境的最重要部分。大量的安全违规事件是由于网络服务配置不当或应用设计不良导致的。因此，务必确保系统的网络“足迹”尽可能狭窄且安全。

与各网络协议、服务和应用相关的安全问题在涉及网络的章节中详细阐述。简而言之，网络安全有三条基本规则：

- 如果运行中的服务不是必需的，请将其禁用。
- 限制对剩余服务的访问，以便只有需要连接的系统和网络能够连接。
- 如果某个应用使用不安全的协议进行通信，应替换为安全的替代方案。

有关详细信息，请参阅本书中关于网络的章节以及本章末尾列出的资源。

## 保护文件访问

AIX 5L，如同所有基于 UNIX 的操作系统一样，使用权限来确定谁可以读取、修改和执行系统中的对象（普通文件、目录和特殊设备文件）。权限可以分别为对象的拥有者、列在 /etc/group 中的组的成员以及所有其他用户（“其他”）单独设置。

### 基本文件权限

传统的或基本的文件访问权限是通过使用 **chmod** 命令分配的权限。用户可以使用 **chmod** 修改其拥有的任何文件的权限。权限可以使用八进制或符号表示法来指定。

```bash
$ chmod 640 a_file
```

```bash
$ ls -l a_file
-rw-r-----  1 jdoe   staff    0 Apr 20 14:54 a_file
```

在上面的例子中，文件的权限设置为例：拥有者 jdoe 可读可写（第一位的 "6"），staff 组成员只读（第二位的 "4"），其他用户无访问权限（第三位的 "0"）。

使用符号模式设置相同的权限：

```bash
$ chmod u+rw,g+r,o-rwx a_file
```

### umask

使用 umask 命令（通常在用户的 shell 配置文件中）、通过 SMIT 快速路径 mkuser（在创建账户时）或通过 SMIT 快速路径 chuser（修改现有账户）可以设置用户账户创建的文件和目录的默认权限。

```bash
# smit chuser
...
文件创建 UMASK                       [22]
```

请注意，umask 值是从默认权限中移除（而不是减去！）的，默认权限对于新创建的目录为 777，对于新创建的文件为 666。因此，umask 值为 022 的结果为

```bash
$ umask 022

$ mkdir a_new_directory ; ls -ld a_new_directory
drwxr-xr-x  2 jdoe staff     512 Apr 20 15:26 a_new_directory

$ touch a_new_file ; ls -l a_new_file
-rw-r--r--  1 jdoe staff     0 Apr 20 15:26 a_new_file
```

### Set-UID 和 Set-GID

root 用户还可以将文件或目录设置为 set-UID 或 set-GID。通常，当执行文件时，它以运行该程序用户的 UID 和 GID 运行。然而，当文件被设置为 set-UID 时，程序将以文件拥有者的有效用户 ID 运行。

在 AIX 中，只有编译过的程序才能被设置为 set-UID 或 set-GID；如果这些权限应用于 shell 脚本，出于安全原因，在执行 shell 脚本时它们会被忽略。

在 /tmp 中创建 /usr/bin/ksh 的副本，并将该副本的拥有者设置为 "root"。

```bash
# cp /usr/bin/ksh /tmp/ksh
# chown root /tmp/ksh
# ls -l /tmp/ksh
-r-xr-xr-x  1 root      system     243374 Apr 20 15:10 /tmp/ksh
```

用户 **jdoe** 通过 `/tmp/ksh` shell 运行 `id` 命令。由于该 shell 对所有用户（"other"）可执行，因此命令成功并打印 **jdoe** 的 UID 和 GID。

```bash
# su - jdoe
$ /tmp/ksh -c "id"
uid=210 (jdoe) gid=1 (staff)
```

然后，root 用户将 `/tmp/ksh` 的权限更改为 set-UID。

```bash
# exit
# chmod u+s /tmp/ksh
# ls -l /tmp/ksh
-r-rsr-x 1 root system 243374 Apr 20 15:10 /tmp/ksh
```

用户 **jdoe** 再次通过 `/tmp/ksh` shell 执行 `id` 命令。由于该 shell 现在设置为 set-UID root，使用该 shell 的任何用户都具有 root 的有效 UID。

```bash
# su - jdoe
$ /tmp/ksh -c "id"
uid=210 (jdoe) gid=1 (staff) euid=0 (root)
```

此示例说明了 set-UID 和 set-GID 程序的固有危险性。在设置程序这些模式时应极其谨慎。完成此示例后，请确保删除 `/tmp/ksh` 副本。

```bash
# rm /tmp/ksh
```

## 访问控制列表 (ACLs)

除了基本访问权限外，AIX 5L 提供了一种更精细的方法，即使用访问控制列表（ACL）。使用三个命令来显示和操作访问控制列表：

| 命令 | 描述 |
| :---- | :---- |
| `aclget` | 打印指定文件上设置的 ACL |
| `acledit` | 在由环境变量 EDITOR 指定的编辑器中编辑 ACL |
| `aclput` | 将 ACL 分配给指定文件，从标准输入或单独的文件读取 |

要确定文件是否有关联的 ACL，可以使用 `aclget` 显示信息，或使用带有 **-e** 标志的 `ls` 命令，该命令将在基本权限右侧显示一个附加字段。如果该字段包含加号 (+)，则表示该文件已设置 ACL。

## 设置 ACL

ACL 由三个部分组成：属性、基本权限和扩展权限：

```bash
$ aclget /home/datafile
attributes:
base permissions
    owner(dJoe): rw-
    group(staff): r--
    others: ---
extended permissions
    disabled
```

前面的 ACL 是为使用 **umask** 为 022 创建且未分配任何扩展权限的文件创建的。

**属性** ACL 的属性部分详细说明了文件上的任何特殊模式，例如 set-UID (SUID)、set-GID (SGID) 或“粘滞位” (SVTX)。这些模式应使用带有符号表示法的 **chmod** 命令设置（原因将在本节稍后解释）。

**基本权限** 基本权限部分显示设置在该文件上的标准权限，也是通过 **chmod** 命令或根据用户的 **umask** 值设置的。

**扩展权限** 扩展权限部分包含访问控制条目 (ACE) 的列表。一个 ACE 由三个字段组成：关键字、符号表示法的权限以及该 ACE 适用的用户和/或组列表。关键字是 **permit**、**deny** 或 **specify** 之一。

```bash
$ aclget /home/datafile
...
extended permissions
enabled
specify    rw-    u:jane
specify    rw-    g:payadmin
deny       rw-    u:fred
permit     r--    g:payroll
```

扩展权限部分的上面几行指定

- 扩展权限已启用（注意“enabled”一词必须如所示出现，否则 ACL 不会激活）。
- 用户 **jane** 可以读取和写入该文件。
- **payadmin** 组的任何成员都可以读取和写入该文件。
- 用户 **fred** 不能读取或写入该文件，即使他是 **staff** 或 **payadmin** 组的成员。
- **payroll** 组的任何成员都可以读取该文件。

