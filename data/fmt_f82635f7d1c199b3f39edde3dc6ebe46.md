
现在，让此脚本具有执行权限并更改其默认权限：
`[root@deep]] chmod 700 /etc/rc.d/init.d/smbd`

使用命令为 Samba 创建符号链接 rc.d 链接：
`[root@deep]# chkconfig --add smbd`

Samba 脚本会在重启服务器时自动启动 `smbd` 和 `nmbd` 守护进程。
你可以通过执行以下命令来更改：
`[root@deep]# chkconfig --level 345 smbd on`

© Copyright 1999 Open Network Architecture ®

关于此页面的意见和建议，请邮件至 `gmourani@videotron.ca`

使用以下命令手动启动 Samba 服务器：
`[root@deep]# /etc/rc.d/init/samba start`

# "/etc/pam.d/samba" 文件的配置

配置你的 `"etc/pam.d/samba"` 文件以使用 `pam` 认证并添加内容：

创建 `samba` 文件（`touch /etc/pam.d/samba`）并添加内容：

```
Auth            required /lib/security/pam_pwdb.so nullock shadow

Account         required /lib/security/pam_pwdb.so
```

# "etc/logrotate.d/samba" 文件的配置

配置你的 `"etc/logrotate.d/samba"` 文件以自动轮转日志文件。

创建 `samba` 文件（`touch /etc/logrotate.d/samba`）并添加内容：

```
/var/log/samba/log.nmb {

    notifyempty

    missingok

    postrotate

        /usr/bin/killall -HUP nmbd

    endrotate

}

/var/log/samba/log.smb {

    notifyempty

    missingok

    postrotate

        /usr/bin/killall -HUP smbd

    endrotate

}
```

# 安全保护 Samba

创建加密密码文件
`"etc/smbpasswd"` 文件是 Samba 的加密密码文件。它包含了用户名、Unix 用户 ID 以及用户的 `smb` 哈希后的密码，以及账户标志和最后更改密码的时间。

**重要提示：** 要创建一个 Samba 账户，你必须先为该用户准备一个有效的 Linux 账户。使用以下命令从你的 `"etc/passwd"` 文件中生成 `smbpasswd` 文件：

```bash
[root@deep]# cat /etc/passwd | mksmbpasswd.sh > /etc/smbpasswd
```

创建用户账户：

```bash
[root@deep]# smbpasswd -a username (记住 "username" 必须是一个有效的 Linux 账户)。

New Samba password:

Retype new Samba password:

Password changed for user username.
```

```bash
[root@deep]# chmod 600 /etc/smbpasswd
[root@deep]# testparam (这将验证 smb.conf 文件是否有错误)。
```

注意：更多信息请参考 `samba/doc/texts/` 中的 `ENCRYPTION.txt`。

# 保护重要的配置文件

不可变位（immutable bit）可以用于防止意外删除或覆盖受保护的文件。它还可以防止有人创建其符号链接。一旦配置了 `smb.conf` 和 `inhosts` 文件，建议使用命令对它们进行保护：

```bash
[root@deep]# chattr /etc/smb.conf
[root@deep]# chattr /etc/inhosts
```

# 更多文档

有关更多详细信息，有几个 man 页面可以阅读：

- `man Samba (7)` - 用于 UNIX 的 Windows SMB/CIFS 文件服务器
- `man smb.conf (5)` - Samba 套件的配置文件
- `man smbian (1)` - 类似于 ftp 的，用于访问服务器上的 SMB/CIFS 资源
- `man smbd (8)` - 服务器向客户端提供 SMB/CIFS 服务
- `man mount (8)` - 挂载系统
- `man smbmount (8)` - Samba 密码文件
- `man smpasswd (8)` - 更改用户密码
- `man nbd (1)` - 

```
[root@#deep] make depend
[root@#deep] make
[root@#deep] cd tests/
[root@#deep] make
[root@#deep] cd ..
[root@#deep] make install
```

`make depend` 命令将构建并生成不同文件所需的依赖关系，`make` 将所有源代码编译为可执行的二进制文件，然后 `make install` 将二进制文件及任何支持文件安装到适当的位置。

`"test"`目录下的 `make` 命令会在安装前执行一些重要的测试，以验证你的 LDAP 服务器的功能。如果某些测试失败，你需要在完成安装之前修复这些问题。

```
[root@#deep] install -m 700 /var/lib
[root@#deep] echo localhost > /etc/openldap/ldapserver
[root@#deep] strip /usr/lib/libldap.so.1.0.0
[root@#deep] strip /usr/lib/libldap.a
[root@#deep] strip /usr/lib/liblberd.a
[root@#deep] strip /usr/bin/in_xfingered
[root@#deep] strip /usr/bin/go500
[root@#deep] strip /usr/bin/go500gw
[root@#deep] strip /usr/bin/mld500
[root@#deep] strip /usr/bin/rp500
[root@#deep] strip /usr/bin/fax500
[root@#deep] strip /usr/bin/rcp500
[root@#deep] strip /usr/bin/libldap
[root@#deep] strip /usr/bin/ldif2dbm
[root@#deep] strip /usr/bin/ldif2xindex
[root@#deep] strip /usr/bin/ldif2dbchildren
[root@#deep] strip /usr/bin/ldbmcmat
[root@#deep] strip /usr/bin/ldif
[root@#deep] strip /usr/bin/onitpeede
[root@#deep] strip /usr/bin/dbmtest
[root@#deep] strip /usr/bin/slurped
[root@#deep] strip /usr/bin/uid
[root@#deep] strip /usr/bin/ldapadd
[root@#deep] strip /usr/bin/ldapsearch
[root@#deep] strip /usr/bin/ldapmodify
[root@#deep] strip /usr/bin/ldapmoddn
[root@#deep] strip /usr/bin/ldappasswd
[root@#deep] strip /usr/bin/ldapdelete
```

`install` 命令将在 `/var` 目录下创建一个名为 `"ldap"` 的新目录，并出于安全考虑，将其模式设置为仅超级用户 `"root"` 可读、可写和可执行（700）。

`strip` 命令将丢弃对象文件中所有的符号。这意味着二进制文件的尺寸会更小。这会稍微提高程序的性能，因为系统在执行二进制文件时需要读取的行会更少。

# 工作清理

```
[root@#deep] cd /var/tmp
[root@#deep] rm -rf openldap ld-version.tgz
```
