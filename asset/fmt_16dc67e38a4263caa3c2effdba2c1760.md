
#### 2.4.3 pSeries 服务

`pSeries` 服务器为快速 64 位原生 `Linux` 服务器提供了可靠的基础。

`IBM` 为新推出的 `pSeries 630 6C4` 和 `630 6E4 Linux` 就绪 `express` 配置提供硬件和软件支持服务，这些配置现已上市。

有关这些型号的信息，请参阅：

`http://www.ibm.com/content/home/store_IBMPublicUSA/en_US/eServer/pSeries/entry/6306C4.html`

`http://www.ibm.com/content/home/store_IBMPublicUSA/en_US/eServer/pSeries/entry/6306E4.html`

随着客户对在该平台上将 `Linux` 用作其原生操作系统的兴趣日益增长，`IBM` 将为 `pSeries` 的 `Linux` 提供更多服务。

有关更多信息，请访问 `IBM Linux for pSeries` 网站：

`http://www.ibm.com/servers/eserver/pseries/linux/index.html`

#### 2.4.4 xSeries 服务

`IBM` 通过 `xSeries Linux` 启用功能以具有吸引力的价格提供企业级可扩展性和可用性。`IBM` 的 `Linux` 与 `xSeries` 的结合已被证明是成功的。许多资源和信息可供有兴趣在 `xSeries` 上使用 `Linux` 作为满足其需求的关键环境的用户使用。

表 2-13 列出了提供有关 `xSeries` 服务器可用服务的基于平台信息的各种参考。

表 2-13 `xSeries Linux` 信息矩阵

| 信息 | 网页位置 |
|---|---|
| 适用于 `xSeries` 的 `Linux` 信息 | `http://www.pc.ibm.com/us/eserver/xseries/index.html` |
| `eServer Blades Center` | `http://www.ibm.com/servers/eserver/blades/` |
| `xSeries` 上的 `Linux` 集群 | `http://www.ibm.com/servers/eserver/clusters/` |
| 适用于 `xSeries` 的 `Linux ISV` 资源 | `http://www.ibm.com/developerworks/offers/linux-speed-start/isv.html` |

#### 2.4.5 统一平台矩阵

有关 `IBM` 所有 `IBM eServer` 服务的 `IBM Linux` 的更多有价值信息，以及最新信息、更新、新服务等，请参阅表 2-14 中列出的每个平台的 `IBM Linux` 专用网站。

表 2-14 每个 `Linux` 平台的 `IBM` 网站矩阵

| 平台 | 网页位置 |
|---|---|
| `zSeries` | `http://www.ibm.com/servers/eserver/zseries/os/linux/index.html` |
| `iSeries` | `http://www.ibm.com/servers/eserver/iseries/linux/index.html` |
| `xSeries` | `http://www.ibm.com/servers/eserver/xseries/linux/index.html` |
| `pSeries` | `http://www.ibm.com/servers/eserver/pseries/linux/index.html` |

## zSeries 和 Linux

本章简要概述了 `IBM eServer zSeries`，重点介绍如何在 `zSeries` 架构上运行 `Linux`。

由于 `Linux` 可以作为 `z/VM` 客户机在 `zSeries` 上运行，本章包含有关 `z/VM` 的背景信息，以便读者了解在这种情况下其 `Linux` 安装将继承的功能和特性。

最后，本章讨论了在 `zSeries` 上扩展和整合 `Linux` 解决方案的场景。

### 3.1 引言

`IBM eServer zSeries` 是 `S/390` 系列的继任者，也是 `IBM` 用于电子商务交易工作负载的首选服务器。`zSeries` 在运行具有无与伦比的可靠性和可用性的商业应用方面有着悠久的历史。1999 年 `Linux` 被移植到 `S/390`，并在 2000 年初发布。此后，添加了许多新特性和设备支持，越来越多的客户使用 `Linux for S/390` 和 `zSeries` 用于运行新工作负载或整合服务器。`Linux for zSeries` 受支持于所有 `zSeries` 机器，以及前身 `S/390` 型号 `G5`、`G6` 和 `MP3000`。这些在图 3-1 中显示。

![](img/da33d6b6aa12b73deb3c350a0a89d424_37_0.png)

图 3-1 `IBM eServer zSeries`

#### 3.1.1 在 zSeries 上运行 Linux 的方式

