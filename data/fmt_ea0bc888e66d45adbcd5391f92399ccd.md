
# Buildroot 组件编译方法

Buildroot 为编译组件提供了两种方法。你可以为每个组件编辑或设置包定义，这些定义仅包含几行（图 1）。对于每个支持的系统，你将使用 `Meson`、`Cmake`、`Autotools` 和 `Waf`。语言是原生处理的：对于 `Go` 使用 `Cargo`，`Rust` 使用，`Erl` 使用 `Rebar`，`Lua` 使用 `Luarocks`，`Perl` 使用 `MB` 或 `EUM`。`Python` 脚本可以通过 `Distutils`、`Setuptools`、`Peps517` 和 `Maturin` 轻松运行。

另一种方法是将你自己的定义与 Buildroot 的源码包混合。`@EXTERNAL` 机制非常简单，允许用户将自定义包定义添加到属于 Buildroot 的包定义中。此外，你还可以配置你的系统和其他文件，例如 `@EXTERNAL root`。这使得你所有的自定义内容都整洁地集中在一个地方。

有时，在 Buildroot 之外编译应用程序更加方便。在较大的项目中，你可能会发现某些开发者并不是每天都使用 Buildroot，如果你直接在开发环境中工作，那么从 IDE 中编译会更容易。该环境由 `Buildroot SDK` 提供，其中包含了编译工具链、所有配置好的库和主机环境（`hosts`）。毕竟，你需要其中一些内容来构建你的项目。它提供了库的选项，并能为 `Google protobuf` 定义生成代码。SDK 是一个 `tar` 包，你可以在任何地方解压。如果你在 SDK 的上下文中设置了 IDE，就可以直接从它进行编译和调试。

# 管理

一旦开发出操作系统，通常会有更新和新代产品随之而来。维护包含安全问题修复和新功能的更新发行版至关重要。Buildroot 自 2001 年以来一直存在，它是最古老的 IoT 工具构建工具之一，这使其成为一个经过验证的产品，而且项目的持续性无疑非常重要。自 2009 年以来，开发者必须保持每年四次的固定发布计划：`20XX.2`、`20XX.5`、`20XX.8` 和 `20XX.11`。每个发布版本都要经过为期月的稳定期，在此期间只接受修复；发布版本将维护三个月（错误修复和安全更新）。之后将发布一个新版本。`20XX.2` 版本是 `LTS`（长期支持版本），维护时间超过一年，并再次每月添加发布。

Buildroot 是社区驱动的，有 100 多人参与贡献，每个版本有 1500 处更改。社区通过邮件列表（`lists@buildroot.org`）或 `Open and Free Technology Community (OFT)` 上的 `IRC` 进行通信。随着时间的推移，开发者可以帮助解决问题并学习新知识。在议程中，社区通过公司决策讨论并决定争议性问题。背后没有额外的控制。然而，有一些公司和自由职业服务为 Buildroot 提供支持。

开发者可以在笔记本电脑上运行操作系统，并具备开发所需的所有功能。

开发者提供了工具帮助你维护 Buildroot。你可以使用 `pkg-help` 列出 Buildroot 中的包，并使用 `pkg-config` 收集包的信息，在网络上搜索新版本，检查漏洞（国家国家漏洞数据库和 `CVE` 报告），并以 `HTML` 和 `JSON` 格式提供结果。

进一步发展 —— 440 项测试。`2027` 年的 `SBC`、`Somtu` 和 `Qemu` 配置都是使用 Buildroot 构建的。最后，有 10 台生成任意配置的构建服务器。这些服务器的报告可以在线获取。

## 结论

Buildroot 多年来演变成了一个在嵌入式世界中成熟且经过验证的系统。Buildroot 使用了大量案例，从只有少量 `MB` 闪存的系统到用于云部署的 `Docker` 镜像，从带有图形栈或数据库的复杂系统。简单、灵活、可重现和维护性使 Buildroot 成为 IoT 系统的选择。通过 `Git` 仓库克隆 Buildroot 后，配置它需要一个月以上。回报是一个运行良好的产品。

## 信息

- [1] Buildroot: `https://buildroot.org/`
- [2] 构建手册: `https://manual.buildroot.org/manual.html`
- [3] `NIST` `CVE` 报告: `https://auto.buildroot.org/stats/master.html`
- [4] 构建服务器报告: `http://auto.buildroot.org`
- [5] Buildroot (`Git` 仓库): `https://git.buildroot.org/netbuildroot`

2022年10月

第 263 期

24

# 将你的想法变为现实！

这不是一本普通的电脑杂志！`MakerSpace` 专注于你可以利用它来构建自己的东西的技术。

如果你对电子产品感兴趣但还没有时间或技能（目前），学习这些创客项目可能是让你起步的最后动力。

