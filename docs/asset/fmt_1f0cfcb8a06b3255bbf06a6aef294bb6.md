
第一条指令在记录活动之前关闭。由于这是一项 CPU 密集型任务，许多人倾向于将其关闭，以收集客户端从哪里连接的统计（例如，按地理区域或域名）。此外，错误日志被指定为独立于访问日志的实体。典型的访问条目如下：

```
192.64.32.12 - [06/Jan/2002:20:55:36 +0000]
GET /cgi-bin/printenv HTTP/1.1" 200 1024
192.64.32.12 - [06/Jan/2002:20:56:07 +0000]
GET /cgi-bin/search.cgi?term=solaris&type=simple HTTP/1.1" 200 85227
192.64.32.12 - [06/Jan/2002:20:58:44 +0000]
GET /index.html HTTP/1.1" 200 94151
192.64.32.12 - [06/Jan/2002:20:59:58 +0000]
GET /pdf/secret.pdf HTTP/1.1" 403 29
```

第一个示例显示客户端 192.64.32.12 在 2002 年 1 月 6 日 20:55:36 访问了 cgi 程序 `printenv`。在记录活动之前关闭日志。由于这是一项 CPU 密集型任务，许多人倾向于将其关闭，以收集客户端从哪里连接的统计（例如，按地理区域或域名）。此外，错误日志被指定为独立于访问日志的实体。典型的访问条目如下：

# 682 第六部分：服务、目录与应用程序

图 33-1

EJB 层

![](img/11bcccd1804574cca0c3018732958dd5_712_0.png)

性能是 Sun Java System Application Server 的首要目标：除了在其托管的 Java 应用程序内置多线程外，Sun Java System Application Server 内部也使用了多线程。此外，某些任务可以使用多个线程并行执行。或者通过跨系统的数据和进程共享支持多进程处理：随着应用程序的增长，可以将任务分配给特定的服务器。例如，一个服务器可能处理身份验证，而另一个服务器可能处理所有指向数据库的 JDBC 请求。以这种方式实现应用程序的原因之一是并不是所有运行应用程序的服务器都需要位于同一个子网：事实上，认证服务器可能位于防火墙之外，而数据库服务器可能是外部最难访问的系统。

由于 Java、CGI、NSAPI 以及其他服务端技术可以由同一个应用程序服务器处理，而不是由多个独立的服务器，因此可以通过集成获得性能提升，因为只需要运行一台服务器。

Sun Java System Application Server 通过支持无状态会话豆（stateless session beans）的故障转移来提供高可用性。这意味着如果由于某种原因存储交互式用户会话数据的系统崩溃，另一个服务器可以恢复这些豆并继续运行。这对于运行在有状态会话豆（stateful session beans）中长时间持久数据的应用程序特别有用——因为实体豆（entity beans）和无状态会话豆存储状态的方式与有状态会话豆不同，降低了支持 EJB 技术的关键风险。对于连接到 EJB 的通用对象代理架构（CORBA）客户端也提供了类似的机制。

Sun Java Application Server 在多个层级执行对象缓存，以确保资源高效利用。这包括对所有数据库的 `JDBC` 连接进行缓存、`JSP` 和 HTML 输出缓存以及其他任务。虽然这种方法存在对象不匹配和检索错误等固有风险，但 Sun Java Application Server 的缓存功能通常是健壮的，并且根据需要开启或关闭。此外，Sun Java Application Server 具有一些预取策略来简化数据操作，包括能够在结果集从数据库表完全检索之前对其进行查看。

Sun Java System Application Server 是一个高度可扩展的系统：它既可以在运行 Windows 的单 CPU 系统上运行，也可以在运行 Solaris 且配备 64 个 CPU 的高端 E1000 系统上运行。除了充分利用单个系统的资源外，Sun Java Application Server 还能跨多个系统扩展，使 CPU 资源的潜力几乎不受限制。由于 Sun Java Application Server 使用分布式数据同步（`DSync`）在配置的服务器之间共享数据，在不同系统之间切换任务的任何开销都降到了最低。不需要额外的安装或重新配置——根据需要使用 Sun Java Application Server Administration Tool 添加新服务器。一旦你将新服务器添加到可用系统池中，就会通过轮询和其他算法计算负载共享，自动在所有系统之间执行负载均衡，无需人工干预。这不需要外部负载均衡，因为负载均衡功能集成在应用程序服务器内部。

