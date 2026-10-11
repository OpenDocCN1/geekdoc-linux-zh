
例如，如果您的 OES 许可是 100 个用户连接，您可以安装任意数量的 OES NetWare 服务器。最多 100 个用户可以连接并使用 OES NetWare 服务器提供的服务。

- OES Linux 服务器。同样的限制也适用于您网络上允许的用户连接数。

然而，与 OES NetWare 不同，您被授权安装的 OES Linux 服务器数量也受到限制，具体如下：

- 对于前 50 个授权用户连接，您被授权每 10 个连接安装一台 OES Linux 服务器。
- 在超过前 50 个用户连接后，您被授权每 50 个连接安装一台 OES Linux 服务器。

例如，如果您的 OES 许可适用于 100 个用户连接，则您被授权安装最多六台 OES Linux 服务器（前 50 个连接对应五台，剩余 50 个连接对应一台）。

有关 OES 许可的更多信息，请参阅 Novell 官方网站上的 OES 许可页面：http://www.novell.com/licensing/oes_licensing.html。

## OES NetWare 许可

当您安装或升级 NetWare 时，服务器安装程序会自动安装 Novell 许可服务 (NLS)。

在树树中安装第一个 NetWare 服务器期间，系统会提示您输入许可/密钥文件对（`*nlf` 和 `*.nfk`）。

安装 OES 后，您可以使用 Novell iManager 在您的 eDirectory 树中安装和管理许可证书，并监控 NetWare 的使用情况。您还可以监控启用了 Novell 许可服务的产品的使用情况。

更多信息，请参阅《NetWare 的 OES 许可服务管理指南》(`nlsadmin.pdf`) 第 13 页的“Novell 许可服务的工作原理”。

您可以通过 http://www.novell.com/documentation/oes 或从 3077 课程 CD 上的 `OES_Docs` 目录访问该指南。

## OES Linux 许可

与在 NetWare 平台上安装 OES 不同，在 Linux 平台上安装 OES 不需要许可/密钥文件对（`*.nlf` 和 `*.nfk`）。

然而，您在任何一个平台上安装 OES 时，都必须接受最终用户许可协议 (`EULA`)。您使用 OES 产品的权利限于 `EULA` 中规定的权利。

> 违反 Novell 许可协议和知识产权的行为将受到法律的最严厉追究。

如需报告盗版和侵权违规行为，请拨打 1-800-PIRATES (800-747-2837) 或发送电子邮件至 pirates@novell.com。

## 升级到 Novell OES NetWare 的目标

随着 Novell Open Enterprise Server (OES) 的引入，您现在可以利用 SUSE LINUX Enterprise Server 运行 Novell 服务和管理工具。

然而，许多 Novell 客户继续将 NetWare 作为其文件、打印和网络服务的首选，直到他们准备好迁移到 Linux 平台。对于计划继续使用 NetWare 的人员，升级到 OES NetWare 是迁移到 Novell Open Enterprise Server 的重要一步。

如果您的迁移计划包括升级到 OES NetWare，您需要执行以下操作：

- 查看 OES NetWare 升级指南选项
- 检查系统要求
- 确定要安装的服务
- 验证升级到 OES NetWare 的权限
- 使用部署管理器（Deployment Manager）准备网络
- 准备计算机
- 启动原地服务器升级（In-Place Server Upgrade）
- 完成 OES NetWare 服务器升级
- 完成安装后任务

有关安装或升级到 NetWare 的更多细节，请参阅《NetWare Novell Open Enterprise Server 安装指南》(`install-nw.pdf`)。

您可以通过 http://www.novell.com/documentation/oes 或从 3077 课程 CD 上的 `OES_Docs` 目录访问该指南。

## 检查 OES NetWare 升级指南选项

用于 OES Support Pack 2 的 NetWare 服务器平台是带有 Support Pack 5 的 NetWare 6.5。

Novell 不再区分 NetWare 6.5 支持包安装和 OES NetWare 安装。NetWare 上的 OES SP2 是同一个产品，并使用相同的安装程序和 CD 组。

在 NetWare 上安装 OES SP2 与安装带有 Support Pack 5 的 NetWare 6.5 相同。应用 NetWare 6.5 SP5 更新等于升级到 NetWare 的 OES SP2。

当您安装或升级到 NetWare 的 OES SP2 时，有以下更新后的产品供您安装：

- Novell iManager 2.5。此 iManager 的跨平台版本允许您同时管理 OES NetWare 和 OES Linux 服务器。2.5 版本还包含了增强的性能和一个不再管理 Virtual Office 1.0 的新管理界面。记住，iManager 取决于安装或升级的 Apache2 Web 服务器和 Tomcat 4 Servlet 容器。有关自 2.0.2 版本之后的其他更改，请参阅《Novell iManager 2.5 管理指南》(`imanager_admin_25.pdf`) 第 7 页的“2.5 版本的新特性”。您可以通过 http://www.novell.com/documentation/oes 或从 3077 课程 CD `OES_Docs` 目录访问该指南。
- Novell QuickFinder™ Server 4.2（取代 NetWare Search Server）。QuickFinder 是一个 Web 和文件搜索引擎，包含了多项新功能和增强。

# 评估并升级到 Novell Open Server

如果您在现有的 Search Server 上安装 QuickFinder Server，QuickFinder 会识别旧安装并迁移配置。然而，在进行搜索之前，您必须重新生成旧索引。

更多细节，请参阅《Novell QuickFinder Server 4.2 管理指南》(`qfadmin.pdf`)。

您可以通过 http://www.novell.com/documentation/oes 或从 3077 课程 CD 上的 `OES_Docs` 目录访问该指南。

- Virtual Office。OES SP2 不包含 Virtual Office。升级到 OES SP2 的现有 Virtual Office 安装将继续运行。如果您正在创建新服务器并安装 Virtual Office，请使用 OES SP1 安装；然后更新服务器到 OES SP2。OES SP1 CD 可从 Novell 支持网站 http://support.novell.com/tools/csp/oes 获取。在 OES SP1 中，Virtual Office 的管理界面从 iManager 中移除并整合到了 Virtual Office 中。
- iManager 2.5。如果您想从 iManager 2.0.2 升级到 2.5，需要使用 NetWare 6.5 SP5 叠加 CD。在从 NetWare 5.1 或 6.0 升级之前，您应该备份任何自定义的服务器配置文件。升级后可以恢复。您还应注意 OES NetWare 中的以下组件已移除，不再可以选择安装：
  - Novell Nterprise™ Branch Office™ Rsync Server。NBO Branch Office - Central Office Server 的模式安装已移除。您可以升级现有的 NBO Central Office Server，但无法安装新的。
  - Novell Nsure® UDDI Server。在之前的 NetWare 6.5 中，此组件与 exND™ J2EE Web 服务器、Apache/Tomcat 服务器以及 Novell Nsure Audit Starter Pack 模式一起安装。仅删除了 UDDI Server 组件，其余三个模式可用。除非文档另有说明，NetWare 6.5 的所有可用产品和功能在 OES NetWare 中继续可用。

以下是 OES NetWare 的服务器部署选项：

| 安装/升级选项 | 使用场景 |
| :--- | :--- |
| 在标准硬件上新安装 OES NetWare | 您有新的服务器级 PC 硬件，并想首次在其安装 OES NetWare。 |
| OES NetWare 的无人安装 | 您想使用响应文件运行 OES NetWare 的无人或静默安装。 |
| 将现有 NetWare 服务器原地升级到 OES NetWare | 您有现有的 NetWare 5 或更高版本的服务器，并想在本地升级到 OES NetWare。 |
