
# Novell Web 服务工具与基础设施

Novell 提供了允许您创建 Web 服务解决方案的工具和基础设施组件。Novell `exeND Workbench` 和 Novell `exeND Application Server` 可以单独提供或通过 Novell Open Enterprise Server 提供，它们提供了开发 Web 服务的集成开发环境（IDE）以及部署它们的平台。`exeND Workbench` 是一个可视化开发界面，拥有丰富的向导、编辑器和部署工具。Novell `exeND Application Server` 是一个强大且完整的 `J2EE` 服务器，运行在 Linux、Netware、Windows NT/2000、Unix、HP-UX 和 AIX 上。

## Novell exeND Workbench

Novell `exeND Workbench` 包含了增强的 `J2EE` 组件和服务创建向导、可视化设计器、基于存档的项目以及一键部署到 `J2EE` 应用程序服务器。`exeND Workbench` 是一个面向 `J2EE` 的 IDE，提供者可以使用它基于 `JAX-RPC` 标准（XML 远程过程调用 Java API）创建、部署和维护 Web 服务。`JAX-RPC` 使 Java Web 技术开发者能够创建基于 `SOAP` 的互操作且可移植的 Web 服务——并将它们部署在任何兼容 `J2EE` 的服务器上。Workbench 还可以用于开发符合 `JAX-RPC` 的基于 Java 的 Web 服务消费者。

Workbench 包含以下工具、向导和能力：

- 组件向导—创建 `J2EE` 组件，如 `JSP` 页面、`EJB`、servlet、Java 类、JavaBeans 和标签库
- Web 服务设施—包括创建基于 Java 的 Web 服务组件的向导、`SOAP` 运行时环境以及用于搜索和发布到 Web 服务注册表的注册管理器
- 可视化和文本编辑器—编辑 Java 文件、`JSP` 文件、`XML` 文件、`WSDL` 文档、部署描述符和纯文本文件；编辑器格式包括开源 NetBeans 或原生 Workbench（部署描述编辑器、部署计划编辑器、`WSDL`）；还包括图像和类查看器
- 项目视图—显示项目的结构
- 项目工具—协助构建项目、创建和部署 `J2EE`
- 部署工具—一键部署到 `J2EE` 应用程序服务器
- 版本控制—与版本控制系统集成
- 迁移—自动将 `J2EE` 1.2 更新到 1.3
- `UDDI` 工具—包括一个测试用的 `UDDI` 和 `UDDI` 浏览器
- Web 服务—为 `JAX-RPC` 提供核心技术
- 调试器—调试基于服务器的应用程序
- 注册管理器—定义配置文件、搜索注册表、发布新服务
- 与其他 IDE 集成—结合 `exeND Workbench` 使用顶尖的 `J2EE` 开发工具，如 WebGain Café、Borland Jbuilder、Inline Standard Edition 和 Macromedia Dream Weaver

Novell `exeND Workbench` 提供了一个直观的图形化工具，消除了传统上繁琐的 `J2EE` 部署过程。通过使用 Novell `exeND Workbench` 向导，开发者可以按照以下 `J2EE` 格式创建项目：

- 企业存档 (`EAR`)
- Web 存档 (`WAR`)
- `EJB` 存档 (`JAR`)
- 客户端存档 (`JAR`)
- 资源适配器存档 (`RAR`)
- 简单 Java 存档 (`JAR`)
- 仅部署（不可编译）

## Novell exeND Application Server

Novell `exeND Application Server` 是一个用于构建和部署企业级应用的全面 `J2EE` 认证平台。它支持完整的 Java 企业版标准，包括服务器页面（`JSP` 页面）、企业级 Bean（`EJB`）、基于标准的数据库编程接口（Java 连接，`JDBC`）、目录（Java 命名和目录接口，`JNDI`）、消息（Java 消息服务，`JMS`）、事务（Java 事务 API，`JTA`）、授权（Java 身份验证和授权服务，`JAAS`）、Java 消息服务（`JMS`）、`XML` 解析（Java 解析 API，`JAXP`）以及其他服务，如 `CORBA` 和 `JavaMail`。Novell `exeND Application Server` 可以在多种 Windows、Unix 和 Linux 平台上。Novell `exeND Application Server` 最近被《Network Computing》杂志评为编辑选择，该杂志赞了 `extND Application Server` 无缝的 IDE 集成和企业级功能集。

