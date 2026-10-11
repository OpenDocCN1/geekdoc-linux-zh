

-   `supported_enctypes` 是对 KDC 为此领域支持的所有加密类型的引用。

列表 13.4 展示了一个典型 `kdc.conf` 文件的完整内容。

## 列表 13.4 典型 kdc.conf 文件的内容

```
[ramon]$ more /var/kerberos/krb5kdc/kdc.conf
[kdcdefaults]
  acl_file = /var/kerberos/krb5kdc/kadm5.acl
  dict_file = /usr/dict/words
  admin_keytab = /var/kerberos/krb5kdc/kadm5.keytab

[realms]
  HONTANON.COM = {
    master_key_type = des-cbc-crc
    supported_enctypes = des-cbc-crc:normal des3-cbc-raw:normal
    des3-cbc-sha1:normal des-cbc-crc:v4 des-cbc-crc:afs3
  }
```

您可能希望为您的 KDC 创建类似的配置。在我的服务器上，我还设置了一个 DNS 别名 `kerberos.hontanon.com`，指向我的服务器 IP 地址，这主要为了方便起见。这样，如果需要更改服务器平台的 IP 地址，我不必更改配置文件，只需通过 DNS 修改主机名指向新地址即可。

### kdb5_util 实用程序

`kdb5_util` 实用程序随 Kerberos 服务器软件包一起提供，允许您对 Kerberos 认证数据库执行管理程序。您可以使用 `kdb5_util` 创建数据库、添加新的主体（人类和机器），以及修改和删除这些主体。

让我们先从使用 `kdb5_util` 实用程序创建 KDC 数据库开始，如列表 13.5 所示。

## 列表 13.5 使用 kdb5_util 创建 KDC 数据库

```
[ramon]$ sudo /usr/kerberos/sbin/kdb5_util create -r HONTANON.COM -s
Initializing database '/var/kerberos/krb5kdc/principal' for realm
'HONTANON.COM',
master key name 'K/M@HONTANON.COM'
You will be prompted for the database Master Password.
It is important that you NOT FORGET this password.
```

输入 KDC 数据库主密钥：
重新输入 KDC 数据库主密钥以验证：

列表 13.5 中的命令会提示您输入 Kerberos 主密钥（您应该选择一个难以猜到的单词，包含混合大小写字母和数字），并创建以下文件：

-   `/var/kerberos/krb5kdc/principal`：这是一个 Kerberos 数据库文件。
-   `/var/kerberos/krb5kdc/principal.kadm5`：这是 Kerberos 管理数据库。
-   `/var/kerberos/krb5kdc/principal.kadm5.lock`：这是与 Kerberos 管理数据库相关的锁定文件。
-   `/var/kerberos/krb5kdc/.K5.HONTANON.COM`：此文件称为 *stash*（暂存文件），是主密钥的本地副本，用于在启动 `kadm5d` 和 `krb5kdc` 守护进程之前对 KDC 进行自认证。

> **警告** 应严格保护 stash 文件，并且该文件的所有者和读取权限应仅授予 root 用户。stash 文件不应是您常规备份方案的一部分，因为这会迫使您保护备份介质的隐私（备份介质中会包含 KDC 的主密钥）。

### kadm5.acl 文件

查看 `kadm5.acl` 文件，它通常位于 `/var/kerberos/krb5kdc` 中。此文件定义了哪些主体被允许使用 `kdb5_util` 修改数据库的哪些部分。您需要在此文件中至少有一个 Kerberos 主体，以及该主体的权限列表。`kadm5.acl` 文件中条目的格式如下：

```
principal permissions [target-principal]
```

这些字段具有以下含义：

-   *principal* 是一个使用以下语法的条目：
    ```
    primary/instance@REALM
    ```
    其中 *primary* 是用户名（例如，以下示例中的 *ramon*），*instance* 定义特定角色（例如，以下示例中的 *admin*），而 *REALM* 对应一个 Kerberos 领域（例如，以下示例中的 *HONTANON.COM*）。例如，完整的主体指定为 *ramon/admin@HONTANON.COM*。
-   *permissions* 字段可以由表 13.1 中列出的一个或多个字符组成。

| 选项 | 含义 |
| :--- | :--- |
| a | 允许添加主体。 |
| A | 禁止添加主体。 |
| d | 允许删除主体。 |
| D | 禁止删除主体。 |
| m | 允许修改主体。 |
| M | 禁止修改主体。 |
| c | 允许更改主体的密码。 |
| C | 禁止更改主体的密码。 |
| i | 允许对数据库进行查询。 |
| I | 禁止对数据库进行查询。 |
| l | 允许列出主体或策略。 |
| L | 禁止列出主体或策略。 |
| * | 允许所有权限。 |

-   *target-principal* 是一个可选字段，您可以使用它将某些操作限制为仅适用于指定的主体。

例如，如果您有一个主体 `alice/admin@HONTANON.COM`，它只需要列出 Kerberos 数据库中的所有主体并更改其密码，您可以使用以下条目：

