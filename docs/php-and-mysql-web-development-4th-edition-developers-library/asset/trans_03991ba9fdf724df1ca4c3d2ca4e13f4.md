
# 12.4.2.3 REQUIRE

REQUIRE X509 对证书的内容没有施加任何约束，仅要求证书必须有效。为了更加严格，REQUIRE 允许您指定客户端的 X509 证书必须具备某些特征。这些特征通过 REQUIRE 子句中的 ISSUER 或 SUBJECT 选项给出。ISSUER 和 SUBJECT 分别指证书的颁发者和接收者。例如，sampledb 发行版中的 ssl 目录包含一个客户端证书文件 `client-cert.pem`，您可以使用它来测试 SSL 连接。可以使用 openssl 命令显示证书中的颁发者和主题值：

```
% openssl x509 -issuer -subject -noout -in client-cert.pem
issuer=  /C=US/ST=WI/L=Madison/O=sampledb/OU=CA/CN=sampledb
subject=  /C=US/ST=WI/L=Madison/O=sampledb/OU=client/CN=sampledb
```

以下 GRANT 语句指示必须呈现符合这两个值之一的客户端证书的账户：

```
GRANT ALL ON sampledb.* TO 'eladio'@'%.snake.net'
  REQUIRE ISSUER '/C=US/ST=WI/L=Madison/O=sampledb/OU=CA/CN=sampledb'
        AND SUBJECT '/C=US/ST=WI/L=Madison/O=sampledb/OU=client/CN=sampledb';
```

您还可以使用 REQUIRE 来指示连接必须使用特定的密码类型进行加密：

```
GRANT ALL ON sampledb.* TO 'eladio'@'%.snake.net'
  REQUIRE CIPHER 'DHE-RSA-AES256-SHA';
```

若要明确指示不需要安全连接，请使用 REQUIRE NONE。这是创建新账户时的默认设置，但对于移除当前具有 SSL 需求的账户的 SSL 要求也是有用的。

使用 REQUIRE 子句时，需要注意以下一些额外要点：

-   发布要求账户仅使用安全连接的 GRANT 语句，只会为该账户设置约束。它实际上并未提供客户端程序使用该账户安全连接的手段。为了实现这一点，必须配置 MySQL 以包含 SSL 支持，并且必须以特定方式启动服务器和客户端。第 13.3 节“设置安全连接”描述了如何做到这一点。

-   如果您指定账户的连接必须使用 SSL，但服务器或客户端程序都不支持 SSL，则该账户实际上无法使用。

-   REQUIRE 仅用于指示账户*是否必须*使用安全连接。如果服务器和客户端程序配置了 SSL 支持，任何用户仍然*能够*使用安全连接，即使并非必须这样做。

-   对于不通过外部网络连接到服务器的账户，使用 REQUIRE 子句几乎没有意义。此类连接无法被窃听，因此对其进行加密不会带来任何好处，反而会增加计算负载而无益处。此类账户包括那些仅通过 Unix 套接字文件、命名管道、共享内存或 IP 地址 127.0.0.1（主机的环回接口）连接到服务器的账户。这些连接使用主机内部处理的接口，没有流量跨越外部网络。

# 12.4.2.4 启用账户管理权限

您可以通过指定 WITH GRANT OPTION 子句来启用账户将其自身权限授予其他账户。要使用此子句，您本身必须拥有 GRANT OPTION 权限。

授予账户 GRANT OPTION 权限的一个原因是为了启用数据库所有者控制对数据库的访问：授予所有者对数据库的所有权限，包括 GRANT OPTION 权限。例如，如果您希望 alicia 能够从 big-corp.com 域中的任何主机连接，并管理 sales 数据库中所有表的权限，请这样设置账户：

```
CREATE USER 'alice'@'%.big-corp.com' IDENTIFIED BY 'shale';
GRANT ALL ON sales.* TO 'alice'@'%.big-corp.com' WITH GRANT OPTION;
```

实际上，WITH GRANT OPTION 子句使您能够将授予访问权限的权利委托给其他用户。但请注意，拥有 GRANT OPTION 权限的两个用户可以互相授予自己的权限。如果您只授予了一个用户 SELECT 权限，而另一个用户除了 SELECT 外还拥有 GRANT OPTION 权限和其他权限，第二个用户可以使第一个用户变得“更强”。

授予 GRANT OPTION 权限的另一种方法是在 GRANT 语句的开头部分简单列出它：

```
GRANT GRANT OPTION ON sales.* TO 'alice'@'%.big-corp.com';
```

然而，像这样的语句将不会起作用：

```
GRANT ALL, GRANT OPTION ON sales.* TO 'alice'@'%.big-corp.com';
```

在 GRANT 语句中，ALL 只能单独使用，而不能在与列出其他权限说明符的列表中一起使用。

GRANT OPTION 适用于授予层级及其下方所有层级的所有权限，而不是针对个别权限。如果您在给定层级授予账户 GRANT OPTION 权限，该账户可以授予其在该层级拥有的任何权限。您无法指定账户可以授予其在该层级拥有的某些权限而不能授予其他权限。

# 12.4.2.5 限制账户资源消耗

