
```ini
[mongodb-org-6.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/6.0/x86_64/
gpgcheck=1
enabled=1
```

`gpgkey=https://www.mongodb.org/static/pgp/server-6.0.asc`

### 2. 安装 MongoDB 软件包

```
yum install -y mongodb-org
```

*图 11.32* 展示了安装过程的输出结果（部分）：

```
[root@rhel ~]# yum install -y mongodb-org  |  tail -15
Installed products updated.

Installed:
  compat-openssl11-1:1.1.1k-4.el9_0.x86_64
  cyrus-sasl-2.1.27-20.el9.x86_64
  mongodb-database-tools-100.6.0-1.x86_64
  mongodb-mongosh-1.6.0-1.el8.x86_64
  mongodb-org-6.0.1-1.el8.x86_64
  mongodb-org-database-6.0.1-1.el8.x86_64
  mongodb-org-database-tools-extra-6.0.1-1.el8.x86_64
  mongodb-org-mongos-6.0.1-1.el8.x86_64
  mongodb-org-server-6.0.1-1.el8.x86_64
  mongodb-org-tools-6.0.1-1.el8.x86_64

Complete!
```

*图 11.32：安装 MongoDB 的输出示例*

在安装 MongoDB 软件包后，需要使用 `systemctl` 命令安装服务 `mongodb`。*图 11.33* 展示了启动服务后其状态的输出：

```
root@ubuntu:~# systemctl start mongod
root@ubuntu:~# systemctl status mongod
● mongod.service - MongoDB Database Server
   Loaded: loaded (/lib/systemd/system/mongod.service; disabled; vendor preset:)
   Active: active (running) since Wed 2022-09-21 20:26:25 UTC; 3s ago
     Docs: https://docs.mongodb.org/manual
  Main PID: 5531 (mongod)
   Memory: 63.8M
      CPU: 176ms
   CGroup: /system.slice/mongod.service
           └─5531 /usr/bin/mongod --config /etc/mongod.conf

Sep 21 20:26:25 ubuntu systemd[1]: Started MongoDB Database Server.
```

*图 11.33：systemctl 命令的输出示例*

该服务的主要配置文件是 `/etc/mongod.conf`，其中包含关于数据和日志的存储位置以及监听 IP 地址和端口等信息，以及其他与相关的配置。以下代码展示了一个 `Ubuntu` 系统中的默认配置：

```
storage:
    dbPath: /var/lib/mongodb
    journal:
        enabled: true
systemLog:
    destination: file
    logAppend: true
    path: /var/log/mongodb/mongod.log
net:
    port: 27017
    bindIp: 127.0.0.1
processManagement:
    timeZoneInfo: /usr/share/zoneinfo
```

默认情况下，该服务仅在本机监听并使用默认端口 27017。与 MongoDB 的通信使用 TCP。

### MongoDB 客户端和任务

用于连接到 MongoDB 服务的命令客户端是 `mongosh`。在运行 `mongod` 的系统中执行该命令将连接到本地实例，并以交互模式进行操作。默认数据库的名称为 `test`。*图 11.34* 展示了输出示例：

```
root@ubuntu:~# mongosh
Current Mongosh Log ID:  632cba7d008ae278fb5b9f59
Connecting to:          mongodb://127.0.0.1:27017/?directConnection=true&serverSelectionTimeoutMS=2000&appName=mongosh+1.6.0
Using MongoDB:          6.0.1
Using Mongosh:          1.6.0

For mongosh info see: https://docs.mongodb.com/mongosh/

------
   The server generated these startup warnings when booting
  2022-09-22T19:36:22.009+00:00: Using the XFS filesystem is strongly recommended with the WiredTiger storage engine. See http://dochub.mongodb.org/core/product-filesystem
  2022-09-22T19:36:22.360+00:00: Access control is not enabled for the database
Read and write access to data and configuration is unrestricted
  2022-09-22T19:36:22.360+00:00: vm.max_map_count is too low
------
```

![](img/863afa537de4eed7deb11978bfbfa90e_358_0.png)

如果运行 MongoDB 数据库的系统接受远程连接，则可以使用命令 `mongosh` 连接到远程节点。指定远程节点的参数如下：`mongodb://ip.address:port`。*图 11.35* 展示了连接到远程服务器的示例：

```
[root@rhel ~]# mongosh --quiet mongodb://192.168.122.43:27017/test>
```

![](img/863afa537de4eed7deb11978bfbfa90e_358_1.png)

可以通过输入 `db` 来检查当前使用的数据库。另一方面，要列出所有可用数据库及其大小，请输入 `show dbs`。*图 11.36* 说明了这两个操作的输出示例：

```
test> db
 test
 test> show dbs
 admin 72.00 KiB
 config 72.00 KiB
 local 72.00 KiB
```

*图 11.36：MongoDB 输出示例*

可以使用语法 `use dbname` 来使用另一个数据库。如果指定的 `dbname` 不是已存在的数据库，将创建一个新数据库。MongoDB 将文档存储在集合中。这些集合类似于关系型数据库中的表。如果指定的 `collection` 不存在，它将被创建。图 11.37 展示了使用 `insertOne` 操作创建名为 `students` 的新数据库和新集合的过程。

```
test> use school
switched to db school
school> db.students.insertOne({
... name: "Alberto",
... lastname: "Gonzalez"
... })
{
 acknowledged: true,
 insertedId: ObjectId("632cd01a414b5296a6629fc4")
}
school>
```

![](img/863afa537de4eed7deb11978bfbfa90e_360_0.png)

上一个示例在集合 `students` 中插入了一个新学生。可以使用操作 `insertMany` 一次性添加多个文档，如图 *图 11.38* 所示：
