
# DB2 自管理和智能数据库技术

## 用于 zSeries DB2 的特定价值主张

zSeries 客户可以扩展并利用他们目前的硬件投资。在 `VM` 环境下，单个 zSeries 上可以有数百甚至数千个 Linux 操作系统与其他操作系统共存。通过 `VM`，客户可以为每个应用程序开发者提供完整的 Linux 服务器环境，同时仍在同一台 zSeries 服务器上运行主机生产系统。

您可以在 Linux 上部署新应用程序，并仍使用 `DB2 Connect` 连接到他们现有的 DB2 数据。您还可以在 Linux for zSeries 上使用 `IBM DB2 Connect` 在主机上汇总所有的网关连接处理。这消除了对中间层硬件的需求。

客户可以利用 `DB2 UDB` 和 Linux for zSeries 上 `DB2 Connect` 针对 UNIX 环境的特性，使得目前面向 UNIX 客户的供应商能够利用 zSeries 平台。

## 用于 xSeries（Intel 架构服务器）DB2 的特定价值主张

xSeries 客户可以降低其总拥有成本 (`TCO`)。用于 xSeries 的 Linux 版 `DB2 UDB` 可以在低成本硬件上运行。此外，客户不会被锁定某种特定的操作系统。用于 Linux 的 `DB2 企业扩展版 (EEE)` 允许客户根据需要为 Web 服务和数据仓库增加额外容量，且价格低于目前可用的其他集群解决方案。

此外，DB2 是 Linux 上的性能领导者。DB2 位列 2002 年 11 月最新的 TPC-H 基准测试之列。更多信息请访问：

```
http://www.tpc.org/results/tpch_results
```

## DB2 产品在 Linux 可用性

DB2 品牌的产品列表包括：

- `DB2 UDB`（工作组版、扩展版、个人版）
- `DB2 Express`（针对中小型企业的特殊提供）
- `DB2 Connect`
- `DB2 Search`
- `DB2 Network`
- `DB2 Relational`

有关 Linux 产品的最新可用性和详细描述，请查看：

```
http://www.ibm.com/cgi-bin/software/track?file=/software/is/mp/linux
```

`DB2 UDB` 运行在多种硬件平台上。除了 Intel 32 位硬件外，目前的 Linux 版已运行在 zSeries 上，并正在 iSeries 进行 Beta 测试。IBM 已宣布支持 64 位 Itanium2 系统，并表示计划支持 PowerPC 平台。IBM 还公开演示了 64 位 AMD Opteron 系统的 Linux 版。

对于 32 位 x86 平台，DB2 需要具有 `2.4` 内核、`glibc 2.1.2` 和 `libstdcc++ 2.9` 或更高版本的 Linux。DB2 8 版本推出了 Linux 验证计划，以确保 DB2 在 Linux 平台上的更好的可用性并增强客户体验。IBM 正密切与 Linux 社区、Linux 发行版合作伙伴以及独立软件硬件供应商合作，使用各种 Linux 内核、发行版、第三方产品、硬件以及与 DB2 交互的其他组件测试 DB2。作为验证计划的一部分，在产品受 DB2 支持之前，会经过严格测试以确保与其他产品开箱即可运行 DB2。

与 IBM 软件的通用 Linux 发行版说明不同，`DB2 UDB` 支持大量通过验证适用于 DB2 的 Linux 发行版，包括 Hat Platform 7.2、7.3 和 8.0；Advanced Server 2.1；SuSE Professional 7.3、8.0 和 8；SuSE Enterprise Server 7 和 8；SCO Linux 4.0；Turbolin Enterprise Server 7.0 和 8.0 以及其他由 UnitedLinux1.0 驱动的发行版。请查看以下验证网站以获取支持平台和发行版的完整最新表格：

```
http://www.ibm.com/db2/linux/validate
```

> 注意：运行随 DB2 的 Java 应用程序和图形工具（如 `Control Center`）需要 `JDK 1.3.1`。为了方便起见，它随 DB2 8.1 光盘片提供。在大多数情况下，它会在安装 DB2 时自动安装。请参阅验证网站（上）获取最新的支持产品列表。

## 8.3.2 Informix 产品族

`Informix` 数据管理产品集广泛部署在 UNIX 和 Windows 等各种服务器上。它为许多中小型客户提供了数据管理的核心支持。

您可以在 Web 上找到有关 `Informix` 产品的详细信息：

```
http://www.ibm.com/software/data/informix/
```

### Informix 在 Linux 上的可用性

Linux 上的 `Informix` 系列产品包括：

- `Informix 4GL 编译器`（以及交互式 调试器）
- `Informix 4GL 快速开发系统`（以及运行时）
- `Informix C-HISAM`
- `Informix 客户端软件开发包 (CSDK)`
- `Informix Connect Runtime`
- `Informix 4GL`
- `Informix Dynamic Server - IDS (工作组、企业版和无限版)`
- `Informix ESQL (Cobol, C)`
- `Informix Excalibur Text Search Datablade`
- `Informix Extended Parallel Server (XPS)`
- `Informix Geodetic Datablade`
- `Informix Image Foundation Datablade Module`
- `Informix Internet Foundation 2000 (IIF2K)`
- `Informix NET`
- `Informix OnLine`
- `Informix Red Brick™ 仓库`
- `Informix SE Personal Edition`
- `Informix Server Administration`
- `Informix Spacial Datablade`
- `Informix TimeSeries Datablade`
- `Informix TimeSeries Realtime Loader`
- `Informix Web Datablade`

有关 IBM Linux 软件产品的最新可用性及详细描述，请参阅：

```
http://www.ibm.com/cgi-bin/software/track3.cgi?file=/software/is/linux/software/pdfs/IBMSoftwareOnLinux.pdf&S_TACT=_S_TACT&_S_CMP=_S_CMP_
```

### Informix 对 Linux 的支持

Linux 可来自多个发行版，包括 Red Hat、SuSE、SCO 和 Turbolinux。`Informix` 已从支持每个发行版的特定版本转变为支持 Linux 组件版本，从而允许 Linux 社区定义支持 `Informix` 产品的发行版。

无论使用哪种 Linux 发行版，只有在正式发布重大 Linux 升级时，才需要对 Linux 上的 `Informix` 产品发布进行正式重新认证。这通过内核或 `glibc` 版本的第二个小数数字的变化来指示。例如，不需要从内核版本 `2.2.5` 升级到 `2.2.6` 的认证。然而，需要从内核 `2.2.5` 到 `2.4.0` 的正式认证。不需要从 `glibc 2.0.7` 升级到 `2.0.8` 的认证，但当版本从 `2.0.7` 变为 `2.1.0` 时就需要认证。

`Informix` 产品路线图提供了一个完整且清晰的支持平台和发行版表格。您可以在 Web 上找到它：

```
http://www.ibm.com/software/data/informix/pubs/roadmaps/linux_rmap.html
```

### 8.3.3 U2 产品族

`U2` 数据管理产品与 `Pick` 操作系统中的产品类似。`U2` 为嵌入垂直领域应用提供了高性能、可扩展的数据管理环境。超过 390 万用户依赖 IBM U2 数据管理解决方案。

您可以在 Web 上找到有关 `IBM U2` 产品的详细信息：

```
http://www.ibm.com/software/data/u2/
```

### U2 在 Linux 上的可用性

Linux 上的 U-2 品牌产品包括：

- `IBM Cobol Direct Connect`
- `MITS`
- `IBM RedBack`
- `IBM SystemBuilder Plus`
- `IBM Unidata`
- `IBM Universe`

有关 IBM Linux 产品的当前可用性及详细描述，请参阅：
