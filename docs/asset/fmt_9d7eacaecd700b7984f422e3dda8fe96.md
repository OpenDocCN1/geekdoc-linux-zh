
```
root@delta:~# cat /etc/pam.d/login
#
# Copyright (c) 2012, Oracle and/or its affiliates. All rights reserved.
#
# PAM configuration
#
# login service (explicit because of pam_dial,auth)
auth definitive pam_user_policy.so.1
auth requisite pam_authtok_get.so.1
auth required pam_dhkeys.so.1
#auth required pam_unix_auth.so.1
auth required pam_unix_cred.so.1
auth required pam_dial_auth.so.1
auth required pam_ldap.so.1
```

我们可以使用 `getent` 工具来检查我们的 Solaris 是否将 Gecko 识别为有效用户。

```
root@delta:~# getent passwd Gecko
Gecko:x:1500:500:/home/Gecko:/bin/bash
```

从现在起，我们可以登录 Solaris 计算机的物理控制台（图 3-7）。

```
delta vt1 login: Gecko
Password:
Last login: Mon Feb 26 01:08:35 2018 on vt/2
No directory! Logging in with home=/
Oracle Corporation SunOS 5.11 11.3 September 2018
-bash-4.1# 09
```

> 图 3-7. 使用 LDAP 用户登录 Solaris

### 总结

在本章中，我们学习了如何使用 OpenLDAP 服务器验证来自不同 Linux 和 Unix 计算机的用户身份。我们研究了 PAM 和 NSS 的基础知识，以及如何配置客户端和服务器以拥有集中式认证服务器。我们还练习了一些故障排除技巧，这些将在书的其余部分非常有帮助。

# 第 4 章

# 将 LDAP 与 Active Directory 和 Kerberos 集成

在当今的异构网络中，网络中使用不同的操作系统越来越常见。在这种环境中，集成不同的系统可能是一个真正的挑战。幸运的是，有很多解决方案允许不同的系统有效地协作工作。

在本章中，我们将涵盖以下概念：

- Kerberos 与 LDAP 的集成。
- 跨平台认证。
- 单点登录概念。
- OpenLDAP 与 Active Directory 的集成。

我们将探索以下术语和工具：Kerberos、Active Directory、单点登录和 DNS。

### Kerberos

Kerberos 是一种计算机网络认证协议，提供安全的认证机制。它通过使用票证（tickets）工作。客户端向认证服务器（AS），服务器将请求转发到密钥分发中心（KDC）。KDC 随后颁发票证get证（TGT），如图 4-1 所示。

![](img/dfa44432604022575079471b648e25ca_140_0.png)

**图 4-1.** Kerberos 认证：获取 TGT

当客户端需要访问不同节点（或 Kerberos 术语中的主体）中的服务时，它将 TGT 和请求的服务的 ID 发送给票证颁发服务器（TGS），TGS 通常也是 KDC。然后 KDC 向客户端发送一个服务访问票证，该票证可用于访问该服务（图 4-2）。

![](img/dfa44432604022575079471b648e25ca_141_0.png)

**图 4-2.** Kerberos 认证：使用 TGS 访问服务

### 在 CentOS 上安装 Kerberos

在 CentOS 中安装 Kerberos 服务器非常简单。我们只需要安装 `krb5-server` 包，但我们还将安装包含在 `krb5-workstation` 包中的客户端工具。

```
[root@alpha ~]# yum install -y krb5-server
```

```
[root@alpha ~]# yum install -y krb5-workstation
```

## 第 4 章 将 LDAP 与 ACTIVE DIRECT AND KERBEROS 集成

默认的 Kerberos 配置文件是 `/etc/krb5.conf`。在全新安装后，文件的内容类似于：

```
[root@alpha ~]# cat /etc/krb5.conf
# Configuration snippets may be placed in this directory as well
includedir /etc/krb5.conf/

[logging]
default = FILE:/var/log/krb5libs.log
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/kadmind.log

[libdefaults]
dns_lookup_realm = false
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
rdns = false
default_realm = EXAMPLE.COM
default_ccache_name = KEYRING

[realms]
```

KDC 的配置文件是 `/etc/krb5.conf`。这是全新安装后的内容：

```
[root@alpha ~]# cat /etc/krb5.conf
# Configuration snippets may be placed in this directory as well
includedir /etc/krb5.conf/

[logging]
default = FILE:/var/log/krb5libs.log
kdc = FILE:/var/log/krb5kdc.log
admin_server = FILE:/var/log/kadmind.log

[libdefaults]
dns_lookup_realm = false
ticket_lifetime = 24h
renew_lifetime = 7d
forwardable = true
rdns = false
default_realm = EXAMPLE.COM
default_ccache_name = KEYRING

[realms]
```

KDC 的配置文件是 `/etc/krb5/kdc.conf`。默认内容如下：

```
[root@alpha ~]# cat /etc/krb5/kdc.conf
[kdc]
kdc_ports = 88
kdc_tcp_ports = 88

[realms]
```

```
[root@alpha ~]# systemctl enable krb5server
```

```
[root@alpha ~]# systemctl start krb5server
```

```
[root@alpha ~]# systemctl enable krb5workstation
```

```
[root@alpha ~]# systemctl start krb5workstation
```

```
[root@alpha ~]#
 kadmin
```

```
[root@alpha ~]# systemctl start kadmin
```

## 配置 EXAMPLE.COM Realm

验证 Kerberos 工作的简单证明是使用 EXAMPLE.COM realm，它预配置在配置文件中。我们只需要对 KDC 和管理员服务器进行细微调整，因此我们需要编辑以下行：

```
[root@alpha ~]#
```

因此，新的配置文件将如下所示：

```
[root@alpha ~]# cat /etc/krb5.conf
```

```
[realms]
EXAMPLE.COM = {
```

```
[domain_realm]
example.com = EXAMPLE.COM
```

当然，我们需要在防火墙中开放相应的端口。

```
[root@alpha ~]# firewall-cmd --add-service=kerberos
success
[root@alpha ~]# firewall-cmd --permanent --add-service=kerberos
success
```

我们使用 `kadmin.local` 来管理 Kerberos。

```
[root@alpha ~]# kadmin.local
Authenticating as principal root/admin@EXAMPLE.COM with password.
kadmin.local:
```
