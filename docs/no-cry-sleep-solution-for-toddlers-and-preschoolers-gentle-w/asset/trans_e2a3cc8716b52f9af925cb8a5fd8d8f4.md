

## Red Hat 和 Fedora Linux

Red Hat Linux 目前是最流行的 Linux 发行版。作为一家公司，Red Hat 提供软件和服务，用于实施和支持专业和商业 Linux 系统。Red Hat 已将其 Linux 开发分为两条线：Red Hat Enterprise Linux 和 Fedora 项目。Red Hat Enterprise Linux 具有面向服务器和工作站的商业企业产品，每两年左右发布一次受控版本。Fedora 项目是一个开源计划，其 Fedora Core 版本平均每六个月发布一次，整合了 Linux 操作系统功能以及受支持应用程序的最新开发成果。Red Hat 根据 GNU 通用公共许可证自由分发其 Fedora 版本的 Linux；公司通过提供专业级支持、咨询服务和培训服务获得收入。Red Hat 认证工程师（RHCE）培训和认证计划旨在为维护和定制专业级 Red Hat 系统提供可靠且能力卓越的管理员和开发人员提供帮助。Red Hat 已与 Oracle、IBM、Dell 和 Sun 等主要公司建立了软件联盟。

目前，Red Hat 提供多种商业产品，称为 Red Hat Enterprise Linux。其中包括用于密集企业级任务的 Red Hat Enterprise Advanced Server；Red Hat Enterprise ES，这是一个专为小型企业和网络设计的 Linux 版本；以及 Red Hat Enterprise Work Station。Red Hat 还为其客户维护 Red Hat Network，可自动更新您系统上的操作系统和软件包。您也可以使用相同的 Red Hat Network 更新工具自动更新 Fedora Linux。专用产品包括 Stronghold 安全 Web 服务器、专为 IBM 和 Itanium 服务器定制的 Linux 版本，以及 GNUPro 开发工具。

Red Hat 还对开源 Linux 应用程序保持坚定的承诺。Red Hat 发明了 RPM 软件包系统，该系统被多个发行版使用，可自动安装和删除软件包。Red Hat 还为 GNOME 桌面提供了大部分软件开发工作，并且是 KDE 的坚定支持者。在 Red Hat 上，GNOME 和 KDE 被配置为外观相同，使用名为 Bluecurve 的标准化界面。

Red Hat 提供了一套广泛的配置工具，旨在管理添加用户、启动服务器、访问远程目录以及配置显示器或打印机等设备等任务。这些工具可在系统设置和服务器设置菜单和窗口中访问，也可通过其名称访问，所有名称均以“redhat-config”开头（请参阅第 4 章和第 5 章）。特别值得注意的是新的软件包管理工具，可让您轻松安装或删除软件包，并按可识别的类别排列。

> 注意 尽管 Red Hat 支持 GNOME 和 KDE 两种桌面界面，但 Bluecurve 界面为两个桌面提供相同的外观和感觉，将它们集成到一个视觉相似的界面中，菜单、窗口和面板看起来大致相同，尽管其底层功能不同（请参阅第 6 章和第 7 章）。

Red Hat 的新版本对关键应用程序进行了关键更新，并用新工具取代了旧工具。Red Hat 包含 GNOME 桌面、Apache Web 服务器、GNU 编译器集合（GCC）和 GNU Java 编译器（GJC）。新增了新的配置工具，包括用于管理软件的 redhat-config-packages 和用于配置显示硬件的 redhat-config-xfree86，并更新了其他工具，例如 redhat-config-networks，现在支持无线网络。Red Hat 现在同时安装 Postfix 和 Sendmail 邮件服务器，并允许您在两者之间无缝切换。

安装 Red Hat 已成为一个相当简单的过程，使用图形界面，每个步骤都显示详细的解释和建议。Red Hat 和 Fedora 发行版的安装方式可满足多种不同的用途，作为服务器、工作站和个人桌面。个人桌面选项安装预选软件（例如办公和多媒体应用程序）供家庭和个人使用。它具有精简的 GNOME 桌面界面。工作站选项安装桌面、办公、开发和<|message|>管理软件。服务器选项安装所有标准服务器，包括邮件和 FTP 服务器，以及默认配置和服务器管理工具。您还可以选择自定义安装，选择自己安装的软件组合。

Red Hat Fedora Linux 发行版可在众多 FTP 站点在线获取。Red Hat Fedora 在 fedora.redhat.com 维护自己的 FTP 站点，您可以在此下载 Fedora Linux 的整个当前版本，以及更新和第三方软件。Red Hat 从一开始就设计为可在众多硬件平台上运行。目前，Red Hat 支持 Sparc、Intel 和 Alpha 平台。有关更多信息，请访问 www.redhat.com，包括 Red Hat 手册、常见问题解答以及指向其他 Linux 站点的链接等大量文档。

如果您从 Red Hat 购买 Red Hat Linux，您有权获得在线支持服务。尽管 Linux 是免费的，但 Red Hat 作为一家公司专门从事支持服务，为客户提供其在开发解决方案方面的专业知识，以解决可能出现的问题，或使用 Linux 执行电子商务或数据库操作等多种可能的任务。

## Fedora 项目

Fedora 核心版本由一个名为 Fedora 项目的开源项目维护和开发。该版本完全由开源软件组成。开发工作由 Linux 开发人员贡献完成，让他们可以自由推广增强功能和新功能。该项目旨在像其他开源项目一样运作，发布速度与快速的在线开发进程保持一致。Fedora Core 版本的 Linux 完全免费。您可以从 fedora.redhat.com 下载最新版本，包括测试版。您可以使用 Red Hat 更新代理（RHN）更新 Fedora，以访问 Redhat Fedora Yum 仓库。更新可由多个 Yum Fedora 仓库中的任何一个支持，您可以在 /etc/sysconfig/rhn/sources 配置文件中配置 RHN 以访问这些仓库。Fedora 项目版本将取代最初的标准 Red Hat Linux 版本，该版本由入门级 Red Hat 版本组成。除了 Fedora Core 软件外，Fedora 项目还将提供流行的兼容软件包作为 Fedora Extras 和 Fedora Alternative Collections 的一部分。

## Red Hat Enterprise Linux

Red Hat Enterprise 产品线专为企业、研究和商业应用而设计。这些产品专注于可靠性和稳定性。它们的发布周期比 Fedora 项目版本受控得多。曾经的低成本消费版 Red Hat Linux 将被替换为面向消费者和小型企业的精简版商业企业版。Red Hat 提供三个企业版本——一个用于工作站，两个用于服务器。Red Hat Enterprise AS 提供了最高级别

