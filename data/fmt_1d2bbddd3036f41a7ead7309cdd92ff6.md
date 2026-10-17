
frontend f_api-facebook-com_http

bind 0.0.0.0:21203

mode http

option http

capture request Host len 50

capture request User-Agent len 150

default_backend b_api_facebook_com_http

```

```

backend b_api_facebook_com_http

mode http

option httplog

option accept-invalid-http-response

server api.api.facebook.com:80 check

 60s fastinter 10s downinter 100s fall 1800

```

```

frontend f_api-facebook-com

bind 0.0.0.0:21204

mode http

option tcplog

default_backend b_api_facebook_com_https

```

```

backend b_api_facebook_com_https

mode http

option tcplog

server api.api.facebook.com:443 check

 60s fastinter 10s downinter 100s fall 1800

```

```

listen stats

bind 0.0.0.0:27199

mode http

stats global

stats Real\ Area

stats url /

#修改此项在 Web 界面设置你的用户密码

stats auth hapxy:mypassword

```

你需要确保在运行 hapxy 代理时，值与本地表格和远程服务器同步。你可以使用 maps 表来创建正确的配置。要应用更改，重启 hapxy 服务器。

```

frontend f_catchall_http

bind 0.0.0.0:2120

mode http

option httplog

capture request Host len 50

capture request User-Agent len 150

default_backend b_deadend

```

最后，我们需要在远程服务器上配置转发：

```

$ sudo /etc/init.d/hapxy restart

```

```

backend b_catchall_http

mode http

option httplog

option accept-invalid-http-response

```

```

frontend f_api_facebook_https

bind 0.0.0.0:2020

mode tcp

option tcplog

top-request inspect-delay 5s

top-request accept content if (req_sql_hello_type 1)

default_backend b_deadend_https

```

在 `/etc/sysctl` 中：

```

net.ipv4.ip_forward = 1

```

这就完成了服务器配置。如果你正确按照教程操作，并且本地和远程服务器都已启动，现在你的 PC 和移动端 App 上应该可以正常使用美国地区的 Facebook 应用。

```

$ sysctl -w net.ipv4.ip_forward

```

## 教程

# Mattermost

## 使用 Mattermost 简化团队通信

![](img/453752f2a570e8fff106aca09a3ea2e3_57_0.png)

我们将看到如何安装 Mattermost 并使用它来增强和简化团队通信。

**Nitish Tiwari** 职业是一名软件开发人员，也是开源爱好者。除了为博客和杂志写文章外，他还为自己的业务需求帮助自由软件。

通信是团队动态中一个非常重要的方面。团队的生产力取决于团队成员之间通信的质量。必须有一种平衡的方法，即团队成员在共享优秀报告的同时，取决于个人本身，也取决于公司文化，你所拥有的工具在团队通信中起着至关重要的作用。当我们查看 Mattermost 时，这是一个可以帮助你简化和增强内部通信的工具，同时托管在你自己的自由（Linux, SVN 等）下，以获取团队状态的统一界面。

### 01 数据库安装

作为一种基于 Web 的软件，Mattermost 需要一个数据库和 Web 服务器来运行。让我们先在 Ubuntu 15.0 上安装 PostgreSQL。首先，我们需要更新系统以获取最新的更新和补丁。

```bash
$ sudo apt-get update
$ sudo apt-get upgrade
```

现在在系统上安装 PostgreSQL：

```bash
$ sudo apt-get install postgresql postgresql-contrib
```

PostgreSQL 会创建一个名为 `postgres` 的用户。让我们创建数据库和用户：

```sql
CREATE DATABASE mostmost;
CREATE USER mmouser WITH PASSWORD 'password';
GRANT ALL PRIVGES ON DATABASE mostmost TO mmouser;
```

完成后，现在访问 PostgreSQL 数据库：

```bash
$ psql -host=localhost -dbname=mostmost -username=mmouser
```

### 02 Mattermost 安装

我们有了数据库和账户，现在下载并安装 Mattermost：

```bash
$ wget https://github.com/mattermost/releases/download/v0.8.2/mattermost.tar.gz
```

这将下载 Mattermost 代码。通过以下命令解压 `tar` 包：

```bash
$ tar -xzf mattermost.tar.gz
```

这将内容解压到当前名为 `mattermost` 的文件夹中。现在创建一个文件夹保存文件：

```bash
$ sudo mkdir -p /mattermost/data
```

下一步是编辑位于 `/mattermost/config.json` 的文件。输入：

```bash
$ cd /mattermost
$ vi config.json
```
