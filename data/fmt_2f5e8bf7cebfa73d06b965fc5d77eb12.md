
`Satisfy all` 指令告知 Apache 仅允许通过身份验证和授权测试的用户访问。当 AOL 用户通过 AOL 连接到 `http://your_server/aolbuddies/` 时，系统会提示用户输入用户名和密码。如果用户输入属于 `aolbuddies` 组的用户名且用户密码正确，则允许用户访问。

> **注意** 你必须将所有你的 AOL 好友添加为 `/path/to/.myusers.pwd` 中的用户，并在 `/path/to/.mygroups` 中创建一个名为 `aolbuddies` 的组，该组中列出所有 AOL 好友（你之前添加的 `/path/to/.aol` 中的用户）。

### 使用关系数据库进行身份验证

如果你在网络（甚至 Web 服务器）上运行关系数据库服务器，并且有大量的用户（即超过 1,000 名用户）需要通过 Web 进行身份验证，你可以使用数据库服务器替代前文讨论的基于文本文件的（`mod_auth`）身份验证。使用数据库服务器处理大量用户有几个优点；主要优点如下：

- 当大量用户存储在文本文件中时，`mod_auth` 身份验证会变得非常缓慢。
- 如果你允许用户通过 Web 使用自定义应用程序更改密码，文本文件是不安全的，因为你必须确保对文件的写访问正确地加锁和解锁。将数据存储在数据库服务器中消除了脚本中的这种额外负担，并提供了更好的整体数据完整性。

在关系数据库中，你可以存储大量关于用户的信息，这些信息可以被你的 Web 应用程序使用。因此，使用 `MySQL` 等数据库服务器集中用户数据库对长期来看是有意义的。

### 注意事项

你可以使用大多数现代关系数据库服务器（如 `MySQL`、`Postgres`、`DB2`、`Oracle` 和 `Microsoft SQL`）作为用户数据库。安装这些数据库服务器中的任何一个超出了本书的范围。我假设你已经在你的网络或 Web 服务器上安装了这些数据库服务器之一。

### 提示

对于拥有许多用户的网站，你可能希望创建一个专用的数据库服务器，使其在你的 Web 网络上可访问。理想情况下，数据库服务器应通过后端网络而不是互联网进行访问。大多数情况下，最好在每台服务器系统上有一个额外的以太网接口，并创建一个仅局域网内的服务器可访问的 `LAN`。（有关如何创建此类网络的详细信息，请参阅第 23 章。）

### 使用 `MySQL` 数据库服务器进行身份验证

`MySQL` 是开源社区中最广泛使用的免费数据库服务器；它在 GNU 公共许可下可用。安装和设置你的服务器作为用户身份验证数据库服务器非常容易。使用 Linux 平台，你可以简单地下载并安装服务器、客户端和开发 `RPM` 包，几分钟内即可就绪！`MySQL` 服务器可在 `www.mysql.com` 下载。

### 在 `MySQL` 服务器中创建用户身份验证数据库

要将 `MySQL` 服务器用作身份验证数据库，你需要在数据库中的表中至少包含用户名和密码信息。如果你已经有了包含此类信息的现有数据库表，则无需遵循此处给出的步骤。

1. 使用 `mysql -u root -p` 命令登录到 `MySQL` 服务器。你将需要输入数据库的 `root` 密码。

### 警告

`MySQL` 服务器的 `root` 密码应始终与你的 Unix 系统上的 `root` 密码不同。它们服务于不同的目的，因此应保持分开。

2. 登录到 `MySQL` 后，运行 `create database auth;` 命令，这将创建一个名为 `auth` 的数据库。

## 创建数据库和表

3. 使用以下命令将当前数据库切换到新创建的 `auth` 数据库：

   ```sql
   use auth;
   ```

4. 现在，在 `MySQL` 命令提示符中输入以下行来创建一个名为 `wwwusers` 的表。

   ```sql
   create table wwwusers (
   username varchar(40) not null primary key,
   passwd varchar(20) not null
   );
   ```

   该表中的每一行由三个字段组成：`username`、`passwd` 和 `groups`。`username` 字段是主键，这意味着 `MySQL` 使用此字段对表进行索引，使得使用 `username` 进行的查找非常快。该字段限制为 40 个字符。使用 `varchar`（可变字符）而不是固定 `char` 类型，如果用户名并非总是 40 个字符，可以节省空间。由于该字段也是主键，因此 `username` 字段不能为空（即不能为空值）。密码字段称为 `passwd`，其长度最大为 20 个字符，类型为 `varchar`。它不能为空。

