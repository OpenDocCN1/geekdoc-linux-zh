
## 使用 JCC 类型 4 驱动的 Java应用程序

在类型 2 和类型 4 JDBC 驱动中，处理 ACR 异常的方法与示例 5-8 相同。但使用 JCC 类型 4 驱动实现重路由时，在获取数据库连接时需要不同的设置。JCC 类型 2 驱动使用特定于所连接数据源的本地客户端库。

Linux, UNIX 和 Windows 上的 DB2 高可用与可扩展性指南

JCC 类型 4 驱动用纯 Java 编写，没有原生客户端组件，并实现了到数据源的网络协议。JCC 类型 4 客户端不需要在客户端侧安装 DB2，可以直接连接到数据源。它不是允许客户端应用程序从本地数据库目录获取信息，而是将服务器名称和端口显式包含在 JCC 连接尝试中。然而，如果在连接时，服务器功能已被备用服务器接管，客户端将不会无法连接，而是将不知道去哪里寻找备用服务器信息。

DB2 Universal JDBC 类型 4 驱动重路由仅适用于使用 `java.sql.DataSource` 接口的连接。示例 5-9 显示了如何使用 DataSource 属性文件获取连接的示例。`DB2SimpleDataSource` 是 DB2 对 `DataSource` 接口的一种实现。

### 示例 5-9 使用 DataSource 接口获取数据库连接

```java
DB2SimpleDataSource dataSource = new DB2SimpleDataSource();

Properties prop = new Properties();

InputStream dsProfile = null;

try{
    dsProfile = new FileInputStream(DSName);
} catch (FileNotFoundException fe) {
    System.out.println(fe.getMessage());
    throw fe;
}

prop.load(dsProfile);
dataource.setServerName(prop.getProperty("serverName"));
String portNum = prop.getProperty("portNumber");
int portNo = (new Integer(portNum)).intValue();
dataource.setPortNumber(portNo);
dataource.setDatabaseName(prop.getProperty("databaseName"));
dataource.setUser(prop.getProperty("username"));
dataource.setPassword(prop.getProperty("password"));
Connection con=datasource.getConnection();
con.setAutoCommit(false);
Statement stmt = con.createStatement();
```

在 WebSphere Application Server 环境中使用 DataSource 的最佳方法，此步骤在 WebSphere Server 的管理控制台中完成。

`clientRerouteServerListJNDName` 有两个功能：

- 允许备用服务器信息跨 JVM 持久化。
- 在首次连接到数据库服务器失败时，提供备用服务器位置。

`clientRerouteServerListJNDName` 用于在 JNDI 仓库中识别指向 `DB2ClientRerouteServerList` 实例的 JNDI 引用，用于备用服务器信息。在成功连接主服务器后，`clientRerouteServerListJNDName` 提供的备用服务器信息将被来自服务器的信息覆盖。

如果定义了 `clientRerouteServerListJNDName`，DB2 Universal JDBC 驱动将在故障转移后尝试将信息传播到 JNDI 存储。如果指定了 `clientRerouteServerListJNDName`，将使用 `DB2ClientRerouteServerList` 指定的主服务器信息进行连接。如果没有指定主服务器，则将使用 DataSource 上的 `serverName` 信息。

新建立的故障转移连接将使用原始 DataSource 属性配置，但服务器名称和数字端口除外。此外，DB2 Universal JDBC 驱动程序会在原始连接期间修改过的任何 DB2 专用寄存器在故障转移连接中重新建立。

### 使用 C 语言的嵌入 SQL 程序

重新建立连接后，嵌入 SQL 应用程序将接收异常 `SQLCode -30108`，指示应用程序连接已自动重新建立到备用服务器。

示例 5-11 是应用程序客户端重路由连接的伪代码。

### 示例 5-11 C 程序处理 ACR 异常

```c
int checkpoint = 0;
check_sqlca(unsigned char *str, struct sqlca sqlca)
{
  if (sqlca)->code == -30108)
    // 由于通信丢失，立即终止应用程序
    exit(1);
  } else {
    // 打印错误
    printf(...);
    if (sqlca)->code == -30108)
      // 如果连接已重新建立，重新执行失败的事务
      if (checkpoint == 0)
```
{ goto checkpoint0; }
else if (checkpoint == 1) {
  goto checkpoint1; }
else if (checkpoint == 2) {
  goto checkpoint2; }
...
exit;
}
main()
{
connect to mydb;
check_sqlca("connect failed"
```

## HADR 最佳实践

在本章中，我们描述了影响 HADR 的 DB2 配置参数和注册表变量。我们还讨论了实施 HADR 解决方案时需要考虑因素，以获得最佳的 HADR 性能。

我们涵盖了以下主题：

- DB2 HADR 配置参数
- DB2 HADR 注册表变量
- 建议与注意事项
- 限制

### 6.1 DB2 HADR 配置参数

在这里我们探索对 HADR 有显著影响的相关数据库管理器配置参数 `dbm cfg parm` 和数据库配置参数 `db cfg subm`。

在大多数情况下，在设置 HADR 后不需要手动更改这些参数。但是，如果以后架构需求发生变化，知道需要更改什么以及为什么始终是有用的。

我们在此节中不提供特定的性能建议，因为每个环境都需要进行调优以匹配其独特特性。尽管如此，这里提供的信息、DB2 手册页面以及列出的其他参考将让您了解哪些设置可以满足您的需求。

在使用配置参数以及下一节中的注册表和环境变量时需要记住的一是：它们只有在数据库处于主或备用状态时才能被识别和使用，否则会被忽略。尽管如此，在 HADR 对的两个服务器上设置并维护这些参数/变量仍然很重要，以备在切换角色或执行强制接管时使用。

#### 6.1.1 基本配置参数

术可以在 DB2 9 Information Center（Reference → Configuration Parameters → Database Systems）以及 DB2 9 Performance Guide SC10-4222: Appendix A 中找到。同样的信息在 DB2 V8.2 Information Center 和 Administration Guide: Performance V8, SC09-4821-01 中也有给出。

- `AUTORESTART`:
在使用自动客户端重路由时，考虑将此 `db cfg parm` 设置为该值，这样损坏的主服务器就不会重新上线并在 HADR 主角色下重启，从而导致脑脑裂场景。

在非 HADR 环境中，将 `AUTORESTART` 设置为 ON 是好的，因为当实例启动并尝试进行首次应用程序连接时，数据库会自动激活，并尝试对数据库去激活时存在的任何正在进行中的/入站事务进行日志/崩溃恢复。

当 `AUTRESTART` 留为 OFF 时，连接尝试将收到 `SQL1015N` 消息。

- `LOGINDEXBUILD`:
此 `db cfg param` 值应设置为 ON，这样主数据库上索引的维护操作（如创建或 REORG）将被记录并执行，以与备用数据库保持一致。

- `LOGRETAIN` / `LOGARCHMETHn`:
为了使用 HADR，你必须至少设置一个 `db cfg param`。不支持循环日志。

`LOGRETAIN` 是在支持原生归档方法 `LOGARCHMETHn` 之前的时代的遗留参数。你仍然可以使用它来指定 HADR 位置。

- `HADR_DB_ROLE`:
此 `db cfg param` 可以通过 STOP、START、TAKEOVER 配置。可能的值为：
