
## 考试要点

能够定义 Oracle 监听器（listener）的主要职责。为了充分理解 Oracle 监听器的功能，你应该理解监听器如何响应客户端连接请求。此外，你应该知道直连连接（bequeath connections）和重定向连接（redirect connections）之间的区别，并知道监听器在什么情况下会使用每种连接。同时，你应该能够概述这些连接类型中涉及的步骤。

能够定义 `listener.ora` 文件以及创建该文件的方法。为了理解此文件的目的，你应该知道它的默认内容以及如何使用 Oracle Net Manager 工具对其进行修改。此外，你应该能够定义文件的不同部分，并了解其中包含的可选参数定义。你还应该理解当配置了一个或多个监听器时 `listener.ora` 文件的结构。

理解如何使用 `lsnrctl` 命令行工具。为了启动和关闭监听器，你应该知道如何使用 `lsnrctl` 命令行工具。你还需要能够解释 `lsnrctl` 工具的命令行选项，例如 `services`、`status` 和 `reload`。在使用该工具时，你还应该知道可供使用的不同选项，并能够定义各种命令。

理解静态服务注册（static service registration）和动态服务注册（dynamic service registration）的概念。能够定义静态服务注册与动态服务注册之间的区别，并知道使用动态服务注册的优势。此外，还要注意必须使用静态服务注册的情况。最后，熟悉为了启用动态服务注册需要设置的 `init.ora` 参数。

理解 Oracle 和 Java 连接的基础。你应该了解配置 Oracle 的基础，以便通过 IIOP 和 HTTP 连接到 Oracle9i JVM。

能够诊断并修复网络连接问题。你应该知道可能发生的服务器端错误类型以及如何诊断和修复这些问题。你应该能够定义记录（logging）和跟踪（tracing）之间的区别，并知道如何使用跟踪文件中可能发现的数据包信息。

## 关键术语

在参加考试之前，请确保你熟悉以下术语：

- 直连连接 (bequeath connection)
- `lsnrctl`
- 专用服务器 (dedicated server)
- `lsnrctl stop`
- 动态服务注册 (dynamic service registration)
- 端口 (port)
- 主机 (host)
- 重定向连接 (redirect connection)
- 监听器 (listener)
- 拒绝数据包 (refuse packet)
- `listener.ora`
- 静态服务注册 (static service registration)
- 记录 (logging)
- 跟踪 (tracing)

## 复习题

+ 1. 为了启动 Oracle 监听器，服务器上必须存在哪个文件？
A. `listener.ora`
B. `lsnrctl.ora`
C. `sqlnet.ora`
D. `tnsnames.ora`

+ 2. 监听器将用户连接到 Oracle9i 实例可能的方法有哪些？（选择所有适用）。
A. 预产生连接 (Prespawn connection)
B. 重定向连接 (Redirect connection)
C. 直连连接 (Bequeath connection)
D. 多路通过连接 (Multipass connection)

+ 3. Oracle 监听器的默认名称是什么？
A. `lsnrctl`
B. Listen
C. `sqlnet`
D. `tnslistener`
E. 以上都不是

+ 4. 监听器处理的数据库最大数量是多少？
A. 1 个数据库
B. 2 个数据库
C. 10 个数据库
D. 25 个数据库
E. 以上都不是

+ 5. 服务器上应该存在的 `listener.ora` 文件最大数量是多少？
+ A. 一个
+ B. 两个
+ C. 四个
+ D. 八个
+ E. 以上都不是

+ 6. 下列描述描述哪个特征：“记录网络上发生的所有事件，即使没有发生错误也是如此。”
+ A. Oracle Net Manager
B. 网络跟踪 (Network tracing)
C. 网络记录 (Network logging)
D. 以上都不是

+ 7. 当使用服务的自动注册时，你不会在以下哪个文件中看到服务列表？
+ A. `sqlnet.ora`
B. `tnsnames.ora`
C. `listener.ora`
D. 以上都不是

+ 8. 下列哪些不是 `listener.ora` 的设置？（选择所有适用。）
+ A. Listener name = LISTENER
B. Port = 1521
C. Protocol = IPX
D. Protocol = TCP/IP
E. Listener name = `lsnrctl`

+ 9. 下列哪项是用于管理监听器的命令行界面？
+ A. LISTENER
B. `lismgr`
C. TCPCTL
D. `lsnrctl`
E. 以上都不是

+ 10. 你应该选择哪个 Oracle Net Manager 图标来管理监听器？
+ A. Services
B. Listener Names
C. Profile
D. Listeners
E. 以上都不是

+ 11. 哪个参数设置了服务器进程等待获取有效客户端请求的秒数？
+ A. `connect_waittime_listener_name`
B. `connect_wait_listener_name`
C. `timeout_listener_name`
D. `connect_timeout_listener_name`

+ 12. 下列哪项是产生产生信息信息的跟踪级别？
+ A. ADMIN
B. USER
C. ALL
D. 以上都不是

+ 13. 可以配置的监听器最大数量是多少？
+ A. 一个
+ B. 两个
+ C. 四个
+ D. 八个
+ E. 以上都不是

