
配额记录以硬设备名称以及正在使用的内存块和节点（`nodes`）开始。段具有硬、软限制的参数。如果这些条目为 `0`，则没有设置限制。你可以同时设置硬、软限制，并将硬限制作为强制性限制。Linux 中的块（`blocks`）目前约为 `1000` 字节。`inodes` 用于文件存储有关构成文件的内存块的信息。要设置软限制的时间限制，使用带有 `-t` 选项的 `edquota` 命令。以下示例显示了 `larisa` 的配额：

`larisa` 的配额：

```
/dev/hda3: blocks in use: 9000, limits (soft = 40000, hard = 60000)
inodes in use: 321, limits (soft = 0, hard = 0)
```

### quotacheck, quotaon, 和 quotaoff

配额记录维护在该分区的配额数据库中。每个启用了配额的分区都有自己的配额数据库。你可以使用 `quotacheck` 命令检查配额数据库的有效性。你可以使用 `quotaon` 和 `quotaoff` 命令开启关闭。当你启动系统时，会运行 `quotacheck` 来检查配额数据库，然后运行 `quotaon` 来开启配额。

### repquota 和 quota

作为系统管理员，你可以使用 `repquota` 命令生成指定文件系统的磁盘使用摘要，检查哪些用户接近或超过了配额。`repquota` 的参数是文件系统；`-a` 选项检查所有。

```
repquota /hda1
```

| 30-5 edquota 选项 | 描述 |
| :--- | :--- |
| -u | 编辑用户。这是默认的。 |
| -g | 编辑组。 |
| -p | 复制指定的配额。这是用于初始化组配额的机制。 |
| -t | 编辑每个文件系统的软限制。 |

## LDAP 协议

### 轻量级目录访问协议

轻量级目录访问协议 (`LDAP`) 设计用于实现网络可访问的目录。在此背景下，目录被定义为只读的、简单的、广泛访问的且快速分发的数据库。它不是为事务或更新设计的。它主要用于提供网络上用户的信息，例如他们的电子邮件地址或电话号码。目录也可用于身份验证，识别用户属于哪个网络。你可以在 `www.ldap.org` 找到更多关于 `LDAP` 的信息。你可以将 `LDAP` 目录想象成互联网访问的电话簿，任何人都可以查询你的电子邮件地址或其他信息。事实上，将此类目录称为数据库更为准确。这些是通过网络访问的用户信息数据库。通常，本地网络上的用户分布在不同的系统中，为了获取有关用户的信息，你需要知道用户在哪个系统中，然后查询该系统。通过 `LDAP`，网络上所有用户的信息都存储在 `LDAP` 服务器中。你只需要查询网络的 `LDAP` 服务器即可获取信息。例如，`Sendmail` 可以使用 `LDAP` 查找用户地址。你也可以使用 `Firefox` 或 `Netscape` 查询 `LDAP`。

> 注意 `LDAP` 是一种访问 `X.500` 目录服务的协议，即 `OSI` 服务。

### LDAP 客户端和服务器

`LDAP` 目录以客户端和服务器的形式实现，你使用 `LDAP` 客户端访问管理 `LDAP` 数据库的 `LDAP` 服务器。大多数 Linux 发行版包括 `Fedora Core` 都使用 `OpenLDAP`，它是 `LDAP` 的开源版本（你可以在 `www.openldap.org` 找到更多关于 `OpenLDAP` 的信息）。此包包含 `LDAP` 服务器 (`slapd`)、`LDAP` 复制服务器 (`slprd`)、`LDAP` 客户端和工具。`slprd` 用于更新网络上的其他 `LDAP` 服务器，你应该有多个。一旦安装了 `LDAP` 服务器，你可以使用 `ldap` 启动脚本或 `system-config` 启动、停止和重启 `LDAP` 服务器 (`slapd`)：

```
service ldap restart
```

![](img/70a65fc8f3408711ddea7ea368f31720_634_0.png)

# 594 第六部分：系统管理

> 提示 `Fedora` 客户端可以使用 `Fedora` 身份验证工具（`system-config-authentication`）启用 `LDAP` 服务，该工具可以通过系统设置菜单和窗口中的“身份验证”项访问（第 4 章）。

### LDAP 配置文件