MySQL 权限系统允许您对账户每小时连接服务器的次数、以及账户每小时可以发出的语句或更新数量设置限制。要指定这些限制，请使用 WITH 子句。以下语句设置了一个账户 'spike'@'localhost'，该账户对 sampledb 数据库拥有完全访问权限，但每小时只能连接 10 次，并且每小时只能发出 200 条语句（其中最多 50 条可以是更新）：

```
CREATE USER 'spike'@'localhost' IDENTIFIED BY 'pyrite';
GRANT ALL ON sampledb.* TO 'spike'@'localhost'
  WITH MAX_CONNECTIONS_PER_HOUR 10
       MAX_QUERIES_PER_HOUR 200
       MAX_UPDATES_PER_HOUR 50;
```

每个选项的默认值为零，这意味着“无限制”。这意味着，如果您对账户设置了资源限制，您可以通过将限制值更改为零来移除该限制。例如，要移除 spike 每小时可连接次数的限制，请使用此语句：

```
GRANT USAGE ON *.* TO 'spike'@'localhost'
  WITH MAX_CONNECTIONS_PER_HOUR 0;
```

用户无法通过使用到服务器的多个连接来规避这些限制，因为对于给定账户的所有连接都会一起计算。

从 MySQL 5.0.3 开始，第四种资源限制 MAX_USER_CONNECTIONS 可用于控制账户可以拥有的最大同时连接数。如果限制为零（默认值），则限制由 max_user_connections 系统变量的值控制。非零值将账户限制为相应数量的同时连接。

WITH 子句中资源管理选项的顺序无关紧要。

任何拥有 RELOAD 权限的管理员都可以通过发出 FLUSH USER_RESOURCES 语句来重置当前计数器值。FLUSH PRIVILEGES 也可以做到这一点。计数器重置后，已达到每小时限制的账户可以再次连接并发出语句。如果您对特定账户发出设置该账户限制的 GRANT 语句，也会重置该账户的计数器。

# 12.4.3 显示账户权限

要查看账户拥有什么权限，请使用 SHOW GRANTS 语句：

```
SHOW GRANTS FOR 'sampadm'@'localhost';
```

要查看您自己的权限，请使用以下语句中的任意一个：

```
SHOW GRANTS;
SHOW GRANTS FOR CURRENT_USER();
```

# 12.4.4 撤销权限和移除用户

要剥夺账户的部分或所有权限，请使用 REVOKE 语句。REVOKE 的语法与 GRANT 语句的语法有些相似，只是将 TO 替换为 FROM，并且没有 IDENTIFIED BY、REQUIRE 或 WITH 子句：

GRANT OPTION 权限不包含在 ALL 中。如果您已授予该权限，请在 REVOKE 语句的 *privileges* 部分明确命名以撤销它：

```
REVOKE GRANT OPTION ON sales.* FROM 'alice'@'%.big-corp.com';
```

要撤销权限，您本身必须拥有该权限，并且必须拥有 GRANT OPTION 权限。

要撤销账户在所有层级持有的所有权限，请使用此语句：

```
REVOKE ALL PRIVILEGES, GRANT OPTION FROM account;
```

请注意，此语法中没有 ON 子句。这需要全局 CREATE USER 权限或 mysql 数据库的 UPDATE 权限。

如果您撤销了账户在数据库、表、列或例程层级的所有权限，MySQL 将从 db、tables_priv、columns_priv 或 proc_priv 表中移除相应的账户行。撤销账户的所有全局权限会将 user 表行中的权限列设置为 'N'，但不会删除该行。也就是说，REVOKE 并不会完全删除账户，这意味着用户仍然可以连接服务器。要完全移除账户，请使用 DROP USER 而不是 REVOKE（参见第 12.4.1 节“高级 MySQL 账户管理”）。

有些吊诡的是，有一些撤销操作是通过 GRANT 完成的。例如，如果您指定账户必须使用 SSL 连接，则没有 REVOKE 语法来取消该要求。相反，请发出一个 GRANT 语句，授予全局层级的 USAGE 权限（以保持现有权限不变），并包含 REQUIRE NONE 子句以指示不需要 SSL：

```
GRANT USAGE ON *.* TO account REQUIRE NONE;
```

同样，如果您为用户设置了资源限制，并不是使用 REVOKE 来移除这些限制。相反，使用带有 USAGE 的 GRANT 将限制值设置为零（“无限制”）：

```
GRANT USAGE ON *.* TO account
  WITH MAX_CONNECTIONS_PER_HOUR 0 MAX_QUERIES_PER_HOUR 0 MAX_UPDATES_PER_HOUR 0;
```

# 12.4.5 更改密码或重置丢失的密码

更改或重置账户密码的一种方法是使用 UPDATE 语句，该语句标识账户 user 表行中的 User 和 Host 值，然后刷新权限：

```
mysql> USE mysql;
mysql> UPDATE user SET Password=PASSWORD('silicon')
    -> WHERE User='boris' AND Host='localhost';
mysql> FLUSH PRIVILEGES;
```

然而，使用 SET PASSWORD 更容易，因为您使用与其他账户管理语句相同的格式来命名账户，并且不需要显式刷新权限：

