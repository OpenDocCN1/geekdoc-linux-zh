
New UNIX password:

Retype new UNIX password:

`passwd: all authentication tokens updated successfully.`

## 13.2. 文件的所有权

我们可以使用此用户作为文件和目录的所有者，而不是使用 `root` 账户。这种方法清晰且安全得多。

```
[root@RHEL52 samba]# chmod -R sambanobody:sambanobody /srv/samba/
```

```
[root@RHEL52 samba]# ls -al /srv/samba/writable/

drwxrxrwx 2 sambanobody 4096 Jan 21 06:01 ..
drwxrxr-x 6 sambanobody 4096 Jan 21 06:01 ..
-rw-r--r-- 1 sambanobody 6 Jan 21 06:16 hoi.txt
```

## 13.3. /usr/bin/smbpasswd

我们在之前的示例中创建的 `nobody` 用户账户尚未用于 `samba`。只需使用我们为共享而创建的文件和目录即可。本节的目标是强制要求通过 `samba` 共享创建的文件所有权属于我们的 `sambanobody` 用户。记住，我们的服务器仍然对所有人开放，没有人需要知道这个账户或密码。我们只是想要一个干净的 `Linux` 服务器。

为了实现这一点，我们首先必须让 `samba` 知道这个用户。我们可以通过将账户添加到 `smbpasswd` 中来实现这一点。

```
[root@RHEL52 samba]# smbpasswd -a sambanobody

New SMB password:

Retype SMB password:

Added user sambanobody.
```

## 13.4. /etc/samba/smbpasswd

要找到 `samba`（目前）存储这些信息的地方，请使用 `smbd -b`。`PRIVATE_DIR` 变量将向你显示 `smpasswd` 数据库的位置。

```
[root@RHEL52 samba]# smbd -b | grep PRIVATE

PRIVATE_DIR:/etc/samba
```

```
[root@RHEL52 samba]# ls -l /etc/samba/smbpasswd

-rw------- 1 root root 110 Jan 21 06:19 smbpasswd
```

你可以使用简单的 `cat` 命令查看 `smbpasswd` 数据库的内容。`sambanobody` 用户有一个密码（它是秘密的）。

```
[root@RHEL52 samba]# cat smbpasswd
```

## 13.5. passdb 后端

注意，最近版本的 `Samba` 将 `tdbsam` 作为 `passdb backend` 参数的默认值。

```
root@ubull110:~# testparam -v 2>/dev/null | grep 'passdb backend'

passdb backend = tdbsam
```

## 13.6. 强制使用此用户

现在 `Samba` 知道了这个用户，我们可以调整我们的可写共享，以强制通过它创建的文件的所有权。为此，我们使用 `force user` 和 `force group` 选项。现在我们可以确保 `Samba` 可写共享中的所有文件都属于同一个 `sambanobody` 用户。

下面是我们在 `smb.conf` 中对共享的更新定义。

```
[pubwrite]

path = /srv/samba/writable

comment = files to write

force user = sambanobody

force group = sambanobody

read only = no

guest ok = yes
```

当你重新连接到共享并写入文件时，这个 `sambanobody` 用户将拥有新创建的文件（并且没有人需要知道密码）。

## 13.7. 练习：第一个 samba 用户账户

- 1. 创建一个用于 `samba` 的用户账户。
- 2. 将此用户添加到 `samba` 的用户数据库中。
- 3. 创建一个可写入的共享目录，并使用 `force user` 和 `force group` 指令强制文件所有权。
- 4. 使用 `smbclient`、`net use` 和 `Windows` 资源管理器测试 `force user` 的功能。

## 13.8. 解决方案：第一个 samba 用户账户

- 1. 创建一个用于 `samba` 的用户账户。
```
useradd -s /bin/false sambanobody

usermod -c "Anonymous Samba Access" sambanobody

password sambanobody
```
- 2. 将此用户添加到 `samba` 的用户数据库中。
```
smbpasswd -a sambanobody
```
- 3. 创建一个可写入的共享目录，并使用 `force user` 和 `force group` 指令强制文件所有权。
```
[userwrite]

path = /srv/samba/writable

comment = files owned by sambanobody

read only = no

guest ok = yes

force user = sambanobody

force group = sambanobody
```
- 4. 使用 `smbclient`、`net use` 和 `Windows` 资源管理器测试 `force user` 的功能。
```
ls -l /srv/samba/writable (并验证所有权)
```

# 第 14 章 samba 认证

## 14.1. 在 Linux 上创建用户

本示例的目标是设置一个多个用户可以访问的共享。用户在访问此共享之前需要使用密码身份验证。我们将创建三个命名的用户，每个都有自己的密码。首先，我们在 `Linux` 上添加这些用户。

```
[root@RHEL52 samba]# useradd -c "Serena" serena

[root@RHEL52 samba]# useradd -c "Justine" justine

[root@RHEL52 samba]# useradd -c "Martina" martina

[root@RHEL52 samba]# password serena

Changing password for user serena.

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully.

[root@RHEL52 samba]# password justine

Changing password for user justine.

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully.

[root@RHEL52 samba]# password martina

Changing password for user martina.

New UNIX password:

Retype new UNIX password:

passwd: all authentication tokens updated successfully.
```

## 14.2. 在 samba 中创建用户

然后我们将相同的密码它们添加到 `smbpasswd` 文件。

```
[root@RHEL52 samba]# smbpasswd -a serena

New SMB password:

Retype SMB password:

Added user serena.

[root@RHEL52 samba]# smbpasswd -a justine

New SMB password:

Retype SMB password:

Added user justine.

[root@RHEL52 samba]# smbpasswd -a martina

New SMB password:

Retype SMB password:

Added user martina.
```

## 14.3. security = user

记住我们在 `[global]` 段中将 `samba` 的安全模式设置为 `share`。由于我们现在要求用户提供用户名和密码才能访问服务器，我们需要更改这一点。设置 `security = user` 后，`[global]` 段如下所示：

```
[global]

workgroup = WORKGROUP

netbios name = TEACHER
```
