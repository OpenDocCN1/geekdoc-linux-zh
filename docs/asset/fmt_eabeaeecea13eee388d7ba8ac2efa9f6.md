
成功将 Domain Restore Operators 作为域组添加到映射数据库中。

为了检查一切是否都正常，我们可以列出现有的组。

```
[root@juliet ~]## net groupmap list
Domain Admins (S-1-5-21-290474568-710709298-978122733-512) -> WinAdmins
Domain Users (S-1-5-21-290474568-710709298-978122733-513) -> WinUsers
Domain Guests (S-1-5-21-290474568-710709298-978122733-514) -> WinGuests
Domain Backup Operators (S-1-5-21-290474568-710709298-978122733-515) -> WinBackupOperators
Domain Restore Operators (S-1-5-21-290474568-710709298-978122733-516) -> WinRestoreOperators
```

完成映射后，我们还需要为不同的组授予相应的权限。

```
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Admins'
SeMachineAccountPrivilege
输入 root 密码：
权限已授予。
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Admins'
SePrintOperatorPrivilege
输入 root 密码：
权限已授予。
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Admins'
SeAddUsersPrivilege
输入 root 密码：
权限已授予。
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Admins'
SeRemoteShutdownPrivilege
```

# 第 15 章 SAMBA 作为 PDC 和 BDC

输入 root 密码：

权限已授予。

```
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Admins'
SeDiskOperatorPrivilege
输入 root 密码：
权限已授予。
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Admins'
SeTakeOwnershipPrivilege
输入 root 密码：
权限已授予。
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Backup Operators' SeBackupPrivilege
输入 root 密码：
权限已授予。
[root@juliet ~]## net rpc rights grant 'MY_SAMBA_DOMAIN\Domain Restore Operators' SeRestorePrivilege
输入 root 密码：
权限已授予。
```

如果我们需要查看每个权限的简短描述，可以使用 `net rpc list` 子命令获取。

```
[root@juliet ~]# net rpc rights list -U root
输入 root 密码：
```

- `SeMachineAccountPrivilege` 将机器添加到域
- `SeTakeOwnershipPrivilege` 夺取文件或其他对象的所有权
- `SeBackupPrivilege` 备份文件和目录
- `SeRestorePrivilege` 恢复文件和目录
- `SeRemoteShutdownPrivilege` 从远程系统强制关机
- `SePrintOperatorPrivilege` 管理打印机
- `SeAddUsersPrivilege` 向域添加用户和组
- `SeDiskOperatorPrivilege` 管理磁盘共享
- `SeSecurityPrivilege` 系统安全

## 现在创建域用户

现在我们将创建几个域用户：一个域管理员、一个域备份操作员和一个域恢复操作员。

```
[root@jullet ~# useradd antonio
[root@jullet ~# usermod -g WinAdmins -G WinUsers antonio
[root@jullet ~# smbpasswd -a antonio
 SMB 密码：
重新输入新的 SMB 密码：
已添加用户 antonio
[root@jullet ~# useradd john
[root@jullet ~# usermod -g WinBackupOperators -G WinUsers john
[root@jullet ~# smbpasswd -a john
 SMB 密码：
重新输入新的 SMB 密码：
已添加用户 john
[root@jullet ~# useradd jane
[root@jullet ~# usermod -g WinRestoreOperators -G WinUsers jane
[root@jullet ~# smbpasswd -a jane
 SMB 密码：
重新输入新的 SMB 密码：
已添加用户 jane.
```

此外，如果我们使用 SELinux，我们应该修改几个布尔值以确保 Samba 能够有效地作为 DC 工作。

```
[root@jullet ~# setsebool -P samba_domain_controller on
```

## 将计算机添加到现有域

一旦我们有了可以工作的 Samba，就可以开始添加工作站，但在在此之前需要考虑一些事情。

当我们尝试将工作站加入新域（或 Samba）时，客户端将尝试查找 NetBIOS 名称。我们将在后续章节深入研究 NetBIOS 和 WINS，但现在我们需要在工作站属性中配置 Samba 作为 WINS。

```
[root@jullet ~# setsebool -P samba_domain_controller on
[root@jullet ~# setsebool -P samba_run_unconfined
```

### WINS

负责响应 NetBIOS 查询的 Samba 服务是 `nmb`，因此如果它没有启动，我们需要启动它。

```
[root@juliet ~]# systemctl enable nmb
创建符号链接 /etc/systemd/system/multi-user.target.wants/nmb.service -> /lib/systemd/system/nmb.service.
[root@juliet ~]# systemctl start nmb
```

在 `/etc/samba/smb.conf` 中，有一些控制服务器行为的参数。我们将包括这两个选项：

```
netbios name
wins = yes
```

正如名称所示，`netbios` 指定服务器，`wins = yes` 也让 Samba 作为 WINS 服务器工作。为了使更改生效，我们需要重启 Samba 服务。

```
[root@juliet ~]# systemctl restart smbd
```

### 域服务器

在系统属性对话框（图 15-2）中将 Windows 工作站加入域。在计算机/域对话框中输入域名并点击确定。然后我们使用管理员权限的用户进行身份验证（图 15-3），并等待过程完成。

![](img/dfa44432604022575079471b648e25ca_411_0.png)

图 15-2. 系统设置

![](img/dfa44432604022575079471b648e25ca_412_0.png)

图 15-3. 将工作站添加到域

### 使用管理员凭据验证

![](img/dfa44432604022575079471b648e25ca_413_0.png)

图 15-4. 使用管理员凭据验证

然而，由于 NT 是一项过老的技术，Windows 7 及更高版本在尝试加入域时可能会显示图 15-5 所示的错误。

![](img/dfa44432604022575079471b648e25ca_413_1.png)

图 15-5. 将 Windows 7 加入域时的错误

# 无法找到机器账户
