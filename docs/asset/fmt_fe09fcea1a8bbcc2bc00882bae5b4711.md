
![](img/0824e0f841046b33f07fbd84ce9da816_288_0.png)

# 业务集群服务安装

现在一切已就绪并安装，仅剩最后步骤。首先，必须安装 BCC。然后，需要配置 Identity Manager eDirectory 驱动程序以同步两个集群之间的数据。之后，可以完成配置的最后阶段：必须配置 BCC 以启用两个到四个集群之间的故障转移。在本节中，您将学习如何安装 BCC 产品。

## 提示

可以从 `www.novell.com/download` 获取 BCC 的免费评估版本。

要安装 BCC，请执行以下步骤：

- 1. 将 BCC CD 盘插入 Windows 工作站，并从 CD 盘运行 `install.exe`。点击“下一步”，然后点击“我接受”开始安装程序。
- 2. 当询问安装哪些组件时，如图 12.4 所示，选择 Novell Business Continuity Cluster 和用于 Novell NetWare 基于管理服务器的 iManager Snaps。然后双击“下一步”。

## 第 12 章：业务连续性集群简介

### 图 12.4

选择 Novell Business Continuity Cluster 以及用于 NetWare 的 iManager Snaps 进行安装。

![](img/0824e0f841046b33f07fbd84ce9da816_289_0.png)

- 3. 现在，您需要输入要添加到 BCC 环境的第一个集群对象的区分名称（见图 12.5）。选择 `cluster1` 并点击“下一步”继续。
- 4. 确保集群中的所有节点都选中，并点击“下一步”继续。
- 5. 接下来，您需要选择要安装 iManager snaps 的 NetWare 服务器。选择 `bcc-node2` 并点击“下一步”继续。这将所有所需软件安装到第一个集群的节点上。
- 6. 安装后，行 `LDBCC.NCF` 被添加到集群中所有节点的 `AUTOEXEC.NCF` 文件中。打开 `AUTOEXEC.NCF` 文件，使用 `REM` 状态或井号 (`#`) 注释此行。
- 7. 对其他集群重复上述步骤。

### 图 12.5

逐个添加您想要放入 BCC 环境的集群。

![](img/0824e0f841046b33f07fbd84ce9da816_290_0.png)

# 配置 Identity Manager eDirectory 驱动程序

现在所有所需的软件组件已安装完毕，是时候开始实际工作了。这部分的第一工作是配置 Identity Manager 驱动程序。您需要在集群的双方都配置 Identity Manager。`site1` 驱动程序负责保留 `site2` 中所有相关对象的副本，而 `site2` 的 Identity Manager 驱动程序必须确保所有相关对象都已保留。为了此目的，您需要在两个站点都配置单独容器，作为来自另一侧站点对象的着陆区。在本例中，我们将使用 `ou=fromsite2.ou=site1.ou=bcc` 和 `ou=from-site1.ou=site2.ou=bcc`。

## 注意

默认情况下，管理 BCC 的相关 snapins 未安装在您树结构中的所有服务器上。从现在起，我们建议您仅连接到安装了 snapins 的服务器。

- 1. 在继续之前，请确保您要配置 iManager 的服务器具有其所在分区的 eDirectory 副本。然后通过 `https://yourserver/nps` 启动 iManager。
- 2. 浏览到 DirXML Utilities 并选择 New Driver。然后选择 `In a New Driver Set` 并点击“下一步”继续。
- 3. 为新驱动集输入以下信息并点击“下一步”继续（见图 12.6）：

## 第 12 章：业务连续性集群简介

- 名称: `BCC site1-site2`
- 上下文: `site1.bcc`
- 服务器: `bcc1-node2.site1.bcc`
- 取消勾选“在此驱动程序集上创建新分区”框

### 图 12.6

输入名称、上下文和负责的服务器以创建 Identity Manager 驱动程序。

![](img/0824e0f841046b33f07fbd84ce9da816_291_0.png)

