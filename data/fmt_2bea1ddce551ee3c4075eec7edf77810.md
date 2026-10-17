
```
version: 1
dn: cn=mhuffman,ou=IF,o=CLE
changetype: add
objectclass: inetorgperson
sn: Huffman
title: Manager

dn: cn=cgrayson,ou=IF,o=CLE
changetype: modify
replace: title
title: Vice President
```

7. 按 `Esc` 键。

8. 输入 `:quit`。

9. 通过打开 web 浏览器并导航至 `https://your_server's_IP_address/nps/iManager.html` 来启动 iManager。

10. 在 **eDirectory 维护实用工具**下，选择 **导入转换导出向导**。

11. 在 **欢迎** 屏幕上，标记 **从磁盘文件导入数据**，然后单击 **下一步**。

12. 在 **文件类型** 下拉列表中，选择 `LDIF`。

13. 在 **要导入的文件** 字段中，浏览并选择 `/tmp/newuser.ldif`。

14. 在 **高级设置** 下，取消勾选 **遇到错误时退出**。

15. 标记 **运行详细模式并添加没有更改类型的记录**，然后单击 **下一步**。

16. 在 **服务器名称/IP 地址** 字段中，输入您的服务器 IP 地址。

17. 在 **端口** 字段中，输入 `636`。

18. 在 **DER 文件** 字段中，输入 `/etc/opt/novell/SSCert.der`。

19. 标记 **认证登录**。

20. 在 **用户 DN** 字段中，输入 `cn=admin,ou=IF,o=CLE`。

21. 在 **password** 字段中，输入 `novell`。

22. 在 **高级设置** 下，取消勾选 **使用 LBURP**。

23. 标记 **允许前向引用**，然后单击 **下一步**。

24. 选择 **完成**。

25. 等待文件导入。

26. 当提示过程完成时，单击 **关闭**。

27. 在 **eDirectory 管理**下，使用 **修改对象** 任务验证 `mhhuffman.IFCLE` 对象是否已创建，以及 `cgrayson.IFCLE` 对象的 `title` 是否已修改。

我们已完成对 LDAP 的介绍。理解这里介绍的 LDAP 基础知识至关重要。回顾一下，我之前说过 eDirectory 是 NNLS 的骨干，因为所有组件都依赖于它。然而，这些组件也依赖于 LDAP 来访问 eDirectory 信息。

现在，让我们讨论如何在 Linux 上管理 eDirectory。

## 在 Linux 上管理 eDirectory

**涵盖的测试目标：**

- 5. 执行 eDirectory 管理任务。

在 Linux 上管理 eDirectory 时，您将主要使用以下三个工具：

- 命令行实用工具

- iManager

- iMonitor

在本节中，我们将讨论每个工具的基本用法。我们还将介绍如何执行 eDirectory 健康检查。

### 命令行实用工具

在 Linux 平台上，eDirectory 包含若干可从命令行使用的实用工具，用于管理您的 eDirectory 数据库。详细讨论每个实用工具超出了本书的范围。在可能的情况下，我们将使用 iManager 和 iMonitor 作为主要的管理工具。

NNLS 中包含的 eDirectory 命令行实用工具列表见表 5.3。

**表 5.3**

# eDirectory 命令行实用工具

| 实用工具 | 描述 |

| :--- | :--- |

| `/etc/init.d/ndsd` | `ndsd` init 脚本用于启动和停止服务器上的 eDirectory 服务。<br><br>它与其他 init 脚本的使用方式类似，带有 `start` 或 `stop` 修饰符。例如，要停止服务，请输入 `/etc/init.d/ndsd stop`。<br><br>要启动服务，请输入：`/etc/init.d/ndsd start`。 |

| `Ldapconfig` | `ldapconfig` 实用工具可用于配置树中的 LDAP 服务器和 LDAP Group 对象。<br><br>在 shell 提示符下输入 `man ldapconfig` 以查看该实用工具使用的各种参数。 |

| `Ndsbackup` | `ndsbackup` 实用工具用于将 eDirectory 目录树的逻辑结构保存到文件中。如果树中的对象发生问题，您可以使用此实用工具从先前创建的备份文件中恢复它们。 |

| `Ndsconfig` | `ndsconfig` 实用工具用于配置 eDirectory 目录树本身。<br><br>可用于创建新目录树、修改现有目录树、向现有目录树添加服务器或从目录树中移除服务器。<br><br>在 shell 提示符下输入 `man ndsconfig` 以查看该实用工具使用的各种参数。 |

| `Ndslogin` | `ndslogin` 实用工具用于检查 eDirectory 认证是否正常工作。<br><br>运行时，您提供一个用户名作为修饰符（例如，`ndslogin cgrayson.if.c1e`）。然后该实用工具提示您输入用户密码。该实用工具随后测试、认证并报告结果。 |

| `Ndsmerge` | 此实用工具可用于将两个独立的 eDirectory 目录树合并为一个目录树。<br><br>这可能是一个敏感的操作。在尝试之前，请在 shell 提示符下输入 `man ndsmerge` 并阅读准备目录树和服务器的说明。 |

| `Ndsrepair` | 由于 eDirectory 的复制和分布式特性，由于通信链路故障和其他问题，错误可能会潜入数据库。<br><br>`ndsrepair` 实用工具可用于检查本地 eDirectory 数据库中的错误并修复它们。<br><br>要运行完整的无人值守修复，请在 shell 提示符下输入 `ndsrepair -U`。<br><br>要查看该实用工具的所有可用选项，请在 shell 提示符下输入 `man nds repair`。 |

## 表 5.3（续）

| 实用程序 | 描述 |

| :-------- | :------------------------------------------------------------------------------ |

| `Ndsstat` | `ndsstat` 实用程序用于显示本地 eDirectory 服务器的信息。它显示树名称、服务器可分辨名称以及已安装的 eDirectory 版本。要使用该实用程序，只需在 shell 提示符下输入 `ndsstat` 即可。 |

| `Ndstrace` | 此实用程序可用于跟踪 eDirectory 的内部活动。此实用程序具有许多选项和参数。有关如何使用此实用程序的更多信息，请查看 `ndstrace` man 手册页。 |

在使用这些实用程序时，您需要记住的一件事是它们是*以服务器为中心*的。也就是说，它们只配置本地服务器上的 eDirectory 服务。

如果您的 eDirectory 树很大并且包含许多服务器，这可能会变得繁琐。在这种情况下，您应该使用 iManager 和 iMonitor。事实上，在 CLE 考试中，您应该首先使用 iMonitor 和 iManager 完成所有可能完成的工作。只有当无法使用这两个实用程序执行任务时，才应考虑使用命令行实用程序。

### 使用 iManager

Novell 的 iManager 是一种基于 Web 的实用程序，用于管理您的 eDirectory 树。在本书的练习中，我们已经多次使用过 iManager。通过打开 web 浏览器并访问 `http://your_server_address/nps/iManager.html` 即可访问 iManager。

执行此操作后，将显示 iManager 身份验证页面，如图 5.38 所示。

iManager 使用 eDirectory 来控制访问权限。您可以在 iManager 中执行的任务取决于您在此页面中提供的凭据。

您应该知道 iManager 使用 LDAP 进行身份验证。如果您正在身份验证的用户存在于与您的服务器对象以及 LDAP Server 和 LDAP 组对象相同的上下文中，则只需提供无类型的用户名即可。

![](img/c7771e8540507f2b00c088c7a411b57b_250_0.png)

**图 5.38**

iManager 身份验证页面。
