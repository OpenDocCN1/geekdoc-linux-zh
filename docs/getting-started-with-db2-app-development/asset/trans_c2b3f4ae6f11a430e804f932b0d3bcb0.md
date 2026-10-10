

这些内容将在下文中详细讨论。

### 1.8.1.1 Amazon Web Services（亚马逊网络服务）

IBM 已与 Amazon Web Services (AWS) 达成合作伙伴协议，以在亚马逊弹性计算云 (EC2) 上运行 DB2。AWS 提供了一组集成的服务，构成了“云中”的计算平台，并采用按量付费模式。也就是说，AWS 允许你“租用”计算资源（虚拟服务器和存储），你只需为你使用的资源付费。例如，假设你配置了一个 EC2 虚拟服务器用于常规数据库操作，并在高峰时段或季节性需求期间额外配置了一个数据库服务器运行几个小时。在这个例子中，你只需为额外配置的数据库服务器在运行的那几个小时向 AWS 付费。

IBM 为在亚马逊云平台上部署 DB2 提供了三种不同的选项：

- 用于评估和开发的 DB2 Express-C Amazon 机器镜像 (AMIs)
- 带有 DB2 Express 和 DB2 Workgroup 的按量付费生产就绪 AMI
- 使用你拥有的 DB2 许可证创建自定义 AMI 的能力

