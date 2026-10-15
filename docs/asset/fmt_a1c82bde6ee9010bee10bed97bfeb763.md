
# 升级到认证 Linux 工程师 10

## 引言

升级到认证 Linux 工程师 10（3076）课程旨在提供有关 SUSE Linux Enterprise Server 版本 9 与版本 10 之间差异的信息，特别是与 Novell 认证 Linux 工程师（CLE）课程中涵盖的主题相关的差异：
- *SUSE Linux Enterprise Server 10 基础*（课程 3071）
- *SUSE Linux Enterprise Server 10 管理*（课程 3072）
- *SUSE Linux Enterprise Server 10 高级管理*（课程 3073）
- *SUSE Linux Enterprise Server 10：网络服务*（课程 3074）
- *SUSE Linux Enterprise Server 10：安全*（课程 3075）

您将了解 SUSE Linux Enterprise Server 10 的新功能以及与您作为 Novell 认证 Linux 工程师的现有知识相比的更改。

该课程可通过互联网作为学习模块提供，完成大约需要 8 小时。为了获得足够的经验以参加新的 Novell 认证 Linux 工程师 10（CLE 10）实践考试。

Novell 强烈建议您在全球 Novell 授权培训合作伙伴处注册参加升级研讨会。基于本课程，内容得到丰富，并在课程结束时有参加新的实践考试的选项。

## 课程目标

本课程教授您以下概念和技能，以理解 SUSE Linux Enterprise Server 10 的差异：
- 安装 SUSE Linux Enterprise Server 10
- 使用 GNOME 桌面环境
- 管理硬件
- 配置 Linux 文件系统分区
- 使用 NetworkManager 配置网络
- 管理用户访问和安全
- 使用 Syslog 守护进程 syslog-ng
- 使用 Xen 管理虚拟化
- 使用 BIND 配置 DNS 服务器
- 配置 DHCP 池和故障转移
- 管理 OpenLDAP
- 配置邮件服务器
- 应用安全
- AppArmor

## 受众

本课程面向 Novell 认证 Linux 工程师或具有同等知识的人员。本课程内容结合全球 Novell 培训合作伙伴提供的升级研讨会，是参加 Novell 认证 Linux 工程师 10（CLE 10）实践考试的理想准备。

## 认证与先决条件

本课程帮助您备考 Novell 认证 Linux 工程师（Novell CLE 10）实践考试，即所谓的实习考核。Novell CLE 10 是面向已通过 Novell CLP 实习考核的人员的更高级别认证。

与所有 Novell 认证一样，建议完成相应课程学习。要获得该认证，您需要通过 Novell CLE 10 实习考核（050–698）。

Novell CLP 实习考核是一项动手操作的、基于场景的考试，您需要运用所学知识解决实际问题，以证明您知道该做什么以及如何去做。

实习考核将测试您在以下 Novell CLE 10 课程中的目标：
- SUSE Linux Enterprise Server 10：网络服务（课程 3074）
- SUSE Linux Enterprise Server 10：安全性（课程 3075）

下图展示了 Novell CLE 10 的培训/测试路径：

## 图 Intro-1 。

![](img/8279afe915b153902294b0e58311b75a_13_0.png)

有关 Novell 认证项目以及参加 Novell CLP 10 和 CLE 10 实习考核的更多信息，请参见 http://www.novell.com/training/certinfo/。

## SUSE Linux Enterprise Server 10 支持与维护

要获得 SUSE Linux Enterprise Server 10 的官方支持与维护更新，您需要执行以下操作之一：
- 注册免费的注册/序列号，该号码为您提供 30 天的支持与维护。
- 从 Novell（或其授权经销商）购买 SUSE Linux Enterprise Server 10 的副本。

您可以在 http://www.novell.com/products/linuxenterpriseserver/eval.html 获取免费的 30 天支持与维护代码。

您需要拥有或创建一个 Novell 登录账户才能访问 30 天评估版。

## Novell 客户中心

Novell 客户中心是一个直观的、基于 Web 的界面，可帮助您管理与 Novell 之间的业务和技术互动。Novell 客户中心整合了对以下信息、工具和服务的访问：
- 新 SUSE Linux Enterprise 产品的自动注册
- Novell 所有在售 Linux 产品的补丁和更新
- 所有 Novell 产品、订阅和服务的订单历史
- 新 SUSE Linux Enterprise 产品的授权可见性
- Linux 订阅续订状态
- 通过合作伙伴或 Novell 进行的订阅续订

例如，一家公司可能有需要下载 SUSE Linux Enterprise 软件更新的管理员、希望查看订单历史的采购人员，以及需要核对许可的 IT 经理。借助 Novell 客户中心，公司可以在一个地方满足所有这些需求，并为每个用户分配适合其角色的访问权限。

您可以在 http://www.novell.com/center 访问 Novell 客户中心。

## 练习约定

在完成练习时，您会看到一些约定，用于指示需要输入的、特定于您服务器的信息。

以下是最常见的约定：
- *斜体/粗体文本*。这是指您的独特情况，例如服务器的 host 名称。

  例如，如果服务器的 host 名称是 DA50，并且您看到以下内容：

  `hostname.digitalairlines.com`

  您应输入

  `DA50.digitalairlines.com`
- `10.0.0.xx`。这是分配给您的 SUSE Linux Enterprise Server 10 服务器的 IP 地址。

  例如，如果您的 IP 地址是 10.0.0.50，并且您看到以下内容：

  `10.0.0.xx`

  您应输入

  `10.0.0.50`
- **选择**。单词 *select* 在练习步骤中用于表示各种操作，包括点击界面上的按钮和选择菜单项。
- **输入和键入**。单词 *enter* 和 *type* 具有不同的含义。

  单词 *enter* 表示在字段或命令行中键入文本，并在必要时按 Enter 键。单词 *type* 表示键入文本但不按 Enter 键。

  如果指示您键入一个值，请确保不要按 Enter 键，否则可能会启动您尚未准备开始的进程。

## SECTION 1 SUSE Linux Enterprise Server 10 的安装

从 SUSE Linux Enterprise Server 9 到 SUSE Linux Enterprise Server 10 的安装过程中变化不大。

在 SUSE Linux Enterprise Server 9 中，默认的身份验证方法是使用 LDAP 服务器。在 SUSE Linux Enterprise Server 10 中，它使用文件 `/etc/passwd` 进行本地身份验证。

另一个新功能是 Novell Customer Center。

### Objective

- 了解 Novell Customer Center 配置和在线更新

### Objective 1: 了解 Novell Customer Center 配置和在线更新

如果 Internet 连接测试成功，您可以配置 Novell Customer Center，该中心是执行在线更新所必需的。如果 SUSE 更新服务器上有任何更新包可用，您可以下载并安装它们以修复已知错误或安全问题。

Figure 1-1

![](img/8279afe915b153902294b0e58311b75a_19_0.png)

选择 **Next** 会启动浏览器并连接到 Novell 网站，您只需输入您的电子邮件地址，以及如果有的话，激活码。

Figure 1-2

![](img/8279afe915b153902294b0e58311b75a_20_0.png)

注册成功后，在线更新对话框打开。您可以通过选择 **Run Update** 和 **Next** 开始在线更新。
（您也可以选择 **Skip Update** 以便稍后在已安装的系统上执行更新。）

YaST 的在线更新对话框打开，显示可用补丁的列表（如果有）。

Figure 1-3

![](img/8279afe915b153902294b0e58311b75a_21_0.png)

选择您想要安装的补丁，然后通过选择 Accept 开始更新过程。
