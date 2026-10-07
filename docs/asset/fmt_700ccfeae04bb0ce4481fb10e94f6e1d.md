
- 2) FQDN（完全限定域名）
- 3) CentOS 服务器
- 4) Ubuntu 服务器
- 5) 服务器的 Root 权限

# 在 CENTOS 中配置 WEBMIN

## 步骤 1

在 `/etc/yum.repos.d/` 中创建一个仓库文件，因为 webmin 不在 CentOS 系统官方仓库中

```
=>sudo vim /etc/yum.repos.d/webmin.repo
```

```
[webmin]
baseurl = http://download.webmin.com/download/yum
mirrorlist=http://download.webmin.com/download/yum/
mirrorlist
enabled=1
gpgcheck=0
```

## 步骤 2

使用 `yum` 命令安装包

```
=>sudo yum install webmin
```

## 步骤 3

安装成功后，它将向你显示消息以及访问 Web 界面的 URL

```
操作系统为 CentOS Linux
正在安装：webmin-1.930-1.noarch 3/3
Webmin 安装完成。你现在可以使用 root 用户和你的 root 密码登录 https://localhost.localdomain:10000/
正在验证：webmin-1.930-1.noarch 1/3
正在验证：perl-EnCode-Detect-1.01-13.el17.x86_64 2/3
正在验证：perl-Net-SSLeay-1.55-6.el17.x86_64 3/3
```

已安装：

`webmin.noarch 0:1.930-1`

## 步骤 4

在 webmin 中使用 root 用户和密码登录

![](img/5e8a2bb431e5309eb9c40e886b58672b_477_0.png)

# 硬件监控

你可以在网页的硬件部分监控硬件负载

# Tanvir Rahman

![](img/5e8a2bb431e5309eb9c40e886b58672b_478_0.png)

# 登录与身份验证

| 登录和身份验证选项 | |
| :--- | :--- |
| 允许密码登录？ | * 是 否 |
| 允许空密码登录？ | * 是 否 |
| 允许 root 登录？ | 是 |
| 允许 RSA (SSH 1) 身份验证？ | * 是 否 |
| 允许 RSA (SSH 2) 身份验证？ | * 是 否 |
| 检查密钥文件的权限？ | * 是 否 |
| 登录时显示 acl？ | * 是 否 |
| 忽略 user-hosts 文件？ | * 是 否 |
| 登录前消息文件 | 无 |
| 用户授权密钥文件 | * 默认 (~/.ssh/authorized_keys) |
| 每个连接的最大登录尝试次数 | * 默认 (6) |
| 使用挑战-响应身份验证？ | * 是 否 |
| 忽略文件？ | * 是 否 |

# 带宽监控与控制

你可以使用带宽监控工具控制不同网络接口的带宽，这是一个对于控制服务器带宽非常实用的工具。

![](img/5e8a2bb431e5309eb9c40e886b58672b_479_0.png)

# 在 UBUNTU 中配置 WEBMIN

## 步骤 1

添加 gpg 密钥和仓库

```
wget -qO- http://www.webmin.com/webmin-key.asc | sudo apt-key add
```

```
sudo add-apt-repository "deb http://download.webmin.com/download repo contrib"
```

## 步骤 2

使用 `apt` 命令安装包

```
sudo apt install webmin
```

## 步骤 3

安装成功后，它将向你显示消息以及访问 Web 界面的 URL

# 通过 FQDN 访问 WEBMIN

我们需要在 apache 配置中设置虚拟主机，以便通过域名访问网站。（此处方法提供了 apache 服务器配置）

假设我们的域名为：`example.com`

## 步骤 1

在 apache 配置中创建虚拟主机 =>`/apache2/sites-available/example.com`

## 步骤 2

添加此配置

```
<VirtualHost *:80>
ServerAdmin example.com
ServerName example.com
ProxyPass http://localhost:10000/
ProxyPassReverse http://localhost:10000/
</VirtualHost>
```

## 步骤 3

更改防火墙规则

```
sudo ufw allow any to any port 10000 tcp
```

## 步骤 4

为了安全将 ssl 设置为 0

```
=>vim /etc/webmin/miniserv.conf
ssl=0
```

