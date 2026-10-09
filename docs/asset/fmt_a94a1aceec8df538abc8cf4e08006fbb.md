
```bash
$ LDDFLAGS="-L/opt/lib -lc" \
CPPFLAGS="-I/opt/include -D_LINUX_SOURCE_COMPAT -DPAM_EXTERN" \
./configure --with-ldap-lib=openldap \
--with-ldap-config-file=/etc/ldap.conf --enable-ssl
```

这条长命令为编译配置源码。然而，你需要在 `Makefile` 中进行几处更改：

* 在 `pam_ldap_LDFLAGS` 定义中添加 `-L/opt/lib`
* 将所有的 `-g root` 改为 `-g system`

创建包含以下内容的 `exports.aix` 文件（它是 `exports.linux` 的拷贝）：

* `pam_sm_authenticate`
* `pam_sm_acct_mgmt`
* `pam_sm_setcred`
* `pam_sm_open_session`
* `pam_sm_close_session`
* `pam_sm_chautok`

现在我们可以继续编译并链接模块：

```bash
$ gmake
...
```

在安装模块之前，我们建议对任何 `/etc/ldap.conf` 文件进行备份。尽管我们指定了另一个名称，安装过程可能仍会将配置文件到 `/etc/ldap.conf`：

```bash
$ su
# cp -p /etc/ldap.conf /etc/ldap.conf.bak
# gmake install
/bin/sh -mkinstalldirs /lib -c root -g system pam_ldap.so /lib/security/pam_ldap.so.1
(cd /lib/security; rm -f pam_ldap.so; ln -s pam_ldap.so.1 pam_ldap.so)
test ! -f /etc/ldap.conf; then
  /bin/sh -mkinstalldirs /etc;
  /install-sh -c -m 644 -o root -g system ./ldap.conf /etc/ldap.conf;
fi
```

注意在编写本红皮书时，`AIX` 不支持 `pam_ldap` 模块。新版本的配置过程可能会更好。

我们在源码目录中还找到了 PAM 配置文件（`pam.conf`）。当然，在没有大量修改的情况下无法使用，但查看其内容可能有所帮助。`pam_ldap` 自身的配置与 Linux 系统基本相同。因此，我们将其推迟到下一章，在其中我们将讨论目录服务的使用。

如你所见，在 `AIX` 上编译 PAM 模块相当复杂，因为 `AIX` 的 PAM 支持是全新的。然而，我们希望在不久未来发生变化。

## 配置 PAM 模块

PAM LDAP 模块安装在 `/usr/lib/security/pam_ldap.so`。我们在示例 1-6 中展示了 `/etc/pam.conf` 的片段以及 PAM LDAP 模块自身的配置 `/etc/pam_ldap.conf`。

**示例 1-6 在 AIX 上使用 PAM LDAP 模块**

```conf
/etc/pam.conf:
sshd auth sufficient /usr/lib/security/pam_ldap.so
sshd auth required /usr/lib/security/pam_aix
sshd account sufficient /usr/lib/security/pam_ldap.so
sshd account required /usr/lib/security/pam_aix
sshd password required /usr/lib/security/pam_ldap.so
sshd session required /usr/lib/security/pam_aix
```

```conf
/etc/pam_ldap.conf:
host r-1linux.example.com
base dc=example,dc=com
```

在这个示例中，`sshd` 守护进程利用 LDAP 和 `AIX` 安全子系统。然而，后者仅在 LDAP 失败时才会被使用。这样我们既支持本地用户，也支持目录中定义的用户。

关于 LDAP 的更多细节，请参见第 2 章“集中化用户管理”。

> **注意**：如果你在 `AIX` 上使用 PAM，应用程序始终向 PAM 模块指定 `use_first_pass` 标志，如下所示：
>
> `telnet auth required /usr/lib/security/pam_ldap.so use_first_pass`
>
> `telnet account required /usr/lib/security/pam_ldap.so`
>
> `telnet password required /usr/lib/security/pam_ldap.so`
>
> `telnet session required /usr/lib/security/pam_ldap.so`

