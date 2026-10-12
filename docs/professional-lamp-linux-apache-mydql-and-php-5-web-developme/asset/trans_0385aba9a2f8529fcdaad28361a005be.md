
在某些情况下，可能已经为所有 PHP 脚本启用了输出缓冲和压缩。要确定这一点，请检查配置变量 `output_handler` 的值，或在 `php.ini` 中查看 `output_handler` 和 `zlib.output_compression` 的值。

要在 PHP 中启用输出压缩，请执行以下操作：

1. 如有需要，请在您的机器上安装 zlib 库。
2. 根据需要配置 PHP 源代码，确保包含 `--with-zlib`，然后正常进行`编译/安装`。
3. 修改您的 `php.ini` 使其包含以下行：
   ```ini
   output_buffering = Off
   output_handler =
   zlib.output_compression = On
   ```
4. 重启 Apache 以使新更改生效。

## 在 Apache 中使用 MySQL

到现在为止，您已经使用 Apache 和基本身份验证创建了一个或两个安全区域，对于大多数情况而言，这可能已经足够了。然而，您可能会发现，虽然使用 Apache 进行基本身份验证很简单，但在控制和定制的程度上略显局限。对于许多此类情况，实际上可以将 Apache 基本身份验证与通过 MySQL 的关系数据库的强大功能相结合。为了这一目的，存在 `mod_auth_mysql` Apache 模块。

与标准的 Apache 基本身份验证类似，`mod_auth_mysql` 可以按目录控制访问，并可以在 `.htaccess` 文件和 `httpd.conf` 中的 `<Directory>` 部分内进行配置。与标准的 Apache 基本身份验证不同的是，所有用户凭据都存储在数据库中，而不是平面文件中。

## 设置数据库

安装和配置 `mod_auth_mysql` 涉及几个步骤，其中第一步是创建必要的数据库结构以存储用户数据。首先加载您喜欢的 MySQL 客户端，并创建数据库。例如：

```sql
CREATE DATABASE apacheauth;
```

接下来，创建一个 Apache 用于访问凭据的用户：

```sql
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY 'apachepass';
```

现在数据库用户已经创建，是时候添加一个用于保存登录信息的表了。先从一个仅保存用户名和密码的简单表开始：

```sql
USE apacheauth;
CREATE TABLE user_info (
   user_name varchar(50) NOT NULL,
   user_password varchar(50) NOT NULL,  
   PRIMARY KEY (user_info)
);
```

您可以随意命名表和列。在上面的示例中，使用 `user_info` 作为表名，并使用 `user_name` 和 `user_password` 作为登录名/密码组合，因为这些是 mod_auth_mysql 识别的默认名称。

> 在 mod_auth_mysql 的后续版本中，密码的默认列是 user_password，而不是模块文档中所述的 user_passwd。

接下来，创建一个初始测试用户账户，以便稍后在测试身份验证时使用：

```sql
INSERT INTO user_info (user_name, user_password)  
VALUES ('testuser', SHA1('testpass'));
```

> 请注意，在该语句中对密码使用了 SHA1() 函数，而不是 PASSWORD() 函数。使用 mod_auth_mysql 时，您可以使用几种密码加密方法——本例恰好使用了 SHA1。

## 安装模块

一旦您建立了数据库表，就需要实际下载 mod_auth_mysql 的源代码，可从 http://modauthmysql.sourceforge.net 获取。截至本文撰写之时，当前版本为 2.9.0，因此您需要下载 mod_auth_mysql-2.9.0.tar.gz。

下载模块源代码后，解压该 tar 包：

```bash
tar -xzvf mod_auth_mysql-2.9.0.tar.gz
```

解压 tar 包后，切换目录到新创建的源代码文件夹：

```bash
cd mod_auth_mysql-2.9.0
```

要从下载的源代码构建模块，您实际上将直接使用 Apache 的 apxs 命令。执行以下命令，使用您系统中 apxs 二进文件的路径；此处使用默认的 Apache 位置 /usr/local/apache2/bin：

```bash
/usr/local/apache2/bin/apxs -c -lmysqlclient -lm -lz mod_auth_mysql.c
```

如果构建成功，您应该看到几行编译信息，且没有错误。相反，如果您遇到关于缺少 mysql.h 文件的错误，以及一系列与 MySQL 相关的错误，您可能需要手动指定 MySQL 库和包含文件的路径。使用 MySQL 的默认位置，您的命令可能如下所示：

```bash
/usr/local/apache2/bin/apxs -c -lmysqlclient -lm -lz \
-L /usr/local/mysql/lib/mysql \
-I /usr/local/mysql/include/mysql \
mod_auth_mysql.c
```

