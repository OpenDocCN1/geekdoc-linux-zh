
| `SHOW VIEW` | 使用 `SHOW CREATE VIEW` 查看视图定义 |

| `TRIGGER` | 创建或删除触发器 |

| `UPDATE` | 修改表行 |

**表 12.5 杂项权限**

| 权限名称 | 权限启用操作 |

|---|---|

| `ALL` (`[PRIVILEGES]`) | 所有操作（`GRANT` 除外） |

| `USAGE` | 一种特殊的“无权限”权限 |

表 12.3 中显示的权限是管理权限。通常，您会谨慎地授予这些权限，因为它们允许用户影响服务器的运行。（例如，`SHUTDOWN` 权限不是您应该日常随意分配的。）表 12.4 中的权限适用于数据库、表、列和存储例程。它们控制对服务器管理数据的访问。表 12.5 中的权限说明符是特殊的。`ALL` 意味着“所有权限”（但不包括 `GRANT OPTION` 权限）。`USAGE` 意味着“无权限”。即，“创建账户，但不授予任何权限”。`USAGE` 还可以用于修改现有账户的非权限相关方面，而不改变其当前权限。（参见 12.4.2.2 节，“使用‘无权限’ `USAGE` 权限”。）

`CREATE VIEW` 和 `SHOW VIEW` 是在 MySQL 5.0.1 中引入的。`ALTER ROUTINE`、`CREATE ROUTINE` 和 `CREATE USER` 是在 MySQL 5.0.3 中引入的，这也是 `EXECUTE` 权限开始生效的版本。`EVENT` 和 `TRIGGER` 是在 MySQL 5.1.6 中引入的。（在 5.1.6 之前，操作触发器需要 `SUPER` 而不是 `TRIGGER` 权限。）

## 12.4 管理 MySQL 用户账户

表 12.3 中的权限属于管理性质，除 `GRANT` 外，只能使用 `ON *.*` 全局权限指定符进行授予。例如，`RELOAD` 权限允许使用 `FLUSH`，因此以下语句创建了一个名为 `flush` 的用户，该用户除了发出 `FLUSH` 语句外什么也做不了：

```sql
CREATE USER 'flush'@'localhost' IDENTIFIED BY 'flushpass';
GRANT RELOAD ON *.* TO 'flush'@'localhost';
```

这种类型的 MySQL 账户对于编写执行日志文件维护等操作（如刷新日志）的管理脚本非常有用（参见第 12.5.7 节，“日志管理”）。

数据库级权限适用于特定的数据库及其中的所有对象。要在此级别授予权限，请使用 `ON db_name.*` 子句：

```sql
CREATE USER 'bill'@'racer.snake.net' IDENTIFIED BY 'rock';
GRANT ALL ON sampdb.* TO 'bill'@'racer.snake.net';
```

```sql
CREATE USER 'reader'@'%' IDENTIFIED BY 'dirt';
GRANT SELECT ON managerie.* TO 'reader'@'%';
```

第一组语句授予 `bill` 在从 `racer.snake.net` 连接时，对 `sampdb` 数据库中任何表的完整权限。第二个语句创建了一个名为 `reader` 的受限访问用户，该用户可以从任何主机连接到 `managerie` 数据库以访问其中的任何表，但仅限于使用 `SELECT` 语句。也就是说，`reader` 是一个“只读”用户。

你可以列出多个要授予的权限，中间用逗号分隔。例如，若要授予用户对 `sampdb` 数据库中现有表的内容进行读取和修改的能力，但不允许创建新表或删除表，则不要授予数据库的 `ALL` 权限。相反，只需指定要启用的具体权限：

```sql
CREATE USER 'jennie'@'%' IDENTIFIED BY 'boron';
GRANT SELECT,INSERT,DELETE,UPDATE ON sampdb.* TO 'jennie'@'%';
```