这本特别刊将帮助你深入了解：

- `Raspberry Pi` (树莓派)
- `Arduino`
- 复古游戏
- 以及更多！

制作一台树莓派收音机！

`MakerSpace #02`

面向创客的实践项目

酷炫招式！

`Amiga 2.0`

在线购买：`shop.linuxnewmedia.com/specials`

# 评测

# 发行版漫游 – 红帽生态系统

# 红帽扩展家族

# 社区与企业的碰撞

红帽衍生出了基于企业和基于社区的发行版分支。以下是这些发行版如何关联的以及它们之间有何不同。

当 `Linux` 在 20 世纪 90 年代后期为人知时，红帽因其通常完整的文档和让 `Linux` 可用的努力成为顶级领先者之一，1999 年 8 月 11 日，红红帽首次上市。红帽作为 `IBM` 价值数十亿美元的子公司，创建了基于 `Linux` 的发行版测试并生成了红帽企业 `Linux (RHEL)` 产品。最近，由于红帽停止了 `CentOS`，`CentOS Linux` 和 `AlmaLinux` 从 `RHEL` 分叉出来。红帽创建了 `Fedora` 的衍生版，结果产生了一个类似于 `Debian` 的相互关联发行版生态系统，但重点关注创新以及网络和服务器。

# Fedora 项目

`Fedora` 项目 [1] 是原始红帽的替代者。红帽任命 `Fedora` 领导者并在 `Fedora` 委员会中拥有席位，但按照其原则运行，许多决定由社区或 `Fedora` 的技术工作组做出。

`Fedora` 作为 `RHEL` 的初始测试平台，每六月发布一次版本。在这个角色上，`Fedora` 引入了如 `DNF`、`PipeWire` 或 `Wayland` 等新技术，这些技术专门由红帽开发。有时，这些新技术需要几次发布才能在大多数情况下流畅运行，`Fedora` 仍然是学习技术的最佳发行版之一。

此外，`RHEL` [2] 是 `SUSE Linux Enterprise` 和 `Ubuntu` 的竞争对手。传统上，它是 `Fedora` 项目的下游，使用相同的包但对其进行测试并提供正式的长期支持，这一过程现在通过 `CentOS Stream` 公开可见。`RHEL` 发布是

# 测评

# 发行版之旅 – 红帽生态系统

## CentOS

`CentOS` 可能会吸引 `Rocky Linux` 及其衍生版（如 `AlmaLinux`）以及传统企业——尤其是现在关注 `Linux` 的企业——以及 `RHEL`，其在 2021 年增长了 17% [41]。

## CentOS Stream

`CentOS Stream` 使用旧的 `CentOS` 图标 [6] 并延续 `CentOS` 的版本命名方式，但这种名称的连续性具有误导性。`CentOS` 是 `RHEL` 的构建版本，而 `CentOS Stream` 是 `Fedora` 和 `RHEL` 之间的中间版本。另一方面，虽然 `CentOS` 是 `RHEL` 的下游，但 `CentOS Stream` 是上游。这意味着，如果 `CentOS` 的下一个版本是 9，它将不是基于仍然支持的 `CentOS 7` 的。`CentOS 8` 在开发停止后被放弃了。它的起点是 `RHEL`。`Fedora` 和 `OS Stream` 之间的关系显而易见，由于它们通常基于红帽的免费发行版，因此这两个发行版的版本号并不一致。

尽管 `RHEL` 在商业上取得了成功，但在自由软件社区中引发了反应。另一方面，`RHEL` 是 `Linux` 内核的主要贡献者。此外，它还贡献了许多进行中的项目，包括 `SELinux` [3]，并开发了包括 `PulseAudio`、`Flatpak` 和 `PipeWire` 在内的众多技术。它的活动在许多方面都很活跃——但并不符合自由软件的最佳传统。特别是 `RHEL` 要求订阅才能尝试或安装，这通常被视为许可的一个漏洞，而 `Fedora` 和 `CentOS stream` 的可用性两者共享相同的代码。然而，商业前景和

## CentOS

`CentOS` [5] 是 `RHEL` 的社区，吸引了那些倾向于不同开发目的的人。它是一个健壮的服务器项目。红帽在 2014 年收购了 `CentOS`，但让其独立运行直到 2021 年 12 月，当时他们宣布了 `CentOS` 开发启动和新的用途。`CentOS 7` 将持续维护到 2024 年 6 月 30 日，但许多用户已转向 `VMware`。

# 访问商店

在 `Linux New Media` 的在线商店发现过去，并投资新一年的 IT 解决方案。数字与纸质订阅

# 想要订阅吗？

寻找你之前在报刊亭真正看中的那个旧期杂志？

# 测评