```
alice/admin@HONTANON.COM cl
```

为了授予主体 `bob/admin@HONTANON.COM` 仅对主体 `*/root@HONTANON.COM`（HONTANON.COM 领域中具有 root 实例的任何主体）的所有访问权限，您应添加以下行：

```
bob/admin@HONTANON.COM    *    */root@HONTANON.COM
```

为了授予主体 `ramon/admin@HONTANON.COM` 修改任何主体的所有数据库字段的权限，请添加以下行：

```
ramon/admin@HONTANON.COM *
```

### kadmin.local 实用程序

接下来，您需要使用 `kadmin.local` 实用程序向 Kerberos 数据库添加管理员。此实用程序是 Kerberos 管理服务器的命令行界面，并且必须在与 Kerberos KDC 相同的主机上执行。您选择添加的管理员主体必须存在于 `kadm5.acl` 文件中。

一旦进入 `kadmin.local` 实用程序，将出现一个 `kadmin.local:` 提示符，您可以在此指定以下命令之一：

-   `addprinc principal`：此命令向数据库添加新的主体。
-   `delprinc principal`：此命令从数据库删除现有的主体。
-   `modprinc principal`：此命令允许您修改现有的主体。
-   `renprinc new old`：此命令将主体从 old 重命名为 new。
-   `cpw principal`：此命令允许您更改主体的密码。
-   `getprinc principal`：此命令显示主体的记录。
-   `listprincs`：此命令列出数据库中的所有主体。
-   `ktadd -k keytab principal [principal]`：此命令向 keytab 添加一个或多个主体。
-   `ktremove -k keytab principal [principal]`：此命令从 keytab 中删除一个或多个主体。

要创建管理员 `ramon/admin@HONTANON.COM`，请输入以下命令。在此示例中，`addprinc` 命令向 Kerberos 数据库添加了一个具有管理员权限的新主体。

```
[ramon]$ sudo /usr/kerberos/sbin/kadmin.local
Authenticating as principal root/admin@HONTANON.COM with password.
kadmin.local: addprinc ramon/admin@HONTANON.COM
Enter password for principal "ramon/admin@HONTANON.COM":
Re-enter password for principal "ramon/admin@HONTANON.COM":
Principal "ramon/admin@HONTANON.COM" created.
```

接下来，您需要创建一个 `kadm5` keytab。Keytab 只是一个密钥，将由 Kerberos 管理守护程序（`kadm5d`）用于在授予管理员访问 Kerberos 数据库权限之前解密管理员的 Kerberos 票据。注意，您将创建 keytab 的两个主体是：`kadmin/admin` 和 `kadmin/changepw`。这两个主体在数据库首次生成时由 Kerberos 自动创建。您像之前一样使用 `kadmin.local` 命令来创建 keytab，如列表 13.6 所示。

## 列表 13.6 使用 kadmin.local 创建 keytab

```
[ramon]$ sudo /usr/kerberos/sbin/kadmin.local
Authenticating as principal root/admin@HONTANON.COM with password.
kadmin.local: ktadd -k /var/kerberos/krb5kdc/kadm5.keytab kadmin/admin
Entry for principal kadmin/admin with kvno 4, encryption type DES-cbc mode with CRC-32 added to keytab /var/kerberos/krb5kdc/kadm5.keytab.
Entry for principal kadmin/admin with kvno 4, encryption type Triple DES cbc mode raw added to keytab /var/kerberos/krb5kdc/kadm5.keytab.
Entry for principal kadmin/changepw with kvno 4, encryption type DES cbc mode with CRC-32 added to keytab /var/kerberos/krb5kdc/kadm5.keytab.
Entry for principal kadmin/changepw with kvno 4, encryption type Triple DES cbc mode raw added to keytab /var/kerberos/krb5kdc/kadm5.keytab.
```

`ktadd` 命令使用 `-k` 开关调用，后跟 keytab 文件的位置。此文件应与 `kdc.conf` 文件中 `admin_keytab` 变量的值匹配（本节前面示例中的 `/var/kerberos/krb5kdc/kadm5.keytab`）。

现在，您可以使用以下命令启动主 KDC 守护程序和管理守护程序：

```
[ramon]$ sudo /usr/kerberos/sbin/krb5kdc
[ramon]$ sudo /usr/kerberos/sbin/kadmin
```

输入这些命令后，进程将分叉并移至后台，从而释放您的终端以用于其他工作。如果您希望这些进程在系统启动时开始运行，您可以将脚本的符号链接添加到以下目录：

-   `/etc/rc.d/init.d/krb5kdc`
-   `/etc/rc.d/init.d/kadmin`

添加到 `/etc/rc.d/rc5.d` 目录。

> **注意** 如果可能，请专门分配一台系统来执行 KDC 功能。在 KDC 上运行其他服务（FTP、WWW 和 SMTP）会增加 Kerberos 数据库通过这些额外服务的漏洞被破坏的风险。