### 1.4.2 PAM 应用程序与 AIX

在 IBM OSS 站点提供的新 `ssh` 包是一个启用了 PAM 的应用程序。你可以在此处下载并找到安装说明：

```
http://oss.software.ibm.com/developerworks/projects/opensshi
```

此 `ssh` 服务仅支持 PAM API 进行身份验证。因此，为了使用该 `ssh` 服务，你必须创建 `/etc/pam.conf` 并正确配置 PAM。我们在第 5 页的示例 1-2 中展示了适用于 `AIX` 标准安全子系统进行身份验证的配置。

如果 `AIX` 应用要通过在 `/etc/security/user` 中设置 `SYSTEM` 语法通过 `AIX` 安全机制使用 PAM 认证服务，它们可以通过设置 `PAM_SERVICE` 变量来选择 PAM 服务：这些 `AIX` 应用和服务设置了 `ftp`、`login`、`password`、`exec`、`rsh`、`su` 和 `telnet`。如果 `/etc/pam.conf` 中不存在该服务，则将使用的 PAM 服务将定义为 `OTHER`（其他）。

## 在 AIX 上编译 PAM 应用程序

`AIX` 5L 版本 5.2 包含了开发 PAM 应用所需的完整工具。作为一个概念验证，我们编译并运行了一个小型的 PAM 辅助程序，其目的是为 `squid` Web 缓存服务器启用 PAM 认证。该程序的作者是 Henrik Nordstrom，辅助程序的源码和部分文档可以在此站点找到：

`http://squid.sourceforge.org/hno/software.html`

源代码由一个 `pam_auth.c` 源文件组成。我们下载该文件并生成了一个可执行镜像：

```bash
$ wget http://squid.sourceforge.org/hno/pam_auth-2.0.c
$ gcc -o squid-pamauth pam_auth-2.0.c -lpam
$ ls -l1 squid-pamauth
-rwxr-xr-x 2 1 joe staff 250945 Nov 06 14:27 squid-pamauth
```

该辅助程序使用的默认 PAM 服务是 `squid`，它支持 `auth`（认证）和 `account`（账户）PAM 阶段。因此，我们在 `/etc/pam.conf` 中放置了以下两行：

| 服务 | 类型 | 控制 | 模块 | 参数 |
| :--- | :--- | :--- | :--- | :--- |
| `squid` | `auth` | `required` | `/usr/lib/security/pam_ldap.so` | |
| `squid` | `account` | `required` | `/usr/lib/security/pam_ldap.so` | |

`squid` 服务器的接口非常简单：`Squid` 会调用 `squid-pamauth` 程序，并在标准输入中使用空格分隔的用户名和密码。因此，我们可以轻松地判断 PAM 程序是否工作正常：

```bash
$ /squid-pamauth
joe catchme
ERR
catch me joe
ERR
joe secret
OK
```

第 1 章 识别与认证 13

## 集中式用户管理

在 UNIX 上，有两种流行的方法提供单点登录和集中式用户管理：网络信息服务 (NIS) 和轻量级目录访问协议 (LDAP)。前者是著名的太阳微系统公司（Sun Microsystems）产品，适用于大多数 UNIX 平台。然而，在过去的几年里，LDAP 变得非常流行，并且有其合理的原因。

网络信息服务 (NIS) 在安全性方面的声誉很差，仅适用于信任环境。旨在替代 NIS 的 `NIS+` 在这方面要好得多，但设置和管理起来相当困难。

单点登录由一个认证方法和一个包含用户和组信息的副本组成。其主要优势是用户使用相同的密码对所有服务进行认证。单点登录的另一个明显优势是用户在一个地方进行管理。这取决于站点中主机的数量，这可以节省时间和资源。

在本章中，我们将讨论设置集中式用户管理和提供单点登录的各种方法。我们的主要目标是为此目的部署 LDAP，并展示 `AIX` 和 Linux 主机如何使用 LDAP 进行认证。