+ 14. 有一个名为 LISTENER 的监听器。启动它的正确方法是哪一个？
+ A. `lsnrctl startup`
B. `lsnrctl start`
C. `listener start`
D. `listener startup`

+ 15. 有一个名为 listener 的监听器。启动它的正确命令是哪一个？
+ A. `lsnrctl startup`
B. `lsnrctl start`
C. `listener start`
D. `listener startup`
E. `lsnrctl start`

+ 16. 使用 Net Manager 对 `listener.ora` 文件进行了修改。这些修改何时生效？
+ A. 立即生效
B. 退出 Net Manager 后
C. 保存 `listener.ora` 时
D. `refresh`
+ E. 以上都不是

+ 17. 有一个名为 listener 的监听器，你想使用 `lsnrctl` 进行编辑。你会使用哪个命令来指定该监听器？
+ A. `set_listener`
B. `accept_listener`
C. `reload`
D. `refresh`

+ 18. 使用 `lsnrctl` 进行了修改。为了使更改永久生效，必须将什么设置为 ON？
+ A. `configuration`
B. `listener.ora`
C. `stop`
D. `save`

+ 19. 管理员想在使用 `lsnrctl` 修改文件后对监听器文件进行备份。执行哪个命令来实现此备份？
+ A. `create_backup`
B. `configuration_stop`
C. `save`
D. `backup`

+ 20. 当为 TCP/IP Oracle9i 配置监听器时，使用的端口号是多少？
+ A. 1521
B. 2482
C. 2481
D. 1526

## 复习题答案

+ A. 监听器是管理连接请求的进程。`listener.ora` 文件用于配置监听器。`sqlnet.ora` 是可选的客户端和服务端文件。`tnsnames.ora` 文件用于本地解析。不存在 `lsnrctl.ora` 这种文件。

+ B. 监听器可以通过两种方式之一处理连接请求：它可以产生进程并将控制传递（bequeath）给该进程，或者在使用共享服务器时将进程重定向到专用进程或分发器。

+ E. 使用 Oracle Net Manager 创建监听器时，助手建议默认名称为 LISTENER。通过命令行工具启动和停止监听器时，如果没有提供监听器名称，工具将假设监听器的名称为 LISTENER。

+ E. 虽然监听器可以监听的服务数量没有物理限制，但只有一个 `listener.ora` 文件。如果配置了多个监听器，仍然只有一个 `listener.ora` 文件。

+ B. 网络跟踪是在没有错误发生时记录网络上所有事件。跟踪应谨慎使用，并仅在出现网络问题时作为最后手段。记录将记录重大事件，如监听器启动和连接请求。

+ C. 当服务自动注册时……

+ A. 默认监听器的名称为 LISTENER，并在端口 1521 上监听 TCP/IP 连接。

# 86 第 2 章 · 在服务器上配置 Oracle Net

- 9. LISTENER 是 Oracle 监听器的默认名称。并没有名为 `lsmgr` 的实用程序，那实际上是一个用于启动和停止 `SQL*NET` 版本 1 监听器的旧实用程序。使用 `lsnrctl` 命令来管理监听器。

- 10. 熟悉 Oracle Net Manager 界面。Listeners（监听器）是正确的选择。Profile（配置文件）用于 `sqlnet.ora` 的管理。其他选项不是有效的菜单选项。

- 11. 当用户发起连接请求时，监听器会将控制权传递给某些服务器进程或调度器（dispatcher）。一旦用户连接到此进程，所有与数据库的协商和交互将通过该进程进行。如果用户提供了无效的用户 ID 或密码，该进程将等待一段时间以获得有效响应。如果用户在规定时间内没有通过有效响应联系服务器进程，则服务器进程将终止，用户必须重新联系监听器，以便监听器能够再次生成进程或将客户端重定向到现有的调度器。进程等待这段时间由 `connect_timeout_listener_name` 参数指定，单位为秒。

- 12. 可用的最高跟踪级别是 SUPPORT 级。这是用于跟踪数据包流量信息的级别。

- 13. E. 每个服务器可以配置的监听器数量没有上限。

- 14. B. 默认监听器名称为 LISTENER。由于这是默认值，只需输入 `lsnrctl start` 即可。在这种情况下，假设 LISTENER 是要启动的监听器。

- 15. E. Oracle 期望监听器的默认名为 LISTENER。启动监听器的设施程序是 `lsnrctl`。使用 `lsnrctl start` 将启动默认监听器。要启动另一个名称的监听器，请输入 `lsnrctl start listener_name`。

- 16. E. 无论使用 Oracle Net Manager 手动修改还是使用 `lsnrctl` 对监听器文件进行任何修改，必须重新加载监听器修改才能生效。要执行此重载，进入命令行并输入 `lsnrctl reload`。你也可以停止并启动监听器，效果是相同的。由于 `lsnrctl reload` 并不是选项之一，上述所有内容都不是正确答案。

