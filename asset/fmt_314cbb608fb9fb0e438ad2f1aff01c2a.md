
```
root@charlie:~ # cd /usr/ports/
root@charlie:~/usr/ports # cd net/ldap24-client/
root@charlie:~/usr/ports/net/ldap24-client # make install
==> Building/installing dialog4ports as it is required for the config
==> Cleaning for dialog4ports-0.1.5_2
==> License BSD2CLAUSE accepted by the user
==> dialog4ports-0.1.5_2 depends on file: /usr/local/sbin/pkg - found
=> dialog4ports-0.1.5.tar.gz doesn't exist in /usr/ports/distfiles/
=> Attempting to fetch http://micro.me/dialog4ports/dialog4ports-0.1.5.tar.gz
```

我们选择带有 GSSAPI 支持的选项（图 3-5）。

![](img/dfa44432604022575079471b648e25ca_129_0.png)

图 3-5. 在 FreeBSD 中安装带有 GSSAPI 支持的 OpenLDAP 客户端

# 第 3 章 LDAP 与 PAM 和 NSS

为了让 LDAP 认证在 FreeBSD 上工作，我们还需要安装两个额外的端口：`security/pam_ldap` 和 `net/nss_ldap`。

```
root@charlie:/usr/ports/security/pam_ldap # make install
```

.

.

正在安装 `pam_ldap-1.8.6_3`...===========================================

将 `/usr/local/etc/ldap.conf.dist` 复制到 `/usr/local/etc/ldap.conf`，然后编辑 `/usr/local/etc/ldap.conf` 以使用该模块。在 4.X 版本中向 `/etc/pam.conf` 添加类似下所示的行，或在 5.X 及更高版本中创建 `/etc/pam.d/ldap` 并添加类似下所示的行：

```
login auth sufficient /usr/local/lib/pam_ldap.so
```

```
root@charlie:/usr/ports/net/nss_ldap # make install
```

.

.

正在安装 `nss_ldap-1.265_12`...========================================

`nss_ldap` 模块期望在以下路径找到其配置文件：

- LDAP 配置：`/usr/local/etc/nss_ldap.conf`
- LDAP 密钥（可选）：`/usr/local/etc/nss_ldap.secret`

在安装过程中，我们将会看到一个询问默认配置参数的窗口（图 3-6）。

![](img/dfa44432604022575079471b648e25ca_131_0.png)

图 3-6. 在 FreeBSD 中配置 `nss_ldap` 模块

我们的 FreeBSD 计算机已准备好对 OpenLDAP 服务器进行认证。我们只需要配置客户端，但在在此之前，我们将确保以 Gecko 用户身份执行 LDAP 查询。

```
root@charlie:~ # ldapsearch -H ldap://alpha.linuxolics.com -x -D "uid=Gecko,ou=users,dc=linuxolics,dc=com" -w suse -b "ou=users, dc=linuxolics,dc=com"
```

```
# Gecko, users, linuxolics.com
dn: uid=Gecko,ou=users,dc=linuxolics,dc=com
uid: Gecko
cn: Gecko
objectClass: account
objectClass: posixAccount
objectClass: top
```

`objectClass: shadowAccount`

如果查询没有返回正确的结果，我们应该再次检查防火墙设置、ACL、权限等。我们在书的前面的部分已经介绍过这些步骤。OpenLDAP 客户端期望在 `/usr/local/etc/ldap.conf` 文件中找到其配置。最初，该文件不存在，但我们可以复制 `/usr/local/etc/ldap.conf.dist` 文件并将其重命名作为起点。

```
root@charlie:~ # cp /usr/local/etc/ldap.conf.dist /usr/local/etc/ldap.conf
```

大部分大部分条目都被注释了，但这两个参数没有：

```
host 127.0.0.1
base dc=padl,dc=com
```

显然，我们需要相应地更改这些值。

```
host alpha.linuxaholics.com
base ou=users,dc=linuxaholics,dc=com
```

我们还必须编辑 `/usr/local/etc/nss_ldap.conf` 文件，它对 `host` 和 `base` 参数具有相同的默认值。

```
root@:~ # cat /usr/local/etc/nss_ldap.conf
# @(@#)$Id: ldap.conf,v 2.49 2009/04/25 01:53:15 lukeh Exp E
#
```

```
# 这是 LDAP 命名服务的配置文件
# 切换库和 LDAP PAM 模块。
```

```
# 网络或连接超时（参见 bind_timimit）。
host alpha.linuxaholics.com
```

```
# 搜索基准的区分名称。
base ou=users,dc=linuxaholics,dc=com
```

此外，我们还需要告诉 NSS 在搜索有效用户时使用 LDAP。`/etc/nsswitch.conf` 原始内容如下：

```
nsswitch.conf(5) - name switch file
# FreeBSD - releng/11.0/etc/nsswitch.conf 2016-06-09 01:28
group: compat
group_compat: nis
hosts: dns
netgroup: compat
passwd: compat
passwd_compat: nis
shells: files
services: compat
services_compat: nis
rpc: files
```

我们更改了 `passwd` 和 `group` 参数，使新文件看起来像这样：

```
nsswitch.conf(5) - name switch file
# FreeBSD - releng/11.0/etc/nsswitch.conf 2016-06-09 01:28
group: files
group_compat: nis
hosts: dns
netgroup: files
passwd: files
passwd_compat: nis
shells: files
services:: files
services_compat: nis
rpc: files
```

现在，FreeBSD 计算机能够使用 LDAP 认证进行工作了。我们可以检查一下。

## 与 PAM 和 NSS 的 LDAP 集成

系统配置完成后，我们可以获取 LDAP 用户列表。

```
root@delta:~# ldaplist
dn: cn=Tux,ou=users,dc=linuxaholics,dc=com
dn: cn=scientists,ou=users,dc=linuxaholics,dc=com
uid: uid=Antonio,ou=users,dc=linuxaholics,dc=com
uid: uid=webmaster,ou=users,dc=linuxaholics,dc=com
uid: uid=Gecko,ou=users,dc=linuxaholics,dc=com
```

我们几乎已经完成了，但仍然需要编辑 `/etc/pam.d/login` 文件，包含 `auth required pam_ldap.so.1` 行，并注释掉 `auth required pam_unix_auth.so.1` 这一行。
