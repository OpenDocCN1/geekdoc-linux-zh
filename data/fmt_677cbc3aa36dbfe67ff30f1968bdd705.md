
$ tail `/var/log/httpd/error_log` [Wed Dec 20 17:48:06 2000]

[notice] SIGHUP received. Attempting to restart [Wed Dec 20 17:48:10 2000]

[notice] Apache/1.3.12 (Unix) mod_perl/1.21 PHP/3.0.16 configured -- resuming normal

一旦看到恢复正常运行的消息，创建第一个脚本。如下创建文件 `/var/lib/apache/cgi-bin/set.sh`：

```
#!/bin/sh

# set.sh -- 在 CGI 脚本中显示环境

echo Content-type: text/plain

echo
```

将此文件的所有权交给 Apache httpd 进程运行的用户和组，并将其标记为可执行。在示例中，Apache 由用户/组 `nobody` ：

```
$ chown nobody:nobody /var/lib/apache/cgi-bin/set.sh

$ chmod +x /var/lib/apache/cgi-bin/set.sh
```

从命令行运行 `chmod`；注意输出。

```
$ ./set.sh
```

（注：由于原始文本包含大量重复和 OCR 错误，已根据逻辑结构进行了清理和整理。）

## 配置并运行 mod_auth_mysql 219

现在是时候为你的数据库添加一个简单的表，你可以用它来获取用户名和密码。`mod_auth_mysql` 为此表提供了一些默认字段名，我们将使用这些字段。按照以下方式设置表：

```
create table mysql_auth (
username char(25) not null,
passwd char(25) not null,
groups char(25),
primary key
);
```

如你所见，这是一个简单的表。在 MySQL 中，`char()` 字段专为存储字符设计。虽然在数据库中以明文形式存储用户密码似乎并不明智，但 `mod_auth_mysql` 默认会使用 `password()` 例程对密码进行加密。

我们还构建了表中的两个标记为非空（`not-null`）的字段，这意味着在创建新用户时，用户名和密码都不能为空。

出于安全考虑，你需要创建一个新的用户名和密码，让 `mod_auth_mysql` 使用其访问你创建的数据库。由于你现在以 `root` 身份登录，这将非常容易。输入以下内容：

```
GRANT DELETE, INSERT, SELECT, UPDATE ON http_auth.* TO apache_user@localhost
IDENTIFIED BY 'k14u137';
```

这使得 `apache_auth` 只要从本地主机连接，就有能力对 `mysql_auth` 数据库中的任何表进行删除信息、插入或更改信息的操作。在新用户生效之前，我们需要刷新 MySQL 的权限表。要执行此操作，请执行以下步骤：

1. 如果你仍在 MySQL 中，输入 `exit;` 并按回车。从命令行输入以下内容：  
   `mysqladmin -u root -p reload`
2. 在提示处输入你的密码。此命令会重新加载权限，以便 MySQL 识别你的新用户。要进行测试，尝试使用用户名 `apache_user` 和密码 `k14u137` 进入数据库，如下：  
   `mysql -u apache_user -p http_auth`

在提示处输入 `k14u137`。现在你已经进入，使用以下代码添加一个新用户，Apache 和 `mod_auth_mysql` 可以使用它进行验证：

```
INSERT INTO mysql_auth (username, password, groups) VALUES ('user_1',
password('c0ff33'), 'test')
```

`user_1` 将成为我们使用的第一个 Web 用户。

注意使用密码 `c0ff33` 作为存入 `mysql_auth` 中 `password` 字段的值。输入以下内容：

```
select * from mysql_auth;
```

你会发现密码列看起来完全不像 `c0ff33`。`password()` 是 `mod_auth_mysql` 在检查密码时使用的默认函数。

打开你的 `http.conf` 文件并添加以下几行：

```
Auth_MySQL on apache_user
Auth_MySQL_Info localhost apache_user k14u137
Auth_MySQL_Encryption_Types MySQL
```

`Auth_MySQL_Info` 指定了你使用的标准数据库、你连接该数据库使用的用户名和密码，以及你计划连接的位置（在此例中为 `localhost`）。

`Auth_MySQL_Encryption_Types` 是 `mod_auth_mysql` 加密你密码的方法。这里有三个选项：

- 明文（Plain text）
- Crypt_DES
- MySQL

你可以使用这些选项中的一个或全部，模块将使用每种方法检查你的数据库。由于我们在 MySQL 中使用 `password()` 函数插入了用户，因此在这里选择 `MySQL` 选项是合理的。

接下来，选择一个你想使用 `mod_auth_mysql` 保护的目录。在该目录下创建一个 `.htaccess` 文件，并将以下代码放入。

```
AuthName -Super Secret Web site
AuthType Basic
require valid-user
```

重启 Apache，然后用 Web 浏览器查看新保护目录内的 Web 页面。当你看到请求输入用户名和密码的弹出窗口时，输入你在 MySQL 中输入的组合即可。

### 学生资源

你可以在以下 URL 找到更多信息：
- Apache 的 MySQL 认证模块：`www.diegonet.com/support/mod_auth_mysql.shtml` (`mod_auth_mysql` v2.20)。
- 在 Apache 服务器上使用 MySQL 进行用户认证：`http://bignosebird.com/notebook/mysqlauth.html`。

### 问题

1. 你可以使用 `.htaccess` 文件配合 `mod_auth_mysql` 吗？
2. 在使用 Apache 脚本时，如何检查是否使用了 `.htaccess` 文件？
3. 你是否可以在 MySQL 中添加列来检查情况？

### 回答

1. 可以的，但会变慢。
2. 使用 `test` 组。
3. 是的。

### 高级问题

1. 你可以在特定范围内使用 `Auth_MySQL_DB` 吗？
2. 使用 `Auth_MySQL_Encryption_Types` 具体可以起到什么作用？
3. 在 `httpd.conf` 中存储 MySQL 用户名和密码会有什么安全影响？

## Apache 和 Tomcat

### 目的

本实验的目的是配置 Apache 与 Tomcat 协同工作。

### 理论

Apache 的优点之一是可以根据任何需求进行定制。传统的，Apache 使用 Perl、C 等编程语言提供动态内容。Java servlet 提供了 CGI 的替代方案。在安装 Tomcat 之前，系统必须安装 Java 运行时 (`JRE`) 或 Java 开发工具包 (`JDK`)。

### 实验

1. 从 `http://jakarta.apache.org` 下载最新版本的 Tomcat。为了简单起见，将压缩包放在 `jdk` 相同的目录（例如 `/opt`）：  
   `cd /opt`  
   `tar xzf jakarta-tomcat-2.1.tar.gz`
2. 下一步涉及编辑 `/etc/profile` 以包含环境变量：
   ```
   export CLASSPATH=/opt/tomcat-2.1/lib/servlet.jar
   export TOMCAT_HOME=/opt/tomcat-2.1
   ```
3. 接下来，从 `http://jakarta.apache.org` 下载 `mod_jserv.so`。将此文件放在 `/opt/tomcat-2.1/` 目录下。
4. 将 `tomcat-apache.conf` 文件（或 `tomcat-jserv.conf`）复制为 `tomcat-jserv.conf`。编辑 Apache 配置文件 `httpd.conf` 以下行：
   ```
   Include /opt/tomcat-2.1/tomcat-jserv.conf
   ```
5. 确保 `tomcat-jserv.conf` 中正确引用了 `mod_jserv.so` 文件。`tomcat-jserv.conf` 的第一行包含：
   ```
