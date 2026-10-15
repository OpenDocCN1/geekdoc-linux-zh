
- f. 选择 `Organizational Chart`（组织架构图）选项卡。将显示你在用户对象属性中定义的组织结构。

#### 6. 配置 eGuide 显示的属性

通过完成以下步骤来配置 eGuide 显示的属性：

- a. 在 eGuide 中，选择 `Administration Utility`（管理实用工具）。
- b. 选择 `LDAP Data Sources`（LDAP 数据源）。
- c. 在 `New_Data_Source`（新数据源）行中，选择 `Edit`（编辑）。
- d. 选择 `Attributes`（属性）选项卡。
- e. 为以下属性勾选相应的复选框：

| 属性 | 复选框 |
|:---|:---|
| Company | Enable |
| directreports | Enable, Searchable |
| facsimiletelephonenumber | Enable, Searchable, Editable |
| Manager | Enable, Searchable |
| telephonenumber | Enable, Searchable, Editable |

- f. 点击 `Save`（保存）。
- g. 点击 `Launch eGuide Client`（启动 eGuide 客户端）图标。
- h. 在第一个 `Find People`（查找人员）下拉列表中，验证前面的可搜索属性是否包含在列表中。
- i. 搜索 `DCoughanour` 用户对象。验证之前配置的属性是否已显示。

这就是关于 eGuide 的全部内容了。它是一款非常稳健的产品，开箱即用的表现非常出色。你在浏览上述内容时可能已经注意到，部署它确实不需要太多的管理干预。

完成 eGuide 配置后，接下来你将了解 NNLS 的 Linux 用户管理组件。

期待着不可能的事情发生。幸运的是，Novell 意识到了这一事实，并在 NNLS 中包含了 LUM。

> `Novell` 实际上在 NNLS 之前就开始研究这个问题了。LUM 源自 Novell 的账户管理（Account Management）产品线。 使用过两者后你会发现，LUM 的使用要简单得多，而且运行可靠得多。

LUM 让 eDirectory 做我们在 1998 年一直期望它做到的事：`它通过 eDirectory 将身份验证重定向到 Linux 系统。` Linux 用户无需在 passwd 文件中存在条目即可*无需*认证到系统。

仅凭这一点，就使 eDirectory 在 Linux 平台上物超所值。回顾第四章“Novell Nterprise Linux Services (NNLS) 简介”，我们讨论了在多个服务器上同步 Linux 用户和组账户所面临的管理挑战。此前，解决这个问题你有两个选择：

- 你可以手动同步账户。在非常大的网络中，这可能是一项艰巨的任务。
- 你可以实现 NIS+。NIS+ 是一种开源服务，用于在 Linux 系统之间同步账户。

无论哪种方式，都不是一项容易的任务。

使用 eDirectory 管理 Linux 用户账户会让管理员的生活轻松许多。eDirectory 作为所有网络信息的中央存储库，无需在多个系统之间尝试同步账户。

> 重要的是，你要理解 eDirectory 并不同步用户账户。

使用 eDirectory 时，组织中的每个用户只需要一个用户账户。你向单个用户账户分配权限，以控制该用户可以和不能使用哪些资源。

回忆上一章我们安装 NNLS 时的情景。我们配置 NNLS 将支持 PAM 的服务的身份验证重定向。PAM 代表*可插拔身份验证模块*（Pluggable Authentication Modules）。PAM 使用一系列共享库文件来创建模块化的身份验证系统。它允许管理员自定义特定服务（如登录或 ftp）所使用的身份验证机制。

诸如 ftp、login 等 Linux 服务已被重定向以使用 eDirectory 用户账户，而不是 passwd 文件中的用户账户。这在实现 Samba 时尤其有用。我们将在后续章节中更详细地讨论此主题。

### LUM 如何与 eDirectory 配合工作

当安装 LUM 时，它会扩展 eDirectory 模式（如果你对 eDirectory 不太熟悉，可能不知道这意味着什么）。回顾第五章“NNLS 安装和管理”，我说过 eDirectory 模式定义了树中允许的对象，定义了它们的属性，并指定了包含规则。

