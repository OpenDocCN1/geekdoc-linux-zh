
- 7. 确保 IP 为 192.168.1.203 的计算机无法访问 `budget` 共享。

- 8. 确保（在 `budget` 共享上）用户只能看到他们有权访问的文件目录。

- 9. 确保在浏览网络时看不到 `sales` 共享。

- 10. `sales` 共享中创建的所有文件都应具有 640 或更高的权限。

- 11. `budget` 共享中创建的所有目录都应具有 750 或更高的权限。

- 12. `budget` 共享文件的权限设置不应超过 664。

- 13. `budget` 共享文件的权限不应小于 500。

## 23.6. 解决方案：保护共享

+ 1. 创建一个名为 `sales` 的可写共享，和一个名为 `budget` 的只读共享。测试其是否工作正常。

```
see previous solutions on how to do this...
```

+ 2. 将 `sales` 共享的访问权限限制为 `ann`、`sandra` 和 `veronique`。

```
valid users = ann, sandra, veronique
```

+ 3. 确保 `roberto` 无法访问 `sales` 共享。

```
invalid users = roberto
```

+ 4. 即使该共享是可写的，`ann` 也应该仅具有读取权限。

```
read list = ann
```

+ 5. 即使 `budget` 是只读的，`sandra` 也应该同样具有写入权限。

```
write list = sandra
```

+ 6. 将一个共享目录限制在 `192.168.1.0/24` 子网内，将另一个共享限制在 IP 地址为 `192.168.1.33` 和 `172.17.18.19` 的两台计算机上。

```
hosts allow = 192.168.1.1.
hosts allow = 192.168.1.33, 172.17.18.19
```

+ 7. 确保 IP 为 `192.168.1.203` 的计算机无法访问 `budget` 共享。

```
hosts deny = 192.168.1.203
```

+ 8. 确保（`budget` 共享）用户只能看到他们拥有访问权限的文件和目录。

```
hide unreadable = yes
```

+ 9. 确保在浏览网络时 `sales` 共享不可见。

```
browsable = no
```

+ 10. 在 `sales` 共享中创建的所有文件权限应为 640 或更低。

```
create mask = 640
```

+ 11. 在 `budget` 共享中创建的所有目录权限应为 750 或更高。

```
force directory mode = 750
```

+ 12. `sales` 共享中文件的权限永远不应高于 664。

```
security mask = 300
```

+ 13. `budget` 共享中文件的权限永远不应低于 500。

```
force security directory mask = 500
```

+ 14. 如果时间允许（或者你正在等待其他学生完成此练习），合并“只读”和“可写”语句以检查哪一个的优先级更高。

+ 15. 如果时间允许，合并 `read list`、`write list`、`hosts allow` 和 `hosts deny`。这些中哪一个具有优先级？

## 第 24 章. samba 域成员

## 24.1. smb.conf 的更改

### 24.1.1. workgroup

全局部分的 `workgroup` 选项应与 Active Directory 域的 `netbios` 名称匹配。

```
workgroup = STARGATE
```

### 24.1.2. security mode

身份验证现在由 `samba` 处理，而是由 Active Directory 域控制器处理，因此我们将 `security` 选项设置为 `domain`。

```
security = Domain
```

### 24.1.3. Linux uid

Linux 要求每个访问其文件系统的用户都必须有一个用户账户，我们需要为 Samba 提供一组它可以用于创建这些用户账户的 `uid` 范围和 `gid` 范围。范围由 `idmap uid` 和 `idmap gid` 参数决定。第一个连接的 Active Directory 用户将获得 Linux `uid` 20000。

```
idmap uid = 20000-22000
idmap gid = 20000-22000
```

### 24.1.4. winbind 使用默认域

`winbind use default domain` 参数使 `winbind` 对名称中不包含域组件的用户操作。

```
winbind use default domain = yes
```

### 24.1.5. smb.conf 中的 [global] 部分

以下是 `smb.conf` 中新的 `[global]` 部分。

```
[global]
workgroup = STARGATE
security = Domain
server string = Stargate Domain Server
idmap uid = 20000-22000
idmap gid = 20000-22000
winbind use default domain = yes
```

### 24.1.6. /etc/krb5.conf 中的 realm

要连接 Windows 2003 或更高版本，需要调整 `/etc/krb5.conf` 中的 `kerberos` realm 并将两个查找设置为 `true`。

```
[libdefaults]
default_realm = STARGATE.LOCAL
dns_lookup = true
dns_lookup_kdc = true
```

### 24.1.7. smb.conf 中的 [share] 部分

`smb.conf` 中不需要 `share` 部分。记住不要在 `smb` 或 `(/etc/passwd)` 中手动创建用户。仅允许 Active Directory 用户访问。

```
[domain]
path = /srv/samba/domain
comment = Active Directory users
read only = no
```

## 24.2. 加入 Active Directory 域

当 Samba 服务器停止时，你可以使用 `net rpc` 加入 Active Directory 域。

```
root@RHEL52 samba]# service smb stop      [ OK ]
Shutting down SMB services:                      [ OK ]
Shutting down NMB services:                     [ OK ]
root@RHEL52 samba]# net rpc join -U Administrator
Password:
Joined domain STARGATE.
```

我们可以为此 `samba` 服务器在 Active Directory 中创建一个计算机账户。

## 24.3. winbind

### 24.3.1. 将 winbind 添加到 nsswitch.conf

`winbind` 进程与 Active Directory 域通信。现在我们需要更新 `/etc/nsswitch.conf` 文件，以便用户和主机名可以通过 `winbind` 进程进行解析![](img/66ba25c822cbe26e00b2d993c1a54248_0.png)。

```
root@RHEL52 samba]# vi /etc/nsswitch.conf
```

### 24.3.2. 启动 samba 和 winbind

```
root@RHEL52 samba]# service smb start
[ OK ]
root@RHEL52 samba]# service winbind start
[ OK ]
```

## 24.4. winbind

### 24.4.1. 验证

可以使用 `wininfo -t` 验证 `samba` 和 Active Directory 之间的信任。

```
root@RHEL52 samba]# wininfo -t
```

### 24.4.2. 列出所有用户

可以使用 `wininfo -u` 获取所有用户列表。

```
root@RHEL52 samba]# wininfo -u
```

### 24.4.3. 列出所有组

可以使用 `wininfo -g` 获取所有组列表。

```
root@RHEL52 samba]# wininfo -g
```

### 24.4.4. 查询用户

可以使用 `wininfo -a` 验证 Active Directory 中的用户。

```
root@RHEL52 samba]# wininfo -a
```
