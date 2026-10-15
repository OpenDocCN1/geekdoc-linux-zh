
MySQL 用户由用户名（在本例中为 `bobby`）、`@` 符号以及来源主机名组成。在例中，`bobby` 是一个本地系统用户，因此我们将用户指定为 `bobby@localhost`。最后，该部分是你定义该用户将使用此密码访问数据库的地方。

`flush` 命令告诉 MySQL 即使你更改了存储在 MySQL 中的用户数据也要更新此权限列表；运行进程不会自动应用任何更改。`flush privileges` 会让你的更改在运行的数据库中生效。

当然，大多数应用程序将通过网络访问数据库，因此当你定义一个用户并赋予权限时，你可能无法预测将来自哪个主机名。在这种情况下，你可以为关联用户的主机名使用通配符（glob）：

```
> grant all privileges on thisdb.* to bobby@"%" identified by "bypasspassword";
> flush privileges;
```

指定 `bobby@"%"` 将接受从任何主机的 `bobby` 用户的登录。如果你知道连接将仅来自一个特定的主机或 IP，请进一步锁定并在此处指定它。

一旦创建了用户，你可以使用以下命令查看它们：

`SELECT User, User FROM mysql.user;`

| Host | User |
| :--- | :--- |
| % | bobby |
| 127.0.0.1 | root |
| ::1 | root |
| localhost | |
| localhost | bobby |
| localhost | root |

6 rows in set (0.00 sec)

## 授予减少的数据库权限

当然，你可能不想授予用户数据库的完全访问权限。完全访问不仅允许用户在数据库中读写数据，还能删除记录并删除整个数据库。与其向用户授予所有权限，不如限制他们可以访问的 SQL 命令。例如，以下命令将允许用户读取、写入和删除数据库中的记录，但不能创建或删除：

```
> select,insert,update,delete privileges on thisdb.* to bobby@"%" identified by 'bobbyspassword';
> flush privileges;
```

如果你想创建一个只读用户，可以改为以下操作：

```
> grant privileges on thisdb.* to bobby@"%" identified by 'bobbyspassword';
> flush privileges;
```

## Postgres

Postgres 提供了一个命令行工具来创建新用户，恰恰其当的是 `createuser`。在 postgres 内部创建一个默认用户非常简单：

```
$ -u postgres createuser -P bobby
Enter password for new role:
Enter it again:
```

> 请记住，`postgres` 用户拥有对 Postgres 数据库的管理权限，它是你用来创建新账户的用户。在本例中，我使用了所有默认设置，这会创建一个没有权限的用户。我传递给 `createuser -P` 的唯一参数是让它提示输入密码（-P），以及我创建的用户名。如果我想显式地确保该用户是普通的无权限用户，我可以添加 `-D`、`-R` 和 `-S` 参数，它们分别设置权限使得无法创建数据库、无法创建角色且不是超级用户，但这些设置是默认的。

在 Postgres 中，你使用 `createdb` 命令行程序来创建新数据库：

```
$ -u postgres createdb thisdb
```

在创建数据库时，还可以指定一个拥有该数据库的用户。数据库所有者对数据库拥有完全权限，因此如果你为每个应用程序创建数据库，可以使用 `-O` 选项将为应用程序创建的用户设置为数据库所有者：

```
$ -u postgres createdb -O bobby thisdb
```

如果你已经创建了数据库并想授予某个用户完全权限，可以使用 `psql` 命令行工具获取 postgres 命令提示符，然后使用 `GRANT` 命令：

```
$ -u postgres psql
ps (9.4.9)
Type "help" for help.
```

```
postgres# GRANT ALL PRIVILEGES ON DATABASE thisdb to bobby;
GRANT
```

# 第2节：数据库加固

## 授予减少的数据库权限

但是，如果用户不需要，你并不非要授予数据库的所有权限。你可以从 `SELECT, INSERT, UPDATE, DELETE, TRUNCATE, REFERENCES, TRIGGER, CREATE, TEMPORARY, EXECUTE, 和 USAGE` 列表中指定数据库权限。与我们之前的 `GRANT` 不同，在这种情况下，我们在运行 `psql` 时需要连接到特定的数据库。例如，如果我们限制用户对数据库进行读取、写入和删除，但不允许创建或删除，我们将使用：

`GRANT SELECT,INSERT,UPDATE,DELETE ON thisdb.* TO bobby@"%" IDENTIFIED BY 'bobbyspassword';`
`FLUSH privileges;`

