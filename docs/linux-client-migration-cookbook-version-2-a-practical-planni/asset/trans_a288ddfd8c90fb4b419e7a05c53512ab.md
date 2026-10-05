

我们在卫星服务器的上下文中详细描述了这些概念中的每一个。其中某些术语在 ZENWorks 中也作为概念存在，但含义可能略有不同。

## 系统 (System)

系统可以是任何安装了 Red Hat Linux 且配置了连接服务器更新的机器。系统通过注册过程连接到卫星服务器，该过程会将系统与卫星服务器上的用户 ID 关联。

## 系统组 (System group)

组是卫星服务器中的一个实体，可以包含系统。创建时，容器是空的。可以将系统添加到系统组中。系统组在卫星服务器中用于对多个系统（组内的系统）同时执行操作。你也可以拥有属于多个系统组的单个系统，例如在你的企业中可能在功能和地理位置上重叠。

## 系统集 (System set)

如果说系统组是固定的，那么系统集就可以用于选择系统以执行操作，可以是针对单个系统、组级级，或者基于系统的某些属性。你可以“动态”构建系统集，以便将系统分组在一起以应用特定操作。

## 权限 (Entitlements)

权限允许订阅访问 RHN 中的服务级产品。可用订阅的数量和类型由购买的 RHN 许可证决定。你可以拥有系统级或软件通道级的权限。

## 模块 (Modules)

模块概念允许选择卫星服务器可以执行的服务权限级别。在当前的 Red Hat Network 和卫星服务器中，有四个模块：

- *更新 (Update)* - 入门级模块，随 Red Hat Network 免费提供，最适用于单个或少数系统。

- *管理 (Management)* - 包含更新模块的功能，以及能够更高效地系统分组、管理和通道定义的额外功能，以支持更大数量的系统。

- *配置 (Provisioning)* - 包含管理模块的功能，以及提供完整的 Linux 基础设施全生命周期管理的额外功能。

- *监控 (Monitoring)* - 需要管理模块和卫星服务器。能够对所有 Linux 系统的性能进行跟踪和监控。

> 注意：有关关于 RHN 模块的最新信息，请参阅 Red Hat 网站：
http://www.redhat.com/rhn

随着每个权限级别的提高，卫星服务器/RHN 的更多功能变得可用。你可以随时更改分配给特定系统或系统组的模块权限级别。

## 通道 (Channel)

通道是更新的集合。通道有两种类型：基础通道和子通道。

基础通道由基于特定架构和 Red Hat Enterprise Linux 版本的包组成。例如，所有适用于 x86 架构的 Red Hat Enterprise Linux 4 的包都是一个基础通道。

子通道与基础通道关联，但它包含额外的包。通过这种方式，组织可以使用基础通道创建一个子通道，其中包含基础包和组织专门需要的额外包。

## 操作 (Action)

可以从卫星服务器对客户端执行操作。由于 `rhnd` 守护进程以 root 身份运行，甚至可以从卫星服务器调度重启。某些可以调度的操作包括：

- 启动 (Boot)
- 软件包更新 (Package update)
- 硬件属性更新 (Hardware properties update)

## 错误列表 (Errata)

Errata 是所有更新和补丁集合的名称。Red Hat 区分了三种类型的错误：

- 安全更新 (Security updates)
- 错误修复更新 (Bugfix updates)
- 增强更新 (Enhancement updates)

这三种类型的错误在应用时各有自己的优先级。安全更新应立即应用，需要时应用错误修复更新，在需要时应用增强更新。

## 激活密钥 (Activation key)

激活密钥用于注册系统、赋予系统服务级权限，并通过命令行工具 `rhnreg_ks` 将系统订阅到特定的通道和系统组。这些密钥只能为管理和配置权限创建。密钥在卫星服务器中生成。对于单个系统，你可以组合多个激活密钥（密钥堆叠/key stacking）。密钥堆叠允许为具有不同订阅级别要求的多个系统减少所需的密钥总数。

## 示例更新场景 (Sample update scenario)

考虑一家大型跨国公司，在企业范围内运行 Red Hat Desktop 作为其主要的用户客户端平台。他们的 IT 部门开发人员在测试平台客户端应用程序上运行最新版本，当它们迁移到最新发布版本并通过质量保证 (QA) 测试后，他们就可以使用 RHN 通道为他们的生产客户端组提供更新。

第 263 页的图 B-2 显示了专注于桌面通道的简化 Red Hat Network 拓扑。卫星服务器提供了三个基础通道。Red Hat Desktop 通道作为一组子通道的基础，这些子通道用于管理开发和测试（在图中编号为 1-2-3）。RHD 基础通道提供 RHD Update 3（基础通道将标记为“RHD_U3”）。因此，每个子通道可以如下如下标记：

- 1. RHD_U3dev
- 2. RHD_U3test
- 3. RHD_U3prod

IT 部门想要以管理 Update 3 部署相同的方式将 RHD Update 4 部署到他们的生产桌面通道。为了做到这一点，他们遵循将 Update 3 推送到企业的相同模式。他们首先在卫星服务器上创建一个“RHD_U4dev”基础通道。他们可以通过克隆 Red Hat 提供的 Red Hat Desktop 通道来完成，或者创建一个新的空通道并从安装媒体将相应的包推送到通道中。这个新的 RHD_U4dev 通道随后被他们的开发人员用于测试和更新任何应用程序。

一旦开发人员完成了在 RHD_U4dev 上的工作，同一个通道将被克隆为 RHD_U3test，然后由 IT 质量保证团队接管。他们测试包并报告错误，还可能请求开发团队对通道中包含的任何包进行修复。

当 QA 团队能够批准 RHD_U3test 通道的生产就时，可以将其克隆为新通道 RHD_U4prod。这个新的生产通道将用于管理向企业的 U4 更新。

![](img/23b949da14ff7bab8762f0f0361af394_290_0.png)

图 B-2 Red Hat Network 拓扑

## Novell ZENworks Linux 管理 (Linux Linux Management)

本节描述 Novell ZENworks，现在称为 ZENworks Suite。ZENworks Suite 是 Novell 用于部署、管理和维护系统的应用程序平台。对于组织内运行大量 Linux 安装的企业客户特别有用。

ZENworks 是 Novell/SUSE 发行的首选工具，它可以管理任何基于 Linux 或 Windows 的桌面。本节关注 ZENworks Linux 管理工具。

## 架构与功能 (Architecture and Functionality)

ZENworks Suite 包含基于 Web 的工具，允许管理员在异构环境中管理系统。套件中有模块管理资产、数据、桌面、手持设备、Linux、桌面设置迁移、服务器、软件和补丁。他们的 Linux 管理解决方案使用策略和自动化来管理 Linux 系统。

ZENworks 套件专注于全生命周期系统管理。要获取 ZENworks Suite 功能的完整概述，请参阅 Novell 网站：

http://www.novell.com/products/zenworks/

参见图 B-3。

![](img/23b949da14ff7bab8762f0f0361af394_292_0.png)

## ZENworks Linux 管理 (ZENworks Linux Management)

Linux 管理模块中的可用管理任务：

- 交付包
- 锁定客户端桌面设置
- 定义预启动活动
- 软件和硬件清单
- 管理远程事件
- 生成报告

ZENworks Linux 管理服务器的系统架构见第 266 页的图 B-4。该服务器由运行在数据库之上的应用程序以及使用 http/https 接口进行通信组成。

> ² 转载自“ZENworks 7 IT Management Suite”概述 (http://www.novell.com/products/zenworks/overview.html)

