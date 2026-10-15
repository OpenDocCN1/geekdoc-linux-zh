
`password requisite pam_cracklib.so minlen=10 dcredit=1 ucredit=1 lcredit=1 difok=4`

注意用于执行密码复杂性的 PAM 称为 `cracklib.so`。要在多次无效登录后锁定账户，可以使用 `pam_tally2.so` 或 `pam_faillock.so`。例如，为了使用 `pam_tally2.so` 在用户在 300 秒 (`unlock_time=300`) 内尝试登录失败三次 (`deny=3`) 后锁定用户，你可以在 `/etc/pam.d` 中添加以下行：

```
auth required pam_tally2.so deny=3 unlock_time=300
```

要使用 `pam_faillock.so` 实施相同的账户锁定设置，你应该在 `/etc/pam.d` 中的相应文件中添加以下行：

```
auth required pam_faillock.so preauth deny=3 unlock_time=300
```

## 第 14 章 安全、故障排除与性能

`faillock` 命令用于列出被 `pam_faillock.so` 锁的用户。要解锁被 `pam_tally2.so` 锁定的用户 `bob`，可以使用 `pam_tally2 --reset --user bob`；而要解锁被 `pam_faillock.so` 锁定的用户 `james`，可以使用 `faillock --user` 命令。

身份验证服务（如 Microsoft Active Directory）也可用于限制对操作系统的未经授权访问。大多数身份验证服务使用安全协议（如 Kerberos）来验证用户，并存储信息和身份验证需求。例如，对于轻级目录访问协议（LDAP），可以使用 LDAP 数据库来确保只有 Accounting 组的成员才能登录 Accounting 部门的计算机。

你可以通过安装适用于 Linux 发行版的 Kerberos 软件包来配置 Linux 系统使用 Kerberos 登录身份验证服务。接下来，你需要在 `/etc/krb5.conf` 文件中提供身份验证服务的名称和服务器。之后，你可以使用 `kinit` 命令登录身份验证服务；例如，`kinit jaason.eckert@trios.com` 将使用 Kerberos 以用户 `jaason.eckert` 的身份登录 `trios.com` 验证服务，并对 LDAP 数据库中的用户 `jaason.eckert` 执行限制。

你可以使用 `klist` 命令查看你的 Kerberos 身份验证信息。大多数 Linux 发行版集成了 `kinit` 功能来显示管理器登录界面，以确保身份验证服务专门验证用户。此外，你可以在 `/etc/pam.d` 内的相应文件中添加 `password sufficient pam_ldap.so` 行，以确保系统在尝试本地身份验证之前，所有区域都允许登录通过 Kerberos 身份验证服务提供的 LDAP 数据库。

某些组织除了用户名和密码外，还使用其他软件和硬件验证方法来进一步限制对操作系统的访问；这种做法被称为**生物识别多因素身份验证**。例如，带有生物识别指纹读取器并安装了相应软件的 Linux 系统会在你提供用户名和密码后提示你扫描指纹。或者，安装了 RSA SecureID 软件的 Linux 系统会在你提供用户名和密码后，提示你输入存储在 RSA SecureID 令牌设备上的一次性密码（OTP）。此 OTP 使用算法频繁更改，该算法与 Linux 系统上为你的用户账户安装的 RSA SecureID 令牌设备及 RSA SecureID 软件相同；通过提供 OTP，你证明你拥有正确的 RSA SecureID 令牌。

另一个安全考虑因素是限制对图形桌面的访问。如果你离开工作站几分钟且仍保持登录状态，其他人在你离开期间可以使用你的操作系统。为了避免这种情况，你应该在离开电脑之前退出命令行壳（`shell`）或锁定你的桌面环境屏幕。要在 GNOME 桌面中锁定屏幕，你可以访问桌面右上角的下拉菜单并选择锁定图标。要再次使用桌面，你需要输入密码。

### 提供 Root 用户访问权限