如果你想创建一个只读用户，可以这样做：

`GRANT PRIVILE ON thisdb.* TO bobby@"%" IDENTIFIED BY 'bobbyspassword';`
`FLUSH privileges;`

### 数据库加固

在 Postgres 中，如果我们想限制用户对数据库进行读取、写入和删除，但不允许创建或删除，我们将使用：

`GRANT SELECT,INSERT,UPDATE,DELETE ON DATABASE thisdb TO bobby;`

如果你想创建一个只读用户，可以这样做：

`GRANT SELECT ON DATABASE thisdb TO bobby;`

在 Postgres 中，你使用 `createdb` 命令行程序创建新数据库。在创建时，还可以指定一个拥有该数据库的用户。数据库所有者对数据库拥有完全权限，因此如果你为每个应用程序创建数据库，可以使用 `-O` 选项将为应用程序创建的用户设置为数据库所有者：

## 数据库网络访问控制

数据库网络访问目的是目的是深度防御。理想情况下，数据库被放在自己的网络中，并使用防火墙规则保护其不受外部世界的影响。然而，人会出错，如果你唯一的防线是防火墙规则，一次错误就会暴露你的数据库。MySQL 网络访问控制的主要方法是基于用户的。每个数据库用户由用户名和主机组合而成，采用 `username@host` 格式。在第1节中，我们提供了这种主机访问数据库的两个极端示例。在实践中，你可能希望在这两个极端之间进行网络访问控制。例如，假设你的内部网络使用 `10.0.0.0/8` 范围，不同类型的应用程序在其中各有一个自己的子网。你可以通过类似 `bobby@10.0.0.0/255.0.0.0` 的用户名来限制账户必须来自本地网络。如果你将服务器角色划分为不同的子网，例如，如果你的应用程序服务器使用 `10.0.5.0/24` 子网，你创建一个名为

## 第 2 部分：数据库加固

`bobby@10.0.5.0/255.255.255.0`。在这种情况下，我们也可以利用 MySQL 的通配符，使用用户 `bobby@10.0.5%` 来代替。

需要注意的是，MySQL 将每个用户和主机的组合视为一个不同的用户。如果你为之前的每个 bobby 用户运行了 `grant` 命令，你将得到如下所示的用户表：

```sql
> SELECT Host, User FROM mysql.user;
```

| Host | User |
| :--- | :--- |
| % | bobby |
| 10.0.0.0/255.255.0 | bobby |
| 10.0.5.% | bobby |
| 10.0.5.0/255.255.255.0 | bobby |
| 127.0.0.1 | root |
| ::1 | root |
| localhost | |
| localhost | bobby |
| localhost | root |

`9 rows in set (0 sec)`

如果你决定收紧访问控制，请记住这一点。如果你创建一个具有更严格限制主机的新用户，请务必删除之前的用户。例如，如果我想移除 `bobby@10.0.5.0/255.255.255.0` 以及限制性较小的 `bobby@%` 和 `bobby@10.0.0.0/0.0`，我将输入：

```sql
> drop user bobby@"10.0.5.0/255.255.255.0";
> drop user bobby@"%";
> drop user bobby@"10.0.0.0/0.0";
> flush privileges;
```

## Postgres

Postgres 通过其 `pg_hba.conf` 文件管理网络访问，在基于 Red Hat 的系统中，它存储在 `/var/lib/postgresql/data` 下，在基于 Debian 的系统中存储在 `/etc/postgresql/<version>/main/` 下。该文件控制允许哪些类型的身份验证，以及适用于哪些数据库、用户和网络。默认情况下，`pg_hba.conf` 文件只允许来自 `localhost` 的连接，看起来可能如下：

```conf
# TYPE      DATABASE        ADDRESS                 METHOD
# "local" 仅用于 Unix 域套接连接
local       all                               peer
# IPv4本地连接:
host        all             127.0.0.1/32            ident
# IPv6本地连接:
host        all             ::1/128                  ident
```

如果你在不同的主机服务器上定位应用程序，这些权限可能运行良好，但大多数人希望从 Postgres 主机连接数据库。由于我们重点是加固，不再深入研究 PostgreSQL 可用的所有身份验证方法，我将处理常见情况。最常见的情况可能是通过密码通过网络访问数据库。假设我们的内部网络是 `10.0.0.0/8`。在这种情况下，我们会在现有配置下的 `pg_hba.conf` 中添加以下行：

```conf
host      all             all            10.0.0.0/8      password
```