有关更多信息以及如何在 Amazon EC2 上开始使用 DB2，请访问：[http://www.ibm.com/db2/cloud](http://www.ibm.com/db2/cloud)

### 1.8.1.2 IBM 开发和测试云

IBM 云平台上的 IBM Smart Business 开发和测试（简称 IBM 开发者云）提供与 AWS 类似的服务，但专注于开发和测试。它允许按需灵活配置资源，成本预先确定。

在撰写本文时，IBM 开发者云上的 DB2 镜像包括：

- DB2 Express-C 9.7.1 PAYG（按量付费）。
  - 此镜像使用基于 32 位 SUSE Linux Enterprise Server (SLES) 构建的 DB2 Express-C 9.7.1。注意，使用 DB2 Express-C 是免费的；但是，你需要为基础设施付费。
- DB2 Enterprise Developer 9.7.1 - BYOL（自带许可证）。
  - 此镜像使用基于 32 位 SLES 构建的 DB2 Enterprise，并带有 IBM 数据库企业版开发者版 (DEDE) 许可证。
- DB2 Enterprise Developer 9.7.1 64 位 - BYOL。
  - 此镜像使用基于 64 位 Red Hat Enterprise Linux (RHEL) 的 DB2 Enterprise，并带有 IBM 数据库企业版开发者版 (DEDE) 许可证。

有关 IBM 开发者云的更多信息，请访问 [http://ibm.com/cloud/enterprise](http://ibm.com/cloud/enterprise)

### 1.8.1.3 用于开发和测试的 IBM CloudBurst

IBM CloudBurst 允许你在公司内部构建自己的私有云。它使用 IBM System x® BladeCenter® 平台，在硬件、中间件和应用之间提供预安装的、完全集成的服务管理功能。它包括来自 IBM 的实施服务。将 IBM CloudBurst 与 IBM WebSphere CloudBurst 设备一起使用。这两个关键产品相辅相成，帮助你的客户更轻松、更快速、更具成本效益地实现目标。

有关更多信息，请访问 <http://www-01.ibm.com/software/tivoli/products/cloudburst/>

### 1.8.1.4 IBM WebSphere CloudBurst

IBM WebSphere CloudBurst 是一种帮助开发人员建立和部署软件镜像和模式到云环境的设备。WebSphere CloudBurst 设备就像是软件环境进入私有云的“分发器”，而 IBM CloudBurst 则是“接收”私有云环境。

在撰写本文时，IBM Websphere CloudBurst 上可用的 DB2 镜像为：

- 32 位 DB2 Enterprise 9.7.0 试用版，评估期为 90 天
  - 此镜像使用基于 32 位 SLES 构建的 DB2 Enterprise

有关更多信息，请访问 <http://www-01.ibm.com/software/webservers/cloudburst/>

### 1.8.1.5 Rightscale

RightScale 是一个云管理平台。它允许你通过自动化、控制和可移植性更轻松地部署和管理业务关键应用。Rightscale 提供在其网站上发布的服务器模板和脚本（称为 RightScripts），允许你轻松实现操作自动化、克隆和重复。

在撰写本文时，*表 1.5* 中列出的模板和 RightScripts 可用于 DB2。

| 类型 | 名称 | 描述 |
| :--- | :--- | :--- |
| ServerTemplate | IBM DB2 Express-C 9.7 (CentOS 5.2) | 安装并配置 DB2 Express-C 9.7 |
| ServerTemplate | IBM DB2 Express-C 9.7 (Ubuntu 8.04) | 安装并配置 DB2 Express-C 9.7 |
| RightScript | VPN Cubed Client Connect | 将服务器添加到现有 VPN |
| RightScript | Add Users to Group | 将用户添加到组 |
| RightScript | Backup DB2 Database | 在运行中的实例上运行 DB2 备份 |
| RightScript | Create database | 创建一个数据库 |
| RightScript | Create Group | 创建一个新组 |
| RightScript | Create sample database | 运行 db2sampp |
| RightScript | Create User | 创建一个用户 |
| RightScript | Delete Group | 删除一个系统组 |
| RightScript | Delete User | 删除一个系统用户 |
| RightScript | Drop a database | 删除一个数据库 |
| RightScript | Install DB2 Express-C | 安装 DB2 Express-C 9.7 |
| RightScript | Remove Users from a Group | 从组中移除用户 |
| RightScript | Run command within db2 | 从 db2 命令行运行命令 |
| RightScript | Set DB2 parameter | 使用 db2set 命令 |
| RightScript | Start DB2 | 通过运行 db2start 启动 DB2 |
| RightScript | Start DB2 Administration Server | 通过运行 db2admin start 启动 DAS 服务器 |
| RightScript | Stop DB2 | 运行 "db2stop" 命令以停止 db2 |
| RightScript | Stop DB2 Administration Server | 通过运行 db2admin stop 停止 DAS 服务器 |

*表 1.5 - DB2 的 Rightscale 模板和 RightScripts*

有关 Rightscale 和 DB2 的更多信息，请访问  
[http://support.rightscale.com/27-Partners/IBM_DB2](http://support.rightscale.com/27-Partners/IBM_DB2)

## 1.8.2 用于 VMware 的 DB2 Express-C 虚拟设备

如果你在公司的环境中使用 VMware，你可以使用适用于 Linux 和 Windows 的 32 位或 64 位 DB2 Express-C 虚拟设备。从 http://www.ibm.com/db2/express/download.html 下载这些设备

## 1.9 示例程序

为了帮助你学习如何使用 DB2 作为数据服务器在不同语言中进行编程，你可以查看随 DB2 服务器安装提供的示例应用程序，这些示例位于 SQLLIB\samples 目录中。下图 1.10 展示了 Windows 平台上随 DB2 提供的一些示例程序。

![](img/5f6ba170efa3a607142589708531bef8_46_0.png)

图 1.10 - 随 DB2 提供的示例程序

## 1.10 练习

- 使用 IBM Data Studio，创建一个什么也不做的存储过程 P2。从 DB2 命令窗口或 Linux shell 中调用此存储过程。
- 使用 IBM Data Studio，创建一个不接收参数并返回值为 2000 的函数 F2。从 DB2 命令窗口或 Linux shell 中调用此函数。
- 修改 P2，使其现在调用 F2。测试一下！

## 1.11 摘要

在本章中，我们探讨了 DB2 如何提供灵活性，以便在服务器数据库内部或通过连接到 DB2 数据服务器的客户端应用程序来编写数据库应用程序。

服务器端应用程序涵盖内容包括存储过程、用户定义函数和触发器。

在客户端方面，我们讨论了 DB2 应用程序开发允许的众多编程接口和方法，再次展示了 DB2 作为数据库服务器的卓越灵活性和容量。

## 1.12 复习问题

1. 列出使用存储过程的一个优点
2. 用户如何扩展 SQL 语言？
3. CLI 和 ODBC 之间的区别是什么？
4. 静态 SQL 和动态 SQL 之间的区别是什么？
5. 提及 JDBC Type 2 和 JDBC Type 4 驱动程序的一个区别？
6. 下列哪些对象存储在 DB2 数据库中？
    - A. 表
    - B. 存储过程
    - C. 用户定义函数
    - D. 以上所有
    - E. 以上都不是
7. 下列哪些语言可用于在 DB2 中编码存储过程？
    - A. SQL PL
    - B. PL/SQL
    - C. Cobol
    - D. Java
    - E. 以上所有
8. 选择正确的陈述：
    - A. 当数据库不断通过大量更新、删除和插入进行更改时，静态 SQL 通常比动态 SQL 更快。
    - B. 嵌入式 SQL 必须是静态 SQL

