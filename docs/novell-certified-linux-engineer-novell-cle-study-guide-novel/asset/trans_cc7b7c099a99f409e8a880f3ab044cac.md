

## 表 5.3（续）

| 实用程序   | 描述                                                                     |
| :-------- | :------------------------------------------------------------------------------ |
| Ndsstat   | ndsstat 实用程序用于显示本地 eDirectory 服务器的信息。它显示树名称、服务器可分辨名称以及已安装的 eDirectory 版本。要使用该实用程序，只需在 shell 提示符下输入 `ndsstat` 即可。 |
| Ndstrace  | 此实用程序可用于跟踪 eDirectory 的内部活动。此实用程序具有许多选项和参数。有关如何使用此实用程序的更多信息，请查看 ndstrace man 手册页。 |

在使用这些实用程序时，您需要记住的一件事是它们是*以服务器为中心*的。也就是说，它们只配置本地服务器上的 eDirectory 服务。

如果您的 eDirectory 树很大并且包含许多服务器，这可能会变得繁琐。在这种情况下，您应该使用 iManager 和 iMonitor。事实上，在 CLE 考试中，您应该首先使用 iMonitor 和 iManager 完成所有可能完成的工作。只有当无法使用这两个实用程序执行任务时，才应考虑使用命令行实用程序。

## 使用 iManager

Novell 的 iManager 是一种基于 Web 的实用程序，用于管理您的 eDirectory 树。在本书的练习中，我们已经多次使用过 iManager。通过打开 web 浏览器并访问 *http://your_server_address/nps/iManager.html* 即可访问 iManager。

执行此操作后，将显示 iManager 身份验证页面，如图 5.38 所示。

iManager 使用 eDirectory 来控制访问权限。您可以在 iManager 中执行的任务取决于您在此页面中提供的凭据。

您应该知道 iManager 使用 LDAP 进行身份验证。如果您正在身份验证的用户存在于与您的服务器对象以及 LDAP Server 和 LDAP 组对象相同的上下文中，则只需提供无类型的用户名即可。

![](img/c7771e8540507f2b00c088c7a411b57b_250_0.png)

**图 5.38**
iManager 身份验证页面。

在之前的练习中，您只需输入 **admin** 即可进行身份验证。如果您想使用其他用户，则必须使用 LDAP 语法提供该用户的有类型可分辨名称。例如，如果我是 Christopher Grayson 并希望对我们刚安装的 CLE-TREE 进行身份验证，我将在用户名字段中输入 cn=cgrayson,ou=IF,0=CLE。

身份验证后，将显示 iManager 主页，如图 5.39 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_250_1.png)

**图 5.39**
iManager 主页。

请注意，屏幕左侧显示了一个标记为 **角色和任务** 的框架。默认情况下，iManager 显示其配置的所有*角色*和*任务*。

角色是以黑色文本显示的上级标题。这些是单个任务的分组。

任务是您可以使用 iManager 执行的具体作业。它们作为链接显示在角色标题下方。

如果您的权限在 eDirectory 树中不足以执行某项任务，当您尝试完成该任务时，右侧框架中将显示一条消息。如果您拥有适当级别的权限，则右侧框架中将显示完成所选任务所需的界面。

iManager 的出色功能之一是能够配置基于角色的服务（RBS）。默认情况下，未配置 RBS，这就是 iManager 为所有用户显示所有角色和任务的原因。如果您配置 RBS，可以将特定角色和任务与特定用户关联。执行此操作时，用户将自动获得在 eDirectory 树中完成相关任务所需的所有权限。

例如，您可以将用户与支持台角色关联，如图 5.40 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_251_0.png)

当该用户身份验证到 iManager 时，他或她仅在左侧框架中看到支持台角色。用户将自动获得在指定树区域内清除入侵者锁定、创建用户和设置用户密码所需的权限。

现在，让我们将注意力转向本章要介绍的最后一个 eDirectory 管理工具：iMonitor。

## 使用 iMonitor

iMonitor 与 iManager 的目的不同。iManager 主要用于管理树——执行添加用户、创建组和分配权限等日常任务。

另一方面，iMonitor 专门设计用于监视和故障排除树中服务器上的 eDirectory 数据库。您可以基于服务器、分区或副本查看当前的 eDirectory 操作。

iMonitor 以两种不同的模式运行：*直接模式*和*代理模式*。简而言之，当您使用 iMonitor 在处理 eDirectory 数据库和服务的服务器上访问 iMonitor 时，iMonitor 正在以直接模式运行。

在代理模式下，您在一个 eDirectory 树的服务器上访问 iMonitor，然后使用它来管理树中另一台服务器上的 eDirectory 数据库和服务。这是 iMonitor 的一个非常有用的功能。如果您将 NNLS 服务器安装到已安装运行旧版本 eDirectory 或 NDS 的服务器所在的现有 eDirectory 树中，您可以使用代理模式来管理这些服务器以及您的 NNLS 服务器。

要访问 iMonitor，请运行 web 浏览器并打开 https://your_server_IP_address:8010/nds。执行此操作时，iMonitor 将显示身份验证屏幕，如图 5.41 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_252_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_252_1.png)

与 iManager 不同，您使用标准的 eDirectory 命名约定来对 iMonitor 进行身份验证。例如，如果您想以先前安装的树中的 admin 用户身份进行身份验证，请在用户名字段中输入 **admin.IFCLE**。

与 iManager 一样，您可以在 iMonitor 中执行的任务受控于分配给用于对树进行身份验证的用户对象的权限。

iMonitor 中的大多数任务要求您使用的用户对象对服务器对象具有监管者（Supervisor）权限。这可以是您的树管理员用户，也可以是另一个您已授予服务器对象权限的用户。

身份验证后，将显示 iMonitor 主页，如图 5.42 所示。

iMonitor 主页显示服务器上 eDirectory 代理的摘要。您可以快速查看副本环中副本的同步状态以及服务器上运行的各种 eDirectory 进程的状态。

iMonitor 的一个关键作用是检查 eDirectory 树的健康状况。现在让我们谈谈它是如何进行的。

# 第 5 章 NNLS 安装和管理

**图 5.42**
iMonitor 主页。

![](img/c7771e8540507f2b00c088c7a411b57b_253_0.png)

## 使用 iMonitor 执行 eDirectory 健康检查

如前所述，eDirectory 使用分布式复制数据库。该服务以及数据库数据分布在树中的各个服务器之间。在大多数情况下，eDirectory 运行完美。目录信息在各个副本环周围同步，eDirectory 进程按计划发生。

然而，可能会出现某些干扰目录正常运行的情况。以下任何一项都可能导致 eDirectory 数据库中出现错误：

- 服务器之间的网络连接断开
- 时间同步丢失
- 硬件故障
- eDirectory 文件损坏

这只是可能向树中引入错误的网络问题的部分列表。幸运的是，Novell 提供了几种可用于修复这些错误的工具，其中 iMonitor 是关键工具之一。在本节中，我们将介绍如何使用 iMonitor 执行 eDirectory 健康检查。

您需要理解这些健康检查有多重要——实际上，如果长时间放任不管，大多数 eDirectory 问题会自动修复。经验丰富的 eDirectory 管理员将此称为“让树沉淀下来”（letting the tree settle down）。“时间能治愈所有伤痛”这句话非常适用。

多年来，我观察到许多 eDirectory 管理员立即着手尝试手动修复树中的问题。然而，这些问题中的大多数最终都会随时间自动修复。

