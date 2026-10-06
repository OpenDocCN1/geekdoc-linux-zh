

## 附录 C：RHEL 特性

经过认证的 RHEL 5 硬件请访问 Red Hat 网站上的硬件目录（http://hardware.redhat.com）。

在商业软件方面，Red Hat 维护了一个包含数百家认证供应商产品的目录，这些产品可以在 RHEL 系统上运行。该供应商列表包含了几家合作伙伴公司，例如 Oracle、IBM、BEA Systems、Veritas Software 和 Sybase。您可以在 Red Hat 软件目录（https://www.redhat.com/apps/isv_catalog）查看 Red Hat 商业软件供应商列表。

Red Hat 还帮助想要开发并在 RHEL 系统上运行商业应用程序的企业。您可以从开发者支持页面（http://www.redhat.com/developers/subscriptions.html）获取有关应用程序支持的信息。

# 培训与认证

如果您正在寻找 Linux 职业生涯，Red Hat 提供了一些备受誉目的计划，帮助您成为 Red Hat 软件认证专家。您可以从 Red Hat 培训网站（https://www.redhat.com/training）了解可用的计划。

如果您计划参加任何 Red Hat 认证计划，在接受完一些理论培训后，如果给您一台配置错误的计算机并要求您修复它，请不要惊讶。获得 Red Hat 认证的人员被认为能够在现实世界中清理和运行 Linux 系统。

以下是 Red Hat 提供的认证列表：

- * Red Hat 认证技术员 (RHCT) —— RHCT 是最基础的 Red Hat 认证。它侧重于 Red Hat 系统管理员所需的的核心技能。除了能够安装和配置 RHEL 系统以接入企业网络外，预计您还需要理解基础的故障排除。
- * Red Hat 认证工程师 (RHCE) —— RHCE 计划建立在 RHCT 计划开发的技能的基础上。然而，对于 RHCE，预计其在安全和部署网络服务方面具备额外的能力。
- * Red Hat 认证安全专家 (RHSS) —— 顾名思，精通管理 Red Hat 企业级系统的安全相关方面。获得此认证的课程包括网络安全、SELinux 策略与管理。
- * Red Hat 认证架构师 (RHCA) —— RHCA 的技能预计超过 RHCT 或 RHCE。RHCA 计划侧重于在整个企业范围内部署和管理多个 Linux 系统，特别关注系统管理、存储管理、性能调优和目录服务。

有关 RHCT、RHCE、RHSS 和 RHCA 的课程，请访问 Red Hat 认证工程师页面（https://www.redhat.com/training/）。在参加 RHCT 考试之前，请查看 RHCE 考试准备指南（http://www.redhat.com/certification/rhce/prep_guide/）。Red Hat 提供许多 Red Hat 培训课程，以及网络、编程（Java、对象、Web 和 IT 管理）等课程。

# 文档与支持

Red Hat 全球服务（https://www.redhat.com/apps/support）提供了强大的工具来帮助您。如果您有评估订阅，可以使用您的登录 ID 和密码来尝试支持服务。访问这些资源就足够从支持站点获取 RHEL 产品。Red Hat 有许多获取帮助的途径。

Red Hat Enterprise Linux 文档（http://www.redhat.com/docs/manuals/enterprise）包含了用于安装、系统管理、安全、SELinux 的手册，以及不同产品的发布说明。您可以使用关键字搜索从 Red Hat 知识库中找到您问题的答案。

# 管理 RHEL 系统

高效管理和扩展您的 Linux 基础设施的能力可能是使用 RHEL 系统的最佳原因。Red Hat 创建了 Red Hat Network，允许您正确地跟踪和更新 RHEL 系统。随着不同的订阅级别，支持级别以及维护从一个到数千个系统的功能也会增加。通过使用包括全局文件系统 (GFS) 和高性能计算 (HPC) 集群技术在内的功能，Red Hat 帮助创建灵活高效的 Linux 基础设施。这种基础设施让您可以在不丢弃的情况下逐步扩展计算能力。

# 使用 Red Hat Network

Red Hat Network（https://rhn.redhat.com）提供了一种管理您的 Linux 系统的服务。您可以使用评估订阅尝试 Red Hat Network。从 Red Hat Network 网站，您可以将系统升级为付费订阅，或注册额外的权限以管理多个 RHEL 系统。

开发 Red Hat Network是为了帮助企业实施和管理其 Linux 基础设施。Red Hat Network 有多种不同的配置架构。这些架构允许您选择直接连接到 Red Hat Network（管理系统权限和更新），还是连接到您所在地设置的卫星服务器或代理服务器。

您选择的架构将影响您对 RHEL 系统的控制程度。以下是可选方案：

- **托管模型 (Hosted model)** —— 在托管模型下，每个 RHEL 系统直接与 Red Hat Network 通信以管理其获取的更新。更新基于您使用的硬件和软件的相应通道。信息存储在 Red Hat 服务器中，而不是在您自己的网络上本地管理。
- **代理模型 (Proxy model)** —— 代理模型的工作方式与托管模型类似，但不是让每个系统单独从 Red Hat Network 获取更新，而是在客户现场设置一个代理服务器，因此更新只需要下载到您的网络中。然后各个系统从本地代理服务器获取它们所需的更新。虽然更新存储在本地，但有关通道的权限仍然由 Red Hat Network 管理。
- **卫星模型 (Satellite model)** —— 所有 Red Hat 功能（系统管理、更新等）都位于您的本地网络上。更新从 Red Hat Network 下载到您的卫星或代理服务器。通常由 RHN 管理的自定义通道和其他任务被卸载到卫星服务器。卫星模型通常用于希望对服务部署保持更多控制和安全性的的大型企业。提供不同级别的支持和培训，但意图是让 Red Hat 充技术顾问，而由您的员工负责网络服务器的数据库管理。

除了基础更新服务外，还可以从 Red Hat 购买不同的支持级别。管理和配置计划旨在帮助您跨整个企业的 RHEL 系统。以下是您将获得的内容：

- **管理 (Management)** —— 在此订阅级别下，组织可以分配管理员来管理一组系统。组织管理员有权分配这些用户以及他们可以的系统。为了管理系统，用户可以的操作包括查看不同系统安装的完整包、搜索系统组的安装包或硬件标签、将系统分组以便作为一个组管理，以及为批量系统添加或删除软件包。
- **配置 (Provisioning)** —— 配置订阅级别包含了更新和管理级别的所有功能，但增加了更多管理多个系统的功能。例如，您可以创建配置文件，允许您安装预设了许多许多系统（如时区、GPG 和 SSL 密钥以及特定的软件包集）。如果您在相似的硬件上安装，甚至可以预设棘手的配置功能（如显卡配置）。配置订阅者还

