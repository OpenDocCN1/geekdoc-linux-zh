
## 应用你的知识

4. 右侧面板中会出现用户管理工具列表。单击“Administrative Roles”工具。

5. 单击位于 SMC 窗口顶部的工具栏中的 Action。从下拉菜单中单击 Add Administrative Role。Add Administrative Role 窗口出现。按以下信息填写字段：

Role Name: adminusr
Full Name: Administrative Assistant
Description: Admin assistant for performing general administrative tasks
Role ID number: <accept the default>
Role Shell: Administrator's Bourne

6. 下一屏幕会要求你输入角色密码。输入长度为 6–15 个字符的密码。单击“下一步”按钮继续。

7. 下一个窗口用于分配权限。在中间窗格中选择 System Administrator 并单击“添加”按钮。在“Granted Rights”窗格下，应显示 System Administrator。单击“下一步”按钮继续。

8. 选择一个主目录，然后单击“下一步”按钮。

9. 在下一个窗口中，标题为 Assign Users to This Role，在第一个字段中输入 admin1，然后单击“添加”按钮。单击“下一步”按钮继续。

10. 当摘要窗口出现时，单击“完成”按钮。分配角色给用户的过程已完成。

11. 注销并以 admin1 身份重新登录。启动 SMC，并测试新的用户角色。你应具有一般系统管理权限，例如添加新用户、安排作业和共享文件系统。

## 复习问题

1. 关于 Solaris Management Console，以下哪三个陈述是正确的？
A. 它提供了一种图形化方式来管理元设备。
B. 它通过将系统管理工具集中在一个位置来简化管理。
C. 它允许在一个位置管理所有 Solaris Management Console 服务器。
D. 它允许系统管理员将管理任务委派给非 root 用户，而无需提供 root 密码。

2. AdminSuite 3.0 用于完成以下哪些任务？选择所有适用项。
A. 管理用户帐户
B. 管理共享资源
C. 管理磁盘
D. 管理进程
E. 安排进程
F. 管理串行端口
G. 设置 AutoClients

## 应用你的知识

3. SMC 用于完成以下哪些任务？选择所有适用项。
- A. 管理用户帐户
- B. 管理共享资源
- C. 管理磁盘
- D. 管理进程
- E. 安排进程
- F. 管理串行端口
- G. 设置 AutoClients

4. SMC 的三个组件是什么？
- A. GUI 工具
- B. SMC Client
- C. SMC Server
- D. Toolbox Editor
- E. RBAC

5. 用于启动 AdminSuite 的命令是什么？
- A. 它必须从 Solaris Management Console 启动。
- B. admapp.
- C. solstice.
- D. adminsuite.
- E. smc.
- F. admsvr.

6. SMC 与 AdminSuite 3.0 之间有哪些主要区别？选择所有适用项。
- A. 只有 SMC 支持基于角色的访问控制。
- B. 只有 AdminSuite 可以管理用户帐户。
- C. 只有 SMC 可以管理磁盘。
- D. 只有 AdminSuite 可以管理打印机。
- E. SMC 需要 SMC Server 运行；AdminSuite 不需要服务器守护进程。

## 复习问题的答案

1. B.、C.、D. SMC 通过将系统管理工具集中在一个位置来简化管理。它还允许在一个位置管理所有 Solaris Management Console 服务器。最后，它允许系统管理员将管理任务委派给非 root 用户，而无需提供 root 密码。

2. A.、B.、F. AdminSuite 3.0 提供了用于管理 Solaris 系统的一套集成工具。向导和对话框为管理用户帐户、组、邮件列表、计算机/网络、文件系统挂载/共享、串行端口、日志文件和名称服务域提供帮助和指导。

## 应用你的知识

3. A.、B.、C.、D.、E.、F. SMC 允许你从远程位置管理服务器上的管理服务和网络服务。使用 SMC，管理员可以在本地和远程系统上管理系统进程、网络资源、用户帐户、串行端口和磁盘分区。

4. B.、C.、D. SMC 有三个组件：
- The SMC Client, called SMC or Console
- The SMC Server
- The SMC Toolbox Editor

5. B. 要启动 AdminSuite，输入以下内容：

```
/opt/SUNWseam/3_0/bin/admapp.
```

6. A.、C. SMC 与 AdminSuite 3.0 之间的主要区别是只有 SMC 支持基于角色的访问控制，并且只有 SMC 可以管理磁盘。

## 目标

本章涵盖以下测试目标：