## 步骤 5

将此域名添加到允许列表

```
=>vim /etc/webmin/config
allowers=example.com
```

## 步骤 6

重启 webmin 服务和 apache 服务应用更改

```
=>systemctl restart webmin
=>systemctl restart apache2
```

现在可以通过 FQDN 访问 webmin

# 数据库服务器

数据库是以非常有组织的方式存储在计算机中的应用程序，几乎所有的 Web 应用都使用某种数据库。数据库分为 SQL、NoSQL。SQL数据库使用 SQL 来查询、更新、存储和删除数据。

SQL数据库有

- MariaDB
- PostgreSQL
- MS SQL
- SQLite

NoSQL数据库有

- MongoDB
- Redis
- LMDB
- CouchDB
- Cassandra

我们将讨论 MariaDB 的安装和配置

# CENTOS & UBUNTU 中的 MARIADB 服务器安装与配置

## 步骤 1

更新仓库并安装 mariadb 服务器，设置为开机自启

- [centos]

```
=>yum update && yum install mariadb-server -y
=>systemctl enable mariadb
=>systemctl restart mariadb
```

- [ubuntu]

```
=>apt update && apt install mariadb-server mariadb-client -y
=>systemctl enable mariadb
=>systemctl restart mariadb
```

## 步骤 2

对于生产环境你必须加固安全性。为了做到这一点，你需要执行此命令

```
mysql_secure_installation
```

```
[root@localhost ~]# mysql_secure_installation
```

注意：为了安全地登录 MariaDB，我们需要 root 用户的当前密码。如果你刚刚安装 MariaDB 尚未设置 root 密码，密码将为空，此时你直接回车即可。

- 匿名用户？[Y/n] Y ... 成功
- 通常情况下，root 只允许从 'localhost' 连接。这确保了没有人能从网络猜测 root 密码。
- 禁止远程登录 root？[Y/n] Y ... 成功
- 默认情况下，MariaDB 自带一个名为 'test' 的数据库，任何人都可以访问。这也是为了测试设计的，在移动到生产环境之前应该删除。
- 删除测试数据库及其访问权限？[Y/n] Y

Tanvir Rahman

你必须输入 root 登录密码并对其进行配置。

### 第 4 步

全部完成！如果你已经完成了上述所有步骤，你的 MariaDB 安装现在应该是安全的。

感谢使用 MariaDB！

安装成功后将将此此消息。

### 第 5 步

```
使用 root 密码登录
=>mysql -u root -p
```

## 在数据库中创建用户

我们将在 mariadb 中创建一个数据库和一个用户，并授予该数据库的所有权限。

```
database 'testdb';create
=>create database testdb;
```

```
MariaDB [(none)] create database testdb;
Query OK, 1 row affected (0.00 sec)
```

```
=>create user 'testuer'@localhost identified by 'password';
```

```
MariaDB [(none)] create user 'testuer'@localhost identified by 'password';
Query OK, 0 rows affected (0.00 sec)
```

```
MariaDB [(none)] grant all on testdn.* to 'testuer' identified by 'password';
Query OK, 0 rows affected (0.00 sec)
```

```
=>grant all on testdb.* 'testuer'identified by 'password';
```

```
MariaDB [(none)] grant all on testdb.* to 'testuer' identified by 'password';
Query OK, 0 rows affected (0.01 sec)
```

Tanvir Rahman

使用用户登录

```
=> mysql -u testuser -p
password: password
```

创建表

```
=>use testdb;
=>create table test(name VARCHAR(100) NOT NULL,id INT NULL);
```

```
MariaDB [(none)]> use testdb;
Database changed
MariaDB [testdb]> create table test(name VARCHAR(100) NOT NULL, id INT NOT NULL);
Query OK, 0 rows affected (0.02 sec)
```

显示表

```
=>describe test;
```

```
MariaDB [testdb]> describe test;
+------------------------------------------------------+
| Field | Type | Null | Key | Default | Extra |
+------+------+------+------+----------+ 
| name | varchar(100) | NO | | NULL | | |
| id | int(11) | NO | | NULL | | |
+------------------------------------------------------+
2 rows in set (0.01 sec)
```

