
在 RHEL 上，使用一种名为 OpenLDAP 的开源 LDAP 实现来提供服务器和客户端功能。关键配置文件是 `/etc/ldap.conf` 和 `/etc/openldap/ldap.conf`，前者包含 PAM NSS LDAP 模块信息，后者持有默认 LDAP 配置。

## LDAP 术语

为了彻底理解 LDAP，掌握以下关键术语至关重要。

### 目录 (Directory)

LDAP 目录又称为目录信息树 (DIT)，类似于一个特殊的数据库，存储关于人员、个人资料、打印机和服务器等对象的信息。它以某种方式组织信息，使得查找和检索所需信息变得更加容易。它列出了对象及其详细信息。LDAP 目录在概念上类似于 Linux/UNIX 目录层次结构。

### 条目 (Entry)

条目是 LDAP 目录的构建块，代表其中的一条特定记录。换句话说，条目是一个由对象的一个或多个属性组成的信息集合。例如，在 LDAP 目录中，`jobTitle` 属性的值可能包含员工、打印机和服务器的条目。

### 属性 (Attribute)

属性包含两部分信息——属性类型和属性值——并与一个或多个条目关联。属性类型代表该属性包含的信息类型。属性值是该条目中特定信息。例如，`jobTitle` 属性类型可以是“director”。表 23-1 列出了一些常见的属性类型。

| 属性类型 | 说明 |
|---|---|
| CommonName (cn) | 条目的通用名称，例如 cn=John Doe |
| DomainComponent (dc) | DNS 组件的区分名称 (DN)，如 dc=ca, dc=abc, dc=com。 |
| Country (c) | 国家，如 c=ca。 |
| Mail (mail) | 电子邮件地址。 |
| Organization (o) | 组织名称，如 o=abc。 |
| OrganizationalUnit (ou) | 组织内单元的名称，如 ou=Printers。 |
| Owner (owner) | 条目的所有者，如 cn=John Doe, ou=Printers, dc=abc, c=ca。 |
| Surname (sn) | 人的姓，如 Doe。 |
| TelephoneNumber (telephoneNumber) | 电话号码，如 (123) 456-7890 或 1234567890。 |

表 23-1 常见 LDAP 属性类型

全名和对应的缩写可以互换。

![](img/3f35ec29a294974bc1a4fdae3ae46652_519_0.png)

### 匹配规则 (Matching Rule)

匹配规则在搜索比较任务中，将寻求的属性值与目录中存储的属性值进行匹配。

例如，与 `telephoneNumber` 属性关联的匹配规则可能导致“(123) 456-7890”匹配“(123) 456-7890”或“1234567890”，或者两者都是。在定义属性时，会与该属性关联一个匹配规则。

### 对象类 (Object Class)

每个条目属于一个或多个对象类。对象类是一组必需和可选属性，定义了条目的结构。

例如，`organizationalUser` 类可能包含 `commonName` 和 `Surname` 作为必需属性，并将 `telephoneNumber`、`UID`、`streetAddress` 和 `password` 作为可选属性。在定义条目时，必须定义最少必需属性。

### 模式 (Schema)

`schema` 是属性和对象类的集合，并带有匹配规则、语法和其他相关信息。

## LDAP 数据交换格式 (LDIF)

LDAP 数据交换格式 (LDIF) 是一种用于在 LDAP 服务器之间导入和导出 LDAP 记录的特殊格式。数据采用文本格式，由条目或对条目的更改或两者的组合组成。

每条记录表示为一组属性，每个属性单独占一行，由“name:value”对组成。以下是一个带有代表 LDIF 中记录的属性的示例目录条目：

```
dn: John Doe,ou=People,c=ca,dc=ca
objectClass: inetMailRecipient
sn: Doe
mail: john.doe@abc.com
cn: John
givenName: John
uid: jdoe
telephoneNumber: (416) 123-4567
```

## 区分名称与相对区分名称

区分名称 (`DN`) 唯一地标识整个目录树中的条目。它在概念上类似于 Linux 层次结构中的绝对路径。

相比之下，相对区分名称 (`RDN`) 代表 `DN` 的各个组成部分。

例如，位于加拿大的打印机的 `DN` 为：在这个示例中，prn1 的 `RDN` 是 `cn=prn1`。同样，打印机的 `RDN` 是 `ou=Printers`，加拿大的 `c=ca`，dc 是 `dc=abc`。因此 `DN` 是由逗号分隔的 `RDN` 序列。

## LDAP 角色

LDAP 环境中的系统可以承担四种角色——服务器、副本、客户端和引用。一个系统可以配置执行多个角色。

### LDAP 服务器

LDAP 服务器是持有 LDAP 目录信息的系统。它可以被称为主 LDAP 服务器。必须配置这样一个服务器来提供目录服务。

### LDAP 副本

LDAP 副本是包含 LDAP 服务器维护的信息副本的系统。副本可以被称为从 LDAP 服务器。建议与 LDAP 服务器一起配置至少一个副本，以增强可用性和负载均衡。

### LDAP 客户端

LDAP 客户端是与服务器或副本绑定以建立会话、对目录目执行查询并进行必要修改的系统。

### LDAP 引用

LDAP 引用是服务器上的一个实体，当它不包含请求的信息时，会将客户端请求重定向到其他 LDAP 服务器或副本。引用包含可能找到请求信息的 LDAP 服务器的名称和位置。

## 配置 LDAP 客户端

LDAP 客户端可以在命令行配置，也可以使用身份验证器进行配置。两种方法将在后续章节中讨论。

### 在命令行配置 LDAP 客户端

要将如 `rhel03` 的系统配置为 LDAP 服务器 `rhel04` 的客户端，请在 `rhel03` 上执行以下操作：

- 确保安装了以下软件包以便 LDAP 客户端功能正常工作：

```
# rpm -qa | grep ldap
openldap-2.3.27-8
openldap-clients-2.3.27-8
nss_ldap-253-5.el5
```

2. 编辑 `/etc/ldap.conf` 文件并按所示插入项：

```
# vi /etc/ldap.conf
host 192.168.0.204      # ldap server IP address
base dc=abc,dc=com         # defines the default DN
ssl start_tls               # encrypts passwords while in transit
pam_password md5 # Use md5 PAM password management
```

3. 编辑 `/etc/ldap.conf` 文件并按所示插入项：

```
# vi /etc/openldap/ldap.conf
URI ldap://192.168.0.204   # ldap server
BASE dc=abc,dc=com         # sets base DN
```

4. 编辑 `/etc/sysconfig/authconfig` 文件并将 `USELDAP` 和 `USELDAPAUTH` 指令设为 yes：

```
# vi /etc/sysconfig/authconfig
USELDAP=yes
USELDAPAUTH=yes
```

5. 编辑 `/etc/nsswitch.conf` 文件并确保在 LDAP 中首先引用认证：

```
# vi /etc/nsswitch.conf
asswd:      ldap files
shadow:     ldap files
group:      ldap files
```

6. 编辑 `/etc/pam.d/system-auth-ac` 文件并追加以下行，将所有认证请求定向到 LDAP 服务器处理：

```
# vi /etc/pam.d/system-auth-ac
auth sufficient pam_ldap.so use_first_pass
account [default=bad success=ok user_unknown=ignore] pam_ldap.so
password sufficient pam_ldap.so use_authtok
session optional pam_ldap.so
```

7. 运行以下命令启用 LDAP 客户端程序在每次系统重启时自动启动：

```
# chkconfig ldap on
```

8. 启动 LDAP 客户端服务：