- 4. 在下一个屏幕中，您需要创建驱动程序。要独立创建 Identity Manager 驱动程序，如图 12.7 所示，选择 `Import a Driver Configuration from the Server (XML File)`，并从列表中选择 `BCCClusterResourceSynchronization.xml`。然后点击“下一步”继续。
- 5. 现在您必须为驱动程序输入特定属性。使用以下信息：
  - 驱动程序名称: `site1site2 driver`。
  - SSL 证书名称: `none`。

## 注意

如果在两个不同的 eDirectory 树之间同步，请在此选择 SSL 证书。但在这种情况下，我们是在同一个树内进行同步，因此不需要 SSL 证书。

### 图 12.7

导入 BCCClusterResourceSynchronization 驱动。

![](img/0824e0f841046b33f07fbd84ce9da816_292_0.png)

- DirXML 节点: `192.168.2.10`（这应该是安装了 Identity Manager 的节点 IP）。
- 端口号: `2002`。
- 此集群的区分名称: `cluster1.bcc`。
- 其他集群的区分名称: `cluster2.bcc`。
- 从此集群同步的启用池和对象的上下文: `fromsite2.bcc`。
- 其他集群的启用池和对象的父容器上下文: `site1.bcc`。这是启用池和卷所在的另一个树的上下文。
- `BCC-TREE`。
- 6. 现在选择 Define Equivalences 并浏览到您的树。这确保了树有足够的权限创建对象。点击“下一步”继续。
- 7. 您将看到驱动程序的摘要（见图 12.8）。摘要概述了创建的 eDirectory。点击“完成”将驱动程序添加到网络。

### 图 12.8

在摘要中提供了驱动程序的概述。

![](img/0824e0f841046b33f07fbd84ce9da816_293_0.png)

## 提示

对于新手来说，Identity Manager 的摘要没有足够的详细信息。要深入了解驱动程序的配置情况，请点击完成。

- 8. 在 `site2` 中同样重复所有任务以创建 Identity Manager 驱动程序。确保在详细屏幕中使用以下信息：
  - 驱动程序名称: `site2site1 driver`。
  - SSL 证书名称: `none`。
  - 其他 DirXML 节点: `192.168.2.20`（这应该是安装了 Identity Manager 的节点 IP）。
  - 端口号: `2002`。
  - 此集群的区分名称: `cluster2.bcc`。
  - 其他集群的区分名称: `cluster1.bcc`。
  - 从此集群同步的启用池和对象的上下文: `fromsite1.bcc`。
  - 其他集群的启用池和对象的父容器上下文: `site2.bcc`。这是启用池和卷所在的另一个树的上下文。

# 启动 Identity Manager 驱动程序、NCS 和 BCC

现在 Identity Manager 驱动程序已已创建，但仍需启动。是在安装了 Identity Manager 的两个服务器上执行的描述的任务：

- 1. 从 iManager，选择 DirXML、DirXML Overview。然后选择 Search Entire Tree 并点击搜索按钮。这将显示如图 12.9 所示的屏幕。
- 2. 点击驱动程序上的停止符号并选择 Start Driver。驱动程序现在将启动。如果启动成功，驱动程序上将显示阴阳图标以表示其正在运行。在第一个驱动程序启动后，对第二个驱动程序执行相同操作。

## 提示

如果您不熟悉 Identity Manager，故障排除将很困难。如果您无法让驱动程序相互同步，且您确定已按照此程序列出的所有步骤进行了操作，我们建议您删除驱动程序并创建新的驱动程序。这比排查在配置 IDM 驱动程序时到底在哪里出了错要容易得多。

## 第 12 章：业务连续性集群简介

- 3. 只有在 Identity Manager 驱动程序成功启动后，在两个集群中的所有节点上使用 `LDNS.NCF` 文件启动 Novell Cluster Services。如果您已按照之前的说明创建了 `INITSTR.NCF` 文件，请不要在启动集群之前运行它。
- 4. 当 NCS 加载后，在两个集群中的所有节点上运行 `DBCC.NCF` 文件以启动 BCC。这将使您的 BCC 环境建立并运行。

### 图 12.9

DirXML Overview 屏幕提供了当前您的 eDirectory 树中存在的所有 Identity Manager 驱动程序的概述。

![](img/0824e0f841046b33f07fbd84ce9da816_295_0.png)
