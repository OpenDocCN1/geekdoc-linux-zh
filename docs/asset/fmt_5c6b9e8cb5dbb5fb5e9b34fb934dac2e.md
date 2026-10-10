
IBM 的所有服务器平台都支持 `Linux`，包括 `zSeries`、`iSeries`、`pSeries` 和 `xSeries` 服务器。`xSeries` 已经通过 `IBM ServerProven` 计划，获得了 `Caldera`、`Red Hat`、`SuSE` 和 `Turbolinux` 发行版的认证。此外，某些型号的 `IBM IntelliStations` 和 `ThinkPad` 也支持 `Linux`。对于大型机系统，可以从发行伙伴处获得 `Linux for zSeries` 和 `Linux for S390`。`IBM` 通过提供 `Linux` 互操作性，将文件服务、数据传输、打印以及其他服务等范围扩展到整个企业内的 `Linux` 客户端，从而增强了 `zSeries` 和 `iSeries` 系统的开放性。

`AIX 5L` 中的 `Linux` 亲和 `API` 支持在运行 `AIX 5L` 的 `pSeries` 产品上重新组合应用程序以在 `Linux` 上执行，这些此前已有描述。虽然这种方法在某些情况下很有用，但业务依赖于运行 `Linux` 应用程序的公司可能希望“原生”运行 `Linux`，即直接运行在 `pSeries` 硬件上。目前有多种可在 `pSeries` 上运行的发行版。最近，`AIX 5L v5.2` 增加了一个基于 `Web` 的系统管理器 `Linux` 客户端。

通常情况下，对于超过 8 个处理器的 `SMP` 服务器，`Linux` 的性能扩展不如 `AIX 5L` 良好。然而，随着开放系统社区的发展，这种情况将会发生变化。如果他们的需求是仅运行 `Linux`，`pSeries` 用户应该考虑入门和中端系统，如 `p615`（1 路和 2 路）、`p630`（1 到 4 路）和 `p650`（2 到 8 路）。如果他们想在一个或多个 `LPAR` 中运行 `Linux`，他们可以从全系列支持 `LPAR` 的 `pSeries` 服务器中选择（`p630`、`p650`、`p655`、`p670`、`p690`）。

希望在 `pSeries` 上运行的用户另一个考虑因素是 `I/O` 设备和适配器的支持比运行 `AIX 5L` 时更有限。这种情况的原因是，支持设备的设备驱动程序代码已移植到 `Linux` 并提供给开源社区。设备驱动程序的初始优先级是 `SCSI`、`以太网`、光纤和 2D 图形适配器。目前，`pSeries Linux` 可以利用 `Ultra-SCSI` 适配器和 `Ultra3-SCSI` 适配器（尚未支持 `RAID`）、最高千兆以太网适配器（`UTP` 和光纤）、2 `Gbps` 光纤适配器以及 `GXT135P` 图形适配器（包括数字支持）。还支持一组特定的媒体设备和磁盘子系统，包括 `IBM 2104 Expandable Storage Plus`、`IBM FaST` 系统和 `IBM` 企业存储服务器 (`ESS`)。

## pSeries 的 Linux 发行版

`SuSE` 率先为 `pSeries` 和 `RS/6000` 系统提供了 `Linux` 发行版。在提供两个使用 32 位内核的 `PC` 版本后，`SuSE` 在 2002 年 12 月为 `iSeries` 和 `pSeries` 引入了支持 `SMP` 能力的 64 位 `SuSE Linux Enterprise Server 8` (`SLES`)。`SLES 8` 现在支持所有可用的 `pSeries` 和 `RS/6000` 服务器，但 32 位服务器除外。

`Red Hat` 在 2002 年初为 `pSeries` 和 `RS/6000` 系统引入了 `Red Hat 7.1 Linux` 发行版，并在 2002 年 12 月支持 64 位内核，但仍支持 32 位应用。`IBM` 最近与 `Red Hat` 达成协议，目标是让 64 位的 `Red Hat Advanced Server` 适用于 `POWER3` 的 `pSeries 640`。

`Turbolinux` 最近在日本推出，预计将在其他亚洲国家宣布 `Turbolinux Linux Enterprise pSeries` (`TLES 8`) 产品。此前，`pSeries` 的唯一 `Turbolinux` 发行版是 32 位产品。`Turbolinux` 是亚太地区的关键分销商，预计 `TLES 8` 未来将对 `pSeries` 有广泛支持。

`IBM` 不销售和支持 `Linux` 操作系统，但多个 `Linux` 发行商为 `pSeries` 用户提供软件、支持和服务。`IBM` 全球服务可以付费提供 `Linux` 服务。为了方便客户，当订购这些“`Linux` 准备绪”配置时，`IBM` 将接受订单并转交给 `SuSE` 提供 `SLES 8`。这种转单订单仅适用于初始系统购买，且由 `SuSE` 提供软件、许可和支持。

## pSeries Linux IBM 应用程序软件

适用于 `pSeries Linux` 的 `IBM DB2` 通用数据库 (`UDB`) 版本现已发布。除了 `DB2 UDB`，`IBM` 还宣布计划在 `pSeries` 上支持许多其他软件产品，包括 `WebSphere` 应用服务器（由 `Apache` 引擎驱动）和特定的 `Tivoli` 管理工具。此外，`IBM` 日志文件系统和 `Linux` 开发 `Kit Java 2` 技术版已在 `SLES 8` 和 `Red Hat 7.1` 上通过认证。

`IBM` 还与其业务合作伙伴和第三方软件供应商合作，在 `pSeries` 上迁移、重新编译并测试其应用程序。用户应向相应的软件供应商查询特定应用程序在 `pSeries` 上的支持情况。

## pSeries Linux：IBM 总结

`AIX 5L` 作为 `IBM` 的高性能 `UNIX` 操作系统，将继续作为 `pSeries` 服务器开发的核心操作系统，并充分利用所有 `pSeries` 创新——处理器和内存扩展性、动态 `LPAR`、动态处理器和内存 `CuOD`、`RAS` 功能以及对各种 `I/O` 设备的支持。但 `IBM` 为需要将 `Linux` 应用程序整合到其 `pSeries` 计算环境的用户提供了广泛支持，无论是将 `Linux` 作为唯一操作系统运行，还是为特定应用程序运行 `Linux`。关键词是“选择”。

# 4 pSeries 通信

`pSeries` 系统的标准功能和选项，同 `AIX 5L` 操作系统及其扩展，为用户各种通信环境配置系统提供了灵活性。然而，这种灵活性在尝试确定特定环境需要哪些选项和程序时也可能导致困惑。本章将引导您了解 `pSeries` 系统可用的通信选项。

第 2 章“选项和外围设备”探讨了 `pSeries` 系统中使用的一些通信硬件选项，并对通信接口和协议进行了简要教程。第 3 章查看了 `AIX` 操作系统提供的某些通信软件。本章将介绍一些最常用的通信环境，并为每个环境提供示例配置。

## 计算机通信——简介
