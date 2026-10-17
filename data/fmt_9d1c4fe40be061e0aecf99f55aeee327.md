
; domains = LDAP

[nss]

[pam]

### 示例 LDAP 域

; [domain/LDAP]

; id_provider = ldap

; auth_provider = ldap

```
[root@alpha ld]# cat /etc/sssd/sssd.conf
[domain/default]
autofs_provider = ldap
cache_credentials = True
ldap_search_base = ou-users,dc=linuxuxolics,dc=com
is_provider = ldap
auth_provider = ldap
chpass_provider = ldap
ldap_uri = ldap://alpha.linuxuxolics.com/
ldap_id_start_tls = True
ldap_tls_cacertdir = /etc/openldap/cacerts
[sssd]
config_file_version = 2
services = nss, pam
# 如果你不配置任何域，SSD 将不会启动。
# 将新的域配置作为 [domain/<NAME>] 部分添加，
# 然后将域列表（按照你希望查询的顺序）添加到下方的 "domains" 属性中并取消注释。
; domains = LDAP

[nss]
[pam]
```

```
[root@alpha ld]# ldadd -Y EXTERNAL -H ldapi:// -f /etc/openldap/schema/nis.ldif
SASL 认证开始
SASL用户名: gidNumber=0+uidNumber=0,cn=peercred,cn=external,cn=auth
SASL SSF: 0
正在添加新节点 "cn=nis,cn=schema,cn=config"
```

```
[root@alpha ld]# cat Gecko.ldif
dn: uid=Gecko,ou=users,dc=linuxolics,dc=com
uid: Gecko
cn: Gecko
objectClass: account
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword: suse
shadowLastChange: 10000
shadowMax: 99999
shadowWarning: 7
loginShell: /bin/bash
uidNumber: 1500
gidNumber: 500
homeDirectory: /home/Gecko
```

```
[root@alpha ld]# slpasswd
新密码:
重新输入新密码:
{SSHA}u4Ajfy93GpnHmheW7o+vqPoBmwrD970s
```

```
userPassword: {SSHA}u4Ajfy93GpnHmheW7o+vqPoBmwrD970s
```

```
[root@alpha ld]# ldapadd -f Gecko.ldif -x -D cn=admin,dc=linuxholics,dc=com
正在添加新节点 "uid=Gecko,ou=users,dc=linuxholics,dc=com"
```

## 第 3 章 与 PAM 和 NSS 的 LDAP 集成

abr 21 06:48:31 alpha.linuxaholics.com slapd[2788]: conn=1002 fd=27 ACCEPT fr...

..

..

我们还应该确保防火墙允许指向 OpenLDAP 服务器中 LDAP 和 LDAPS 端口的流量。

```
[root@alpha ~]# firewall-cmd --get-default-zone public
[root@alpha ~]# firewall-cmd --zone=public --list-services dhcpv6-client http ldap ldaps ssh
```

我们也可以从客户端客户端执行 `ldapsearch`。

```
[root@bravo ~]# ldapsearch -x ZZ -b dc=linuxaholics,dc=com "(uid=Gecko)"
```

```
# Gecko, users, linuxaholics.com
dn: uid=Gecko,ou=users,dc=linuxaholics,dc=com
uid: Gecko
cn: Gecko
objectClass: account
objectClass: posixAccount
objectClass: top
objectClass: shadowAccount
userPassword=: e1NTSEF9MjramJ1Y0VO0ZohmTjZCRzRoTFd1Whh1Kz1FUE41TVag
```

..

..

我们还可以通过查看 `/var/log/messages` 文件以及位于 `/var/log/sssd/` 文件夹下的 sssd 日志文件获取一些重要信息。

为了从日志文件中获取更多信息，我们可以停止 `sssd` 服务并手动启动它，添加参数来增加调试信息。

```
[root@alpha ~]# ssd -d10 -f
```

### 第 3 章 与 PAM 和 NSS 的 LDAP 集成

这是我们在 `/var/log/sssd/sssd_default.log` 文件可能看到的示例。

.
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_sys_connect_done]
(4): Executing START TLS
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_connect_done]
(3): START TLS result: Success(0), null)
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(6): calling ldap_search_ext with [objectclass*].
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [*]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [altServer]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [namingContexts]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [supportedControl]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [supportedExtension]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [supportedFeatures]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [supportedLDAPVersion]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [supportedASLMechanisms]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [defaultNamingContext]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
(7): Requesting attrs: [lastUSN]
(Fri Aug 7 01:00:23 2015) [sssd[be[default]]] [sdap_get_generic_step]
