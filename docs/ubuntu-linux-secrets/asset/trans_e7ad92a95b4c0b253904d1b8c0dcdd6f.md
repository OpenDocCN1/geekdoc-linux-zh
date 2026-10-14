

## 表 24-5：PostgreSQL 数据库集群文件夹

| 文件夹 | 描述 |
|---|---|
| base | 包含每个已创建数据库的一个文件夹 |
| global | PostgreSQL 的系统表 |
| pg_clog | 事务提交的状态文件 |
| pg_multixact | 用于表锁定的多事务状态信息 |
| pg_subtrans | 子事务状态信息 |
| pg_tblspc | 数据库表的链接 |
| pg_twophase | 两阶段事务提交过程的阶段文件 |
| pg_xlog | 事务日志文件 |

Ubuntu 将 PostgreSQL 系统日志文件放在 /var/log/postgresql 文件夹中。该文件记录了所有对数据库的连接，以及数据库运行时发生的任何系统错误。定期浏览日志文件以检查问题始终是一个好主意。

## 配置服务器

与 MySQL 不同，PostgreSQL 使用多个配置文件来控制 PostgreSQL 服务器行为的不同方面。所有 PostgreSQL 配置文件都位于 /etc/postgresql/8.3/main 文件夹中。配置文件显示在表 24-6 中。

## 表 24-6：PostgreSQL 配置文件

| 文件 | 描述 |
|---|---|
| pg_hba.conf | 定义哪些主机允许连接到服务器以及该主机上的用户应使用什么身份验证方法 |
| pg_ident.conf | 将 PostgreSQL 用户映射到系统用户账户 |
| postgresql.conf | 包含 PostgreSQL 服务器设置 |
| start.conf | 定义 PostgreSQL 在启动时如何启动数据库：手动、自动或禁用 |

postgresql.conf 配置文件控制 PostgreSQL 的每个功能在系统上的行为方式。配置文件由定义每个 PostgreSQL 功能的记录组成。功能记录的格式为

```
featurename = value
```

尽管这是功能记录的默认格式，但等号是可选的。此文件中的第一部分定义了其他配置文件的位置：

```
data_directory = '/var/lib/postgresql/8.3/main'
hba_file = '/etc/postgresql/8.3/main/pg_hba.conf'
ident_file = '/etc/postgresql/8.3/main/pg_ident.conf'
external_pid_file = '/var/run/postgresql/8.3-main.pid'
```

你可以通过编辑 pg_hba.conf 配置文件来限制客户端如何连接到 PostgreSQL 服务器。此文件定义了 PostgreSQL 连接的四个特性：

- 哪些网络主机允许连接到服务器
- 可以从该主机连接的 PostgreSQL 用户账户
- 用户从该主机登录服务器时必须使用的身份验证方法
-经过身份验证的客户端可以从该主机连接的 PostgreSQL 数据库

这是一个相当复杂的访问控制系统，但它在控制数据库用户方面提供了很大的灵活性。不仅可以限制用户，还可以根据他们连接的远程主机限制其访问。

pg_hba.conf 文件中每个记录的格式为

```
connection-type database user network-address login-method options
```

Ubuntu 中默认的 pg_hba.conf 文件定义了四条记录：

```
local all postgres ident sameuser
local all all ident sameuser
host all all 127.0.0.1/32 md5
host all all ::1/128 md5
```

默认情况下，PostgreSQL 允许特殊管理员账户 postgres 和所有其他用户使用 Ubuntu 系统身份验证系统从本地系统连接。sameuser 选项告诉 PostgreSQL 将 PostgreSQL 用户账户映射到连接到服务器的 Ubuntu 登录账户。两种主机连接类型允许本地网络上的所有用户使用 MD5 加密算法连接。

pg_ident.conf 文件允许你将远程用户账户映射到 PostgreSQL 用户账户。默认情况下 Ubuntu 将所有本地用户账户映射到 PostgreSQL 用户账户。如果你想允许远程系统的用户以自己的身份连接，可以将他们的信息添加到此配置文件中。

> 默认的 Ubuntu 配置将 PostgreSQL 服务器绑定到本地主机地址，仅允许 Ubuntu 服务器上的应用程序连接。要允许远程用户连接到 PostgreSQL 服务器，必须修改 postgresql.conf 文件设置：
> 
> listen_addresses = 'localhost'
> 
> 只需使用 Ubuntu 服务器上网络接口的 IP 地址即可允许远程用户连接。pg_hba.conf 配置文件必须设置为允许网络上的主机访问 PostgreSQL 服务器。通过在文件中添加主机条目来实现：
> 
> host all all 192.168.0.0/24 md5
> 
> 这允许 192.168.0 本地子网上的主机用户使用密码身份验证连接到 PostgreSQL 服务器。

## 与服务器交互

PostgreSQL 包为与 PostgreSQL 服务器一起工作提供了一些文件和脚本。表 24-7 显示了在 PostgreSQL 服务器环境中工作时可能有用的文件。

