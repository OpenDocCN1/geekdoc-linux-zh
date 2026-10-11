
| Linux 版 WebSphere Application Server Edition | 4 | zSeries | SuSe 7.0 (内核 2.216)，基于 SuSe 31b 2.4 内核的 zLinux 上的 390 TurboLinux Server  WAS V4.0.3 |
| Linux 版 WebSphere Advanced Single Edition | 4 | zSeries | SLES Linux 2.4 |
| Linux 版 WebSphere Server Edition | 3.5 | zSeries | SuSe 7.0 (内核 2.216)，适用于 390 的 TurboLinux Server 6 (内核 2.2) |
| WebSphere Server for Developers | 5 | zSeries | 基于内核 2.4 的 SLES (SuSe) 或 Red Hat 7.2 |
| WebSphere Server Enterprise | 5 | zSeries | 带有 2.4 内核的 SLES |
| WebSphere Enterprise for Developers | 5 | zSeries | 带有 2.4 内核的 SLES |
| WebSphere Network Deployment | 5 | zSeries | 基于内核 2.4 的 SLES (SuSe) 或 Red Hat 7.2 |
| Linux 版 WebSphere Business Edition | 5.4 | zSeries | 2.4 Kernel SuSe Linux Enterprise Server (SLES) 7.0 |
| WebSphere Host on Demand | 7 | zSeries | Å |
| WebSphere Host on Demand | 6 | zSeries | 服务器：zSeries 上的 Linux

## 4.6 z/390 上的

`z/390` Linux 运行在 `z/OS` 上的 s390 具有可用性。第 106 页 Linux 手册：IBM Linux 解决方案和资源指南。

## 4.6 Boscov's 商店

`Boscov's` 是一家私有的百货商店，目前在宾夕法尼亚州、特拉华州、新泽西州、纽约州经营着 37 家商店。所有商店位于公司总部和中央配送中心 300 英里范围内。目前约有 9000 名全职和兼职员工，不包括季节性员工。年营业额达 10 亿美元的 `Boscov's` 一直在收购并开设新店以满足当地客户。

`Boscov's` 需要停止其 `Windows NT` 服务器群的增长，同时提高可用性、扩展性以及许多不同应用的备份。`Boscov's` 还需要支持运行 `Linux` 的现有 `CICS`、`DB2` 和 `IMS` 增长，以及 `z/OS v1.1` 上的新关键应用。

`Boscov's` 多年来一直依赖大型机处理关键业务，包括 `s390`、`CICS`、`DB2` 和 `IMS`。大型机传统上提供了其业务所需的特性，如 `CICS` 和 `DB2`。当 `IBM` 增加了 `zSeries` 和 `S/390` 大型机上托管 `Linux` 系统的能力时，使得大型机的高质量服务能够扩展到服务器群中的现有分布式应用。该公司评估了基于大型机的 `Linux` 解决方案的能力和优势，包括其无与伦比的灵活性、处理能力以及在 `WebSphere Suite` 下运行电子商务应用程序的能力。接下来，他们决定将服务器群整合到运行 `zSeries` 和 `S/390` 的大型机上。

`Boscov's` 在 2001 年 7 月将 `S/390` 服务器 `R44` 型替换为 `zSeries 900 102` 型，以处理 `z/OS` 业务关键应用并将服务器群整合到大型机上的 `Linux` 虚拟机。`Boscov's` 部署了在 `z/VM` 上的由一个 `i6` 引擎驱动的 `SUSE Linux` 服务器。`zSeries 900` 还被用于运行 `Linux` 的多个分区。通过运行在大型机上的 `Linux` 有助于 `Telekom` 的应用。

要了解完整故事，请访问：
`http://www.ibm.com/servers/eserver/news/pressreleases/2002/zlinuxtele_07-html`

### 4.6.2 Boscov's 商店

`Boscov's` 是一家私有的百货商店，目前在宾夕法尼亚州、特拉华州、新泽西州、纽约州经营着 37 家商店。所有商店位于公司总部和中央配送中心 300 英里范围内。目前约有 9000 名全职和兼职员工，不包括季节性员工。年营业额达 10 亿美元的 `Boscov's` 一直在收购并开设新店以满足当地客户。

`Boscov's` 需要停止其 `Windows NT` 服务器群的增长，同时提高可用性、扩展性以及许多不同应用的备份。`Boscov's` 还需要支持运行 `Linux` 的现有 `CICS`、`DB2` 和 `IMS` 增长，以及 `z/OS v1.1` 上的新关键应用。

`Boscov's` 多年来一直依赖大型机处理关键业务，包括 `s390`、`CICS`、`DB2` 和 `IMS`。大型机传统上提供了其业务所需的特性，如 `CICS` 和 `DB2`。当 `IBM` 增加了 `zSeries` 和 `S/390` 大型机上托管 `Linux` 系统的能力时，使得大型机的高质量服务能够扩展到服务器群中的现有分布式应用。该公司评估了基于大型机的 `Linux` 解决方案的能力和优势，包括其无与伦比的灵活性、处理能力以及在 `WebSphere Suite` 下运行电子商务应用程序的能力。接下来，他们决定将服务器群整合到运行 `zSeries` 和 `S/390` 的大型机上。

* 软件 (`z/OS`) 的总成本和环境成本降低了
  - 主机应用 (`z/OS`) 和 `Linux` 应用工作负载随着（`IFL` 驱动的）`Linux` 工作负载而增加。
  - 维护独立 `Windows NT` 服务器的成本得以减少或消除。
  - 管理主机所需的时间少于服务器集群。
* 灵活性
  - `zSeries 900` 高效地运行混合工作负载，包括 `PeopleSoft`、数据仓库、`IMS`、`DB2` 和 `Linux` 应用。
  - 允许运行数千个 `Linux for zSeries` 虚拟机和分区的扩展性，允许将所有工作负载整合到一个中央机器上。
  - `Linux for zSeries` 还可以在不同的 `LPAR` 和 `z/OS DB2` 分区之间提供负载均衡。
* 可用性
  - 单 `zSeries 900` 主机中的 `Parallel Sysplex` 环境为使用 `CICS` 销售点应用程序的电子商务生成的信用卡授权提供了 24 小时可用性。

您可以在 Web 上找到这个故事：
`http://www.ibm.com/servers/eserver/zseries/os/linux/css/boscov1.html`

## 4.6.3 zSeries 服务解决方案

`IBM` 全球服务（`IBM Global Services`）为 `zSeries` 和 `Linux` 解决方案提供许多服务。以下章节提供了可用服务的概述。更多详情，请参阅 `IBM` 全球服务网站：