5. 现在输入 `describe wwwusers;` 命令，应显示以下输出：

   ```text
   mysql> describe wwwusers;
   +----+-----+------+-----+---------+-------+
   | Field | Type | Null | Key | Default | Extra |
   +----+-----+------+-----+---------+-------+
   | username | varchar(40) | | PRI | | |
   | passwd | varchar(20) | | | | |
   +----+-----+------+-----+---------+-------+
   2 rows in set (0.00 sec)
   ```

   这是对表 `wwwusers` 已按预期创建的事实进行验证。

6. 现在您需要向表中添加用户。若要手动添加用户，您需要运行以下 SQL 语句：

   ```sql
   insert into wwwusers (username , passwd)
   values ('user_name',
   'user_password');
   ```

   例如：

   ```sql
   insert into wwwusers (username , passwd)
   values ('esmith', 'sale007');
   ```

   这里添加了一个名为 `esmith` 的用户，密码为 `sale007`，属于 `sales` 组。您可以添加任意数量的用户。有关如何使用实用脚本管理用户的详细信息，请参见 [在任意 RDBM 中管理用户和组](https://www.example.org/managing_users)。

7. 如果您计划使用用户组进行身份验证，请创建以下表。

   ```sql
   create table wwwgroups ( username  varchar(40), groupname  varchar(40) );
   ```

8. 现在输入 `describe wwwgroups;` 命令，应显示以下输出：

   ```text
   +------------+------------+------+-----+--------+
   | Field      | Type       | Null | Key | Default |
   +------------+------------+------+-----+--------+
   | username   | varchar(40)| YES  |     | NULL   |
   | groupname  | varchar(40)| YES  |     | NULL   |
   +------------+------------+------+-----+--------+
   2 rows in set (0.00 sec)
   ```

   这是对表 `wwwgroups` 已按预期创建的事实进行验证。

9. 您可以使用以下 SQL 语句将现有用户添加到新组中：

   ```sql
   insert into wwwgroups (username , groupname)
      values ('user_name',
              'name_of_the_group'
      );
   ```

   例如：

   ```sql
   insert into wwwgroups (username , groupname)
      values ('kabir',
              'www_wheel'
      );
   ```

   这将用户 `Kabir` 添加到一个名为 `www_wheel` 的新组中。请注意，您可以将同一用户添加到多个组中。

## 授予 Apache 服务器访问 MySQL 中的用户身份验证数据库

与大多数现代 `RDBM` 服务器一样，`MySQL` 自身使用基于用户名和密码的身份验证来允许访问其存储的数据库。因此，在使用 `Apache` 配合 `MySQL` 之前，您应该创建一个名为 `httpd` 的 `MySQL` 用户，该用户应能访问您计划与 `Apache` 一起使用的任何数据库。以下是如何为 `Apache` 创建 `MySQL` 用户：

1. 使用 `mysql -u root -p` 命令登录到 `MySQL` 服务器。系统会提示您输入数据库的 `root` 密码。

2. 登录 `MySQL` 后，您可以发出如下 `grant` 语句：

   ```sql
   grant all privileges on name_of_database
   to username@hostname identified by 'user_password'
   with GRANT option;
   ```

   例如，要授予名为 `httpd` 的用户（即 `httpd.conf` 文件中 `user` 指令指定的用户名）对名为 `auth` 的数据库的所有权限，当使用 `2manyscrets` 密码从 `localhost` 连接时，请运行：

   ```sql
   grant all privileges on auth
       to httpd@localhost identified by '2manyscrets'
       with GRANT option;
   ```

   这允许 `httpd` 用户从 `localhost` 访问 `auth` 数据库。此操作假设 `MySQL` 服务器和 `Apache` 服务器运行在同一台机器上。如果数据库位于另一台机器上，您应使用相应的主机名替换 `localhost`。

   如果您不打算添加需要向用户身份验证数据库写入的 Web 应用程序，请勿授予 Web 服务器用户 `all privileges`。例如，如果您只是想验证用户身份，但从不通过 Web 服务器（即使用 CGI 脚本或其他 Web 应用程序）更新或删除用户，请将 `all privileges` 替换为 `select`。这确保 Web 服务器用户仅允许对数据库执行 `select` 查询，相当于只读访问。

3. 输入 `flush privileges` 命令，指示 `MySQL` 服务器重新加载授权表。

4. 现在您应该通过输入 `exit` 退出 `MySQL` 监控程序。

现在，通过输入 `mysql -u httpd -p` 命令并提供适当的密码（在此情况下为 `2manysecrets`）登录 `MySQL`。在 `mysql>` 提示符下，您应该能够通过输入 `use auth;` 访问数据库 `auth`。如果您无法访问数据库，请确保您位于早期发出的 `grant` 语句中指定的主机上。

## 编译和安装 mod_auth_mysql 模块

`MySQL` 数据库服务器在开源社区中的良好声誉促成了一个名为 `mod_auth_mysql` 的 `Apache` 模块的开发。该模块可用于与 `MySQL` 服务器接口以进行身份验证。您可以从 `www.mysql.com/Downloads/Contrib/` 下载此模块的最新版本。以下是如何编译和安装 `mod_auth_mysql`。

1. 以 `root` 身份在 `/usr/local/src` 目录中提取 `mod_auth_mysql` 源代码发行版。这将创建一个名为 `mod_auth_mysql-version` 的新子目录。切换到该目录并运行：

   ```bash
   ./configure --with-apache=/usr/local/src/apache_version
       --with-mysql=/usr
   ```

   请务必将 `/usr/local/src/apache_version` 更改为 `Apache` 源代码发行版的路径，并将 `/usr` 更改为 `MySQL` 头文件安装的路径。如果您使用默认配置安装了 `MySQL`，头文件安装在 `/usr/local/mysql`，并且提供 `--with-mysql=/usr` 是正确的值，因为 `mod_auth_mysql` 脚本通过将 `/local/mysql` 附加到 `/usr` 来生成 `/usr/local/mysql`。

2. 运行 `make`，然后切换到 `Apache` 源代码发行版目录，并运行 `./config.status --activate-module=src/modules/auth_mysql/libauth_mysql.a`（如果您已经编译了 `Apache`）或 `./configure --activate-module=src/modules/auth_mysql/libauth_mysql.a --prefix=/usr/local/apache`（如果您第一次编译 `Apache`）。

3. 最后，运行 `make && make install` 来编译并安装带有 `mod_auth_mysql` 支持的 `Apache`。

4. 现在使用 `/usr/local/apache/bin/apachectl restart` 命令重启 `Apache` 服务器。

### 使用 mod_auth_mysql 模块对用户进行身份验证

在您编译并安装了 `mod_auth_mysql`，创建了包含用户和组表的数据库，并且为 `Apache` 创建了访问这些表的数据库级用户之后，您可以按如下方式配置 `Apache`：

1. 在 `httpd.conf` 中，在任何 `<VirtualHost>` 或其他类型的容器（如 `<Directory>`、`<Location>` 等）外部添加以下行。

   ```apache
   Auth_MySQL_Info db_hostname db_username db_password
   Auth_MySQL_General_DB database_name
   ```

   第一个指令告诉 `Apache` 使用哪个数据库用户名和密码连接哪个数据库服务器。数据库用户名和密码是在 `MySQL` 中创建的。此用户名密码对必须与您系统上的任何交互式用户账户不匹配。

   第二个指令说明要连接哪个数据库。如果您使用单个数据库来满足所有用户身份验证需求，可以在此处直接设置数据库名称。这样可以避免在每个身份验证配置段中重复输入数据库名称。

2. 若要要求对文档根目录下名为 `protected_dir` 的子目录进行身份验证，您可以在 `httpd.conf` 中创建 `<Directory>` 或 `<Location>` 容器，或者使用 `.htaccess` 文件（假设您已在 `httpd.conf` 中将 `AllowOverride AuthConf` 设置为主服务器或适当的虚拟主机），使其具有以下配置段：

   ```apache
   AuthName "Members Only"
   AuthType Basic
   require valid-user
   Auth_MySQL on
   ```

   ```apache
   Auth_MySQL_DB database_name
   Auth_MySQL_Password_Table password_table_name
   Auth_MySQL_Username_Field username_field_name
   Auth_MySQL_Password_Field password_field_name
   Auth_MySQL_Group_Table group_table_name
   Auth_MySQL_Group_Field group_field_name
   Auth_MySQL_Empty_Passwords off
   Auth_MySQL_Encrypted_Passwords on
   Auth_MySQL_Encryption_Types Crypt_DES
   Auth_MySQL_Scrambled_Passwords off
   Auth_MySQL_Authoritative on
   Auth_MySQL_Non_Persistent off
   ```
