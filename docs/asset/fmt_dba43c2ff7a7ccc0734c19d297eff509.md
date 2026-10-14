
## 8.13 其他主题

GnomeVFS 是一个模块化系统，因此编写自己的 GnomeVFS 模块是为 GNOME 应用提供新数据访问方法的逻辑方式。这一过程相当复杂，书中未详细介绍。然而，GnomeVFS 已经支持如此多的访问方法，你可能不需要编写自己的。

另一个书中未涵盖的主题是可以在运行时更改 MIME 类型数据库的 GnomeVFS API。用户可以通过应用程序注册表覆盖系统、mime 和 keys 文件。作为应用程序，你很少这样做。

书中也没有涉及 Bonobo，包括对 Bonobo 组件的 MIME 支持。

# 第 9 章：接下来的路

## 概述

读到这本书的这里，你应该对如何使用 GNOME 开发软件有了相当好的了解。本章将脱离编程讨论，通过回答潜在 GNOME 开发者可能会提出的问题：

- 我如何跟进 GNOME 的任何变化？
- 我如何联系其他 GNOME 开发者？
- 我可以如何为 GNOME 社区做出贡献？
- 未来将如何？

## 9.1 阅读、讨论与协作

你可以通过挖掘更多 GNOME 信息并寻找与其他 GNOME 爱好者交流的方式，来开始你对 GNOME 社区的探索。

也许你觉得，为了回报这些以免费许可提供的软件，你有义务向 GNOME 项目回馈一些。或者你可能有实用的理由与 GNOME 合作——也许你正在使用的某个软件运行得并不正常，或者缺少某些功能。

无论你的目标是什么，都有许多方法开始探索 GNOME 社区。请查看 `http://www.gnome.org/resources/`

### 9.1.1 现实生活

GNOME 项目志愿者和几家公司经常参加大型计算机贸易展，特别是那些与自由软件相关的展会。此外，每年还会举办一次 GNOME 用户与开发者大会（GUADEC）。

更多详情请参阅 GNOME 网站；查看活动日历：`http://www.gnome.org/resources/calendar.html`

### 9.1.2 万维网

大部分的 GNOME 资源都在万维网上。由于 GNOME 广泛的国际基础和各种组件项目的范围，无数与 GNOME 相关的网站遍布在互联网上。

主要的 GNOME 网站是 `http://www.gnome.org/`，你应该在这里找到其他资源，例如 GNOME 常见问题解答、关于贵公司如何支持 GNOME 的信息以及开发者列表。

# 官方 GNOME 2开发者指南

## GNOME 基金会

GNOME 基金会是在加利福尼亚州注册的非政治、非营利、民主组织。查看 `http://foundation.gnome.org/` 上的章程和细则可以了解该基金会的工作。如果你深度参与 GNOME，你可以成为投票成员并竞选正式职位。

## 新闻

Fragments (`http://www.gnomedesktop.org/`) 是一个半官方的由用户维护的 GNOME 新闻网站。除了最新的通用公告外，你还会找到每周摘要、CVS 活动统计数据和 Bugzilla 活动。

## 软件下载

GNOME 软件的分发中心网站是 `http://download.gnome.org/`。请参考附录 D 获取如何选择软件的信息。

所有第三方 GNOME 软件的目录请访问 `http://www.gnome.org/softwaremap/`。如果你正在寻找特定的内容，这里是首选；如果你正在编写应用程序，你应该在这里添加一个条目。

RDF 站点摘要 (RSS) 信息可以从 `http://ftp.gnome.org/pub/GNOME/LATEST.xml` 获取。使用 Starview 等程序可以查看此类信息。

## GNOME Bugzilla

GNOME 用户和开发者最重要的资源之一是 GNOME 错误跟踪系统，即 GNOME Bugzilla (`http://bugzilla.gnome.org/`)。如果你审阅过任何包中的 `ChangeLog`，你可能已经见过诸如“Fixes #88325”和“fix mem leak (bug #72976)”之类的内容。这里的数字是你可以在 Bugzilla 中查询的索引。

