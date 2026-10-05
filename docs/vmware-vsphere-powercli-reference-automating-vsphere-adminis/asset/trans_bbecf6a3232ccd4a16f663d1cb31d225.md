

# Apache Subversion

如果你正在寻找一种可以在 Windows 环境中安装且相对直接的源码控制系统，那么 Apache Subversion (https://subversion.apache.org/) 可能非常适合你。Subversion 是一个开源版本控制系统，支持大多数操作系统，并为基于 Windows 的服务器运行它以及通过 Windows 客户端访问提供了优秀选项。在本章中，我们将介绍基于 Apache Subversion 构建的免费和商业软件包。有一些高级源码控制功能你可能会发现对商业企业非常有用，这些功能可以在付费软件中获得。根据你对开源软件的经验，你可能倾向于付费让公司为你提供相应级别的功能。

在本章中，我们将使用基于 Windows 的 Subversion 服务器和客户端产品 VisualSVN Server 和 TortoiseSVN（客户端）。VisualSVN 仅为 Visual Studio 提供了一个插件作为客户端来补充其 Subversion 服务器产品。由于大多数 PowerShell 代码编写者并不使用 Visual Studio，我们喜欢并推荐在开发 PowerShell 代码时使用 TortoiseSVN 客户端进行客户端源码控制操作。如果需要，TortoiseSVN 客户端也可以用于与其他 Subversion 服务器产品配合。

# VisualSVN Server

VisualSVN Server 由 VisualSVN Limited (https://www.visualsvn.com/) 提供，为在 Windows 上设置和配置 Subversion 服务器提供了一种简单的方法。它有两个版本：标准版（Standard Edition）和包含某些高级功能的付费企业版（Enterprise Edition）。

> 注意：标准版包含了足够入门的功能，这也是我们在本章中将使用的版本。一旦你熟悉了该系统，请考虑你是否会从商业许可企业版的任何高级功能中获益。

![](img/62596f5acc979040608a4e5111beb7d6_874_0.png)

# 系统要求

VisualSVN Server 可以运行在 Windows Server 2008 或更高版本上，并满足以下最低硬件规格：

- 1.4 GHz CPU
- 512 MB 内存
- 500 MB 硬盘空间

# 安装与初始配置

下载最新版本的 VisualSVN Server并将服务器软件安装到符合系统要求的 Windows 系统上。安装过程非常直观；只需按照屏幕上的提示操作，接受所有默认设置并选择标准版（图 24.1）。

**图 24.1** VisualSVN Server 安装

![](img/62596f5acc979040608a4e5111beb7d6_875_0.png)

安装完成后，打开 VisualSVN Server 管理控制台并查看可用功能（图 24.2）。

此时，请考虑在你的 VisualSVN 安装中使用证书。你可以使用内置的自签名证书，也可以用组织内部证书颁发机构 (CA) 的证书或商业第三方的证书替换它。本章后面的一些基于客户端的示例将受到此决定的影响。你组织内的安全需求可能会决定你的证书使用，通常情况下，向负责人员寻求建议是最好的。

# 图 24.2 VisualSVN Server 管理控制台

![](img/62596f5acc979040608a4e5111beb7d6_876_0.png)

> 提示：在 VisualSVN 中使用证书的更多详细信息可以在此处找到：https://www.visualsvn.com/support/topic/00034。

# TortoiseSVN 客户端

TortoiseSVN (http://tortoisesesn.net/) 也是免费使用的，即使在商业环境中也是如此。它提供了一个实现为 Windows 扩展的客户端——本质上是 Subversion 的一个良好图形界面。

# 系统要求

TortoiseSVN 可以运行在任何 Windows XP SP3 或更高版本的 Windows 系统上，包括 32 位和 64 位版本。安装需要管理员权限。

# 安装与初始配置

下载最新版本的 TortoiseSVN并将软件安装到符合系统要求的 Windows 客户端机器上。接受所有默认设置（图 24.3）。

# 图 24.3 TortoiseSVN 安装

![](img/62596f5acc979040608a4e5111beb7d6_877_0.png)

# 用户与组

一旦运行了 VisualSVN Server 和 TortoiseSVN 实例，首先需要做的工作是配置身份验证，以便分配代码访问的权限。可以在系统中创建本地用户（Users）和组（Groups）。但是，如果你已将 VisualSVN Server 加入活动目录（Active Directory），你就可以使用该系统中的用户和组，利用组织内现有的身份验证系统。

> 提示：在 VisualSVN 标准版中，你可以配合活动目录使用基本身份验证。这种方法存在一些缺点，特别是在安全性方面。企业版提供了具有增强安全功能的集成身份验证。你应该考虑哪个版本最符合你的需求。你可以在 https://www.visualsvn.com/server/features/windows-auth/ 找到功能概述。为了本章的目的，我们将使用标准版来演示 AD 用户和组的使用。

要从 VisualSVN Server 管理控制台配置身份验证，请导航到服务器上的身份验证（Authentication）选项卡。选择 Windows 身份验证（Windows Authentication）并勾选基本身份验证（Basic Authentication）框（图 24.4）。

# 图 24.4 VisualSVN 服务器身份验证

![](img/62596f5acc979040608a4e5111beb7d6_878_0.png)

# 创建仓库

你可以创建一个用于存储和管理代码的仓库。

1. 在 VisualSVN 服务器控制台中，右键点击存储库（Repositories），启动创建仓库向导，并选择 FSFS 仓库作为仓库类型（图 24.5）。
2. 为仓库命名。在本次练习中，使用 Repository01（图 24.6）。
3. 选择首选的仓库结构。在本次练习中，选择空仓库（Empty Repository）（图 24.7）。
4. 在向导的仓库访问权限（Repository Access Permissions）步骤中，选择自定义权限（Customize Permissions），点击自定义（Custom）按钮，然后从组或用户列表中选择你想要授予权限的组。（我们选择了一个包含我们想要授权的用户的组）。权限（Permissions）允许你授予多种权限。默认是读/写（Read / Write），这对于本示例是合适的（图 24.8）。点击确定设置组或用户权限，并点击创建以完成仓库的创建。

# 图 24.5 选择仓库类型

# 图 24.6 指定仓库名称

# 图 24.7 选择仓库结构

# 图 24.8 创建仓库权限

向导提供了仓库的摘要详情（图 24.9）。仓库 URL（Repository URL）是重要信息，你将用它从 TortoiseSVN 客户端连接到仓库。将其记录下来很有用，但必要时也可以重新获取。

单个仓库中可以维护一个或多个代码项目，或者根据你的需求，可以使用多个仓库来存储单个或多个项目。单个仓库适用于较低水平的持续服务器维护任务；反之，多个仓库可以在不同项目之间在触发器或电子邮件通知等项目上提供更大的灵活性。VisualSVN 网站包含关于如何规划 VisualSVN Server 仓库的优秀指南：https://www.visualsvn.com/support/svn/reposadmin/planning/。你还可以在更多关于在每个项目内部创建的默认文件夹的信息。

在 VisualSVN 服务器管理控制台中，右键点击刚刚创建的 Repository01 仓库，并选择新建 > 项目结构（New > Project Structure）。

# 图 24.9 摘要详情