![](img/550f8fc128bac37c2a15bd674b67bcf1_32_0.png)

## 2.1 轻量级目录访问协议 (LDAP)

LDAP 的设计是为了让访问 ISO.500 目录更容易。ISO 标准及其目录访问协议 (DAP) 是极其复杂的规范，定义了跨越所有 OSI 七层的协议。最初，LDAP 是用于访问操作系统网络栈（TCP/IP）上 X.500 目录服务的客户端应用程序，仅支持重要的 DAP 操作，因此实现简单得多。后来，LDAP 规范也被应用于服务器端。LDAP 变得与 X.500 有了区别。

LDAP 基于开放标准。没有单一供应商控制 LDAP 规范，但它是由许多 IT 公司和专业人士共同努力，并由互联网工程任务组 (IETF) 协调开发的。今天，几乎任何计算机平台都支持并实现了 LDAP。这些是将 LDAP 作为目录服务的主要原因。

### 2.1.1 LDAP 简介

目录最常见的例子是电话簿，它由名称（条目）、电话号码以及可能的地址和其他有用信息组成。电话簿最重要的特征是它的组织方式简单，便于按名称快速查找。存储在 LDAP 目录中的数据没有太大区别；有对象（条目）及其属性。顺便提一下，如果你在互联网上遇到电子电话簿，它很有可能是用 LDAP 实现的。

目录方案（Directory schemes）描述存储在目录中的数据。它们定义了条目必须包含哪些属性、哪些属性是可选的、属性可以取什么类型的值以及是否允许有多个值。LDAP 目录中的每个条目都有一个名为区分名（Distinguished Name, DN）的唯一名称，它是电话中名称的 LDAP 对应项。这是一个示例：

```
dn=Joe R. User,dc=weorg,dc=com
```

这种格式被称为 LDAP 数据格式 (LDIF)，你可能会遇到它。DN 由一系列属性=值对组成。在这个示例中，`cn` 代表通用名称，`dc` 代表域组件。所有这些属性都定义在模式中。让我们看看这个条目中还有什么：

* `cn`: `Joe R. User`
* `cn`: `User`
* `cn`: `Jack`
* `sn`: `User`
* `givenName`: `Jack`
* `title`: `Dr`
* `mail`: `joe@weorg.com`
* `lineNumber`: `11`
* `objectClass`: `top`
* `objectClass`: `person`

属性名在左侧，后面跟着冒号。行的其余部分是属性值。注意，值可以包含各种格式的字符串（尽管如果有意义通常会有帮助）。事实上，可以为属性分配任何值，包括照片之类的二进制数据。点在于 LDAP 不关心目录中存储了什么；这由应用程序来解析和理解。LDAP 仅提供访问，并可能限制值。此外，如你所示，一个属性可能有多个值。

`objectClass` 属性是特殊的；它引用定义属性的模式。模式是相关类和属性的集合。每个类定义了可能存在的属性。

DN 的值表示数据是以层次结构组织的。DN 的编码与域名系统 (DNS) 主名相似，但使用逗号而不是点分隔。

LDAP 没有规定如何在目录中存储数据以及如何访问数据。当然，每个 LDAP 服务器都有一个数据库（通常称为后端），用于存储和检索信息。数据库应该能够快速检索数据。此外，假设目录数据不会频繁更改。如果确实经常更改，你可能希望使用通用数据库而不是目录。

### 2.1.2 使用 LDAP 进行认证

在上一小节中，我们说属性可以分配任何值。这并不完全正确。某些属性在 LDAP 服务器本身可能具有特殊含义，即 LDAP 服务器有时是一个 LDAP 应用程序，在这种角色下，它对所提供的数据具有选择性。特别是，所有 LDAP 服务器都实现某种认证方法。

一种实验性标准在请求注释 (RFC) 2307 中被描述：一种将 LDAP 作为网络信息服务的方法（有时称为 `RFC2307bis`）。该标准描述了用于识别和认证目的的对象类和属性。尽管它尚未被归类为 IETF 标准，但它已经存在多年，并且通常是……的共同点。

