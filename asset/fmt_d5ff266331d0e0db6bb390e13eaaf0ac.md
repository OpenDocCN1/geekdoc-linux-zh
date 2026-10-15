
`AllowOverwrite`

`</Directory>`

这些行告诉系统在根目录（`/`）下应用`AllowOverwrite`指令——换句话说，除非在子目录中有其他指令覆盖它。目录块定义了上下文，支持不同的指令集。表 24.1 总结了你可能想要调整的一些指令。不过这不是 `ProFTPpd`选项的完整列表。请咨询 `ProFTPpd`网站上的详情。

## 24.1 重要 PROFTPD 指令

| 指令 | 值 | 含义 |
|---|---|---|
| `ServerName` | 字符串 | 设置 `ProFTPd`在连接时交付的描述性名称。 |
| `ServerType` | `standalone`或`inetd` | 告诉 `ProFTPd`它是从 `SysV`或本地启动脚本（`standalone`）还是超级服务器（`inetd`）运行。 |
| `User` | 用户名 | `ProFTPd`使用的用户名。 |
| `Group` | 组名 | `ProFTPd`使用的组名。 |
| `AllowUser` | 用户列表 | 允许指定的用户访问目录。 |
| `DenyUser` | 用户列表 | 禁止指定的用户或用户访问目录。 |
| `UseFtpUsers` | `on`或`off` | 指定是否拒绝访问`/etc/ftusers`列出的用户。默认值为`on`，这是一个非常有用的安全措施。 |
| `UserAlias` | 两个用户名 | 告诉 `ProFTPd`接受第一个指定的用户名登录，就像是第二个指定的用户名一样。 |
| `RequireValidShell` | `on`或`off` | 指定用户账户是否需要有效的`shell`定义。 |
| `AllowOverwrite` | `on`或`off` | 允许用户覆盖现有文件，假设他们对目标目录有写入权限。 |
| `<Directory>` | 目录名称 | 开始适用于指定目录树的上下文。 |
| `<Anonymous>` | 目录名称 | 开始授予指定目录树匿名访问的上下文。`ProFTPpd`在此树内将其锁定在`chroot`监狱中。 |
| `<VirtualHost>` | 主机名或 IP 地址 | 开始一个上下文，允许`ProFTPpd`对与指定主机名或 IP 地址相关的网络接口做出不同的响应。 |

默认的`ProTPd`配置通常会启用身份验证登录，因此在计算机上拥有账户的个人可以使用该系统的 `FTP`服务器。如果你想启用匿名访问，可能需要添加一个类似下方的`<Anonymous>`指令块：

```
<Anonymous>
    /var/ftp
    User ftp
    Group ftp
    RequireValidShell off
    UserAliases anonymous ftp
</Anonymous>
```

此配置告诉系统接受使用`ftp`账户进行匿名登录，并以用户和组`ftp`运行。如果`/etc/passwd`中`ftp`用户的指定的`Shell`不在`/etc/ftpsusers`文件（该文件包含`ftp`用户）中列出，则你可能需要从`ftpsusers`文件中删除该条目。

一旦你更改了`ProTPd`配置，就必须重启服务器。这在第 22 章中有更详细的介绍。通常你使用`SysV`启动脚本选项如下：

```
# /etc/rc.init.d/proftpd restart
```

注意：如果你从超级服务器（super server）运行`ProTPd`，则在更改配置时不需要显式地重启它。如果你想启用或禁用`ProTPd`或更改在命令行上传递给它的选项，则必须重启服务器以重新加载其配置文件。

## vsftpd 配置

`vsftpd`服务器非常强大，但有时可能需要更简单的服务器。此类服务器至少提供了更高安全性和速度的潜力。`FTP`服务器因这些特性而迅速受到关注的是`vsftpd`，它适用于`Debian`、`Mandrake`、`Red Hat`和`SuSE`。

通常，`vsftpd`按照第 22 章描述的那样从超级服务器运行；但是，如果你愿意，它也可以作为`SysV`或本地启动脚本运行。`vsftpd`配置文件为`/etc/vsftpd.conf`。该文件包含以井号（`#`）开头的注释行，以及采用如下形式的指令行：

```
option=value
```
