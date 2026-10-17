
## 第 22 章 Samba 身份验证

### 22.1. 在 Linux 上创建用户

我们将为 Samba 服务器创建一个用户，并让该用户成为通过 Samba 共享创建的文件的所有者。这个匿名用户有一个清晰的描述，但没有登录 shell。

```
[root@RHEL52 samba]# useradd -s /bin/false sambanobody
[root@RHEL52 samba]# usermod -c "Anonymous Samba Access" sambanobody
[root@RHEL52 samba]# passwd sambanobody
Changing password for user sambanobody:
New UNIX password:
Retype new password:
passwd: all authentication tokens updated successfully.
```

### 22.2. 创建用户

我们可以使用此用户作为文件和目录的所有者，而不是使用 `root` 账户。这种方法更清晰且安全。

```
[root@RHEL52 samba]# chmod -R sambanobody:sambanobody /srv/samba/
[root@RHEL52 samba]# ls -al /srv/samba/writable/
total 12
drwxr-xr-x 6 sambanobody 4096 Jan 21 06:01 ..
drwxr-xr-x 6 sambanobody 4096 Jan 21 06:01 ..
-rw-r--r-- 1 sambanobody 6 Jan 21 06:16 hoi.txt
```

### 22.3. `/usr/bin/smbpassword`

我们在之前的示例中创建的匿名用户账户尚未被 Samba 使用。仅用于我们为共享创建的文件和目录。本节的目标是强制让通过 Samba 共享创建的文件所有权属于`sambanobody`。记住，我们的服务器仍然对所有人开放，他们需要这个账户密码。为了实现这一点，我们首先必须告诉 Samba 关于这个用户。我们可以通过将账户添加到`smbpasswd`来做到。

```
[root@RHEL52 samba]# smbpasswd -a sambanobody
New SMB password:
Retype SMB password:
Added user sambanobody.
```

### 22.4. `/etc/samba/smbpassword`

要找到这些信息保存在何处（目前），请使用`smbd -b`。`PRIVATE_DIR`变量将向你显示 Samba 数据库的位置。

```
[root@RHEL52 samba]# smbd -b | grep PRIVATE
PRIVATE_DIR: /etc/samba
[root@RHEL52 samba]# ls -l smbpassword
-rw------- 1 root root Jan 21 06:16
```

你可以使用简单的`cat`来查看`smbpassword`数据库的内容。`sambanobody`用户有一个密码（它是秘密的）。

```
[root@RHEL52 samba]# cat smbpassword
```

### 22.5. `passdb backend`

注意，最近版本的 Samba 将`tdbsam`设置为`passdb backend`参数的默认值。

```
root@RHEL52 ~]# samba -v>/dev/null | grep 'passdb backend'
passdb backend = tdbsam
```

### 22.6. 强制使用此用户

现在 Samba 知道了这个用户，我们可以调整可写共享，以强制通过它创建的文件的所有权。为此，我们使用`force user`和`force group`选项。现在我们可以确保 Samba 共享中的所有文件都属于`sambanobody`用户。下面是我们在`smb.conf`中对共享的新定义。

```
[pubwrite]
path = /srv/samba/writable
comment = files to write
force user = sambanobody
force group = sambanobody
read only = no
guest ok = yes
```

当你重新连接到共享并写入文件时，`sambanobody`用户将拥有新创建的文件（无需知道密码）。

### 22.7. 练习：第一个用户账户

1. 创建一个用于 Samba 的用户账户。
2. 将该账户添加到 Samba 数据库中。
3. 确保所有人都能读写文件，使用`smbclient`和微软计算机进行测试。
4. 验证由（各种）用户创建的文件的归权情况。

### 22.8. 解决方案：可写文件服务器

1. 创建一个目录并用 Samba 共享。

```
mkdir /srv/samba/writable
chmod 777 /srv/samba/writable
```

`smb.conf`中的共享部分可能如下：

```
[pubwrite]
path = /srv/samba/writable
comment = files to write
read only = no
guest ok = yes
```

2. 确保所有人都能读写文件，使用`smbclient`和微软计算机进行写入测试。

使用`smbclient`测试写入：

```
echo one > count.txt
echo two >> count.txt
echo three >> count.txt
smbclient //localhost/pubwrite
Password:
smb: \put count.txt
```

3. 验证由（各种）用户创建的文件的归权情况。

```
ls -l /srv/samba/writable
```

### Samba 认证

然后我们使用正确的密码，并验证我们可以访问共享上的一个文件。

```
[root@RHEL52 samba]# smclient //teacher0/authwrite -U martina stargate
Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.el5]
smb:> more serena.txt
getting file serena.txt of size 14 as /tmp/smbmore.QQfmSN (6.8 kb/s)
one
two
three
smb:> q
```

### 22.9. 验证所有权

我们现在拥有了一个带有身份验证访问的简单独立 Samba 文件服务器。共享中的文件属于它们相应的所有者。

```
[root@RHEL52 samba]# ls -l /srv/samba/authwrite/
total 8
-rw-r--r-- 1 martina martina 0 Jan 21 20:06 martina.txt
-rw-r--r-- 1 serena serena 14 Jan 21 20:06 serena.txt
-rw-r--r-- 1 serena serena 6 Jan 21 20:09 ser.txt
```

### 22.10. 常见问题

#### 22.10.1. `NT_STATUS_BAD_NETWORK_NAME`

当你忘记创建目标目录时，会得到`NT_STATUS_BAD_NETWORK_NAME`。

```
[root@RHEL52 samba]# rm -rf /srv/samba/authwrite/
[root@RHEL52 samba]# smclient //teacher0/authwrite -U martina stargate
Domain=[TEACHER0] OS=[Unix] Server=[Samba 3.0.33-7.el5]
tree connected: NT_STATUS_BAD_NETWORK_NAME
```

#### 22.10.2. `NT_STATUS_LOGON_FAILURE`

当你输入错误的密码或使用不存在的用户名时，会得到`NT_STATUS_LOGON_FAILURE`。

```
[root@RHEL52 samba]# smclient //teacher0/authwrite -U martina STARGATE
session setup failed: NT_STATUS_LOGON_FAILURE
```

#### 22.10.3. 用户名（不）区分大小写

记住 Linux 上的用户名是区分大小写的。

```
[root@RHEL52 samba]# su - MARTINA
su: user MARTINA does not exist
```

### Samba 认证