Novell `extEnd Application Server` 包含一个丰富的 `POA` 管理控制台，允许管理员执行所有系统管理功能，包括图形化查看使用情况和性能、查看日志文件、更改安全设置等。管理功能还通过 `SNMP` 代理提供，用于配合 Tivoli 或 CA (Computer Associates) 管理控制台。

Novel `extEnd Application Server` 的其他功能还包括：

- `jBroker MQ`—包含完整的 Java 消息服务 (`JMS`) 1.0.2 实现，具有点对点和发布/订阅功能。
- `jBroker ORB`—提供 `CORBA` 2.3 服务以及 `RMI-IIOP` 协议；功能包括正向（`IDL` 到 Java）和反向（JavaRMI 到 `IIOP`）协议转换、便携对象适配器 (`POA`)、按值 Java 对象、服务器激活、`IIOP` 连接连接器、可插拔认证支持、`IIOP/SSL`、多播调用、`COS` 名称服务以及对象事务服务的扩展性。
- 企业级 JavaBeans (`EJB` 1.1)—提供功能完备的 `EJB` 服务器，支持会话豆（session beans）和复杂管理的实体豆（entity beans）；`EJB` 能够部署面向对象、分布式、企业级的应用程序。
- Servlets 2.2—支持基于服务器的动态 HTML；servlets 实例化一次并通过缓存重用以获得更好的性能；支持将 `WAR` 既作为打包机制，又作为运行时的应用上下文。
- Java 页面 (`JSP` 1.1)—包含 `JSP`-to-servlet 编译器，可实现更快的编译和错误报告；还通过使用嵌入式 Java 标签实现动态 HTML。
- 其他 `J2EE` 平台服务：
    - `JNDI` 1.2 (Java 命名和目录接口)—标准化了对各种命名和目录服务的访问。
    - `JDBC` 2.0 (Java 数据库连接)—提供对关系型数据库和其他数据存储的访问。
    - `JavaMail` 1.1—提供向服务器发送和接收电子邮件消息的能力。
    - `JTA` 1.0 (Java 事务 API)—为 `J2EE` 组件和客户端提供管理自身事务的方法，并允许多个组件参与单次事务。
    - `XML` (扩展性标记语言)—提供数据定义以及消息和通信层级。

## 第 3 章：现实世界中的开源

- 企业数据连接器—实现与非关系数据库和封装应用程序的连接，例如 `SAP`、`PeopleSoft` 和 `Lotus Notes`（连接器随 Novell `extEND Composer` 提供）。
- 数据源对象—实现自动数据绑定，其中客户端的、感知数据的控件（如文本框、列表框和下拉框）可以无需编写代码绑定到数据源对象的列；还可以与事务处理监器和服务器交互，如 `CICS`、`Tuxedo`、`Microsoft Transaction Server` 等。

### 注意

Imperial Sugar 公司是美国最大的糖精和加工商之一，需要增强客户服务并降低订单处理成本，以便在利润极低的行业中保持竞争力。通过 `extEND` 技术，Imperial Sugar 将旧系统中启用了 `XML` 的销售交易汇成适当的业务流，并在一个先进的基于 Web 服务的门户中将其暴露为 Web 服务，该门户允许客户以电子方式下单，并查看其与公司关系的实时状况。Novell `extEND` 直观的可视化设计环境从主机应用程序中创建服务仅需少量培训，Imperial Sugar 在六周内完成了其 Web 服务架构的设计和实现，随后经过了两个月的测试，之后开始向 10,000 名客户推行。Imperial Sugar 使用 Novell `extEND Application Server` 管理其 Web 服务组件和新的 Imperial 外部网门户应用程序的所有运行时执行。`extEND Application Server` 的负载均衡功能为 Imperial Sugar 外部网的分阶段推行提供了必要的扩展性和性能，其容错性确保了其客户的高可用性。

## 开源 Web 服务工具

你也可以从开源社区获取 Web 服务组件和工具。JBoss（公司）提供 JBoss Application Server，这是一个 `J2EE` 服务器。JBoss 提供了 `CORBA` 2.3 服务以及 `RMI-IIOP` 协议；功能包括正向（`IDL` 到 Java）和反向（JavaRMI 到 `IIOP`）协议转换、便携对象适配器 (`POA`)、按值 Java 对象、服务器激活、`IIOP` 连接连接器、可插拔认证支持、`IIOP/SSL`、多播调用、`COS` 名称服务以及对象事务服务的扩展性。