- 17. A. 如果在使用 `lsnrctl` 时想要管理默认监听器以外的任何监听器，必须指定该监听器。`set` 命令用于更改 `lsnrctl` 会话设置。因此，`set current_listener listener1` 是正确的命令。

- 18. C. 在 `lsnrctl` 设施中对 `listener.ora` 文件进行的更改可以是永久的。要使更改永久，将 `save_config_on_stop` 设置为 ON。

- 19. C. DBA 在使用 `lsnrctl` 对现有的 `listener.ora` 文件进行修改后，可以进行备份。备份将命名为 `listener.bak`。这是通过 `save_config` 选项实现的。

- 20. B. 当你想为通过 TCP/IP 使用 SSL 的 HTTP 和 IIOP 连接配置 Oracle Net 时，使用端口 2482。当使用 TCP/IP 用于 HTTP 和 IIOP 连接时，使用端口 2481。

## 为客户端配置 Oracle Net

ORACLE9i: DBA 基础 II 本章涵盖的考试目标：

- 描述主机命名（Host Naming）与本地服务名解析（local service name resolution）之间的区别。
- 使用 Oracle Net 配置助手（Oracle Net Configuration Assistant）配置：主机命名、本地命名方法、网络服务名。
- 执行简单的连接故障排除。

> 考试目标可能会随时更改，恕不另行通知，并由 Oracle 单方面裁权决定。请访问 Oracle 认证网站（http://www.oracle.com/education/certification/）查看最新的考试目标列表。

![](img/4d4ebf1b63c52ce2a364aa79830c39e0_134_0.png)

一旦正确配置了 Oracle 服务器，你就可以专注于配置客户端，以允许其连接到 Oracle 服务器。本章详细说明了 Oracle 客户端配置的基本网络元素。它讨论了在创建网络服务名时可以选择的不同类型的服务名模型。此外，它还详细说明了可用的服务解析配置，以及如何使用 Oracle Net Manager 配置主机命名和本地命名。它还讨论了可能发生的客户端故障类型以及如何排查客户端连接问题。

理解如何配置 Oracle 客户端以连接 Oracle 服务器至关重要。如果没有如何配置客户端的正确知识，你的连接选择将受到限制。DBA 必须理解组织的网络需求和所需的连接类型（例如，客户端/服务器连接、三层架构连接），以便对客户端配置做出适当选择。本章将阐明你可用的客户端连接选项以及如何排查客户端连接问题。

# 客户端名称解析选项

当客户端需要连接到 Oracle 服务器时，客户端必须提供三部分信息：用户 ID、密码和网络服务名。服务名以连接描述符（connect descriptor）的形式提供必要信息，用于在网络中定位 Oracle 服务器的名称。

此连接描述符描述了 Oracle 服务器的路径及其服务名，服务名是 Oracle 数据库的别名。根据你选择的名称解析方法，这些信息存储在不同的位置。

## 客户端名称解析

> 注意：服务名可能会随时更改，恕不另行通知，并由 Oracle 单方面裁权决定。请访问 Oracle 认证网站（http://www.oracle.com/education/certification/）查看最新的考试目标列表。

服务名以连接描述符的形式提供必要信息，用于在网络中定位 Oracle 服务器的名称。此连接描述符描述了 Oracle 服务器的路径及其服务名，服务名是 Oracle 数据库的别名。根据你选择的名称解析方法，这些信息存储在不同的位置。

## 主机命名方法

在服务器较少的小网络中，你可以利用主机命名。主机命名可以让你避免在客户端上进行配置，尽管它具有局限性。使用主机命名的四个前提是：

# 配置主机命名方法

默认情况下，Oracle 在尝试使用本地命名连接后才会尝试使用主机命名方法。如果你想覆盖解析名称的默认搜索路径，请设置客户端 `sqlnet.ora` 文件中的 `NAMES.DIRECTORY_PATH` 参数，使其仅搜索主机命名。你可以使用 Oracle Net Manager 配置此参数（见图 3.1）。

使用 Oracle Net Manager 配置参数，从 Local 选项卡选择 Profile，并在屏幕顶部下拉列表中选择 Naming。这会列出可用的命名方法列表。Selected Methods（已选方法）列表显示正在使用的命名方法以及使用这些方法解析服务名的顺序。Available Methods（可用方法）列表

更改可用方法列表，使用鼠标高亮名称并点击箭头 (>) 将其包含在已选列表中。你可以通过在已选列表中选择它并点击另一个键 (<) 来移除名称。你还可以使用 Demote（下移）和 Promote（上）按钮来更改列表顺序。从 Selected Methods 列表中选择一个名称并点击 Demote 按钮将其向下移动，或点击 Promote 按钮将其向上移动。确保 HOSTNAME（主机）出现在 Selected Methods 列表中。

# 图 3.1 Oracle Net Manager - Oracle 配置屏幕

![](img/4d4ebf1b63c52ce2a364aa79830c39e0_136_0.png)

# 客户端名称解析选项 93

一旦保存配置，Oracle 将根据你所做的更改更新 `sqlnet.ora` 文件。以下是 `sqlnet.ora` 文件的示例。
