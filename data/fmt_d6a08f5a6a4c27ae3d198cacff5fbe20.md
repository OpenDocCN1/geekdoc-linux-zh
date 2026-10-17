
在这个场景中，你是 ServersRUs, Inc. 的顾问，这是一家专门从事 Novell 产品部署的网络咨询公司。InfoTec, Inc. 已聘请 ServersRUs 在整个公司内部实施 NNLS。作为一名经验丰富的顾问，你将尝试在单一 Linux 服务器的实验室环境中模拟此部署，然后再尝试在生产网络上部署。

## 关于 InfoTec, Inc.

InfoTec, Inc. 专门从事深夜和周末电视时段的信息广告（infomercials）制作。它为客户提供一整套解决方案，包括以下内容：

- 市场分析
- 客户焦点小组
- 前期制作规划
- 剧本开发
- 视频制作
- 后期制作
- 电视和有线频道时段购买
- 订单履行

InfoTec, Inc. 在马里兰州列克星敦公园拥有一套单独的办公室。为了服务其客户，InfoTec 雇用了一支庞大的流动销售队伍。销售代表在客户现场工作，帮助他们度过产品周期的初始阶段。视频制作在 InfoTec 拥有的工作室或客户附近的租用工作室进行。

后期制作在 InfoTec 办公室内广阔的剪辑间进行。所有时段购买和订单履行功能也在 InfoTec 的办公室内进行。

InfoTec 雇用 800 名员工。InfoTec 的顶级组织架构图如 **图 12.1** 所示。

![](img/c7771e8540507f2b00c088c7a411b57b_537_0.png)

项目要求列在 **表 12.1** 中。

**表 12.1** InfoTec, Inc. NNLS 部署商业需求

| 规格说明 | 详细信息 |
| :--- | :--- |
| SLES 8 服务器名称 | InfoTec-1 |
| 静态 IP 地址 | 使用适用于你网络的 IP 地址、子网掩码和默认路由器地址。 |

### 表 12.1（续）