## MARIADB 中的密码恢复

### 第 1 步

首先停止 mariadb 服务

```
=>systemctl stop mariadb
```

### 第 2 步

```
=>mysqld_safe -skip-grant-tables &
```

```
[root@localhost]# 190929 12:41:04 mysqld safe sudo systemctl stop mariadb
[root@localhost]# mysqld_safe --skip-grant-tables &
[1] 61842
[root@localhost]# 190929 12:41:04 mysqld safe Logging to '/var/log/mariadb/mariadb.log'
190929 12:41:04 mysqld_safe Starting mysqld daemon with databases from /var/lib/mysql
```

### 第 3 步

不带任何密码以 root 用户登录

```
=>mysql -u root
```

```
[root@localhost ~] mysql -u root
Welcome to the MariaDB monitor. Commands end with; or \g.
Your MariaDB connection id is 1
Server version: 5.5.60-MariaDB MariaDB Server
Copyright (c) 2000, Oracle, MariaDB Corporation Ab and others.
Type '\help' or '\h' for help. Type '\c' to clear the current input stream.
MariaDB [(none]> mysql;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A
Database changed
```

### 第 4 步

使用 mysql 数据库再次设置密码

```
=>use mysql
=>update user SET PASSWORD=PASSWORD('your_password')
WHERE USER='root';
```

```
MariaDB [mysql]
MariaDB [mysql]> update user SET PASSWORD=PASSWORD('open12345') WHERE USER='root'
Query OK, 3 rows affected (0.01 sec)
Rows matched: 3 Changed: 3 Warnings: 0
MariaDB [mysql]> flush privileges;
Query OK, 0 rows affected (0.00 sec)
MariaDB [mysql]>
```

UBUNTU $ CENTOS 管理员

### 第 5 步

启动服务并使用新密码登录

```
=>systemctl start mariadb
=>mysql -u root -p <new_password>
```

```
[root@localhost ~]# sudo systemctl start mariadb
[root@localhost ~]# mysql -u root -p
Enter password:
Welcome to the MariaDB monitor. Commands end with; or \g.
Your MariaDB connection id is 3
Server version: 5.5.60-MariaDB MariaDB Server
```

```
> Copyright (c) 2000, 2018, Oracle, MariaDB Corporation Ab and others.
Type 'help'; or '\h' for help. Type '\c' to clear the current input statement.
```

```
MariaDB [(none)]
MariaDB [(none)]
MariaDB [(none)]
MariaDB [(none)]
```

## IPA 服务器

IPA 服务器是一个集成的安全信息管理解决方案，结合了：

- Linux (操作系统)
- 389 Directory Server
- MIT Kerberos
- NTP (网络时间协议)
- DNS (域名服务器)
- Dogtag (证书系统)
- web 界面 (Apache web 服务)

## 配置 IPA

UBUNTU

### 第 1 步

为服务器设置静态 IP

```
nmcli device down <NIC>
nmcli device up <NIC>
```

> 如果你需要公共 DNS 如 8.8.8.8，请查看 IP 部分以获取静态 IP

### 第 2 步

使用 `hostnamectl` 设置静态主机名

```bash
hostnamectl set-hostname ipa.it.local
```

### 第 3 步

编辑服务器的 `/etc/hosts`

```bash
vim /etc/hosts
```
添加此行：
`192.168.0.102 ipa.it.local`
`192.168.0.103 client1`

### 第 4 步

使用 ping 命令测试

```
=> ping ipa.it.local
```

### 第 5 步

更新服务器仓库

```
=>apt update -y
```

### 第 6 步

(附加)：重启系统

```
=>reboot
```

### 第 7 步

在服务器上安装 rng-tools 包

`rng tools` 主要用于加密

```
=>apt install rng-tools -y
```

### 第 8 步

配置 rng-tools

```
=>vim /etc/default/rng-tools
```

通过添加行设置随机数据源

```
HRNGDEVICE=/dev/urandom
```

### 第 9 步

启用并启动 rng-tools

```
=>systemctl enable rng-tools
=>systemctl start rng-tools
```

### 第 10 步

在服务器上安装 freeipa-server 包

```
[server]
=> apt install freeipa-server -y
```