实现 NNLS 时安装的基本模式并不是静态的。你可以向树中添加、删除或修改对象类和属性。LUM 安装时正是这样做的。它扩展模式并将 LUM 特定的属性添加到默认的用户、组和模板对象类中。如图 6.11 所示，用户对象获得了一个名为 Linux Profile（Linux 配置文件）的新属性页。

![](img/c7771e8540507f2b00c088c7a411b57b_277_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_277_1.png)

用户对象添加了以下属性：

- 用户 ID
- 主要组 ID
- 主要组名称
- 登录 Shell
- 主目录
- 注释

在图 6.12 中，你可以看到组对象类也添加了一个名为 Linux Profile（Linux 配置文件）的新属性页。

![](img/c7771e8540507f2b00c088c7a411b57b_278_0.png)

**图 6.12** 组对象的 Linux 配置文件页面。

组对象添加了以下属性：

- 组 ID
- uamPosixWorkstationList
- 描述
- memberUid

LUM 还扩展模式，向树中添加两种新类型的对象，如表 6.1 所列。

**表 6.1** LUM eDirectory 对象

| LUM 对象 | 描述 |
| :--- | :--- |
| Linux 工作站 | 包含 Linux 系统的访问控制信息。每个 Linux 系统在树中都有一个关联的工作站对象。 |
| Linux 配置 | 包含 LUM 配置信息。 |

安装 LUM 还会向系统中添加表 6.2 中列出的组件。

**表 6.2** LUM 组件

| LUM 组件 | 位置 | 描述 |
| :--- | :--- | :--- |
| `nss_nam.so` | `/usr/lib` | 从 eDirectory 树中检索用户和组信息。此模块使用 LDAP 访问 eDirectory。 |
| `nss_nam.so` | `/usr/bin/` | 用于配置服务器上的 LUM。 |
| `pam_nam.so` | `/usr/lib/security` | 使用 eDirectory 提供 Linux 服务器上的身份验证、账户和密码管理服务。 |

这些新对象和模块在 LUM 中起着关键作用。重定向到 eDirectory 时遇到的一个问题之一是上下文（context）的问题。回忆一下，eDirectory 使用分层数据库结构。对象通过其用户名及其上下文（例如，`DCoughanour.SLC.CLE`）进行引用。另一方面，Linux passwd 文件是一个平面文件。用户账户没有按层次结构排列。

这引发了一个新问题：在一个之前没有该概念的系统上，如何处理上下文问题？为解决此问题，LUM 为 Linux 用户提供了一种称为无上下文登录（contextless login）的身份验证过程，顾名思义即可。用户可以使用典型的 Linux 用户名登录到 Linux 系统。

LUM `nss_nam.so` 模块将用户在登录期间提供的无上下文用户名解析为 eDirectory 树中特定系统的工作站对象。该对象在图 6.13 中显示。

![](img/c7771e8540507f2b00c088c7a411b57b_279_0.png)

工作站对象包含已获准访问 Linux 系统的所有组的列表。这显示在图 6.14 中。

![](img/c7771e8540507f2b00c088c7a411b57b_280_0.png)

![](img/c7771e8540507f2b00c088c7a411b57b_280_1.png)

只有属于这些组的用户才被允许对 Linux 系统进行身份验证。在图 6.14 中，只有 `IFEmployees.IFCLE` 组或 `SLCEmployees.SLC.CLE` 组的成员才被允许对 `CLE1` Linux 系统进行身份验证。

用户提供的用户名将与关联的 LUM 组中的用户名进行比较。如果找到匹配项，用户将经过身份验证，并且其 Linux 配置文件将用于配置系统环境。

让我们更详细地看看这个重定向过程。

#### LUM 重定向如何工作

LUM 重定向基于集成到 Linux 中的名称服务切换（Name Service Switch，NSS）组件。NSS 允许你配置希望在系统中如何进行身份验证。NSS 配置由 `/etc/nsswitch.conf` 文件控制。