所有 `LDAP` 都存储在 `/etc/ldap` 目录中。这些包括 `slapd.conf`（`LDAP` 服务器配置文件）和 `ldap.conf`（`LDAP` 客户端和工具配置文件）。要启用 `LDAP` 服务器，你必须手动编辑 `slapd.conf` 文件，并将后缀（`suffix`）和根节点（`rootdn`）的域值（`dc`）更改为你的网络域名地址。该网络即为由 `LDAP` 服务器提供服务。

要启用 `LDAP` 客户端及其工具，你必须在 `ldap.conf` 文件的 `BASE` 选项中指定正确的地址，并在 `HOST` 选项中指定服务器地址（域名或 IP 地址）。对于客户端，你可以直接编辑 `ldap.conf` 文件，也可以使用系统设置中的“身份验证”工具，在“用户信息”或“身份验证”面板上点击“配置 LDAP”按钮。在这里你可以输入域名和 `LDAP` 服务器地址。有关 `LDAP` 选项的详细说明，请参考 `ldap.conf` 手册。

> 提示请记住，`ldap.conf` 和 `/etc/ldap/ldap.conf` 文件是不相同的：`/ldap.conf` 用于配置名称服务（Nameservice）和 `PAM` 的支持，而 `/etc/ldap/ldap.conf` 用于所有 `LDAP` 客户端。

### 配置 LDAP 服务器：/etc/slapd.conf

你通过 `/etc/slapd.conf` 文件来配置服务器。在这里，你会找到加载架构（`schemas`）、指定访问控制、数据库目录和密码的条目。该文件有详细的注释，大多数选项都有默认设置，尽管你必须为某些选项输入设置。首先，你需要指定你的域后缀和根域管理器。此处显示了默认设置：

```
suffix      dc=my-domain, dc=com
rootdn     cn=Manager, dc=my-domain, dc=com
```

在这个示例中，`suffix` 被更改为 `mytrek`，而 `mytrek.rootdn` 保持不变。

```
suffix      dc=mytrek, dc=com
rootdn     cn=Manager, dc=mytrek, dc=com
```

接下来，你必须使用 `rootpw` 指定密码。这里有明文和加密版本的条目。两者都已注释。请取消其中一个的注释。在以下示例中使用了明文密码“secret”：

```
rootpw    secret
# rootpw   {crypt}ijFYNCscByG
```

对于加密密码，你可以使用 `slapppasswd` 创建加密版本。这将为密码生成一个文本加密字符串。将生成的加密字符串复制到 `rootpw` 条目。在 `GNOME` 上，你可以简单地从终端窗口复制并粘贴到文本编辑器（附件）中的 `/etc/slapd.conf` 文件。你也可以将加密字符串重定向到文件并在以后读取。默认将使用 `SSHA` 加密。

```
@ slappasswd
New password:
Re-enter new password:
{SSHA} 0a+7zaAwE1K57Y8AoD5uMvLSfUCfg5
```

`rootpw` 密码条目应该如下：

```
rootpw
(SSHA) 0a+7zaAwE1K57Y8AoD5uMvLSfUCfg5
```

使用你在 `slapppassword` 提示中输入的密码来访问你的 `LDAP` 目录。配置文件还列出了要使用的架构。架构通过 `include` 指令包含。

- `include /etc/openldap/schema/core.schema`

- `include /etc/openldap/schema/cosine.schema`

- `include /etc/openldap/schema/inetorgperson.schema`

- `include /etc/openldap/schema/nis.schema`

> 注意 `LDAP` 支持简单身份验证与安全层 (`SASL`)，用于 `MD5` 和 `Kerberos` 的安全身份验证。

### LDAP 目录：条目

`LDAP` 数据库中的记录（也称为条目）以名称开始，即区分名（`distinguishing name`），随后是一组属性及其对应值。区分名唯一地标识该记录。例如，一个名称可以是用户名，属性可以是用户的电子邮件地址，而该地址即为属性的值。允许的属性由 `/etc/openldap/schema` 目录中的架构定义。此条目将包含各种架构定义，每个定义都有架构扩展。某些定义依赖于其他定义，以增强它们支持的类和属性。核心属性集定义在 `core.schema` 文件中。你会找到如国家名称和街道地址等属性的定义。其他架构（如 `inetorgperson.schema`）将 `core.schema` 指定为依赖架构，使其属性对 `inetPerson` 类可用。`inetOrgPerson` 架构还会定义自己的属性，如用于人物照片的 `jpegPhoto`。