要安装新编译的模块，您需要以 root 身份执行以下命令。照常操作，将 `apxs` 的路径更改为指向您的 `apxs` 二进文件：

```bash
/usr/local/apache2/bin/apxs -i mod_auth_mysql.la
```

您需要执行的下一个安装任务是找到在 httpd.conf 中加载模块所需的命令。为此，打开您的 httpd.conf 文件，添加一个合适的位置来插入模块定义——通常在配置文件的末尾，或其他 `LoadModule` 语句旁边——并添加以下内容：

```apache
LoadModule mysql_auth_module modules/mod_auth_mysql.so
```

最后，重启 Apache。

## 配置和使用

一旦您的数据库表准备就绪且模块已安装，剩下的就是告诉 Apache 需要保护什么了。与标准的 Apache 基本身份验证类似，您需要找到一些配置指令，放在 httpd.conf 的 <Directory> 部分中，或者在您可以选择保护的目录中创建一个 .htaccess 文件。

告诉 Apache 针对您的 MySQL 数据库验证用户凭据通常至少涉及以下内容：

```apache
AuthName   "<zone name>"
AuthType   Basic
AuthMySQLDB  dbname
AuthMySQLUser  userid
AuthMySQLPassword  password
AuthMySQLEnable On
require  valid-user
```

这些指令的前两行和最后一行对您来说应该已经熟悉。它们简单地定义了受保护区域的名称、身份验证类型，以及检查资源中找到的任何有效用户均允许访问。其他行告诉 Apache 在哪里查找身份验证信息。您并没有向 Apache 提供包含每个有效用户密码的文件名，而是提供了数据库信息——数据库名称、用户名和密码——以便 `Apache` 和 `mod_auth_mysql` 知道去哪里查找。第六行 `AuthMySQLEnable On` 只是告诉 Apache 实际使用 `mod_auth_mysql`——这是一种在不完全卸载或移除模块的情况下禁用 `MySQL` 身份验证的方法。

要使用您之前创建的身份验证表，您会在 <Directory> 或 .htaccess 定义中添加以下内容：

```apache
AuthName   "MySQLAuth"
AuthType   Basic
AuthMySQLDB  apacheauth
AuthMySQLUser  apache
AuthMySQLPassword  apachepass
AuthMySQLEnable On
AuthMySQLPwEncryption  sha1
require  valid-user
```

在这里，您正在告诉 Apache 和 mod_auth_mysql 针对您的 apacheauth 数据库验证用户。Apache 将使用您之前创建的 apache 账户登录数据库，并且您还在告诉 mod_auth_mysql 在将给定密码与数据库中的值匹配之前，先用 SHA1 对其进行哈希处理。

此时，您应该能够通过 Web 浏览器登录到受保护的区域，提供添加到 user_info 表中的用户凭据 (testuser:testpass)，并成功在该目录中进行身份验证。

虽然本例相当简单且精简，但 mod_auth_mysql 实际上提供了大量的配置选项，因此您可以针对几乎任何情况进行自定义身份验证。以下各节描述了一些配置选项。

### AuthMySQLEnable On | Off

这会启用或禁用 mod_auth_mysql 身份验证，而无需直接从 Apache 中移除或卸载该模块。

### AuthMySQLHost localhost | hostname | ipaddress

这是 MySQL 数据库服务器的主机名或 IP 地址。如果您的环境在不同机器上运行 Apache 和 MySQL，您将需要使用此设置。默认值为 `localhost`，因此同时运行 Apache 和 MySQL 的机器通常可以忽略此设置。

### AuthMySQLPort port_number

这是 MySQL 正在监听的 TCP/IP 端口。MySQL 的默认端口值为 3306，但可以更改。此选项的默认值也是 3306，因此仅当 MySQL 正在非标准端口上监听时才需要指定此选项。

### AuthMySQLSocket socket_file_path

这是在 UNIX 机器上访问 MySQL 所使用的 UNIX 套接字文件。默认值是 `/tmp/mysql.sock`，与 `AuthMySQLPort` 一样，仅在非标准安装中需要使用。

### AuthMySQLUser userid

这是用于访问保存身份验证信息的 MySQL 数据库的用户 ID。大多数数据库系统不允许用户或 Apache 进程在没有正确的 userid/密码组合的情况下访问数据库，因此请将此设置与 `AuthMySQLPassword` 一起设置为具有访问身份验证表的非 root 用户账户。至少，该用户需要对身份验证表具有 `SELECT` 访问权限。

### AuthMySQLPassword password

与 `AuthMySQLUser` 配合使用，此选项指定访问 MySQL 身份验证表的用户账户的密码。

### AuthMySQLDB dbname

这是 MySQL 中保存身份验证表的数据库名称。如果未指定名称，将使用默认值 `test`。

