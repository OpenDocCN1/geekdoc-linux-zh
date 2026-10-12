
| 有效起始时间 | 过期 服务主体 |
| :--- | :--- | :--- |
| 21/04/17 17:35:02 | 22/04/17 17:35:02 | krbtgt/EXAMPLE.COM@EXAMPLE.COM |

`-bash-4.2$`

### 配置自定义 Realm

另一方面，我们可能想使用自定义的 Kerberos realm。如果是这样，我们需要使用 `kdb5_util` 命令创建它：

```bash
[root@alpha ~]# kdb5_util create -s -r LINUXAHOLICS.COM -d /var/kerberos/krb5kdc/linuxholics

Loading random data

Initializing database '/var/kerberos/krb5kdc/linuxholics' for realm 'LINUXAHOLICS.COM'

You will be prompted for the Database.

Enter KDC master key:

Re-enter KDC master key to verify:
```

我们需要通过 `-d` 指定 realm 数据库的位置，通过 `-r` 指定 realm 的名称。还需要编辑 Kerberos 配置，打开 `/etc/krb5.conf` 文件并在 `EXAMPLE.COM` 下添加一个新的 realm。

```ini
[realms]

EXAMPLE.COM = {
kdc = alpha.linuxaholics.com
admin_server = alpha.linuxaholics.com
}

LINUXAHOLICS.COM = {
kdc = alpha.linuxaholics.com
admin_server = alpha.linuxaholics.com
database_name = /var/kerberos/krb5kdc/linuxholics
}
```

如果我们查看 `krb5.conf` 的 man 页面，会发现文件中包含许多参数。其中一个参数是 `database_name`，它决定了数据库的位置。对于 `EXAMPLE.COM` realm，该参数的默认值是 `/var/kerberos/krb5kdc/principal`，因此当使用 `EXAMPLE.COM` 时不需要显式包含它。然而，现在我们使用的是位于不同路径的 `LINUXAHOLICS` realm，必须包含此参数。

我们还在 `domain_realm` 部分添加以下行：

```ini
linuxaholics.com = LINUXAHOLICS.COM
.linuxaholics.com = LINUXAHOLICS.COM
```

我们将新 realm 设置为默认：

```ini
default_realm = LINUXAHOLICS.COM
```

最后，文件将如下（配置片段也可以放在 `/etc/krb5.conf` 目录下）：

```ini
[logging]
default = /var/log/krb5.log
kdc = /var/log/krb5kdc.log
admin_server = /var/log/kadmind.log

[libdefaults]
dns_lookup = false
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
rdns = false
default_realm = LINUXAHOLICS.COM
default_ccache_name = KEYRING:persistent:%u

[realms]
EXAMPLE.COM = {
kdc = alpha.linuxaholics.com
admin_server = alpha.linuxaholics.com
}

LINUXAHOLICS.COM = {
kdc = alpha.linuxaholics.com
admin_server = alpha.linuxaholics.com
database_name = /var/kerberos/krb5kdc/linuxaholics
}
```

```ini
[domain_realm]
.example.com = EXAMPLE.COM
example.com = EXAMPLE.COM
linuxaholics.com = LINUXAHOLICS.COM
.linuxaholics.com = LINUXAHOLICS.COM
```

我们还需要编辑 `/var/kerberos/krb5kdc/kdc.conf` 文件以包含新的 realm。

```ini
[kdcdefaults]
kdc_ports = 88
kdc_tcp_ports = 88
```

```ini
[realms]
EXAMPLE.COM = {
#master_key_type = aes256-cts
acl_file = /var/kerberos/krb5kdc/kadm5.acl
dict_file = /usr/share/dict/words
admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
supported_encypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal camellia256-cts:normal camellia128-cts:normal des-hmac-sha1:normal des-cbc-md5:normal des-cbc-crc:normal
}

LINUXAHOLICS.COM = {
#master_key_type = aes256-cts
acl_file = /var/kerberos/krb5kdc/kadm5.acl
dict_file = /usr/share/dict/words
admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab
supported_encypes = aes256-cts:normal aes128-cts:normal des3-hmac-sha1:normal arcfour-hmac:normal camellia256-cts:normal camellia128-cts:normal des-hmac-sha1:normal des-cbc-md5:normal des-cbc-crc:normal
}
```

我们像之前那样重启 `krb5kdc` 和 `kadmin` 服务。之后，我们就可以准备使用 `kadmin` 命令管理 Kerberos 了。

```bash
[root@alpha ~]# kadmin.local
```

使用密码以主体 `root/admin/LINUXAHOLICS.COM` 的身份进行验证。`kadmin.local:` 

由于更改了 `/etc/krb5.conf` 文件中的默认 realm，我们不需要指定要连接到哪个 realm。否则，我们需要像下面的示例一样使用 `-d` 和 `-r` 参数：

```bash
[root@alpha ~]# kadmin.local -r LINUXAHOLICS.COM -d /var/kerberos/krb5kdc/linuxaholics
```

我们可以列出主体。

```bash
kadmin.local: listprinces
Gecko@LINUXAHOLICS.COM
K/M@LINUXAHOLICS.COM
kadmin/admin@LINUXAHOLICS.COM
kadmin/alpha.linuxaholics.com@LINUXAHOLICS.COM
kadmin/changepw@LINUXAHOLICS.COM
krop/alpha.linuxaholics.com@LINUXAHOLICS.COM
krbtgt@LINUXAHOLICS.COM
```

我们可以添加新的主体。

```bash
kadmin.local: addprincince Gecko
WARNING: no policy specified for Gecko@LINUXAHOLICS.COM; defaulting to no policy
```
