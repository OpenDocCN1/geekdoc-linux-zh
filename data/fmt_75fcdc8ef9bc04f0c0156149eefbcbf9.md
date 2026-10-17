
## 在 Additional Properties 下，选择 bus connector 中的 Users and Groups。出现图 8-8 所示窗口。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_179_0.png)

图 8-8 Bus Connector Role 中的 Users and Groups

New。出现图 8-9 所示窗口，可以输入用户 ID

![](img/5b458d26d6ded58c4d2c82af59a3d71c_179_1.png)

图 8-9 向 Bus Connector Role 添加 LocalOSUserID

输入用户 ID `LocalOSUserID` 后，点击 OK，将出现第 159 页的图 8-10 所示。

### 图 8-10 总线连接器中的用户和组

当 WebSphere Application Server 未启用管理安全功能时，Trade 6 应用程序启动并成功运行，无需对 `LocalOSUserId` 用户 ID 进行上述两个更改。在进行更改后，会出现图 8-11 所示的窗口，并且需要保存更改。此时，Trade 6 应用程序成功启动，无需停止并重启 WebSphere Application Server。对于其他配置更改，可能需要使用 `stopServer.sh` 和脚本停止并重启服务器。

#### 消息

您的本地配置已发生更改。您可以：

* 直接保存到主配置。
* 在保存或丢弃之前检查更改。

服务器可能需要重启以使这些更改生效。

图 8-11 保存配置更改的消息

图 8-12 显示了 IBM WebSphere Application Server V6.1.0.0 的安装摘要窗口。应用程序服务器的默认名称为 `server1`。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_181_0.png)

**图 8-12** WebSphere 应用安装结果

从这里，可以访问第 161 页图 8-13 所示的第一步控制台，以启动应用程序并运行安装验证测试。

**160** 使用适用于 System z Linux 的 Oracle 解决方案

### 图 8-13 WebSphere Application Server 启动第一步

也可以使用启动控制台安装 IBM HTTP Server V6.1.0.0。

图 8-14 显示了 HTTP 服务器的安装摘要窗口。Web 服务器的默认名称为 `webserver1`。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_182_0.png)

### 图 8-14 HTTP 服务器安装结果

## 8.3 下载 IBM Trade Performance 应用程序

第一步是下载并解压 Trade 6 压缩包 `tradeInstall.zip`。可以从 IBM 免费下载：

https://www14.software.ibm.com/webapp/iwm/web/preLogin.do?source=trade6

`tradeinstall` 是下载的 trade 压缩包中的高级目录。Trade 6 应用程序的概述和架构描述位于 `tradeinstall/Trade.pdf` 文件中的 PDF 中，安装说明位于 `tradeinstall/Readme.html` 中的 readme 文件。创建 Trade 6 使用的表和索引的 DDL 位于 `tradeinstall/Oracle/Table.dl`。

### 8.3.1 为 Trade 6 设置现有的 Oracle 数据库

`linux25` 现有 Oracle 数据库（SID = `psft1`）用于 Trade 6 的表和索引。使用示例 8-1 所示的 DDL 为 Trade 6 应用程序创建了新的表空间和新的临时表空间。

> 示例 8-2 创建表空间的 SQL 语句

```sql
CREATE TABLESPACE TRADE61_DEFAULT_TS DATAFILE
'/oracle2/trade61/oradata/psft1/trade61ldts.dbf' SIZE 400M EXTENT
MANAGEMENT LOCAL UNIFORM SIZE 1M SEGMENT SPACE MANAGEMENT AUTO;
```

```sql
CREATE TEM TABLESPACE TRADE61_TEMP_TS TEMPFILE
'/oracle2/trade61/oradata/psft1/trade61lts.dbf' SIZE 100M EXTENT
MANAGEMENT LOCAL UNIFORM SIZE 1M;
```

```sql
ALTER DATABASEFILE '/oracle2/trade61/oradata/psft1/trade61ldts.dbf'
AUTOEXTEND ON NEXT 10M MAXSIZE UNLIMITED;
```

```sql
ALTER TABLEFILE '/oracle2/trade61/oradata/psft1/trade61lts.dbf'
AUTOEXTEND ON NEXT 10M MAXSIZE UNLIMITED;
```

在现有的 Oracle 数据库中创建了用户名并为 trade 用户 ID 授予了权限（参见示例 8-2）。

> 示例 8-2 创建示例

```sql
user trade identified by trade default tablespace
TRADE61_DEFAULT_TS
temporary tablespace TRADE61_TEMP_TS account unlock;
```

```sql
GRANT CREATE SESSION to trade;

GRANT CREATE table to trade;
alter user trade quota unlimited on trade61_default_ts;
```

使用此处显示的用户名和密码连接到 Oracle 数据库：

```
connect trade/trade@psft1
```

通过运行 DDL，在 `TRADE61_DEFAULT_TS` 表空间的 trade 架构中创建了 Trade 6 表和索引：

```bash
tradeinstall/Oracle/Table.dbl1
```

## 8.4 将 Trade 6 安装为 WebSphere Application Server 应用程序

根据安装 readme，将 `tradeinstall` 目录设置为当前目录，并在 `linux25` 命令行运行了 WebSphere Application Server 脚本 `wsadmin.sh -f trade.jacl` 以交互式安装 JDBC/JMS 资源和 Trade 6 应用程序：

```bash
[root@linux25 tradeinstall#]
/oracle2/IBM/WebSphere/AppServer/wsadmin.sh -f trade.jacl
-user admin -password wasadmin
```

由于启用了管理安全，必须作为选项添加相应的用户名和密码，以便 WebSphere Application Server 命令能够执行。脚本是交互式运行的，以下是某些交互示例：

选择后端数据库类型 (db2|oracle|db2) [db2]:

oracle

输入数据库驱动路径

c:/oracle/product/10.1.0/db_1/jdbc/lib/ojdbc14.jar:

/oracle1/db1/jdbc/lib/ojdbc14.jar

输入 Oracle 数据库 SID (traded):psft1

脚本完成后，停止并重启 WebSphere Application Server：

```bash
[root@linux25 bin]# #stopServer.sh server1 -user wasadmin -password
wasadmin
[root@linux25 bin]# #startServer.sh server1 -user wasadmin -password
wasadmin
```

当应用程序启动后，浏览器指向：

http://linux25:9080/trade

并访问 Trade 6 应用程序（参见图 15）。

![](img/5b458d26d6ded58c4d2c82af59a3d71c_185_0.png)

## 8.5 填充 (Populate)

| 配置 | 描述 |
|---|---|
| 概述 | 服务器可能需要重启以使这些更改生效。 |
| 技术 | 可能需要使用 `stopServer.sh` 和脚本停止并重启服务器。 |
| 需求 | 可能需要使用 `stopServer.sh` 和脚本停止并重启服务器。 |
| 配置 | 可能需要使用 `stopServer.sh` 和脚本停止并重启服务器。 |
