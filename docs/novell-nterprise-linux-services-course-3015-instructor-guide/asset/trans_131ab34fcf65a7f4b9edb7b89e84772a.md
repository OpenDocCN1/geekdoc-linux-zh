

i. （条件项）如果您的容器未被列出，请添加**您的容器**（使用放大镜图标）；然后选择**保存**。

4. 验证您的 POP 代理是否已启用：
   - a. 在**DAx 消息服务器**下，选择**POP 代理**。
   - b. 验证代理是否已启用。
   - c. （条件项）如果代理未启用，请选择**已启用**，然后选择**保存**。

5. 设置服务器时区：
   - a. 在左侧，选择**模块化 Web 代理**。
   - b. 在右侧的默认时区下拉列表中，选择**您的时区**。您这样做是为了确保消息服务器的时区与 NNLS 服务器的时区相同。
   - c. 选择**保存**。

6. 测试配置。
   - a. 在当前 Mozilla Web 浏览器窗口中，通过按**Ctrl+N** 打开一个新的浏览器窗口。
   - b. 输入 **http://DAx.your container.digitalairlines.com:52080**。
   - c. 当提示登录时，输入用户名为 **JJackson**，密码为 **novell**；然后选择**确定**。此时将显示 WebAccess 页面。
   - d. 在左侧，选择**撰写**图标。
   - e. 在收件人字段中，输入 **AGresko@your container.digitalairlines.com**。例如，如果您正在 DA3 上工作，则输入 **AGresko@atl.digitalairlines.com**。
   - f. 在主题和正文字段中，输入*文本*。

如果正文字段留空，消息将不会发送。

   - g. 选择**发送**。
   - h. 等待发送窗口关闭；然后，在 Web/Access 页面顶部，选择**退出**图标。
   - i. 选择**登录**。
   - j. 当提示登录时，以用户名为 **AGresko**，密码为 **novell** 进行身份验证。
     您应该能看到刚从另一个账户发送的消息。
   - k. 选择该*消息*。
   - l. 尝试向您树中的其他用户发送电子邮件。
   - m. 尝试向另一棵树中的用户发送电子邮件消息。
   - n. 完成后，关闭浏览器窗口。

*（练习结束）*

## 摘要

| 目标 | 摘要 |
| :--- | :--- |
| **1. 识别 NetMail 功能** | Novell NetMail 是一个基于互联网标准消息和安全协议的高性能电子邮件和日历系统。 |
| | NetMail 旨在适应多种网络环境。它已在单个 Linux 服务器上成功测试支持多达 30,000 名用户。 |
| | NetMail 高效的分层架构将运行电子邮件和日历系统所需的服务器数量降至最低。 |
| | NetMail 与 Novell eDirectory 紧密集成。 |
| | NetMail 还可以将电子邮件和日历服务分布在多个服务器上。这提高了性能，同时防止关键进程因系统故障而中断。 |

| 目标 | 摘要 |
| :--- | :--- |
| **2. 描述 NetMail 组件** | NetMail 由以下组件组成：<ul><li>Internet 服务容器</li><li>消息服务器</li><li>父对象</li><li>模板</li><li>列表服务器和邮件列表</li><li>NetMail 代理<ul><li>地址簿代理</li><li>别名代理</li><li>反垃圾邮件代理</li><li>防病毒代理</li><li>自动回复代理</li><li>日历代理</li><li>连接管理器</li><li>IMAP 代理</li><li>列表服务器代理</li><li>模块化 Web 代理</li><li>NMAP 代理</li><li>POP 代理</li><li>代理服务器代理</li><li>SMTP 代理</li><li>WebAdmin</li></ul>在安装默认设置时，NetMail 文件被复制到 /var/opt/novell/netmail 和 /opt/novell/netmail 目录。</li></ul> |

| 目标 | 摘要 |
| :--- | :--- |
| **3. 描述 NetMail 工作原理** | 安装 NetMail 时，它会扩展 eDirectory 架构，以包含与 NetMail 相关的对象和属性。<br><br>现有的目录对象，如容器、用户甚至服务器对象，将具有新的 NetMail 属性。<br><br>NetMail 的核心功能是消息处理。进入您消息系统的每个消息都必须由 NetMail 代理进行处理。<br><br>根据在您的消息系统中运行的代理不同，消息可能会对照系统黑名单进行检查、转发到另一个电子邮件地址，或根据用户定义的规则进行过滤。 |