### 理解基于角色的访问控制
- 传统的基于超级用户的系统会向任何可以成为超级用户的人授予完全的超级用户权限。在 Solaris 8 操作环境中，通过基于角色的访问控制 (RBAC)，管理员可以将有限的管理能力分配给非 root 用户。本章描述了 RBAC 与 Solaris 安全性的关系。

### 理解 RBAC 支持数据库
- RBAC 依赖于四个数据库来为用户提供访问特权操作的权限。本章描述了 RBAC 数据库和配置命令。

## 第 20 章

## 基于角色的访问控制 (RBAC)

- **介绍** 731
- **使用 RBAC** 731
- **RBAC 组件** 737
  - 扩展用户属性 (user_attr) 数据库 738
  - 授权 (auth_attr) 数据库 740
  - 权限配置文件 (prof_attr) 数据库 742
  - 执行属性 (exec_attr) 数据库 745
- **摘要** 747
- **应用你的知识** 749

以下策略有助于你为考试做准备：
- 熟悉本章末尾“关键术语”部分中我提供的术语。准备好说明 RBAC 在 Solaris 安全方面的目的。还要准备好选择描述 RBAC 数据库特性的陈述。
- 练习使用 RBAC 以熟悉其功能。在 Solaris 系统上，逐步完成本章提供的示例。

## 介绍

向非 root 用户授予超级用户访问权限一直是 UNIX 系统中的一个问题。过去，你必须依赖第三方软件包 sudo 来提供此功能。问题在于 sudo 是一个不受支持的免费软件，必须从互联网下载并安装到你的系统上。在极端情况下，系统管理员必须在文件上设置 UID 权限位，以便用户可以以 root 身份执行命令。

在 Solaris 8 操作环境中，通过基于角色的访问控制 (RBAC)，管理员可以将有限的管理能力分配给非 root 用户。这是通过以下三个新功能实现的：
- 授权。授予访问受限功能的<|message|> 用户权利。
- 执行配置文件。用于对授权和具有特殊属性的命令进行分组的捆绑机制；例如，用户和组 ID 或超级用户 ID。
- 角色。用于执行一组管理任务的特殊类型的用户帐户。

> CAUTION
最常见的是，你可能会使用 RBAC 为系统内的管理任务提供超级用户访问权限。请谨慎行事，避免通过向未经授权的用户提供对管理功能的访问而造成安全漏洞。

## 使用 RBAC

为了更好地描述 RBAC，更容易先描述系统管理员如何在 Acme Corp 的虚构环境中利用 RBAC 将管理任务委派给非 root 用户。

在虚构公司 Acme Corp.，系统管理员任务繁重。他将把部分职责委派给工程部门的用户 Neil，后者有时会帮助进行系统管理任务。

系统管理员首先需要定义他希望 Neil 协助的任务。他已确定了三个任务：
- 更改用户密码，但不添加或删除帐户
- 挂载和共享文件系统
- 关闭系统

在 RBAC 中，当我们谈论委派管理任务时，它被称为角色帐户。角色帐户是一种特殊类型的用户帐户，旨在执行一组管理任务。它在大多数方面与普通用户帐户类似，只是用户只能在以其正常登录帐户登录系统后，通过 su 命令访问它。角色帐户不能用于正常登录，例如通过 CDE 登录窗口。从角色帐户中，用户可以访问具有特殊属性的命令，通常是 root 用户 ID，而这些 ID 在普通帐户中不可用。

在 Acme Corp.，系统管理员需要为他想要委派的任务定义一个角色用户名。让我们使用角色用户名“adminusr”。Neil 在使用其正常登录名 ncalkins 登录后，然后需要发出 su 命令并在每次想要执行管理任务时切换到 adminusr。

定义角色帐户最简单的方法是使用 Solaris Management Console，如上一章所述。第 19 章“Solaris Management Console 和 Solstice AdminSuite”提供了你为用户定义此管理角色所需的所有信息。然而在本章中，我将描述如何通过命令行创建角色。

到目前为止，我们已确定希望将角色帐户命名为 adminusr。系统管理员使用 roleadd 命令创建角色帐户。roleadd 命令将角色帐户添加到 /etc/passwd、/etc/shadow 和 /etc/user_attr 文件中。roleadd 命令的语法如下：

```
roleadd [-c comment] [-d dir] [-e expire] [-f inactive] \
[-g group] [-G group] [-m] [-k skel_dir] [-u uid] \
[-s shell] [-A authorization] <role username>
```

你会注意到 roleadd 看起来与第 5 章“设置用户帐户”中描述的 useradd 命令非常相似。表 20.1 描述了 roleadd 命令的选项。
