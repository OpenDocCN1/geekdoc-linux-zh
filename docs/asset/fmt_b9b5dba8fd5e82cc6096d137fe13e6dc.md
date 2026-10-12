
现在我们编辑 `/etc/sysconfig/slapd` 文件，向 `SLAPD_URLS` 中添加 `ldaps:///`：

```bash
SLAPD_URLS="ldap:/// ldaps:///"
```

然后我们重启服务。

```bash
[root@alpha alpha]# systemctl restart slapd
```

如果查询查询 LDAP，我们将看到条目已经发生了更改。

```bash
[root@alpha alpha]# slapcat -b "cn=schema,cn=config" | less
dn: cn=config
objectClass: olcGlobal
cn: config
olcArgsFile: /var/run/openldap/slapd.args
olcPidFile: /var/run/openldap/slapd.pid
structuralObjectClass: olcGlobal
entryUUID: 42310ode-8e3f-1036-840d-f3757e7c29
creatorsName: cn=config
createTimestamp: 20170223181136Z
olcTLSCertificateFile: /etc/openldap/certs/alpha.linuxaholics.com.crt
olcTLSCertificateKeyFile: /etc/openldap/certs/alpha.linuxaholics.com.key
olcTLSCACertificateFile: /etc/openldap/cacerts/ca.cert.pem
olcTLSCACertificatePath: /etc/openldap/cacerts
```

当我们与 LDAP 服务器建立客户端连接时，ldap 假设我们正在使用 `/etc/openldap/ldap.conf` 文件中指定的参数。默认情况下，这是该文件的原始内容：

```conf
#
### LDAP 默认值
#
### 详情见 ldap.conf(5)
# 此文件应该是可读的，但不能对 world 可写。

#BASE dc=example,dc=com
#URI ldap://ldap.example.com ldap://ldap-master.example.com:666

#SIZELIMIT 12
#TIMELIMIT 15
#DEREF never

TLS_CACERTDIR /etc/openldap/certs

# 关闭此项会破坏 rdn = false 时使用 krb5 的 GSSAPI
SASL_NOCANON
```

我们可以在此文件中指定多个选项，正如在手册页中看到的。以下是一些常用选项：

- `URI`: 正如其名，该选项指定要连接的 LDAP 服务器的 URI。
- `BASE`: 定义后，所有搜索将使用此默认 DN 执行。
- `TIMEOUT`: 一旦超过此阈值且没有响应，查询将终止。
- `PORT`: 指定要连接的端口。
- `TLS_CACERTDIR`: 这是包含证书的路径。
- `TLS_REQCERT`: 该选项根据分配的值指定如何处理证书：
  - `never`: 客户端永远不会请求服务器证书。
  - `allow`: 客户端请求服务器证书，但如果没有提供有效的证书，会话将正常继续。
  - `try`: 客户端请求证书。如果呈现了错误的证书，会话将立即终止。
  - `demand|hard`: 这些选项等同于 try。这是默认设置。

然而，在带有适当参数执行 `ldapsearch` 时，这些选项可以被覆盖。在我们的案例中，我们必须将 `TLS_CACERTDIR` 参数的值改为 `/etc/openldap/certs`。

```conf
#
# # LDAP 默认值
#
### 详情见 ldap.conf(5)
# 此文件应该是 world 可读的，但不能对 world 可写。

#BASE dc=example.com,dc=com
#URI ldap://ldap.example.com ld://ldap-master.example.com:666

#SIZELIMIT 12
#TIMELIMIT 15

TLS_CACERTDIR /etc/openldap/certs

# 关闭此项会破坏 rdn = false 时使用 krb5 的 GSSAPI
```

正如我们看到的，端口被过滤了，因此我们需要在 OpenLDAP 服务器的防火墙中允许流量。在防火墙中允许这些入站连接简单的方法如下：

```
[root@alpha ~]# firewall-cmd --add-service=ldap
success
[root@alpha ~]# firewall-cmd --add-service=ldaps
success
```

这些更改将立即生效，但为了让它们永久生效，我们需要使用 `--permanent` 参数运行相同的两条命令。

```
[root@alpha ~]# firewall-cmd --permanent --add-service=ldap
success
[root@alpha ~]# firewall-cmd --permanent --add-service=ldaps
success
```

我们将能够从客户端计算机进行连接。

```
[root@bravo ~]# ldapsearch -x -H ldap://alpha.linuxaholics.com -b dc=linuxaholics,dc=com
# extended LDIF
#
# LDAPv3
# base <dc=linuxaholics,dc=com> with scope subtree
# filter: (objectclass=*)
# requesting: ALL
#
```

## 第 2 章 目录安全

linuxaholics.com
dn: dc=linuxaholics,dc=com
objectClass: dc0Object

我们已经从另一台计算机建立了 LDAP 连接。然而，如果我们想通过使用 LDAPS 进行安全连接，仍然需要一些额外的工作。目前，防火墙允许到 636 TCP 端口的入站连接，但客户端计算机并不信任服务器使用的证书。

```
[root@bravo ~]# ldapsearch -x -ZZ -H ldap://alpha.linuxaholics.com -b dc=linuxaholics,dc=com
ldap_start_tls: Connection error (-11)
```

附加信息：TLS error -8172: 证书颁发者已被用户标记为不可信。

正如我们之前看到的，系统系统将在 `TLS_CACERTDIR` 参数指定的文件夹中搜索 CA 证书，该参数在客户端计算机的 `/etc/openldap/ldap.conf` 中定义。

```
[root@bravo ~]# cat /etc/openldap/ldap.conf
#
### LDAP Defaults
#
```
### 详情见 ldap.conf(5)
# 此文件应该是全局可读但非全局可写的。
```
#BASE dc=example,dc=com
#URI ldap://ldap.example.com ldap://ldap-master.example.com:666
#SIZELIMIT 12
#TIMELIMIT 15
#DEREF
ever
```
TLS_CACERTDIR /etc/openldap/certs
```
# 关闭此项会导致在 rdns = false 时 kerbd 使用 GSSAPI 效
SASL_NOCANON on
```

在之前的章节中，当我们保护 LDAP 服务器的 LDAP 连接时，我们创建了 `/etc/openldap/cacerts` 来存放 CA 证书。为了保持一致，我们将在客户端上执行相同的操作。稍后我们将修改 `/etc/openldap/ldap.conf` 文件：

```
[root@bravo ~]# cat /etc/openldap/ldap.conf
```
TLS_CACERTDIR /etc/openldap/cacerts
```

我们将 CA 证书从服务器复制到客户端，并执行 `cacertdir_rehash`。

```
[root@bravo ~]# mkdir /etc/openldap/cacerts
[root@bravo ~]# scp root@alpha.linuxaholics.com:/etc/openldap/cacerts/ca.cert.pem /etc/openldap/cacerts
```
