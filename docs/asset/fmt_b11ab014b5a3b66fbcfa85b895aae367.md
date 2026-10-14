
你可以使用以下命令启动 `postmaster` 程序（确保你仍是 `postgres` 用户）：

```
matthew@seymour:-$ postmaster -D /usr/local/postgresql/data &
```

如果你决定使用 `/usr/local/postgresql/data` 以外的目录作为数据目录，你应该将 `postmaster` 命令行中的目录替换为你正在使用的目录。

> 提示：默认情况下，Ubuntu 将 PostgreSQL 数据目录设置为 `/var/lib/postgresql/data`。这并不是存储数据的极佳位置，因为大多数人在 `/var` 分区中没有足够的空间来存放任何类型的数据存储。请注意，如果你将数据目录更改为其他内容（例如本节示例中的 `/usr/local/postgresql/data`），你需要编辑位于 `/etc/init.d` 中的 PostgreSQL 启动文件（名为 `postgres`）以反映该更改。

## 在 PostgreSQL 中创建数据库

在 PostgreSQL 中创建数据库非常简单，但必须由具有 PostgreSQL 创建数据库权限的用户执行——例如，名为 `postgres` 的初始用户。然后你可以直接从 shell 提示符（不是 `PSQL` 客户端提示符，而是普通的 shell 提示符）使用以下命令：

```
matthew@seymour:-$ su - postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，它使得无需登录并使用 `psql` 就能更容易创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

在在调用 `psql` 时，你需要通过 `psql` 命令行使用 `CREATE DATABASE` 语句来创建数据库，如下：

```
matthew@seymour:-$ psql sampledata
```

如果你在调用 `psql` 时没有指定数据库名称，它将尝试连接到默认数据库。

在 PostgreSQL 中创建用户，方法如下：

```
matthew@seymour:-$ su - postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，它使得无需登录并使用 `psql` 就能更容易创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

在调用 `psql` 时，你需要通过 `psql` 命令行使用 `CREATE DATABASE` 语句来创建数据库，如下：

```
matthew@seymour:-$ psql sampledata
```

如果你在调用 `psql` 时没有指定数据库名称，它将尝试连接到默认数据库。

在 PostgreSQL 中创建用户，方法如下：

```
matthew@seymour:-$ su - postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，它使得无需登录并使用 `psql` 就能更容易创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

在调用 `psql` 时，你需要通过 `psql` 命令行使用 `CREATE DATABASE` 语句来创建数据库，如下：

```
matthew@seymour:-$ psql sampledata
```

如果你在调用 `psql` 时没有指定数据库名称，它将尝试连接到默认数据库。

在 PostgreSQL 中创建用户，方法如下：

```
matthew@seymour:-$ su - postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，它使得无需登录并使用 `psql` 就能更容易创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

在调用 `psql` 时，你需要通过 `psql` 命令行使用 `CREATE DATABASE` 语句来创建数据库，如下：

```
matthew@seymour:-$ psql sampledata
```

如果你在调用 `psql` 时没有指定数据库名称，它将尝试连接到默认数据库。

在 PostgreSQL 中创建用户，方法如下：

```
matthew@seymour:-$ su - postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，它使得无需登录并使用 `psql` 就能更容易创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

在调用 `psql` 时，你需要通过 `psql` 命令行使用 `CREATE DATABASE` 语句来创建数据库，如下：

```
matthew@seymour:-$ psql sampledata
```

如果你在调用 `psql` 时没有指定数据库名称，它将尝试连接到默认数据库。

在 PostgreSQL 中创建用户，方法如下：

```
matthew@seymour:-$ su - postgres
bash-2.05b$ createdb database
```

其中 `database` 是你想要创建的数据库名称。

`createdb` 程序实际上是一个包装器，它使得无需登录并使用 `psql` 就能更容易创建数据库。然而，你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：

```
CREATE DATABASE database;
```

你需要在登录 `psql` 之前创建一个数据库。在登录 `psql` 之后，你可以使用 `CREATE DATABASE` 语句创建数据库。你也可以在 `psql` 内部使用 `CREATE DATABASE` 语句创建数据库。这是一个示例：