如果你对 Linux 系统拥有 `root` 权限，那么尽可能缩短你作为 `root` 用户登录的时间是非常重要的，因为这可以减少在你不小心离开系统且未锁定桌面或退出 `shell` 时，其他用户访问你终端的几率。最佳实践是创建一个普通用户账户，用于检查邮件和执行其他日常任务。回想第 2 章，你只有在需要执行管理任务时才能使用 `su` 获取 `root` 权限。完成后，你可以使用 `exit` 命令返回上一个 `shell`，此时你是以普通用户账户身份登录的。

> 注意：`root` 用户可以使用 `su` 命令切换到任何其他用户账户，而无需指定该账户的密码。

尽管如此，某些普通用户（如软件开发人员）在某些情况下需要以 `root` 用户身份运行某些命令。与其给他们 `root` 密码，最好的方法是通过 `sudo` 命令赋予他们运行某些命令的能力。`sudo` 命令检查 `/etc/sudoers` 文件以查看你是否有权以不同用户的身份运行命令。以下 `/etc/sudoers` 文件允许开发人员 `mary` 和 `bob` 在 `server1` 和 `server2` 计算机上以 `root` 身份运行 `killall` 命令：

```
[root@server1 ~]# cat /etc/sudoers

User_Alias SD = mary, bob

Cmnd_Alias KILL = /usr/bin/kill, /usr/bin/killall

Host_Alias SERVERS = server1, server2

SD SERVERS = (root) KILL

[root@server1 ~]#
```

现在，如果 `mary` 需要杀死 `server1` 上的 `cron` 进程（该进程以 `root` 用户身份启动）以测试她编写的程序，她需要使用 `sudo` 命令（如下输出所示），并提供她的密码：

```
[mary@server1 ~]$ ps -ef | grep cron
root      2281      1 0 21:20? 00:00:00 /usr/sbin/crond -n
[mary@server1 ~]$ kill -9 2281
-bash: kill: (2281) - Operation not permitted
[mary@server1 ~]$ sudo kill -9 2281
[sudo] password for mary: ********
[mary@server1 ~]$_
```

记住，大多数 Linux 发行版创建的第一个普通用户会自动分配到 `wheel` 组。`wheel` 组的成员被授予使用 `sudo` 的权限。

### 使用加密保护数据

加密可以防止具有物理访问权限的人读取数据。这对于容易被盗的笔记本电脑尤为重要。最好使用 Linux 密钥设置（LUKS）加密整个文件系统。密码作为对称加密密钥，每次挂载文件系统时必须指定。

在安装后设置 LUKS，你可以运行 `cryptsetup` 命令。例如，对空的 `/dev/sdb` 分区配置 LUKS 加密，你可以运行以下命令并在提示时提供密码：

```
[root@server1 ~]# cryptsetup luksFormat /dev/sdb
WARNING!
=======
这将不可逆地覆盖 /dev/sdb 上的数据。
确定吗？（输入大写的 yes）：YES
Enter passphrase for /dev/sdb: ********
Verify passphrase: ********
[root@server1 ~]#
```

接下来，你可以将加密的 `/dev/sdb` 分区作为卷映射 Linux 设备映射，并创建文件系统。要将 `/dev/sdb` 作为名为 `securedata` 的卷并在映射卷（`/dev/mapper/securedata`）上创建 `ext4` 文件系统，你可以运行以下命令：

```
[root@server1 ~]# cryptsetup luksOpen /dev/sdb securedata
Enter passphrase for /dev/sdb: ********
[root@server1]# mkfs -t ext4 /dev/mapper/securedata
mke2fs 1.43.1 (Jan-2018)
创建一个包含 2096379 个块和 524288 个节点的文件系统
文件系统 UUID: dc3e7bb4-bda4-4aaa-b499-8a9687e57b1
超级块备份存储在块上：
32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632
分配组表：完成
写入节点表：完成
创建日志（16384 个块）：完成
写入超级块和文件系统统计信息：完成
```
[root@server1]#_
```

在创建文件系统后，你可以创建一个挂载点目录并像挂载任何其他文件系统一样挂载映射卷。后续