如你所见，我们更改的主要两个字段是地址字段和列出 `password` 的方法字段。`password` 方法的缺点是它以明文形式通过网络发送密码！虽然 postgres 提供了 `password` 方法的 MD5 替代方案，可以通过多次迭代封装密码，但如今的哈希算法不够强大，无法抵抗攻击。但别担心；在下一节中，我们将讨论如何通过将连接封装在 TLS 中来加固密码身份验证。

与其授予每个用户访问每个数据库的权限并仅通过密码限制，你还可以根据每个网络或数据库应用不同的限制。例如，假设我们有一个客户数据库和一个库存数据库。我们的客户应用程序服务器位于 `10.0.5.0/24` 子网上，库存应用程序服务器位于 `10.0.6.0/24` 上。我们可以创建特定的 `pg_hba.conf` 规则将它们限制在特定的数据库上：

```conf
host      customer      all            10.0.5.0/24      password
host      inventory     all            10.0.6.0/24      password
```

这样，如果有人通过某些漏洞入侵了库存应用程序，我们就无法利用它来猜测客户数据库的密码。

## 启用 SSL/TLS

安全领域的一个矛盾点是，数据库流量是网络上最敏感的流量之一，因此许多组织对其进行加密。人们认为由于数据库位于防火墙后或网络深处，其流量是安全的。在现代，特别是当你在云端进行托管时，情况已不再是这样；你必须假设任何网络（包括内部网络）可能是敌意的。考虑到这一点，使用 TLS 保护与数据库的通信比任何时候都更重要。

将流量封装在 TLS 中为你提供了两种主要的保护方法。首先，它加密流量，因此任何在网络上嗅探的人都看不到。这尤为重要，因为数据库客户端经常通过网络以明文发送密码，如果不是明文，也是使用 MD5 等弱哈希算法加密的。此外，你部门一些最敏感的信息可能就在你的数据库中，即使你不希望其他部分可见。TLS 的第二个用处是它可以对客户端进行服务器身份验证，这样你的客户端就知道它正在与真实的服务器通信。

设置 TLS 的一个方面是本节未涵盖的如何生成自己的证书。有很多方法可以解决这个问题，尽管创建自签名证书或使用像 Let’s Encrypt 的服务。无论你如何获取证书，最后都需要一个私钥以及相应的 CA 证书。

## MySQL

使用 TLS 配置 MySQL 非常简单。编辑你的 `my.cnf` 文件（通常位于 `/etc/`），找到文件中的 `[mysql]` 部分并添加以下选项。结果如下：

```ini
[mysql]
ssl-ca=/path/to/ca.crt
ssl-cert=/path/to/server.crt
ssl-key=/path/to/server.key
```

MySQL 期望所有内容均为 PEM 格式。如果你做了更改，重启 MySQL 即可接受连接。默认情况下，MySQL 会允许可能不安全的套件。要加固，请在配置中添加加密套件列表。例如，使用 Mozilla 推荐的“Intermediate”。

## 客户端要求 TLS

一旦服务器端设置了 TLS，你可能希望客户端使用它。你可以在创建用户时通过 `GRANT` 语句末尾添加 `REQUIRE SSL` 参数来实现：

```sql
> grant privileges on tls.* by bobby@'10.0.5.%' identified by 'password' REQUIRE SSL;
> flush privileges;
```

你可以通过查看用户表中的 `ssl_type` 行来查看哪些用户启用了此功能：

```sql
> SELECT Host, User, ssl_type FROM mysql.user;
```

| Host | User | ssl_type |
| :--- | :--- | :--- |
| localhost | root | |
| 127.0.0.1 | root | |
| :: | root | |
| localhost | bobby | |
| 10.0.5.% | bobby | ANY |

`5 rows in set (0.00 sec)`

## Postgres

在 Postgres 中启用 TLS 相对简单。首先，编辑主 `postgresql.conf` 文件，它在基于 Red Hat 的系统中存储在 `/var/lib/postgresql`，在基于 Debian 的系统中存储在 `/etc/postgresql/<your postgres version>/main/`。该文件的默认包含许多注释的选项。在文件中找到 `ssl` 选项设置为：

```ini
ssl = on
```

可选，你还可以使用 `ssl_ciphers` 指定一组允许的 TLS 加密算法。要使用更“严格”的加密进行进一步加固：

```ini
ssl_ciphers = ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-AES256-GCM-SHA384:DHE-RSA-AES128-GCM-SHA256:DHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES256-SHA384
```