在 `zSeries` 上运行 `Linux` 有三种方式，分别是：

- 基本或原生模式

  `Linux` 使用整台机器，而没有任何其他操作系统。在基本模式下，您可以在 `zSeries` 的“裸机”上使用单个 `Linux` 映像。

- 逻辑分区或 `LPAR`

  您可以将 `zSeries` 硬件逻辑划分为最多 15 个独立的 `LPAR`。例如，单个 `zSeries` 可以在一个分区中托管 `z/OS` 应用，在另一个分区中托管 `VM`，并在其他分区中托管 `Linux` 应用。

- `z/VM`

  客户可以使用 `z/VM` 作为 `hypervisor` 将 `Linux` 作为虚拟机运行。`z/VM` 提供 `CPU` 处理器、输入/输出（`I/O`）子系统和内存的虚拟化。运行 `z/VM` 的客户可以在单个 `zSeries` 上运行数百个 `Linux` 系统。例如，使用 `z/VM`，客户可以为每个应用开发人员提供完整的 `Linux` 服务器环境，并在同一 `zSeries` 服务器上托管生产系统。

关于如何在 `zSeries` 上运行 `Linux` 的决策通常基于预期的工作负载：

- 很少（如果有的话）工作负载需要在基本模式下运行 `Linux`。

- `Linux` 工作负载的资源需求较大（如内存占用和处理能力）可能最适合在 `LPAR` 中运行。这在特别如此，如果 `Linux` 系统将在长时间内处于峰值负载运行，因此资源共享的机会有限。当只需要少量映像时，使用 `LPAR` 也可能是合适的，因为在这种情况下，`z/VM` 的额外资源和支持需求可能不合理。

- 将 `Linux` 作为 `z/VM` 客户机运行可提供最大灵活性。运行在 `z/VM` 下的 `Linux` 客户机数量可根据工作负载需求进行调整。唯一限制并发运行实例数量的是硬件资源。大多数客户选择此选项以最大化其投资。

最后两种选项在图 3-2 中有所描述。请注意，该图仅供说明，在实际生产环境中，您还应期望有一个运行 `z/OS` 的 `LPAR`，如第 26 页图 3-4 所示。

![](img/da33d6b6aa12b73deb3c350a0a89d424_38_0.png)

#### 3.1.2 S/390 和 zSeries 架构

`zSeries` 和 `S/390` 架构的核心是多芯片模块（`MCM`），其包含多达 20 个处理单元（`PU`）。这些通常被称为中央处理单元（`CPU`）或引擎。

所有 `PU` 都是相同的，但可以在系统中承担不同的角色。每个 `PU` 可以是以下之一：

- 中央处理器（`CP`）`PU`：由操作系统用于执行客户工作

- 系统辅助处理器（`SAP`）`PU`：这是一个运行通道子系统授权内部代码以控制 `I/O` 操作的 `PU`。

- `Linux` 集成设施（`IFL`）`PU`：`IFL` 引擎仅限于运行 `Linux` 或 `z/VM`。

- 集成耦合设施（`ICF`）`PU`：该引擎用于运行耦合设施功能，供 `Parallel Sysplex` 使用。

### IFL 引擎

`IFL` 是为 `Linux` 或 `VM` 下的 `Linux` 保留的处理器。其意义在于它不能用于运行其他操作系统，并且其存在不会反映在系统型号、`MIPS` 评级或其他功率评级中。这些功率评级方法对软件成本有重大影响。添加 `IFL` 不会影响这些成本，允许在不影响其他软件成本的情况下使用 `Linux`。

第 26 页图 3-3 显示了 `IFL` 如何分配给逻辑分区（`LPAR`）。

![](img/da33d6b6aa12b73deb3c350a0a89d424_39_0.png)

图 3-3 `IFL` 与 `LPAR` 之间的关系

注：`IFL` 必须专用于运行 `Linux` 或 `z/VM` 的 `LPAR`。它们可以由多个 `LPAR` 共享，前提是这些 `LPAR` 运行 `Linux` 或 `z/VM`。此外，`LPAR` 不能同时包含 `IFL` 或 `CP` 的混合。

图 3-4 为运行 `z/VM` 下 `Linux` 及其他工作负载的 `zSeries` 服务器的 `CP` 配置提供了一个示例。

![](img/da33d6b6aa12b73deb3c350a0a89d424_39_1.png)