许多 LDAP 服务器和客户端实现都支持这些平台。现在，如果我们想为各种操作系统使用 LDAP 目录服务，识别出共同点似乎是合理的。

RFC2307 包含了以下对象类（还有更多，但本文重点介绍了这几类）：

* `posixAccount`
* `posixGroup`
* `shadowAccount`

`posixAccount` 和 `posixGroup` 类描述了 `/etc/passwd` 文件中存在的字段。`shadowAccount` 类由与 `/etc/shadow` 文件中的字段对应的属性组成。在示例 2-1 中，我们展示了 RFC2307 的相关节录。对象类的定义初看起来可能令人望而生畏，但请参考 MAY 和 MUST 句子，这些句子包含了可选和强制属性的列表。`uid` 和 `userPassword` 属性用于用户身份验证。在第 19 页的示例 2-2 中，我们展示了 LDAP 格式的一个典型条目。顺便提到，尽管我们使用混合大小写编写对象名称，但这并没有关系，即使在属性值中也是如此，这显然对认证有某些影响（注意给出的用户名）：

```bash
$ telnet r-linux
Trying...
Connected to r-linux.
Escape character is '^'
Red Hat Linux Version 8.0 (Psyche)
Kernel 2.4.18-14 on i686
login: Joe
Password:
Last login: Tue Nov 5 10:54:21 from 9.3.5.25
[@localhost joe]$
```

当然，密码对大小写敏感，因为它们是以哈希值存储的。

### 示例 2-1 对象类定义

```
nSchema.2.0 NAME 'posixAccount' SUP top AUXILIARY
DESC 'Abstraction of an account with POSIX attributes'
MUST ( cn $uid $uidNumber $gidNumber $homeDirectory )
MAY ( userPassword $ loginshell gecos $ description )

nSchema.2.1 NAME 'shadowAccount' SUP top AUXILIARY
DESC 'Additional attributes for shadow passwords'
MUST $uid
MAY ( userPassword $shadowLastChange $shadowMin
shadowMax $shadowWarning $shadowInactive $
shadowExpire $shadowFlag $ description )

( nisSchema.2.2 NAME 'posixGroup' SUP STRUCTURAL
DESC 'Abstraction of a group of accounts'
MUST ( cn $ gidNumber
MAY ( userPassword $ memberUid description ) )
```

**示例 2-2 用户 LDIF 条目**

```
uid=joe,ou=People,dc=weeorg,dc=com
uid: joe
cn: Joe R. User
objectClass: posixAccount
objectClass: shadowAccount
objectClass: top
userPassword: {crypt}$WA58b9dz5nI
loginShell: /bin/bash
uidNumber: 1000
gidNumber: 100
homeDirectory: /home/users/joe
gecos: Joe R. User
shadowLastChange: 11627
shadowMax: 99999
shadowWarning: 7
```

## 2.2 LDAP 认证规划

我们假设大家已经习惯了供应商按照自己的方式实现服务，尽管服务本身可能由行业共同认可的标准所描述。检查所有可用选项并查看它们之间的关系是非常重要的。部署 LDAP 也不例外。因此，我们检查了在 `AIX` 和 Linux 上的许多 LDAP 认证解决方案。

我们需要一个 LDAP 服务器来提供身份识别和认证数据的访问，以保持其良好状态。我们还需要一个充分集成到操作系统中的 LDAP 客户端，以便能够接管身份识别和认证任务。我们还需要其他一些，例如实施安全策略和加密通信（我们将在本章稍后部分讨论这些问题）。

`AIX` L5 Version 5.2 同时带了 LDAP 服务器（IBM Directory Server）和 LDAP 客户端。当然，由于来自同一家供应商，这两者协作得很好。如果你运行的是仅限 `AIX` 的环境并计划坚持下去，这可能是最佳的解决方案。随着最近加入了对 PAM 的支持，`AIX` LDAP 认证模块不是唯一的选择，但它是保留标准 `AIX` 安全子系统中完整用户属性集的唯一方法。
