
## LDAP Group 对象
LDAP Group 对象还用于存储 LDAP 配置参数。该对象在安装过程中也会自动创建，并放置在与服务对象相同的上下文中，如图 5.36 所示。其名称为 LDAP Group – *your_server_name*。单个 LDAP Group 对象可以与树中的多个 LDAP 服务器相关联，使它们共享公共配置。如果网络和目录树规模非常大，这会非常有益。

![](img/c7771e8540507f2b00c088c7a411b57b_242_0.png)

**图 5.36**
eDirectory LDAP 对象。

## LDAP 绑定到 eDirectory
当客户端通过 LDAP 服务绑定到 eDirectory 时，前文讨论的 eDirectory 规则和权限同样适用，就好像客户端使用原生 eDirectory 调用访问目录一样。

如果 LDAP 客户端在未提供用户名或密码（即匿名）的情况下访问目录，它将被认证为 [Public] 并授予对目录树根的浏览权限（除非您修改了 [Public] 的默认权限分配）。

使用 LDAP Group 对象，您可以更改默认的匿名用户。您可以在树中创建一个用户，分配匿名 LDAP 用户所需的权限，并将新用户与 LDAP Group 关联。修改 LDAP Group 对象的属性（如图 5.37 所示）即可实现此操作。请记住，代理用户不能有密码或任何密码限制。

除非有非常充分的理由，否则建议保留默认的 [Public] 级别访问权限。您赋予该代理的权限将自动授予未认证的 LDAP 客户端。您应当谨慎行事。

![](img/c7771e8540507f2b00c088c7a411b57b_243_0.png)

如果 LDAP 客户端访问目录并提供有效的用户名和密码，则使用这些凭证进行认证。与认证用户对象关联的有效权限将授予该 LDAP 客户端。

鉴于此，让我们简要讨论如何使用 LDAP 和文本文件将对象导入您的树中。

## LDAP 数据互换格式 (LDIF)
LDAP 的一个非常实用的功能是 LDAP 数据互换格式 (LDIF) 规范。它允许您在简单的文本文件中定义目录对象（使用标准化格式），并将该文件导入目录树中。

您可以在文件中完成添加、删除和修改操作。您可以在同一文件中执行多个操作。详细讨论完整的 LDIF 规范超出了本书的范围。然而，我们将探索一个符合 LDIF 的文本文件中的两个示例条目：

> **注意** 如果您想了解有关创建 LDIF 文件的更多信息，请访问 http://developer.netscape.com/docs/manuals/directory/admin30/ldif.htm。

```
version: 1
dn: cn=mhuffman,ou=IF,o=CLE
changetype: add
objectclass: inetOrgPerson
sn: Huffmann
title: Manager

dn: cn=jcorry,ou=SLC,o=CLE
changetype: delete

dn: cn=cgrayson,ou=IF,o=CLE
changetype: modify
replace: title
title: Vice President
```

如果将此信息保存在文本文件中，就可以将其导入您的 eDirectory 树。该文件在 IFCLE 容器中创建一个名为 **mhuffman** 的新用户对象。

此文件中的第二个操作从 SLC.CLE 容器中删除一个名为 **jcorry** 的用户（假设该用户已存在于此）。最后一个操作修改 IFCLE 中的 **cgrayson** 对象，并更改其 title 属性的值。

eDirectory 包含一个名为 *Import Convert Export* 实用工具 (*ice*) 的工具，可用于将 LDIF 文件导入树中，以及将对象 *从* 树中导出到 LDIF 文件。iManager 包含一个图形界面，可用于配置 ice 作业并运行 ice 引擎以导入文件。

让我们在实验练习 5.6 中练习导入 LDIF 文件。

## 实验练习 5.6：导入 LDIF 文件
在这个实验中，您将创建一个 LDIF 文件，该文件向树中导入新用户并修改现有用户。完成以下步骤：