| 规格说明 | 详情 |
| :--- | :--- |
| DNS 服务器地址 | 您的服务器 IP 地址。 |
| 服务器软件 | 在部署 NNLS 之前，InfoTec-1 服务器应已部署以下应用程序：<br>• **OpenSLP** — 应将 InfoTec-1 配置为服务于 InfoTecScope 范围的 DA（目录代理）。<br>• **named** — 应将 InfoTec-1 配置为解析 InfoTec.com 区域的 DNS 服务器。应为 InfoTec-1 创建 A 记录和 NS 记录。<br>• **Mozilla 1.5 或更高版本**。<br>• **NTP** — 应在 InfoTec-1 上安装 NTP 包，并配置其与 Internet 上的公共 NTP 服务器同步时间。 |
| eDirectory 树名称 | InfoTec-Tree |
| 树中的顶级容器 | O=InfoTec |
| 管理员名称和上下文 | CN=admin.O=InfoTec |
| 服务器上下文 | OU=IS.O=InfoTec |
| eDirectory 结构 | 根据功能组织您的 eDirectory 树。在公司中为以下每个功能组创建组织单元：<br>• 信息系统<br>• 销售<br>• 市场营销<br>• 管理<br>• 预制作<br>• 视频制作<br>• 后期制作<br>• 订单履行<br><br>请务必使用简短、易记的组织单元名称或缩写来代表这些组。 |
| eDirectory 用户帐户 | 请在树初次安装后运行 eDirectory 健康检查。<br><br>输入表 12.2 中显示的用户帐户。应根据图 12.1 中的图表为每个用户对象配置报告关系。 |
| Red Carpet 更新 | 应部署 Red Carpet 以下载 NNLS 更新。 |
| eGuide | 应部署并配置 eGuide 以显示以下用户信息：<br>• 公司<br>• 经理<br>• 直接下属<br>• 员工编号<br>• 传真号码<br>• 电话号码<br><br>除默认可搜索属性外，eGuide 还应配置为允许搜索电话号码和部门属性。 |
| Linux 用户管理 (LUM) | 应完成以下 LUM 任务：<br>• 应在系统上启用 LUM。<br>• 树中的每个组织单元应有一个启用 LUM 的组对象。<br>• 特定容器中的每个用户都应为相应 LUM 组的成员。<br>• 树中的每个用户都应启用 LUM。<br>• 树中的每个用户都应使用 LUM 在服务器的 `/home` 目录下创建主目录。<br>• 每个 LUM 用户对象都应配置为使用 bash shell。 |
| DirXML | InfoTec, Inc. 使用遗留的员工管理应用程序，目前暂无计划迁移到新软件包。该应用程序可配置为导入和导出来自逗号分隔文本文件的员工数据。<br><br>您需要配置 DirXML 以导入和导出 CSV 文件中的数据。eDirectory 应配置为权威数据源。<br><br>外部应用程序中的所有员工数据都需要从 eDirectory 数据重建，因此请务必在驱动程序首次启动后从树中导出所有用户。 |
| iFolder | 根据以下参数配置 iFolder：<br><br>• 每个用户都应启用 iFolder 并拥有 iFolder 帐户。<br>• 每个用户帐户的存储配额应为 300MB。<br>• 应为所有用户启用加密。用户不得能够关闭此功能。<br>• 用户不得能够在客户端中保存密码和口令短语。<br>• 网络管理员应能够恢复遗忘的口令短语。<br>• iFolder 必须自动同步数据。用户不得能够关闭此功能，除了 GVanAlfen 以外，他需要能够根据需要关闭和开启此功能。<br>• 每个用户工作站必须安装 iFolder 客户端。<br>• iFolder 必须配置为在 `/var/opt/novell/iFolder/DocumentRoot/logs` 目录中保存日志。 |
| Samba | 根据以下规格说明配置 Samba：<br><br>• 每个用户都应启用 Samba。<br>• Samba 服务器应配置为参与 InfoTecWorkgroup 工作组。<br>• 每个用户的主目录应有一个 Samba 共享。只有该用户应能访问其共享。<br>• 每个职能组织在 `/var` 目录下应有一个目录。<br>• 这些目录中的每一个都应配置 Samba 共享。<br>• 只有特定容器中的用户才能访问关联的共享。 |
| NetStorage | 根据以下参数配置 NetStorage：<br><br>• 每个职能组织的每个 Samba 共享都应创建一个存储位置（Storage Location）对象。<br>• 应为每个存储位置对象创建一个存储位置列表（Storage Location List），该列表仅允许相关容器中的用户访问。 |
| iPrint | 根据以下参数配置 iPrint：<br><br>• 每个用户工作站都应安装 iPrint 客户端。<br>• 应为马里兰州利灵顿帕克（Lexington Park, Maryland）办公室站点创建一个基于位置的打印映射，并在其上显示每个网络打印机。<br>• 应为每个打印机上传 Windows 2000 和 Windows XP 的驱动程序。 |
| NetMail | 根据以下规格说明配置 NetMail：<br><br>• 树中的所有用户都必须拥有电子邮件帐户。<br>• NetMail 必须支持 IMAP 和 POP3 电子邮件客户端，并提供基于 Web 的电子邮件界面。<br>• 无论用户使用的是工作站电子邮件客户端还是 NetMail 的基于 Web 的电子邮件界面，都必须能够搜索 eDirectory 树中的用户电子邮件地址。<br>• 来自 spam.com 的邮件必须不得进入系统。<br>• NetMail 必须配置为使用英语作为默认语言。<br>• NetMail 必须配置为使用东部时区。<br>• 除 Mike Huffman 外，所有用户都将使用 WebAccess 模板，他要求使用 WebMail 模板。<br>• 大于 5MB 的消息必须不被允许。<br>• 由于 Mike Huffman 经常不在办公桌旁，需要为他配置自动回复，将发件人引导至联系他的行政助理。 |
| 虚拟办公室 (Virtual Office) | 使用以下规格说明配置虚拟办公室：<br><br>• 用户主页上的公司信息字段需要反映 InfoTec, Inc. 提供的服务。<br>• 虚拟办公室必须配置为使用同一 NNLS 服务器上的 NetStorage、iPrint、eGuide 和 NetMail 服务。<br>• 虚拟办公室必须配置为使用 NetMail 服务器进行电子邮件通知。<br>• 只有管理团队成员才允许创建虚拟团队。<br>• 公司的每个职能单元都需要创建一个虚拟团队，并以该组织命名。例如，信息系统需要一个名为“信息系统团队”的虚拟团队。由于用户是 NNLS 的新手，您需要创建初始团队。<br>• 每个组织的首席负责人需要被指定为其团队的拥有者。<br>• 特定组织中的所有用户必须是其相应团队的成员。<br>• 每个团队都需要为所有团队成员安排一次预约，以培训他们使用虚拟办公室。 |
