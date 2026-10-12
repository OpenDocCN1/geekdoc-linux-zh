
`server string = Samba Server`

`security = user`

## 14.4. 配置共享

我们在`smb.conf`中添加`[share]`段（并且不要忘记创建`/srv/samba/authwrite`目录）。

```ini
[authwrite]
path = /srv/samba/authwrite
comment = authenticated users
read only = no
guest ok = no
```

## 14.5. 使用 `net use` 测试访问

重启`Samba`后，我们将从微软计算机测试不同的用户。截图显示了从`Windows XP`使用`net use`。

```bash
C:\>net use m: \\teacher0\authwrite /user:serena

The command completed successfully.
```

```bash
C:\>m:echo greetings from Serena > serena.txt
```

下一张截图是`Windows 2000`上的`martina`，她成功写入了文件，但无法覆盖`serena`文件。

```bash
C:\>net use k: \\teacher0\authwrite /user:martina

The command completed successfully.
```

```bash
C:\>k:

k:\echo greetings from martina > Martina.txt

K:\echo overwrite > serena.txt

Access is denied.
```

## 14.6. 使用 `smbclient` 测试访问

你也可以使用`smbclient`测试带身份的连接。

```bash
[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina wrongpass

session setup failed: NT_STATUS_LOGON_FAILURE
```

然后我们使用正确的密码，并验证我们可以访问共享上的文件。

```bash
[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

smb: \> more serena.txt

getting file serena.txt of size 14 as /tmp/smb.XXXX (6.8 kb/s)

one

two

three

smb: \> q
```

## 14.7. 验证所有权

我们现在有一个带认证访问的简单服务器。共享中的文件属于它们相应的所有者。

```bash
[root@RHEL52 samba]# ls -l /srv/samba/authwrite/

total 8

-rw-r--r-- 1 martina martina 0 Jan 21 20:06 martina.txt

-rw-r--r-- 1 serena serena 14 Jan 21 21:25 serena.txt

-rw-r--r-- 1 serena serena 6 Jan 21 20:09 ser.txt
```

## 14.8. 常见问题

### 14.8.1. `NT_STATUS_BAD_NETWORK_NAME`

当你忘记创建目标目录时，会得到`NT_STATUS_BAD_NETWORK_NAME`。

```bash
[root@RHEL52 samba]# rm -rf /srv/samba/authwrite/

[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

tree connected failed: NT_STATUS_BAD_NETWORK_NAME
```

### 14.8.2. `NT_STATUS_LOGON_FAILURE`

输入错误的密码或使用不存在的用户名时，会得到`NT_STATUS_LOGON_FAILURE`。

### 14.8.3. 用户名大小敏感

记住`Linux`上的用户名是大小敏感的。

```bash
[root@RHEL52 samba]# su - MARTINA

su: user MARTINA does not exist
```

# `Samba` 认证

```bash
[root@RHEL52 samba]# su - martina

[martina@RHEL52 ~]#
```

但微软计算机中的用户名是不区分大小写的。

```bash
[root@RHEL52 samba]# smbclient //teacher0/authwrite -U martina stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

smb: \> q

[root@RHEL52 samba]# smbclient //teacher0/authwrite -U MARTINA stargate

Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.7.el5]

smb: \> q
```

## 14.9. 练习：`Samba` 认证

- 0. 确保你已经为之前的练习中的`smb.conf`做了适当的备份。
- 1. 创建三个用户（在`Linux`和`Samba`上），并记住它们的密码！
- 2. 设置一个仅允许身份验证用户访问的共享目录。
- 3. 使用`smbclient`和`Windows`计算机访问你的共享，使用多个用户账户（`Windows`需要为此进行注销/重新登录）。
- 4. 验证这些用户创建的文件是否属于他们。
- 5. 尝试从另一个用户处更改或删除文件。

## 14.10. 解决方案：`Samba` 认证

- 1. 创建三个用户（在`Linux`和`Samba`上），并记住它们的密码！

```bash
useradd -c 'SMB user1' user
passwd user
```

- 2. 设置一个仅允许身份验证用户访问的共享目录。
`smb.conf`中的共享部分可能如下：

```ini
[authwrite]
path = /srv/samba/authwrite
comment = authenticated users only
read only = no
guest ok = no
```

- 3. 使用`smbclient`和`Windows`计算机访问你的共享，使用多个用户账户（`Windows`需要为此进行注销/重新登录）。

```bash
On Linux: smbclient //studentX/authwrite -U user1 password

On Windows: net use p: \\studentX\authwrite password /user:user
```

- 4. 验证这些用户创建的文件是否属于他们。

```bash
ls -l /srv/samba/authwrite
```

- 5. 尝试从另一个用户处更改或删除文件。
你不应该能够更改或覆盖其他的文件。

# 第 15 章 `Samba` 共享安全

## 15.1. 基于用户名的安全

### 15.1.1. `valid users`

要限制每个共享的访问用户，你可以使用`valid users`参数。在示例中，只有列出的有效用户才能访问网球共享目录。

```ini
[tennis]
path = /srv/samba/tennis
comment = authenticated and valid users only
read only = No
guest users = serena, kim, venus, justice
```

### 15.1.2. `invalid users`

如果你非常多疑，也可以使用`invalid users`显式地拒绝列出的用户访问。当一个用户同时出现在两个列表中时，该用户将没有访问权限！

```ini
[tennis]
path = /srv/samba/tennis
read only = No
guest users = No
valid users = kim, serena, venus, justice
invalid users = venus
```

### 15.1.3. `read list`

在可写共享目录上，你可以使用`read list`参数设置一个只读用户列表。

```ini
[football]
path = /srv/samba/football
read only = No
```