安全是应用程序服务的关注重点，Sun Java Application Server 提供了 JEE 市场上提供的最佳安全set，因为它与 Sun Java Directory Server 集成。通过使用 `LDAP` 进行身份验证和授权，并在所有支持的应用程序上单点登录，你可以显著降低安全风险。

Sun Java Application Server 使用标准的 Java SQL API 支持 `JDBC` 和数据库访问，还通过统一集成框架 API（Unified Integration Framework API）将特定于厂商的 JDBC 驱动操作抽象出来。Sun Java Application Server 使用高度优化的多线程驱动程序支持 `DB2`、`Informix`、`Oracle`、`Sybase` 和 `SQL Server`，这些驱动程序与单个事务管理器协同工作，协调处理事务所需的许多底层活动。此外，Sun Java Application Server 现在配备了集成版本的 `PointBase` 数据库，它支持关系和对象存储。`PointBase` 有它自己的 JDBC 驱动，可以在存在第三方数据库的情况下在开发和测试中使用。

![](img/11bcccd1804574cca0c3018732958dd5_713_0.png)

Sun Java System Application Server 相比竞争对手的另一个关键优势是 Sun Java System Application Server Tool，它对服务器操作的所有方面提供了实时管理能力。通过使用 Administration Tool，可以管理服务、监控系统活动、管理数据库、查看事务进度、检查系统日志、使用 `SNMP` 处理事件、负载均衡和集群以及配置单个应用程序。其直观的基于 `Swing` 的界面使得 Administration Tool 易于使用，这对于不是 `J2EE` 开发人员但负责管理组织 `J2EE` 环境的系统管理员来说特别重要。此外，可以使用 Administration Tool 用于管理安全、授权、访问，并在多个服务器之间执行应用程序性能调优和分区。

## 架构

每个 Sun Java System Application 实例都有与其关联的服务，特别包括执行服务器 (`KXS`)、`Java` 服务器 (`KJS`)、`C++` 服务器 (`KCS`) 和 `CORBA` 执行服务器 (`CXS`)。它们分别负责管理系统服务、`Java` 应用程序、`C++` 应用程序和 `CORBA` 服务。`KXS` 的性能取决于许多参数，包括：

- CPU 负载
- 磁盘 I/O 活动
- 已就绪请求的平均响应时间
- 等待请求数
- 等待处理的请求数
- 缓存的结果数量
- 可处理请求的线程数
- 未处理的线程请求数
- 当前服务的用户会话数
- 峰值请求
- 数据吞吐量
- 请求总数
- 虚拟内存交换

同样，`KJS`、`KCS` 和 `CXS` 提供服务的性能取决于若干因素，包括：

- 等待处理的请求
- 平均响应时间
- 活跃数据库连接数
- 可用数据库连接数
- 数据库提交数
- 数据库回滚数
- 就绪请求
- 接收请求数
- 等待请求数
- 可处理请求的线程数
- 未处理的线程请求数
- 数据吞吐量
- 数据库查询总数
- 创建线程数

## 服务器配置

要管理服务器，你需要启动 Java System Server Administration Tool。界面由三个主要区域组成。第一个区域是一行按钮，定义了要执行的操作类型。这些操作包括设置常规、监控服务、管理数据库、审查事务、配置日志、监控事件、设置负载均衡、应用安全措施以及配置单个应用程序。

按钮下方有两个面板：左面板提供每个操作的对象层次结构，而右面板包含执行特定操作的多个选项卡。在常规部分，左面板的对象层次结构显示所有配置的 Java System Server 实例列表，因为 Administration Tool 可以同时管理多个实例。每个服务器实例都有若干关联服务器，包括 `KXS`、`KJS`、`KCS` 和 K。右面板显示了多个选项卡，包括 Server、Request Manager、`SNMP`、`LDAP`、`EJB` 和 Cluster。

# 686 第六部分：服务、目录与应用程序
