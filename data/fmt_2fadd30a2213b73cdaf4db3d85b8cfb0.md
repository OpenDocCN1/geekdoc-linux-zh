
## 安装和管理 Squid 代理服务

[js@rhel9_bbp ~]$ sudo systemctl enable squid

[js@rhel9_bbp ~]$ sudo systemctl start squid

检查 Squid 代理服务的状态：

[js@rhel9_bbp ~]$ sudo systemctl status squid

- 3. 在验证 Squid 正在运行后，让我们使用 `firewalld` 调整防火墙以允许访问端口 `3128`：
```
[js@rhel9_bbp ~]$ sudo firewall-cmd --permanent --add-port=3128/tcp
[js@rhel9_bbp ~]$ sudo firewall-cmd --reload
```

- 4. 最后，让我们通过你的 RHEL 9 机器的 IP 地址测试 Squid 代理缓存服务是否在运行。使用你的代理服务器主机的 IP 地址替换：`http://the-squid-proxy-ip-`
```
[js@rhel9_bbp ~]$ curl -x http://the-squid-proxy-ip:3128 https://bpbononline.com/
```
`curl` 命令应该返回 `https://bpbononline.com` 的一些 HTML 元素，这将确认你的 Squid 代理缓存正在工作。

## 教程 #37：安装和管理 MySQL

MySQL 是一种流行的开源数据库服务器，是 LAMP 栈的一部分，也是 Linux 安装中最流行的数据库软件包之一。由于其特性，它是专有数据库系统的流行备选方案。Oracle 目前领导着 MySQL 的开发和分发，组织在运行关键任务型应用程序时可以直接从 Oracle 获得官方支持。在本教程中，让我们介绍在 RHEL 9 上设置 MySQL 服务器的基础性知识：

- 1. RHEL 在应用程序流（Application stream）存储库中提供了 MySQL 8。确保你的存储库（stores）已更新，并从控制台中安装 `mysql-server` 软件包：
```
[js@rhel9_bbp ~]$ sudo dnf install mysql-server
```

- 2. 一旦安装了 `mysql-server` 软件包，启动 `mysqld` 服务并使其在启动 RHEL 9 系统时自动启动：
```
[js@rhel9_bbp ~]$ sudo systemctl start mysqld.service
[js@rhel9_bbp ~]$ sudo systemctl enable mysqld.service
```

- 3. 为了提高你的 MySQL 服务器设置的安全性，运行 `mysql_secure-installation` 提示来保护你的设置，这包括设置 MySQL root 密码、删除匿名用户以及禁用主机机之外的 root 用户远程登录：
```
[js@rhel19_bp own ~]$ sudo mysql_secure_installation
```
在完成提示后，你 RHEL 9 上的 MySQL 数据库服务器现在已准备就。

## 教程 #38：安装和管理 PostgreSQL

PostgreSQL（也称为 Postgres）是 RHEL 9 中另一种流行的开源关系型数据库。Application Stream 存储库中提供的版本是 PostgreSQL 13。让我们介绍安装和配置 PostgreSQL 的步骤。

- 1. 确保你的存储库（stores）已更新，并从控制台中安装 `postgresql-server` 软件包：
```
[js@rhel9_bbp ~]$ sudo dnf install postgresql
```
初始化数据库：
```
[js@rhel9_bbp ~]$ sudo postgresql-setup --initdb
```

- 2. 启动 postgresql 服务并使其在启动 RHEL 9 系统时自动启动：
```
[js@rhel9_bbp ~]$ sudo systemctl start postgresql
[js@rhel9_bbp ~]$ sudo systemctl enable postgresql
```

- 3. 在上面的配置文件中，Squid 被启用在端口 `3128` 上监听 HTTP 请求并运行一些基本的缓存规则。（注：这句话似乎是原文中的合并错误，在 PostgreSQL 部分提到了 Squid）。

PostgreSQL 允许你通过 `pg_hba.conf` 创建用户和权限。完成后，你 RHEL 9 上的数据库服务器已准备就绪。本教程仅介绍了 RHEL 9 上安装和配置 PostgreSQL 的基础知识。要获取更多信息，请参考 https://www.postgresql.org/docs/

## 教程 #39：安装和管理 MariaDB

MariaDB 是另一种流行的关系型数据库服务器，由社区维护但由合作伙伴提供商业支持。它是 MySQL 数据库分支，安装、配置和管理 MySQL 的大部分甚至所有方面都适用于 MariaDB。在 RHEL 9 中，提供了 MariaDB 10.5。由于 MySQL 和 MariaDB 代码库通常相似，无法在 RHEL 9 中同时安装两者。作为系统管理员，确定使用 MySQL 还是 MariaDB 非常重要。

- 1. 从控制台更新软件存储库以确保获取最新软件包，然后安装 `mariadb-server` 软件包：
```
[js@rhel19_byp ~]$ sudo dnf update
[js@rhel19_byp ~]$ sudo dnf install mariadb-server
```

- 2. 启动 MariaDB 服务并使其在开机时启动：
```
[js@rhel19_byp ~]$ sudo systemctl start mariadb
[js@rhel19_byp ~]$ sudo systemctl enable mariadb
```

- 3. 你还可以按照教程 #32 和 #37 运行 `mysql_secure_installation` 脚本来保护你的 MariaDB 安装。MariaDB 有详尽的文档。你可以从 MariaDB 官网获取更详细的文档：https://mariadb.com/kb/en/documentation/

## 教程 #40：安装和管理 MongoDB 社区版

MongoDB 是一种跨平台的文档型数据库平台。它被认为是 NoSQL 数据库，并将数据存储在一种称为 BSON 的 JSON 格式中，它是二进制编码。BSON 格式使其在网络中传输更高效。MongoDB 是 NoSQL 构建高可用且可扩展应用程序的流行选择。由于其灵活的文档 schema，它非常适合在构建云原生应用时采用敏捷开发方法的开发团队。现在让我们来看看在 RHEL 9 上部署和配置 MongoDB 的步骤：

- 1. 使用文本编辑器在 `/etc/yum.repos.d/mongodb-org-6.0.repo` 创建 MongoDB 存储库，并按所示添加存储库，保存文件：
```ini
[mongodb-org-6.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/6.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc
```

- 2. 更新您的存储库并安装 `mongodb-org` 包：
```bash
$@rhel9_bpp ~$ sudo update -y
$@rhel9_bpp ~$ sudo install -y mongodb-org
```

- 3. 启动 `mong` 服务并设置为系统启动时自动运行：
```bash
$@rhel9_bpp ~$ systemctl start mongodb
$@rhel9_bpp ~$ systemctl enable mongodb
```

- 4. 你也可以检查 `mongod` 服务的状态以确保一切运行正常：
```bash
$@rhel9_bpp ~$ sudo systemctl status mong
```

在验证所有内容运行正常并配置完成后，通过从控制台访问数据库壳登录 MongoDB：
```bash
$@rhel9_bpp ~$ sudo mongosh
```