1. 如有必要，启动您的服务器并使用密码为 **novell** 的 **student** 用户进行认证。
2. 打开一个终端会话。
3. 输入 **su -** 并提供密码 **novell**，以切换到 root 用户账户。
4. 在 shell 提示符下，输入 `vi /tmp/newuser.ldif`。
5. 按 **Ins** 键。
6. 将以下文本输入到文件中：
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
7. 按 **Esc** 键。
8. 输入 **:quit**。
9. 通过打开 web 浏览器并导航至 https://your_server's_IP_address/nps/iManager.html 来启动 iManager。
10. 在 **eDirectory 维护实用工具**下，选择 **导入转换导出向导**。
11. 在 **欢迎** 屏幕上，标记 **从磁盘文件导入数据**，然后单击 **下一步**。
12. 在 **文件类型** 下拉列表中，选择 **LDIF**。
13. 在 **要导入的文件** 字段中，浏览并选择 `/tmp/newuser.ldif`。
14. 在 **高级设置** 下，取消勾选 **遇到错误时退出**。
15. 标记 **运行详细模式并添加没有更改类型的记录**，然后单击 **下一步**。
16. 在 **服务器名称/IP 地址** 字段中，输入您的服务器 IP 地址。
17. 在 **端口** 字段中，输入 **636**。
18. 在 **DER 文件** 字段中，输入 `/etc/opt/novell/SSCert.der`。
19. 标记 **认证登录**。
20. 在 **用户 DN** 字段中，输入 `cn=admin,ou=IF,o=CLE`。
21. 在 **password** 字段中，输入 **novell**。
22. 在 **高级设置** 下，取消勾选 **使用 LBURP**。
23. 标记 **允许前向引用**，然后单击 **下一步**。
24. 选择 **完成**。
25. 等待文件导入。
26. 当提示过程完成时，单击 **关闭**。
27. 在 **eDirectory 管理**下，使用 **修改对象** 任务验证 mhhuffman.IFCLE 对象是否已创建，以及 cgrayson.IFCLE 对象的 title 是否已修改。

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
| /etc/init.d/ndsd | ndsd init 脚本用于启动和停止服务器上的 eDirectory 服务。<br><br>它与其他 init 脚本的使用方式类似，带有 start 或 stop 修饰符。例如，要停止服务，请输入 /etc/init.d/ndsd stop。<br><br>要启动服务，请输入：/etc/init.d/ndsd start。 |
| Ldapconfig | ldapconfig 实用工具可用于配置树中的 LDAP 服务器和 LDAP Group 对象。<br><br>在 shell 提示符下输入 man ldapconfig 以查看该实用工具使用的各种参数。 |
| Ndsbackup | ndsbackup 实用工具用于将 eDirectory 目录树的逻辑结构保存到文件中。如果树中的对象发生问题，您可以使用此实用工具从先前创建的备份文件中恢复它们。 |
| Ndsconfig | ndsconfig 实用工具用于配置 eDirectory 目录树本身。<br><br>可用于创建新目录树、修改现有目录树、向现有目录树添加服务器或从目录树中移除服务器。<br><br>在 shell 提示符下输入 man ndsconfig 以查看该实用工具使用的各种参数。 |
| Ndslogin | ndslogin 实用工具用于检查 eDirectory 认证是否正常工作。<br><br>运行时，您提供一个用户名作为修饰符（例如，ndslogin cgrayson.if.c1e）。然后该实用工具提示您输入用户密码。该实用工具随后测试、认证并报告结果。 |
| Ndsmerge | 此实用工具可用于将两个独立的 eDirectory 目录树合并为一个目录树。<br><br>这可能是一个敏感的操作。在尝试之前，请在 shell 提示符下输入 man ndsmerge 并阅读准备目录树和服务器的说明。 |
| Ndsrepair | 由于 eDirectory 的复制和分布式特性，由于通信链路故障和其他问题，错误可能会潜入数据库。<br><br>ndsrepair 实用工具可用于检查本地 eDirectory 数据库中的错误并修复它们。<br><br>要运行完整的无人值守修复，请在 shell 提示符下输入 ndsrepair -U。<br><br>要查看该实用工具的所有可用选项，请在 shell 提示符下输入 man nds repair。 |