当你使用 GNOME Bugzilla 或 Bug Buddy（应用程序 > 编程 > 错误报告工具）提交报告时，会得到一个大数字。为了管理报告，Bugzilla 创建了这些字段：

- `Product`（产品）：包含问题的包（例如 nautilus）。
- `Component`（组件）：出现问题的文档部分。组件依赖于产品；例如，Documentation 是 Nautilus 包的一个组件，General 是默认的通用分类。
- `Short Summary`（短期摘要）：问题的简短描述。
- `Opened by`（提交者）：报告错误的人。
- `Long Description`（详细描述）：问题的详细描述，你可以添加描述层并包含文件（类似于邮件附件）。
- `Status`（状态）：以下状态之一：
    - `UNCONFIRMED`（未确认）：还没有人确认这确实是一个错误。具有足够权限的 Bugzilla 用户可以在确认错误后将此状态更改为 `NEW`（新建），在立即解决问题后更改为 `RESOLVED`（已解决）。
    - `NEW`（新建）：有人确认了该错误，但还没有人负责。
    - `ASSIGNED`（已分配）：有人决定修复此该错误。
    - `NEEDINFO`（需信息）：修复此错误时遇到了一些困难，最初报告错误的人需要提供更多信息。
    - `RESOLVED`（已解决）：有人修复了错误，报告错误的人应该验证修复结果。
    - `REOPENED`（已重新打开）：已解决错误仍存在某些问题。
    - `VERIFIED`（已验证）：有人已验证该错误已修复。
    - `CLOSED`（已关闭）：错误完全消失（没有进一步行动的原因）。
`Severity`（严重程度）：错误严重程度的指示：
- `Blocker`（阻塞）：问题阻止了包的新发布。
- `Critical`（严重）：导致崩溃和数据丢失的严重问题。
- `Major`（主要）：问题仅影响包的一个一小部分。
- `Normal`（普通）：问题使其无法使用。
- `Trivial`（微要）：这是一个拼写错误。
- `Enhancement`（增强）：对功能的建议。
- `Urgent`（紧急）：尽快。
- `High`（高优先级）：在下次发布之前。
- `Low`（低优先级）：任何时候都可以。
- `FIXED`（已修复）：有人修复了它。
- `WONT`（不修复）：不修复。
- `DUPLICATE`（重复）：有人已经报告过了。
- `INCOMPLETE`（不完整）：我们需要更多信息。
- `NOTGNOME`（非GNOME）：这与 GNOME 无关。
- `Assigned To`（分配给）：有人负责。
- `Depends`（依赖）：这取决于其他内容。
- `Blocks`（阻塞）：这阻塞了其他内容。
- `Operating System`（操作系统）：这是一个操作系统问题。
- `Accessibility`（辅助功能）：这是针对残障用户的。
- `Translation`（翻译）：用于翻译 GNOME。
- `GNOME Webhackers`：在这里，GNOME Webhackers 构建并维护各种网站。
- `GNOME Documentation Project`：该项目提供文档。
- `GNOME Usability Project`：该项目提供指南和标准。
- `GNOME Accessibility Project`：该项目为残障人士提供支持。
- `GNOME Translation Project`：该项目旨在翻译 GNOME 软件。

如果你是 GNOME 爱好者，应该定期访问 GTK+ 网站 (`http://www.gtk.org/`)。

# GNOME 2 开发者官方指南

- `gtk-app-dev-list`: GTK+ 应用开发。
- `desktop-dev-list`: 桌面应用及相关领域的通用讨论。
- `gnome-accessibility-list`: 辅助功能问题的讨论（ATK、界面开发等）。
- `gnome-doc-list`: 文档问题。
- `gnome-i18n`: 国际化讨论。
- `garnome-list`: 为使用 GARNAME（一种 GNOME 发行版；附录 D）的用户提供的讨论。

## 9.1.4 IRC

设有互联网中继聊天（IRC）通道用于 GNOME 的实时讨论。位于 `irc.gimp.org` 的 GIMPnet 服务器负责讨论 GNOME、GTK+ 和 GIMP。以下通道始终可用：

- `#gnome`: GNOME 通用议题。
- `#gnome-help`: GNOME 寻求帮助。
