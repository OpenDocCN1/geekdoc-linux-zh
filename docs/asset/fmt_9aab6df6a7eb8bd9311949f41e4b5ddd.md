
#### 5.4.2 示例 2：涉及 HADR 数据库

在此用例中，我们为 `KANAGA` 和 `ATLANTIC` 之间的数据库 `SAMPLE` 设置了 HADR 配置。在 `KANAGA` 上，创建了主数据库 `SAMPLE`。在主机 `ATLANTIC` 上也创建了备用 HADR 数据库，端口为 `50030`。

在客户端机器上，数据库 `SAMPLE` 被编类到节点 `KANAGA`。节点 `KANAGA` 引用主机名 `KANAGA` 和端口 `50030`。

要激活自动客户端重路由，您需要如下所示更新 `KANAGA` 上数据库 `SAMPLE` 的备服务器：

```
db2 update alternate server for database sample using hostname atlantic
port 50030
```

为了在 `ATLANTIC` 上的备服务器启用一个备服务器，使其能够回退到 `KANAGA` 端口 `50030` 主服务器并重新整合到 HADR 对中，您需要在主机 `ATLANTIC` 上运行此命令。

```
db2 update alternate server for database sample using hostname kanaga
port 50030
```

在没有设置自动客户端重路由功能的情况下，应用程序将收到错误 `SQL30081N`。当主数据库故障时，如果 HADR 成功启动了备服务器，应用程序将收到 `SQL30081N` 错误。

如果设置了自动客户端重路由，`DB2` 将尝试重新建立与 `KANAGA` 的连接。如果仍然无效，`DB2` 将尝试备服务器位置（主机 `ATLANTIC`，端口 `50030`）。假设连接到备服务器位置的连接没有通信错误，应用程序可以继续运行后续语句或重试失败的事务。备服务器位置是 HADR 备机所在地。为了让客户端重路由成功，HADR 必须成功地将备机提升为主机。

#### 5.4.3 示例 3：涉及 HACMP 集群中的 HADR 数据库

在在这种场景下，我们在 `KANAGA` 和 `ATLANTIC` 上设置了 HADR 对，由集群管理器提供服务。在 `KANAGA` 上，创建了主数据库 `SAMPLE`。在主机 `ATLANTIC` 上也创建了备用 HADR 数据库，端口为 `50030`。

`HACMP` 软件将检测到活动节点宕机并接管，使备机变为主机。要激活重路由，您需要使用服务 IP 更新 `KANAGA` 上数据库 `SAMPLE` 的备服务器：

```
db2 update alternate server for database sample using hostname 9.43.86.111
port 5030
```

为了在 `ATLANTIC` 上的备服务器启用一个备服务器，使其能够回退到 `KANAGA` 端口 `5030` 主服务器，您需要在主机 `ATLANTIC` 上运行此命令。同样，使用服务 IP 作为主机名。

```
db2 update alternate server for database sample using hostname 9.43.86.111
port 5030
```

回退旧服务器后，旧主 `KANAGA` 应该重新整合到 HADR 对中。

在客户端机器上，数据库 `SAMPLE` 被编类到服务 IP 地址 `9.43.86.111`，端口为 `5030`。

在带有 `HACMP` 的 HDR 环境中，服务 IP 地址 `9.43.86.111` 被用于主备两个服务器的备服务器。在客户端编类数据库 `SAMPLE` 时，服务 IP 地址 `9.43.86.111` 也被用主机名。如果 `KANAGA` 上的主数据库服务器宕机，`DB2` 将不断尝试建立到备服务器位置（主机 `9.43.86.111`，端口 `50030`）的连接。假设 `HACMP` 已成功执行了 IP 接管并将资源组移动到 `ATLANTIC`，且连接到备服务器的连接没有通信错误，应用程序就可以继续运行后续语句或重试失败的事务。

在客户端机器上，对节点 `KANAGA` 数据库 `SAMPLE` 进行目录。节点 `KANAGA` 引用主机名 `KANAGA` 和端口 `50030`。

在主 HADR 数据库主机 `KANAGA` 上，使用主机名而不是服务 IP 指定备用服务器：

```
db2 update alternate server for database sample using hostname port 50030
```

在备用 HADR 数据库主机 `ATLANTIC` 上，也同样使用主机名而不是服务 IP 指定备用服务器：

```
db2 update alternate server for database sample using hostname kanaga port 50030
```

使用服务 IP 地址作为备用服务器配置比 `HACMP` 检测到节点宕机并执行 IP 故障转移更快。当客户端重路由检测到通信失败时，首先尝试连接到原始服务器。很有可能是 `HACMP` 的接管和资源组切换已经成功，`DB2` 可以在原始服务器（服务 IP 地址 `9.43.86.111`）上获得成功连接，该地址现在已切换到主机 `ATLANTIC`。

`HACMP` 的操作可以非常无缝，以至于当客户端机器使用服务 IP 地址在节点上对数据库进行目录注册后，并不清楚哪台机器当前是主服务器。要查找主数据库主机名，可以执行以下查询：

```
db2 select substr(host_name,1,8) from table (db_partitions()) as t
```

#### 5.4.4 处理自动客户端重路由的示例应用程序代码

在本节中，我们将展示一个嵌入 SQL C 和使用 `DB2` Universal JDBC 类型 2 或类型 4 驱动的 Java 应用程序处理自动客户端重路由异常的伪代码示例。

##### 处理 ACR 异常的 Java 应用程序

重新建立后，`DB2` Universal JDBC 驱动向应用程序抛出一个 `SQLCODE` 为 `-4498` 的 `java.sql.SQLException`，告知应用程序连接已自动重建到备用服务器。

示例 5-8 显示了通过捕获异常 `-4498` 来自动客户端重路由异常的 Java 应用程序代码。

##### 示例 5-8 在 Java 中处理 ACR 异常

```java
// 在重试逻辑中，不需要重试连接或重新创建
// 或预处理语句
Connection con = DriverManager.getConnection(url, "USER", "PSWD");
Statement stmt = con.createStatement();
pstmt = con.prepareStatement("SELECT NAME FROM STAFF WHERE ID = ?");
// 当我们遇到客户端重路由
// 异常时，上面的语句不需要重试
do { // while 循环开始
    try {
        // 事务逻辑
        npstmt.setInt(1,10);
        int rowsUpdated = stmt.executeUpdate(
            "UPDATE employee SET firstname = 'SHILI' WHERE empno = '10'");
        con.commit();
    } catch (SQLException se) { // 处理客户端重路由异常
        int errorcode = se.getErrorCode();
        System.out.println("MySQLErrorCode: " + errorcode);
        if(con != null) {
            try {
                con.rollback();
            } catch (Exception e) {
                e.printStackTrace();
            }
        } 
        if(errorCode == -30108 || (errorCode == -4498)){
            System.out.println("connection is re-established, re-executing the failed transaction."); 
            retry = true;
        }
    } finally { // 关闭资源 }
    } // catch
} while(retry);
```