为了实现比数据库级别更细粒度的访问控制，你可以针对单个表甚至表中的单个列授予权限。列级特定权限在你想向用户隐藏表的某些部分，或者希望用户只能修改特定列时非常有用。假设有人自愿在历史联盟（Historical League）担任办公室助理帮助你。这是个好消息，但你决定先授予你的新助理对包含会员信息的 `member` 表的只读访问权限，以及该表中与到期日地址相关列的列级 `UPDATE` 权限。这样，你的助理将仅拥有写入权限，用于执行更新会员续费到期日及更改地址等较为简单的任务。设置此 MySQL 账户所需的语句如下：

```sql
CREATE USER 'assistant'@'localhost' IDENTIFIED BY 'officehelp';
GRANT SELECT, UPDATE (expiration,street,street_city,state,zip)
ON sampdb.member TO 'assistant'@'localhost';
```

该 `GRANT` 语句授予对整个 `member` 表的读取访问权限（因为 `SELECT` 后面没有列列表），并仅授予在 `UPDATE` 权限关键字后括号内命名的列的更新访问权限。

若要在 `GRANT` 语句中为多个权限授予列级权限，括号内的列列表必须紧跟在每个权限名称之后。

如果在 `GRANT` 语句中引用数据库、表或列名，请将其作为标识符引用，而不是作为字符串引用。例如：

```sql
GRANT SELECT, UPDATE (`expiration`, `street`, `city`, `state`, `zip`)
ON `sampdb`.`member` TO `assistant`@`localhost`;
```

授权表中的行不会“跟随”数据库对象的改名操作。例如，如果你重命名了某个表或列，针对该表或列的权限将不再适用。

### 12.4.4.2.2 使用“无权限” USAGE 权限

特殊的 `USAGE` 权限指定符意味着“无权限”。乍一看这可能似乎没什么用，但它确实有用。它允许你更改账户的某些特征（即与权限无关的特征），同时保留现有权限不变。若要使用它，请在全球级别授予 `USAGE` 权限，指定账户名称，并提供账户新的非权限特征。例如，如果你想更改账户密码，要求用户必须使用 SSL 连接，或者在不影响账户所持权限的情况下对账户施加连接限制，请使用类似这样的语句：

```sql
GRANT USAGE ON *.* TO account IDENTIFIED BY `new_password`;
GRANT USAGE ON *.* TO account REQUIRE SSL;
GRANT USAGE ON *.* TO account WITH MAX_CONNECTIONS_PER_HOUR 10;
```

### 12.4.4.2.3 要求账户使用安全连接

MySQL 允许客户端使用 SSL（Secure Sockets Layer）协议建立安全连接，该协议会对客户端与服务器之间的数据流进行加密，以防止数据以明文形式传输。此外，X509 可作为客户端通过 SSL 连接提供身份信息的一种手段。安全连接提供了额外的保护，但代价是需要额外的 CPU 周期来执行加密和解密。

若要指定安全连接的要求，请使用 `REQUIRE` 子句。若要仅要求用户通过 SSL 连接，而不具体指定用户必须建立的安全连接类型，请使用 `REQUIRE SSL`：

```sql
CREATE USER 'eladio'@'%.snake.net' IDENTIFIED BY `flint`;
GRANT ALL ON sampdb.* TO 'eladio'@'%.snake.net' REQUIRE SSL;
```

为了更严格，你可以要求客户端出示有效的 X509 证书：

# 12.4.2.3 REQUIRE

`REQUIRE X509` 对证书的内容没有施加任何约束，仅要求证书必须有效。为了更加严格，`REQUIRE` 允许您指定客户端的 X509 证书必须具备某些特征。这些特征通过 `REQUIRE` 子句中的 `ISSUER` 或 `SUBJECT` 选项给出。`ISSUER` 和 `SUBJECT` 分别指证书的颁发者和接收者。例如，sampledb 发行版中的 ssl 目录包含一个客户端证书文件 `client-cert.pem`，您可以使用它来测试 SSL 连接。可以使用 `openssl` 命令显示证书中的颁发者和主题值：

```
% openssl x509 -issuer -subject -noout -in client-cert.pem
issuer=  /C=US/ST=WI/L=Madison/O=sampledb/OU=CA/CN=sampledb
subject=  /C=US/ST=WI/L=Madison/O=sampledb/OU=client/CN=sampledb
```

以下 `GRANT` 语句指示必须呈现符合这两个值之一的客户端证书的账户：
