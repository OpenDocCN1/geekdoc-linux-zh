

of an NTP problem. 默认的 realm 设置为 AD 域，并且密钥分发中心，即 KDC，已配置为 AD 域控制器。**krb5.log** 在调试时可能会派上用场。

通过运行 **kinit** 命令向 Active Directory 控制器请求票据。指定一个有效的域用户账户。“administrator” 通常是一个不错的测试账户，但任何账户都可以。当提示时，输入域密码。

```
ubuntu$ kinit administrator@ULSAH.COM
Password for administrator@ULSAH.COM: <password>
```

使用 **klist** 显示 Kerberos 票据：

```
ubuntu$ klist
Ticket cache: FILE:/tmp/krb5cc_1000
Default principal: administrator@ULSAH.COM

Valid starting       Expires              Service principal
10/11/09 13:40:19    10/11/09 23:40:21    krbtgt/ULSAH.COM@ULSAH.COM
renew until 10/12/09 13:40:19

Kerberos 4 ticket cache: /tmp/tkt1000
klist: You have no tickets cached
```

如果显示了票据，则表示身份验证成功并且你已正确配置了 Kerberos。在这种情况下，票据有效期为 10 小时，并且可以续期 24 小时。 （你可以使用 **kdestroy** 命令使票据失效。）

有关其他配置选项，请参阅 **krb5.conf** 的 man 手册。

## Samba 作为 Active Directory 域成员

与其它 Samba 组件一样，**winbind** 在 **smb.conf** 文件中进行配置。使用 security = ads 选项将 Samba 配置为 AD 域成员。

下面复现了一个可用的配置。我们设置了 Kerberos realm 并将 Samba 身份验证指向域控制器。我们还使用 **smb.conf** 的 idmap 选项设置了用户身份映射。请注意，**smb.conf** 中各个共享的配置与 AD 身份验证服务的配置是分开的；此处仅显示域身份验证。

```ini
[global]
    security = ads
    realm = ULSAH.COM
    password server = 192.168.7.120
    workgroup = ULSAH
    winbind separator = +
    idmap uid = 10000-20000
    idmap gid = 10000-20000
    winbind enum users = yes
    winbind enum groups = yes
    template homedir = /home/%D/%U
    template shell = /bin/bash
```

```
client use spnego = yes
client ntlmv2 auth = yes
encrypt passwords = yes
winbind use default domain = yes
restrict anonymous = 2
```

这里的大多数选项都很直观，但请参阅 **man smb.conf** 了解详情。

特别值得注意的是 winbind use default domain 选项。如果你使用多个 AD 域，此值应为 no。但是，如果你只使用一个域，将此值设置为 yes 就可以在身份验证时省略域（例如，你可以使用“ben”而不是“ULSAH\\ben”）。此外，winbind separator 值指定了在输入用户名时反斜杠的替代字符。workgroup 值应为域的短名称。像 linux.ulsah.com 这样的域将使用 LINUX 作为 workgroup 值。

配置 Samba 后，重新启动 Samba 和 **winbind** 服务以使这些新设置生效。

现在是时候将系统加入域了；使用 Samba 提供的 **net** 工具，其语法借鉴自同名的 Windows 命令。**net** 接受多种与 Windows 通信的协议。我们使用 ads 选项来定位 Active Directory。

确保票据存在，运行 **klist** （如果不存在则使用 **kinit** 请求一个），然后使用以下命令加入域：

```
ubuntu$ sudo net ads join -S DC.ULSAH.COM  -U administrator
Enter administrator's password: <password>
Using short domain name -- ULSAH
Joined 'UBUNTU' to realm 'ulsah.com'
```

我们在命令行中指定了一个 AD 服务器 dc.ulsah.com（并非严格必要）以及 administrator 账户。默认情况下，AD 将新系统添加到域层次结构中的 Computer 组织单元。如果系统出现在 Windows 的 AD Users and Computers 工具中的 Computers OU 中，则域加入操作成功。你也可以使用 **net ads status** 命令检查系统状态。有关更多选项，包括 LDAP 搜索操作，请参阅 **net man** 手册页。

名称服务切换配置很简单。系统的 **passwd** 和 **group** 文件应始终首先被查阅，但随后你可以通过 **winbind** 转到 Active Directory。**nsswitch.conf** 中的以下条目即可实现：

```
passwd:   compat winbind
group:    compat winbind
shadow:   compat winbind
```

配置完 NSS 后，你可以使用 **wbinfo** 命令测试 AD 用户和组的解析。使用 **wbinfo -u** 查看域的用户列表和