| 目标 | 摘要 |
| :--- | :--- |
| **4. 安装 NetMail** | NetMail 可以通过 2 种方式进行配置：<br><ul><li><strong>单服务器消息处理</strong></li><li><strong>分布式服务器消息处理</strong></li></ul><br>在设计您的 NetMail 系统时，您需要确定以下内容：<br><ul><li>哪些服务器将承载 NetMail 代理？</li><li>哪些代理将位于给定服务器上？</li><li>每个消息服务器将服务哪些域？</li><li>您的组织是否需要在多个服务器上部署相同的代理以实现故障耐受性和可扩展性？</li></ul><br>要安装 NetMail，必须满足以下系统要求：<br><ul><li>确保您正在运行以下其中一种：<ul><li>Red Hat Linux AS 2.1</li><li>Red Hat Linux ES 2.1</li><li>SuSE 8.0</li></ul></li><li>确保已安装 Linux 版 eDirectory 8.7.3 或更高版本。</li><li>确保您的系统 CPU 至少为 750 MHz Pentium III 或 Athlon。</li><li>确保您至少有 512 MB 的系统 RAM。</li></ul> |

| 目标 | 摘要 |
| :--- | :--- |
| **4. 安装 NetMail（续）** | - 确保您有 20 MB 的可用磁盘空间用于安装。<br>- 每个承载 NetMail 服务的服务器必须有一个副本。<br>- 确保 eDirectory 树已同步且状态良好。<br>- 确保您对 eDirectory 树具有管理员权限。<br>- 确定消息服务器对象的名称。<br>- 确定您的 Internet 域 DNS 服务器 IP 地址。<br>- 检查服务器上的端口分配是否存在重复。 |
| **5. 配置和使用 NetMail** | WebAdmin 是用于配置 NetMail 系统的实用程序。它是一个基于浏览器的实用程序，集成在 iManager 中。<br><br>要直接访问 WebAdmin，请打开 Web 浏览器并输入 http://your_server_IP:8018 或 https://your_server_IP:8020。<br><br>NetMail 系统为 NMAP 代理的上下文属性中配置的容器内的所有用户提供服务。<br><br>默认情况下，NetMail 附带 2 个模板：<br>- WebAccess (Webacc.CTP)<br>- WebMail (WebMail.CTP) |

## 第 9 节：将 NNLS Web Access 与 Virtual Office 统一

在本节中，您将了解使用 Virtual Office 执行诸如创建和管理团队等任务的基础知识。

### 目标

- 1. 描述 Virtual Office
- 2. 安装 Virtual Office
- 3. 配置 Virtual Office

### 简介

如今工作场所的员工正在变得更加移动化，经常远程办公、在分支机构工作，或在公共场所通过 Internet 网吧亭通信。

在这种环境中，员工需要访问他们的电子邮件和工作文件。他们可能还需要访问打印、聊天、团队日历和团队讨论等服务。

Novell Virtual Office 帮助企业解决这些问题。通过员工门户网站，它实现了个人和团队生产力功能以及 Internet 协作能力，如下所示：

#### 图 9-1

![](img/d63035f3fce0eaaf97203dde900affb7_225_0.png)

在本节中，您将学习如何安装和配置 Virtual Office，以利用 NNLS 产品使员工在远程工作时更具生产力。

### 目标 1

### 描述 Virtual Office

Virtual Office 是一个 Web 访问门户网站，允许远程用户与工作组团队进行协作和信息共享。

以下是默认的 Virtual Office 登录页面：

#### 图 9-2

![](img/d63035f3fce0eaaf97203dde900affb7_226_0.png)

要描述 Virtual Office，您需要了解以下内容：

- Virtual Office 工作原理
- Virtual Office 示例场景

### Virtual Office 工作原理

Virtual Office 通过让用户设置和管理许多自己的网络、信息共享和数据备份过程，优化了用户的自助服务概念。

Virtual Office 还允许用户创建自己的功能团队，称为虚拟团队，用于交互式实时协作。

加入虚拟团队的人员可以访问共享文档、讨论线程、书签和团队日历。团队的所有成员都可以访问团队信息和服务。

