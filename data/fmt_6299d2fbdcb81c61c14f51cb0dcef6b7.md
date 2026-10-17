
或者，也可能完全不使用分隔符和域名，即使用默认域的方式。要启用此项，在 `smb.conf` 文件中添加以下行：

```
windbind use default domain = yes
```

并可能将 `template homdir` 修改为：

```
template homdir = /home/%U
```

所有域用户显示时都不带目录名和分隔符。如果本地用户和域用户同名，可能会导致问题。

> 提示：不确定时使用默认域选项。分隔符和域名可能会应用程序中引起问题。对默认域使用 `pam_mount` 可以避免很多问题。

`idmap uid` 和 `idmap gid` 告诉 `winbind` 可为域账户生成 `uids` 和 `gids` 的范围。请选择一个与本地用户不重叠的范围。

> 重要：如果你有一个非常大的域，可能需要调整范围。

这些更改后，必须启动 `winbind` 守护进程。对于大多数发行版，使用以下命令完成：

```
/etc/init.d/winbind start
```

要测试 `winbind` 功能，使用 `wininfo` 命令。示例 9-6 `wininfo` 示例：

```
[root@client1]# wininfo -u
AD6380\Administrator
AD6380\Guest
AD6380\TsInternetUser
AD6380\idsadmin
AD6380\krbtgt
AD6380\HOST\client1
```

这些 `idmap` 后端非常新，因此仍然处于某种实验性阶段。它们都消除了 `winbind` 作为企业环境解决方案的一个一个缺点。

### idmap_rid 后端

该后端根据域 SID 为用户计算 `uid` 和 `gid`。要启用此选项，请在 `smb.conf` 文件中包含示例 9-8 中的配置行。

示例 9-8 在 `smb.conf` 中使用 `idmap_rid` 后端的项示例

| `idmap uid = 10000-20000` |

| `idmap gid = 10000-20000` |

| `idmap backend = idmap_rid:AD6380=15000-20000` |

| `allow trusted domains = no` |

使用这些设置并设置默认域，使其不明确区分域账户。`getent passwd` 的部分输出如示例 9-9 所示。

示例 9-9 使用 `idmap_rid` 时 `getent passwd` 的部分输出

```
root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/bin/bash
AD6380+administrator:x:15500:15513:Administrator:/home/administrator:/bin/bash
AD6380+guest:x:15511:15514:Guest:/home/guest:/bin/bash
AD6380+w2k3ad_:x:16003:15516:w2k3AD:/home/w2k3ad_:/bin/bash
AD6380+krbtrgt:x:15502:15513:krbtrgt:/home/krbtrgt:/bin/bash
AD6380+testuser:x:16108:16121:Test User:/home/testuser:/bin/bash
AD6380+rhd45:x:16112:15515:rhd45:/home/rhd45:/bin/bash
AD6380+rhd4a_:x:16113:15515:rhd4a_/home/rhd4a_:/bin/bash
AD6380+idmapbind:x:15517:15513:idbind:/home/idbind:/bin/bash
AD6380+nld9_:x:16120:15519:nld9_/home/nld9_:/bin/bash
```

从示例 9-9 的输出可以明显看出，这不再是在允许范围内按顺序选择 `uid` 和 `gid` 的简单算法。这种方法的主要优势是，`AD6380` 域内所有客户端的映射关系都是相同的。

### idmap_ad 后端

在下一节关于 LDAP 的内容中，解释了 Microsoft UNIX 服务（SFU）的概念。通过 SFU，Active Directory 的架构（schema）扩展了 `uid` 和 `gid` 信息。使用 `idmap_ad` 后端，可以获取这些信息并与 `winbind` 使用。

通过这种方式，所有客户端上的映射是一致的，因为映射实际上是在 Active Directory 中完成的。

通过 `smb.conf` 文件中的以下行启用 `idmap_backend`：

```
idmap_backend = idmap_ad
```

## 9.3 如何使用 LDAP 连接到 Active Directory

Active Directory 是轻量级目录访问协议（LDAP）的一种实现。因此，我们可以使用 LDAP 客户端连接到 AD 以收集用户信息。然而，由于 AD 并非为存储 UNIX/Linux 用户而设计，默认架构中缺少一些必要的对象。第一步之一是使用所需的对象类（`object-classes`）扩展架构。

扩展架构的一种简单方法是安装微软的“UNIX 服务”（SFU）。这些包含了存储所需信息的对象类。

按照以下步骤使用默认设置安装 SFU：

1. 将文件提取到非 `C:\SFU` 的目录，例如 `C:\Temp\SFU`。
2. 运行 `setup.exe`。
3. 接受标准安装（Standard Installation）。
4. 在安全设置（Security Settings）窗口中，将两个选项留空。
5. 选择本地用户名映射服务器（Local Username Mapping Server）和网络信息服务（Network Information Services）。
6. 选择域名。
7. 重启 AD 服务器。

此安装扩展了 AD 架构，包含了 `uid` 和 `gid` 等字段。

下一步是在 Active Directory 中创建一个用户，供 LDAP 客户端绑定到目录。选择一个高强度密码并将其设置为不过期。

由于架构的扩展，现在可以为组提供 `gid` 字段，为用户提供 `uid`、`shell` 和主目录，如第 205 页的图 9-1 所示。

## 用户属性

![](img/23b949da14ff7bab8762f0f0361af394_232_0.png)

图 9-1 带有 UNIX 属性的 Active Directory 用户属性窗口

在此示例中，我们创建了一个名为 `tester` 的用户，UID 为 5000，拥有登录 Shell 和主目录。我们还创建了一个名为 `Linuxusers` 的组（或主组名/GID），其 `gid` 为 5000。

关于 UNIX 服务以及将 Active Directory 集成 Linux 或 UNIX 客户端的目录的更多信息，可以在微软提供的《Solution Guide for Windows Security and Directory Services for UNIX》文档中找到。

要启用系统使用 LDAP 连接到 Active Directory，必须配置 LDAP 配置文件 `/etc/ldap.conf`。该配置文件包含以下信息：

- 目录的主机，即如果有多个 Active Directory 服务器，则用空格分隔的 IP 地址
- 从目录中开始搜索的基节点
- 连接 AD 的绑定用户（`bind user`）
- 绑定用户的密码（明文形式，因此你需要保护该配置文件）
- 搜索范围
- SSL 启用
- 将域架构对象映射到 NSS 所需若干条目

示例 9-10 显示了 `/etc/ldap.conf` 的示例配置文件。

## 示例 9-10 `/etc/ldap.conf` 文件

```
host 192.168.100.110
base cn=Users,dc=AD6380,dc=LOCAL
binddn cn=Users,dc=AD6380,dc=LOCAL
```

## 9.4.1 如何使用 windbind 和 PAM 认证用户

由于不同 Linux 发行版的 PAM 实现有所不同，我们将详细查看各个发行版。

### Red Hat 桌面上的 Winbind 和 PAM

Red Hat 实现了 `pam_stack` 模块。这意味着 `/etc/pam.d/` 下的配置文件可以使用其他文件的设置，本质上是设置的堆叠。为了这个目的，Red Hat 在 `/etc/pam.d/system-auth` 文件中实现了大部分设置。这意味着我们只需要将 `windbind` PAM 模块添加到此文件中，然后所有应用程序都将识别 `windbind`。

由于 `/etc/pam.d/system-auth` 文件是由 `authconfig` 生成的，在手动修改后执行该命令时需要小心。

示例 9-12 示例的 `system-auth` 文件包含示例 9-12 中的行。以下是 `/etc/pam.d/system-auth` 文件用于 `windbind` 认证的部分示例：
