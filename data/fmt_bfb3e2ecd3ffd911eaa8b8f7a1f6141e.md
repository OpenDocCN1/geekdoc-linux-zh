
> 注意：一旦完成将 IMP 的 "imp-version" 目录重命名为新名称 "imp"，我们将删除该压缩包。

包含定义 `phphlib` 行为的设置，并按照其指令定义你想要使用的存储容器，你需要取消注释：

```
[root@deep1] # cp /home/httpd/horde/phphlib/phphlib.inc /home/httpd/php/local.inc

cp: overwrite /home/httpd/php/local.inc ?
```

编辑 `local.inc` 文件（`vi /home/httpd/php/local.inc`），然后取消注释并设置以下行以将 SQL 设为默认数据库：

```
/ 若要使用 SQL 数据库，请取消注释并编辑以下内容：

var $Host = 'localhost';

var $Database = 'horde';

var $User = 'www';

var $Password = 'some-password';

var $Port = '5432';
```

```
function halt($msg) {

    printf("<b>Database error (HordeDB):%s</b><s>\n", $msg);

}
```

```
class HordeDB extends CT_Sql {

    var $database = 'HordeDB'; // 使用哪个数据库

    var $table = 'active_sessions'; // 并在该表中查找我们的数据。

}
```

不要忘记使用你想要用于 Webmail IMP 的存储容器文件。记住只取消注释一种类型。在我们的情况下，我们选择了使用 SQL。此外，你为 SQL 数据库设置的参数是 `var $User =`、`var $Password =` 和 `var $Port =`。在我们情况下，`var $User =` 对应你的 httpd 用户 "www"，`var $Password =` 对应你在 PostgreSQL 中定义的用户 "www" 的密码，`var $Port =` 是连接到 SQL 数据库的 IP 端口。

第 6

最后编辑 `prepend.php` 文件（`vi /home/httpd/php/prepend.php`）并指定你的默认数据库类型。
编辑 `prepend.php` 将 PostgreSQL 定义为你的数据库类型：

```
require($PHPLIB["libdir"]); // .db_mysql.inc
To read:
require($PHPLIB["libdir"]); // .db_pgsql.inc"
```

# 为 PHP4 配置你的 "php.ini" 配置文件

你需要做的另一个设置是在你的 PHP4 配置文件 "/etc/phpd.ini" 中。此调整是为了定义你想要支持并由 PHP4 自动加载的功能（如 IMAP、PostgreSQL 等）。由于我们决定使用 PostgreSQL 作为数据库，并在 Webmail 软件中使用 IMAP 功能，我们必须在 PHP4 的 "php.ini" 文件中定义它们。

第 1

编辑 `php.ini` 文件（`vi /etc/httpd/php.ini`），并在 Dynamic Extensions（动态扩展）部分下添加你所需的选项。在我们情况下，我们选择了 IMAP 和 PostgreSQL 支持：

```
extension=imap.so ; 为支持 IMAP 添加
```

关于本书的意见和建议应邮寄至 `gmourani@videotron.ca`

```
extension=pgsql.so ; 为支持 PostgreSQL 添加
extension=mysql.so ; 为支持 MySQL 添加
extension=ldap.so ; 为支持 LDAP 添加
```

### 第 2

你必须告诉 "php" 去哪里查找，包括没有绝对路径的文件，还要自动将 phplib/"prepend.php3" 的内容附加到每个文件前面，并关闭魔法引号（magic quotes）。

通过 `/etc/httpd/php.ini` 编辑 `php.ini` 文件并在相关行添加以下参数：

```
magic_quotes_gpc = Off

auto_prepend_file = "/home/httpd/horde/prepend.php3"

include_path      = "/home/httpd/horde/httpd/php"
```

# 配置 Apache 以识别 Webmail IMP

一旦在系统中安装了 Webmail IMP，必须在 Apache 的 "httpd.conf" 文件中添加以下行以定位并使用它。

### 第 1

编辑 `httpd.conf` 文件（通过 `/etc/httpd/conf/httpd.conf`），并在 `<IfModule mod_alias.c>` 和 `</IfModule>` 之间添加以下行：

```
Alias /horde="/home/httpd/horde/"

<Directory "/home/httpd/horde/">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>
```

```
Alias /imp="/home/httpd/imp/"

<Directory "/home/httpd/horde/imp/">

  Options None

  AllowOverride None

  Order allow,deny

  Allow from all

</Directory>
```

你必须重启 Apache Web 服务器使更改生效：
重启 Apache 请使用以下命令：
`[root@$ # /etc/init.d/httpd restart`
`Shutting down http: [ OK ]`
`Starting http: [ OK ]`

# 通过网页浏览器配置 Webmail IMP

配置 Webmail IMP 有多种方法，我们选择的是新的设置引擎 "setup.php"，它让人们能够通过网页浏览器进行配置。

### 第 1

出于安全原因，默认是禁用的，但你可以通过以下方式启用 Webmail IMP：
- 要启用 "setup.php"，请使用以下命令：
`[root@$ # cd /home/httpd/horde/`
`[root@$ # sh setup.php`
为了支持 IMAP，我们选择了 PostgreSQL 启用 "setup.php"：
你的空白配置文件已创建，请通过以下 URL 访问：
- 访问：`http://web-server/setup.php`
由于我们决定使用 PostgreSQL 作为数据库，并在 Webmail 软件中使用 IMAP 功能，我们必须在 PHP4 的 "php.ini" 配置文件中定义它们。

为了支持 IMAP，我们选择了 PostgreSQL 启用 "setup.php"：
你的空白配置文件已创建，请通过以下 URL 访问：
- 访问：`http://web-server/setup.php`

第 2

在此阶段，我们必须验证 Webmail IMP 是否正常工作：
- 当你完成后，禁用 "setup.php"，请使用以下命令：
`[root@$ # cd /home/httpd/horde/`
`[root@$ # sh secure.sh`

第 3

在此阶段，我们通过以下地址验证 Webmail IMP 是否正常工作：
- 访问：`http://web-server/setup.php`

## 软件包

Samba 主页：`http://us1.samba.org/samba/samba.html`
你必须确保下载了：`samba-2.0.6.tar.gz`

# 压缩包

在安装 Samba 之前列出系统文件列表，在安装之后也列出一次，并使用 `diff` 比较它们以找出文件被放置在什么位置。在安装软件后，只需运行 `find * > smb1` 和 `find * > smb2`，然后使用 `diff smb2 > smb` 获取更改内容的列表。

## 编译

解压压缩包 (`tar.gz`)。

```
[root@deep] # cp samba.version.tar.gz /var/tmp

[root@deep] # cd /var/tmp

[root@deep tmp]# # tar xzf samba.version.tar
```

# 配置

移动新的 Samba 目录并进入 "sources" 子目录。

## 步骤 1

编辑 `smbsh.in` (`vi +3 smbwrapper/smbsh.in`) 并修改该行：

```
SMBW_LIBDIR=$SMBW_LIBDIR/@builddir/@smbwrapper
```

修改为：
