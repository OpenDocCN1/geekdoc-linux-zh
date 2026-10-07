
- 8. 回到浏览器，刷新 `http://IP`。你的网页显示正常了吗？

- 9. 在你的 Linux 虚拟机上，运行 `sestatus` 查看 SELinux 状态。SELinux 处于 `enforcing` 模式吗？

- 10. 使用 `setenforce 0` 将 SELinux 设为 `permissive` 模式，再次刷新网页。网页现在显示正常了吗？

- 11. 使用 `setenforce 1` 将 SELinux 恢复 `enforcing` 模式。

## 探索练习 14-9

**预计时间：** 40 分钟

**目标：** 探索 AppArmor。

**描述：** 查看你的 Ubuntu Linux 虚拟机上的默认 AppArmor 配置。注意强制执行的 AppArmor 配置文件及其设置。接下来，用一份短备忘录总结你在探索 AppArmor 和 SELinux 时发现的差异。

## 探索练习 14-10

**预计时间：** 40 分钟

**目标：** 将 Linux 与 Active Directory 集成。

**描述：** 如果你的网络包含你拥有用户账户的 Active Directory 域，将你的 Ubuntu Linux 系统加入该 Active Directory 域。你必须首先运行 `apt install sssd ssd-tools realm adcli` 来安装 sssd 和 realm 需要的包，并运行 `pam-auth-update --enable mkhomedid` 以确保为身份验证系统的 Active Directory 用户自动创建本地主目录。之后，你可以使用 `realm join domainname -v` 命令加入域。接下来，在网络上的 Windows 系统上，通过在文件资源管理器搜索框中输入 `\ubuntu` 来访问你的系统。注意，你的 Windows 用户可以使用该主目录共享并向其复制文件。然后，以相同的用户登录 Ubuntu Linux 虚拟机的终端，并查看你的主目录内容。最后，使用 `klist` 命令查看你的 Kerberos 票证信息。

## 附录 A

### 认证

随着技术的发展，管理技术所需的高素质人才也随之增加。公司面临的首要风险之一是聘用合格的人员管理、使用或开发 Linux 程序。为了降低这种风险，公司会寻找在技术领域表现出精通程度的人才。虽然这种精通程度可以通过实践经验来证明，但公司在招聘某些技术职位时，实践经验往往是不够的。认证测试具有技术能力的标准基准，并受到许多公司的青睐。认证测试根据技术认证类型而异，但它们通常涉及由授权的测试中心管理的计算机考试。全球每年获得数十万份计算机相关的认证证书，随着技术的发展，认证过程在未来可能会变得更加重要。

> 重要的是要认识到认证不能取代能力，它证明了能力。雇主可能会获得 30 名合格的申请者，招聘过程的一部分将是能力的展示。雇主不太可能花费成本和时间去测试所有 30 个人。相反，雇主更有可能寻找基准认证（这代表了基础能力），并对这个较小的子群体进行测试。

此外，认证是一项国际推崇和认可的标准。尽管雇主可能不熟悉在加拿大某特定大学或德克萨斯州某特定学院获得计算机科学学位的标准，但认证考试标准发布在网站上，并且是广为人知的。此外，在哪个国家参加认证考试并不重要，因为测试是标准化的，并由同一机构使用通用规则进行。

### 认证类型

认证分为两类：厂商特定认证和厂商中立认证。厂商特定认证是由特定操作系统或技术的供应商设定需要满足的标准并评阅考试的认证。获得其中一种认证证明了对某个特定产品或操作系统的了解。例如，微软、红帽和思科都为其产品提供了厂商特定的认证。厂商中立考试，例如由计算培训协会 `CompTIA` 和 Linux 专业协会 `LPI` 提供的考试，展示了在特定领域的知识，但不涉及任何特定产品或品牌。由于 Linux 是一种通用的操作系统类别，多个 Linux 发行版共享共同的内核和实用程序，因此厂商中立认证非常适合 Linux。虽然在某个发行版上认证可能表明具有迁移到另一个发行版并良好工作的能力，但最好展示大多数发行版共享的 Linux 最常用特性能。

无论认证考试是厂商特定的还是厂商中立的，创建这些考试的组织都会确保它们具有最高质量和完整性，以作为全球基准。行业使用的两种全球认可的厂商中立 Linux 认证别是 `CompTIA Linux+` 认证和 `LPI` 的 `LPIC-1：系统管理员认证`。本本书涵盖了这两种认证 2023 版本考试目标中列出的所有主题。

> 注意 2：在 2019 年之前，`CompTIA` 提供过一种名为 `Linux+`（由 `LPI` 提供支持）的认证，它与 `LPIC-1：系统管理员认证` 相同。然而，今天，`Linux+` 和 `LPIC-1：系统管理员` 是完全不同的认证。

### Linux+ 认证

`CompTIA Linux+` 由单场考试 `XK0-005` 组成。你可以在全球任何 `VUE` 或 `Prometric` 测试中心参加考试。考试由一系列多选题和模拟题组成。

> 注意 3：要了解更多关于 `Linux+` 认证考试的信息以及如何预约，请访问 `CompTIA` 网站：https://www.comptia.org/certifications/linux。

以下表格列出了认证考试主题在本书中的涵盖范围。每个表代表考试所衡量的一个独立领域或技能集。

## 1.0 系统管理

| 目标 | 章节 |
|---|---|
| 1.1 总结 Linux 基础知识 | 2, 4, 5, 6, 8, 11, 13 |
| 1.2 给定场景，管理文件和目录 | 3, 11, 12, 13 |
| 1.3 给定场景，使用适当工具配置和管理存储 | 5, 6 |
| 1.4 给定场景，配置并使用服务 | 8, 9 |
| 1.5 给定场景，使用网络工具 | 12 |
| 1.6 给定场景，构建并安装软件 | 11 |
| 1.7 给定场景，管理配置 | 6, 8, 11, 13 |

## 2.0 安全

| 目标 | 章节 |
|---|---|
| 2.1 总结 Linux 环境中的安全实践目的 | 1, 7 |
| 2.2 给定场景，实施身份管理 | 2, 7, 10 |
| 2.3 给定场景，配置防火墙 | |
| 2.4 给定场景，配置并执行远程连接 | 8, 12 |
| 2.5 给定场景，应用访问控制 | 4, 14 |

## 3.0 脚本、容器与自动化

| 目标 | 章节 |
|---|---|
| 3.1 给定场景，创建简单的自动化脚本 | 3, 7 |
| 3.2 给定场景，执行基础容器操作 | 13 |
| 3.3 给定场景，使用 Git 进行基础版本控制 | 7 |
| 3.4 总结常见的基础设施即代码技术 | 1, 7, 12 |
| 3.5 总结容器、云和编排概念 | 12, 13 |

## 4.0 故障排除

| 目标 | 章节 |
|---|---|
| 4.1 给定场景，分析并排除存储问题 | 5, 6, 8, 14 |
| 4.2 给定场景，分析并排除资源问题 | 12, 14 |
| 4.3 给定场景，分析并排除中央处理器 `CPU` 和内存问题 | 5, 6, 9, 14 |
| 4.4 给定场景，分析并排除用户访问和文件权限 | 4, 5, 10 |
| 4.5 给定场景，使用系统诊断并解决 Linux 系统的常见问题 | 8, 12 |

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

备注 4
要了解更多关于 `LPIC-1：系统管理员认证` 考试以及如何预约的信息，请访问 `LPI` 网站：https://www.lpi.org/our-certifications/lpic-1-overview。

下表列出了本书中涵盖认证主题的章节。每个表格代表一个考试所衡的领域或技能集。领域 101 至 104 将在 101-500 认证考试中进行测试，而领域 105 至 110 将在 102-500 认证考试中进行测试。

## 101 系统架构

| 目标 | 章节 |
| :--- | :--- |
| 101.1 确定并配置硬件设置 | 5, 6 |
| 101.2 启动系统 | 2, 5, 6, 8 |
| 101.3 更改运行级别/启动目标并关机或重启系统 | 2, 8 |

## 102 Linux 安装与包管理

| 目标 | 章节 |
| :--- | :--- |
| 102.1 设计磁盘布局 | 5 |
| 102.2 安装启动管理器 | 8 |
| 102.3 管理共享库 | 11 |
| 102.4 使用 Debian 包管理 | 11 |
| 102.5 使用 RPM 和 YUM 包管理 | 11 |
| 102.6 作为虚拟化访客的 Linux | 6, 12, 13 |

## 103 GNU 和 UNIX 命令

| 目标 | 章节 |
| :--- | :--- |
| 103.1 在命令行下工作 | 2, 3, 4, 7 |
| 103.2 使用过滤器处理文本流 | 3, 7, 11 |
| 103.3 执行基础文件管理 | 3, 4, 11 |
| 103.4 使用流、管道和重定向 | 7 |
| 103.5 创建、监控和杀死进程 | 2, 9, 14 |
| 103.6 修改进程执行优先级 | 9 |
| 103.7 使用正则表达式搜索文本文件 | 3, 7 |
| 103.8 基础文件编辑 | 3, 7 |

## 104 设备、Linux 文件系统、文件系统层级结构

| 目标 | 章节 |
| :--- | :--- |
| 104.1 创建分区和文件系统 | 5 |
| 104.2 维护文件系统的完整性 | 5, 6 |
| 104.3 控制文件系统的挂载和卸载 | 5, 8 |
| 104.4 管理磁盘配额 | 5 |
| 104.5 管理文件权限和所有权 | 4 |
| 104.6 创建和更改硬和符号链接 | 4 |
| 104.7 查找系统文件并将文件放置于正确位置 | 4 |

## 105 Shell、脚本编写与数据管理

| 目标 | 章节 |
| :--- | :--- |
| 105.1 自定义并使用 Shell 环境 | 7, 10 |
| 105.2 自定义或编写简单脚本 | 7, 9 |

## 106 用户界面与桌面

| 目标 | 章节 |
| :--- | :--- |
| 106.1 安装并配置 X11 | 8, 12 |
| 106.2 图形化桌面 | 8, 12 |
| 106.3 辅助功能 | 8 |

## 107 行政管理任务

| 目标 | 章节 |
| :--- | :--- |
| 107.1 管理用户和组账户及相关系统文件 | 10 |
| 107.2 通过调度作业自动化系统管理任务 | 9 |
| 107.3 本地化与国际化 | 10 |

## 108 核心系统服务

| 目标 | 章节 |
| :--- | :--- |
| 108.1 维护系统时间 | 8, 13 |
| 108.2 系统日志 | 10 |
| 108.3 邮件传输代理 `MTA` 基础 | 1, 13 |
| 108.4 管理打印机和打印 | 10 |

## 109 网络基础

| 目标 | 章节 |
| :--- | :--- |
| 109.1 互联网 协议基础 | 12 |
| 109.2 持久化网络配置 | 12 |
| 109.3 基础网络排排除 | 12 |
| 109.4 配置客户端 DNS | 12 |

## 110 安全

| 目标 | 章节 |
| :--- | :--- |
| 110.1 执行安全管理任务 | 2, 4, 5, 9, 10, 14 |
| 110.2 设置主机安全 | 8, 10, 14 |
| 110.3 使用加密保护数据 | 12, 14 |

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

## 附录 B

### 搜索引擎

为了优化搜索结果，你可以使用各种运算符。例如，使用减号 `-` 可以从结果中排除特定单词。使用双引号 `" "` 将搜索精确短语。星号 `*` 可以作为通配符匹配任何字符序列。你还可以使用 `site:` 操作符将搜索限制在特定网站，或使用 `filetype:` 操作符搜索特定文件类型。

### 有用的互联网资源

有数百个网站致力于 Linux。许多网站提供了 Linux 命令的特定帮助、Linux 相关文档或按主题组织的论坛。表 B-1 列出了你可能觉得有用的网站。

`YouTube` 频道也是 Linux 资源的优质来源，它们提供了 Linux 配置演示以及易于理解的 Linux 相关评论。表 B-2 列出了相关的 `YouTube` 频道。

网站和 `YouTube` 视频会在社交媒体上分享。因此，在社交媒体上关注 Linux 相关账号是获取最新动态的一种简单方法。表 B-3 列出了你可以关注的一些 `Twitter` 账号。

#### 表 B-1 有用的 Linux 相关网站

| 网站 | 标题 | 描述 |
| :--- | :--- | :--- |
| opensource.com | The Open Organization | 按主题维护 Linux 资源链接。你可以选择输入电子邮件以接收社区内的最新 Linux 文章摘要。 |
| commandlinefu.com | Command Line | 用户提交的 Linux 命令和命令行技巧 |
| crab.org | Contab Guru | 允许你解释并创建用于 Linux 或 Unix cron 的调度格式 |
| explainshell.com | Explain Shell Commands | 你可以在该网站上输入任何 Linux 命令，并获得关于该命令功能的简单描述 |
| fullcirccmagazine.org | Full Circle Magazine | 一本在线杂志，包含许多专注于 Ubuntu 系列 Linux 发行版的易读文章。 |
| toforge.com | HowTo | 该网站包含许多针对多种 Linux 发行版广泛主题的用户提交的易读 Linux 教程，同时也包含一个用于帮助和 Linux 相关讨论的论坛。 |

## 附录 B 在互联网上寻找 Linux 资源 647

| 网站 | 标题 | 描述 |
| :--- | :--- | :--- |
| kernelnewbies.org/LinuxChanges | Kernel Newbies | 该网站以易读的形式解释了可用的 Linux 内核以及最新的内核特性。 |
| linuxjournal.com | Linux Journal | 一本致力于 Linux 相关新闻的在线杂志，拥有许多操作指南、博客、软件评测、提示和技巧。 |
| lxer.com | Linux News | 提供 Linux 和开源社区内最新新闻的列表。 |
| linuxpromag.com | Linux Pro Magazine | 包含大量 Linux 和开源文章及论文，并按系统管理主题（例如：网络、管理、安全、桌面）进行分类。 |
| linuxquestions.org | Linux Questions | 这是一个在线论坛，用户、管理员和开发者可以在这里就 Linux 主题提问。这里还托管了多个 Linux 教程和文章。 |
| linuxsurvival.com | Linux Survival | 这是一个为几乎没有 Linux 操作系统经验的人士提供的免费目录。它涵盖了关键命令的使用，这些命令可以帮助用户快速开始使用 Linux。 |
| linux.com | Linux | 除了寻找 Linux 相关博客和论坛外，该网站还包含热门资源的目录，包括书籍、视频、软件、发行版和社区。 |
| linux.org | Org | 该网站为许多 Linux 发行版提供了广泛 Linux 资源（教程、文档、链接）。此外，它还托管了许多主题的论坛、指南以及面向 Linux 用户和管理员的信息。 |
| phoronix.com | Phoronix | 提供硬件相关的新闻和资源，包括按硬件分类的评论和 Linux 基准测试。 |
| sourceforge.net | Source Forge | 这是一个用于开源软件的在线软件和代码库。可以通过搜索可用目录从 Source Forge 获取各种软件。 |
| shellcheck.net | Shell Check | 该网站会自动发现你粘贴的 shell 脚本中的 bug。 |
| ss64.com/bash | SS64 BASH 参考 | 该网站为各种系统和编程环境中的命令提供了易搜索的参考。 |
| teknix.com | Technix | 包含广泛的 Linux 使用和管理教程。 |
| fsf.org | The Free Foundation | 自由软件基金会的网站包含了有关自由软件运动和许可的信息，还包含指向价值的 Linux 和开源资源及网站的链接。 |

## 表-2 有用的 Linux 相关 YouTube 频道

| YouTube 频道名称 | 描述 |
| :--- | :--- |
| Ubuntu | 提供与基于 Ubuntu 的 Linux 发行版相关的各种主题和教程 |
| Network Chuck | 探索广泛的技术主题，包括许多以 Linux 为中心的主题 |
| Nixie Pixel | 涵盖安全、Linux、Android 和 IOS 等领域的广泛主题，以及各种 Linux 主题和教程 |
| The Linux Experiment | 评测 Linux 相关的新闻、教程、应用亮点以及面向新 Linux 的观点 |
| The Linux Foundation | 讨论 Linux 操作的开发和特性相关信息，包括新特性 |
| The Urban Penguin | 包含各种不同 Linux 发行版和 Unix 变体的教程，侧重于认证培训 |

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

### 表 B-3 有用的 Linux 相关 Twitter 账号

| Twitter 账号 | 名称 |
| :--- | :--- |
| @omubuntu | omg! ubuntu! |
| @linuxfoundation | The Linux Foundation |
| @Linux4everyone | Linux For Everyone |
| @itsfoss2 | It's FOSS - Linux Portal |
| @fedora | The Fedora Project |
| @ubuntu | The Ubuntu Linux Distribution |
| @AskUbuntu | The Stack Exchange Network |
| @linux_pro | Linux Pro Magazine |
| @LinuxVoice | Linux Voice Magazine |
| @fullcirclemag | Full Circle Magazine |

## 附录 C

## 将你的 Linux 知识应用于 macOS

回想第 1 章的内容，Linux 是 UNIX 操作系统的开源演进版本。因此，我们在书中讨论的大多数概念、命令和文件同样适用于 UNIX 操作系统，包括 macOS 和 FreeBSD（在附录 D 中讨论）。

与通常用于从嵌入式硬件系统到云服务器等各种不同系统的 Unix 不同，macOS 主要作为终端用户操作系统使用，并专为 Apple 计算机授权。macOS 的大部分由一个名为 Darwin 的 NEXTSTEP 操作系统的开源版本组成。Darwin 使用一个基于 NEXTSTEP MACH 和 BSD 的内核称为 XNU。Apple 将 XNU（代表“X is Not UNIX”）结合了一起。macOS Ventura 是写作时最新的 macOS 版本；它支持带有 Intel 或 Apple Silicon `ARM64` 处理器的 Apple 计算机。

由于许多组织购买 macOS 系统，许多 Linux 管理员在组织内部支持 macOS。本附录概述了 Linux 和 macOS 系统管理之间的相似之处和主要区别。

## macOS 文件系统

虽然早期版本的 macOS 使用分级文件系统 `HFS+`，但最近版本的 macOS 使用的默认文件系统是苹果文件 `APFS`。`HFS+` 和 `APFS` 与任何其他 Linux 或 UNIX 系统具有相同的功能和约定。文件名可达 255 个字符，可以包含大写字母、小写字母、数字、下划线 `_` 和连字符 `-`。隐藏文件以点 `.` 开头，每个目录包含指向当前目录 `.` 和父目录 `..` 的引用。

由于 macOS 支持文件系统层次结构 `FHS`，它与 Linux 使用相同的目录结构。然而，macOS 增加了其他几个以大写字母开头的目录来存储密钥和用户文件。

### 表 C-1  macOS 目录

| 目录 | 描述 |
| :--- | :--- |
| /Applications | 存储应用程序 |
| /bin | 包含二进制可执行文件 |
| /etc | 包含大多数系统配置（指向 /private/） |
| /Library | 包含应用程序库、设置和文档 |
| /opt | 包含第三方可执行文件和文档 |
| /private | 包含系统相关文件 |
| /sbin | 包含超级用户 `root` 可执行文件 |
| /System | 包含组成系统组件的文件 |
| /tmp | 包含应用程序使用的临时文件（指向 /private/） |
| /Users | 常规用户目录的默认位置 |
| /usr | 存储大多数可执行文件和文档 |
| /var | 包含日志文件和输出目录（指向 /private/） |
| /Volumes | 包含用于挂载设备的子目录 |

在图形桌面中，只有 `/Applications`、`/Library`、`/System` 和 `/Users` 文件夹是隐藏的。所有其他目录都可以使用命令行显示。

## 使用 macOS 桌面

如图 C-1 所示，macOS 桌面与 GNOME 桌面非常相似。底部的启动器是 Dock，相当于 GNOME 桌面中的收藏启动器。图 C-1 所示 Dock 最左侧的图标打开 Finder 应用程序，该程序用于浏览系统上的文件和目录。图 C-1 所示 Dock 中的齿轮图标打开系统偏好应用程序，该程序用于配置 macOS 操作系统的各个方面。macOS 桌面顶部栏的左半包含控制前内容的菜单，而右半包含状态图标和执行连接 Wi-Fi 网络等常见任务的菜单。通过选择菜单最左侧的 Apple 图标，你可以更新软件、强制停止运行的应用程序，以及关机或重启系统。

# 在 macOS 中使用 Z Shell

与 Linux 不同，macOS 不支持桌面环境之外的本地终端。然而，你可以打开 Finder 应用程序并导航到 `/Applications/Utilities/Terminal`，以启动终端应用程序，该程序允许你与 shell 交互。当你的终端应用程序被放置在你的主目录（`/Users/username`）中时，它包含一组你用于存储用户内容的子文件夹，如图 C-2 所示。

# 图 C-2 终端应用程序

![](img/0065b92b6d2dfbf8ba2a41373880797d_666_0.png)

> 虽然 shell 在现代 macOS 系统上是默认的，但你可以使用 `bash - /bin/bash` 命令将你的 shell 更改为 BASH。

如果你想以 root 用户身份进行系统管理，必须先使用 `disableroot` 命令启用 root 用户。

你在 Linux 上使用过的所有功能都适用于 macOS，包括大小写敏感、元字符、重定向、管道、引号、环境变量和 shell 脚本。同样，Tab 键可以扩展命令和文件路径，而 Ctrl+c 可以用于转到队列中的命令。

你所熟悉的许多 Linux 命令及相关选项在 macOS 上的工作方式相同。表 C-2 列出了书中讨论的可以在 macOS 的 BASH shell 中使用的命令。对于未在表 C-2 中列出的 Linux 命令，有独立的命令或过程在 macOS 内部提供相同的功能。表 C-3 列出了有用的 macOS 特有命令。

# CompTIA Linux+ 和 LPC-1：Linux 认证指南

# 表 C-2 macOS 中用的 Linux 命令

| 类别 | 命令 |
| --- | --- |
| 系统文档 | man, apropos, info, help |
| 文件管理 | pwd, cd, ls, locate, which, find, where, type, cp, mv, rm, unlinking, renice, mkdir, id, newgrep, touch, chown, chmod, umask |
| 文本工具 | cat, less, head, tail, pair, uniq, cut, paste, tr, split, nl, sort, wc, diff, grep, egrep, vi (vim), emacs |
| 文件系统管理 | mount, umount, fsck, df, du, quota, quotan, quotaoff, edquota, quota, quotatack |
| 压缩与软件 | gzip, unzip, zcat, zgrep, zmore, split, compress, bzip2, bczat, zgrep, bzip, tar, cpio, dd, make, gcc |
| BASH 管理与脚本 | set, unset, env, alias, ualiases, tee, xargs, printenv, history, export, source, git |
| 进程管理 | ps, top, kill, killall, fg, bg, nice, renice, at, atm, crontab, pkill, nohup, lsof |
| 用户与组管理 | we, whoami, groups, id, newgrp, chfn, chsh, passwd |
| 打印 | lp, lstat, indent, cancel, lpr, lpm, capset, cupspresject, cuspidable |
| 网络与安全 | ifconfig, ping, which, arp, netstat, route, traceroute, trace6, hostname, nslookup, id, su, sudo, last, rsync, scpy, ftp, curl, ssh, ssh-keygen, ssh-agent, ssh-copy, id, apachectl, mailig, newailases, showmount, brt, kill, tcpdump |
| 系统与杂项 | shut-down, halt, reboot, cal, exit, echo, clear, reset, uname, uptime, chmod, chrt, dmesg, iconv, logger, sysctl, screen |

# 表 C-3 有用的 macOS 特有命令

| 命令 | 说明 |
| --- | --- |
| asr | 这是系统工具恢复（System Utility Restore）。它用于从磁盘镜像恢复系统 |
| bless | 设置卷的可启动性和和启动磁盘选项 |
| caffeinate | 防止系统休眠 |
| flags | 这修改文件的属性（例如，不可变）。它等同于 Linux 中的 chmod 命令 |
| defaults | 设置 macOS 系统偏好，带有显示隐藏字段的选项 |
| diskutil | 创建、格式化和修复文件系统 |
| ditto | 复制文件和文件夹 |
| drutil | 与 CD/DVD 设备交互 |
| dsacheutil | 显示或清除 DNS 缓存 |
| dseditgroup | 编辑、操作或删除组 |
| dsableroot | 启用 root 用户 |
| dscl | 这是目录服务命令。它用于管理系统上的用户和组 |

# 附录 C 将 Linux 知识应用于 macOS

| 命令 | 说明 |
|---|---|
| fdesup | 配置 FileVault（Apple 等同于 LUKS 的磁盘加密） |
| hdiutil | 创建并管理 ISO/DMG 磁盘镜像 |
| kextfind | 这列出内核扩展，等同于 Linux 系统上的 lmod。 |
| kextload | 这加载内核扩展，等同于 Linux 系统上的 modprobe。 |
| kextstat | 显示系统内核扩展的状态 |
| kextunload | 这卸载内核扩展，等同于 Linux 系统上的 rmod。 |
| launchctl | 用于加载或卸载守护进程/代理。功能上等同于 Linux 系统上的 systemctl。 |
| networksetup | 配置网络接口设置，包括 IP 信息和无线设置 |
| newfs_type | 这在由类型识别的分区上创建文件系统，类型可以是 bfs, hfs, udfs 或 extfs。它等同于 Linux 系统上的 mkfs。 |
| nvram | 显示并修改启动参数 |
| open | 执行函数二进制文件 |
| pkgutil | 查询并管理已安装的 macOS 应用程序 |
| plutil | 检查 .plist 文件的状态，并将 .plist 转换为其他格式 |
| pmset | 配置电源选项 |
| say | 使用内置系统声音朗读参数 |
| screencapture | 截图并将其保存到参数指定的文件 |
| scselect | 在网络位置之间切换 |
| scutil | 创建并管理网络位置 |
| softwareupdate | 更新系统软件包 |
| security | 配置证书和密码存储（钥匙串）设置 |
| spctl | 显示并配置用于 ...Assessment 的内核安全参数（macOS 等同于 SELinux） |
| sw_vers | 显示操作系统版本 |
| system_profiler | 显示系统信息 |
| syset vm_stat | 显示内存和统计数据 |

# 管理 macOS

要在 macOS 上管理用户，你可以使用 `dscl` 命令。这是目录服务命令，用于管理系统上的用户和组。要启用 root 用户，使用 `dsableroot` 命令。要编辑、操作或删除组，使用 `dseditgroup`。要显示或清除 DNS 缓存，使用 `dsacheutil`。要与 CD/DVD 设备交互，使用 `drutil`。要复制文件和文件夹，使用 `ditto`。要创建、格式化和修复文件系统，使用 `diskutil`。要设置 macOS 系统偏好（带有显示隐藏字段的选项），使用 `defaults`。要修改文件的属性（例如，不可变），使用 `flags`。这等同于 Linux 中的 chmod 命令。要防止系统休眠，使用 `caffeinate`。设置卷的可启动性和启动磁盘选项，使用 `bless`。从磁盘镜像恢复系统，使用 `asr`。

# 文件系统管理

你在 Linux 上使用的所有功能都适用于 macOS，包括大小写敏感、元字符、重定向、管道、引号、环境变量和 shell 脚本。同样，Tab 键可以扩展命令和文件路径，而 Ctrl+c 可以用于转到队列中的命令。

macOS 原生启用配额，但 macOS 不使用 `/etc/fstab` 文件在启动时指定挂载选项。相反，你必须在每个启用的文件系统的挂载点目录中创建 `quota.opts` 和 `user.quota.opts` 文件。对于这些，可以使用与 Linux 相同的命令来配置和管理配额。

> > 注意 3：如果你不小心更改了 macOS 系统文件的权限，系统会在屏幕上报告错误。在磁盘工具中检查错误将恢复这些文件的默认权限。

# 理解 macOS 应用程序

当你在 Linux 系统上使用包管理器安装应用程序时，组成应用程序的文件分布在各个目录，例如 `/etc`, `/bin`, `/opt`, `/usr` 和 var。包管理器存储这些位置，以便以后可以快速删除。

在 macOS 中，所有的二进制执行文件、支持文件、配置信息和其他相关信息都存储在一个具有 `.app` 扩展名的目录中。在 macOS Finder 中查看时，这些显示为图标（没有 `.app` 扩展名），执行它们即可运行应用程序。要从 BASH shell 中执行应用程序，可以使用 `open` 命令加上路径。例如，要打开 Firefox 浏览器，你可以运行 `/Applications/Firefox.app`。

要在 macOS 桌面内删除应用程序，可以将应用程序图标拖到 Dock 栏中的垃圾桶。要在 shell 中删除应用程序，可以跟踪路径到该项目并使用 `rm` 命令。

# 附录 C 将 Linux 知识应用于 macOS

macOS 应用的配置信息和设置存储在与相关包一起的具有 `.plist` 扩展名的 XML 文件中。在互联网上搜索与 macOS 或 macOS 相关问题的解决方案时，解决方案通常涉及修改应用程序内部的 `.plist` 文件。

与 Linux 应用一样，许多 macOS 应用依赖于共享库。然而，许多 macOS 共享库依赖于框架（framework），并存储在 `/System/Library/Frameworks` 目录下具有 `.framework` 扩展名的包文件中。

你也可以在 macOS 上使用 `make` 命令从源代码编译应用，大多数应用程序是通过在线仓库安装的。你可以通过启动应用程序从该仓库搜索并安装应用。你也可以通过选择 macOS 桌面苹果图标上的“App”来启动 App Store。

或者，许多开发者会在他们的网站上提供 macOS 应用的下载。当你从网站获取 macOS 应用时，一个具有 `.dmg` 扩展名的 ISO 镜像会被下载到家目录下的 Downloads 文件夹中。当你打开 `.dmg` 文件时，ISO 会被挂载，并在桌面上创建一个快捷方式。然后你可以打开此快捷方式，并将应用程序包拖到 `/Applications` 文件夹进行安装。

你还可以在 macOS 上安装任何开源代码。然而，要做到这一点，你必须使用 Apple 的 Xcode 工具编译源码。或者，你可以按照 brew.sh 上的说明在 macOS 系统上安装 Homebrew 包管理器。安装 Homebrew 后，你可以从 Z shell 运行 `brew install` 命令从网络源仓库编译并安装开源程序，或者运行 `brew uninstall` 命令删除通过 Homebrew 安装的程序。

## macOS 设备

在 Linux 系统上，许多专用硬件设备（如网络接口和视频卡）在 `/lib/modules` 目录下拥有设备驱动程序，这些驱动程序在启动时加载到 Linux 内内核。在 macOS 系统上，专用硬件的设备驱动程序被称为内核扩展（kernel extensions），它们从 `/System/Library/Extensions` 中的 `.kext` 文件加载到 XNU 内核中。

要查看当前的内核扩展，你可以使用 `kext` 命令。同样，可以使用 `kextload` 命令来激活和禁用扩展。你还可以使用图形化的“系统信息”工具（/Applications/System Information）查看已加载的内核扩展。

## macOS 系统初始化

基于 Intel 的苹果电脑使用 UEFI BIOS 来控制 macOS 启动加载程序的加载，而基于芯片的电脑则直接加载 macOS 启动加载程序。从不同的存储设备，你可以在启动期间按住键盘上的 Option 键（非苹果键盘上的 Alt 键），并在提示时选择相应的设备。

你还可以在启动期间按住苹果键盘上的 Command-V 键（非苹果键盘上的 Windows-V）来查看有关启动过程的详细信息，并与 macOS 启动本身进行交互。

启动加载程序从 `/System/Library/Kernels/kernel` 文件加载 XNU。然后 XNU 加载 Launch Daemon（`/sbin/launchd`），其功能等同于现代 Linux 系统上的系统守护。Launch Daemon 加载所有其他系统守护到 `/Library/Agents/LaunchDaemons` 以及 `/System/Library/StartupDirectories` 中的任何可选路径，从而将系统带入稳定状态。你可以在系统启动后使用 `launchctl` 命令启动、停止和监控守护。你可以以 root 用户运行 `launchctl list` 命令来查看守护的状态。

在系统启动期间按住 Command+S 键会指示 launch 进入单用户模式，你可以在该模式下修复系统。或者，你可以在启动期间按住 Command+R 键来启动 macOS 恢复工具，它可以用于修复或重新安装操作系统。

## macOS 安装与更新

虽然电脑预装了 macOS，但如果操作系统损坏，你可能需要重新安装 macOS。重新安装 macOS 最简单的方法是使用前面讨论过的 macOS 恢复工具。恢复工具允许你从 App Store 下载并重新安装 macOS，这需要网络连接。或者，你可以插入包含 macOS 安装文件的 USB 介质，在按住 Option 键的同时启动电脑，并选择 USB 开始安装。

无论你选择如何开始安装，安装程序都允许你执行不同类型的安装。清洁安装会删除文件系统和所有数据。然而，你可以选择重新安装操作系统，同时保留系统、应用程序和用户文件。你还可以选择将当前系统移动到 /Previous OS disk 并安装新的操作系统，保留应用程序和用户文件。

安装完成后，你可以使用前面讨论过的 App Store 或 `softwareupdate` 命令获取 macOS 更新。要查看成功安装的 macOS 更新，你可以使用 `softwareupdate --history` 命令，或查看 `/Library/Receipts` 目录的内容。

## 日志文件管理

与 Linux 类似，macOS 系统在 `/var/log` 目录下记录事件。例如varvar/log/install 包含安装事件，而var/log/system 记录内核事件。你可以使用 shell 中的文本工具、Console 应用程序（/Applications/Utilities/Console，包含关键系统日志文件的快捷方式）来查看这些许多日志文件。你可以使用 Console 应用程序按严重程度对日志进行排序，并在网上研究应用程序崩溃等解决方案。

## 管理 macOS 进程

虽然你使用相同的进程管理命令来管理 macOS 进程，但图形化的“活动监视器”更容易管理进程（/Applications/Utilities/Activity Monitor）。活动监视器根据系统活动和使用对进程进行排序，并在活动监视器中显示系统信息或问题进程。如果你遇到阻止你打开活动监视器的流氓应用程序，可以使用 Command-Shift-Option-Esc 键组合来杀死前台应用程序，或者在 Dock 中右键点击相关的应用程序图标并选择“强制退出”。

## 网络与网络服务配置

网络接口在 macOS 中使用一种命名规范。第一个以太网接口也称为 en0。

要在 macOS 中配置网络服务，你可以使用系统设置应用程序中的“共享”部分，如图 C-3 所示。你选择的每个服务都会配置 macOS 上特定的网络服务。屏幕共享使用 VNC 服务器，文件共享 Samba，使用 CUPS 的打印机共享，远程登录则配置 SSH 守护进程。

## 附录 D

## 将你的 Linux 知识 FreeBSD

与 macOS（在附录 C 中讨论过）一样，将 Linux 概念应用于 FreeBSD UNIX 操作系统并不困难。FreeBSD 是仅次于 macOS 的最流行的 Unix 系统，完全使用宽松的 BSD 开源许可证开发。本文写作时 FreeBSD 的最新版本为 13.1，并支持多种架构（Intel x86、ARM/ARM64、RISC-V 和 PowerPC）。你可以将 FreeBSD 配置为带有 X Windows 的工作站，并配备 GNOME 或 KDE 等桌面环境；由于 FreeBSD 的网络性能优于 Linux，它经常被那些提供跨互联网大规模数据服务的组织使用，例如 Netflix。

与 Unix 和 macOS一样，FreeBSD 使用文件系统层级标准 `FHS` 并使用相同的标准目录结构。然而，FreeBSD 使用 `/usr` 下的家目录而不是 `/home`。在默认情况下，普通用户使用简化的 BASH shell (`/bin/bash`)，而 root 用户使用 C shell (`/bin/sh`)。你可以在 FreeBSD 上安装和配置你熟悉的网络服务（例如 Apache、PostgreSQL、Samba、NFS、NTP、DHCP、DNS 和 SSH），以及许多相同的命令（例如 chmod、find、which、ps、nice、reboot、poweroff 和 ifconfig）。

## 安装 FreeBSD

与 Linux 类似，你可以通过包含 FreeBSD 安装介质的 CD 或 USB 驱动启动来开始裸 FreeBSD 安装，或者通过从 FreeBSD ISO 镜像启动开始 FreeBSD 虚拟安装。要获取安装 FreeBSD ISO 镜像以及如何将其写入 CD 或 USB 驱动的说明，请访问 freebsd.org。

## 系统配置

几乎所有的系统配置，包括系统主机、网络接口配置以及开机时启动的守护进程（服务），都存储在一个名为 `/etc/rc.conf` 的单个文件中。该文件中的行采用“参数-值”语法，可以使用文本编辑器或通过 `sysrc` 命令进行编辑（例如 `sysrc parameter=value`）。你也可以使用 `sysrc` 命令查看来自 `/etc/rc.conf` 的所有参数及其值。

FreeBSD 配置文件的参数存储在 `/etc/defaults` 目录下的文本文件中。例如，`/etc/rc.conf` 存储了系统配置参数，这些参数可以通过 `/etc/rc.conf` 中定义的相同参数进行覆盖；而 `/boot/loaders` 存储了引导加载程序配置参数，这些参数可以通过 `/boot/loader` 中的条目进行覆盖。需要系统默认值的软件包会在 `/etc/rc.conf.d` 目录下放置一个包含所需参数的文本文件。

## 内核配置

与 Linux 类似，FreeBSD 使用内核模块提供额外的功能和硬件支持。这些模块具有 `.ko` 扩展，并存储在 `/boot/kernel` 目录下。你可以使用 `kldstat` 命令插入模块，或使用 `kldunload` 命令移除模块。例如，你可以使用 `kldload` 命令将 Linux 文件系统模块加载到内核中。为了让这些模块在每次启动时自动加载，你可以将 `kldload /boot/kernel/lin_profs.ko` 行添加到 `/boot/loader.conf` 中。FreeBSD 内核还可以在启动期间查看和配置的属性和参数。要查看当前配置的所有内核参数，可以使用 `sysctl` 命令。例如，`sysctl kern.securelevel` 显示内核安全级别参数的值；而 `sysctl kern.securelevel=2` 则将其配置为 2（高安全性）。你还可以运行 `sysctl -a` 查看所有参数及其默认值。为了确保特定参数在启动时已配置，你可以修改或向 `/etc/sysctl.conf` 添加适当的行。

## 系统初始化

FreeBSD 具有交互式启动菜单，如图 D-1 所示。FreeBSD 启动会显示 10 秒菜单，允许你正常启动系统（多用户模式）、进入单用户模式进行系统维护或使用不同的内核或启动选项启动系统。

图 D-1 FreeBSD 引导程序

启动 FreeBSD 内核后，init 守护进程执行 `/etc/rc` 脚本，该脚本通过执行 `/etc/rc` 目录下的相应守护进程脚本，启动 `/etc/rc.conf` 中列出的其他守护进程。`/etc/rc` 脚本还会运行其他系统初始化，包括使用 `/etc/rc.conf` 指定参数连接网络接口的 `/etc/netstart`。要查看系统初始化期间 FreeBSD 内核检测到的硬件和加载的模块，可以查看 `/var/run/dmesg` 日志。或者，要查看由 init 启动的守护进程和组件（包括相关错误），可以查看 `/var/log/messages` 文件。

## 存储配置

如表 D-1 所示，FreeBSD 使用与 Linux不同的设备文件来标识存储设备。对于物理存储设备，你可以使用 `geom` 命令。例如，运行 `geom disk show` 可以显示系统中可用设备列表。

表 D-1 常见 FreeBSD 存储设备文件

| 设备文件 | 描述 |
| :--- | :--- |
| /dev/ada0 | 第一个 SATA 驱动 |
| /dev/ada1 | 第二个 SATA 驱动 |
| /dev/da0 | 第一个 SCSI 驱动 |
| /dev/da1 | 第二个 SCSI 驱动 |
| /dev/md0 | 第一个虚拟磁盘 |
| /dev/s0 | 第一个 IDE 驱动 |
| /dev/nvme0 | 第一个 NVMe 驱动 |
| /dev/nvme0n1 | NVMe 0 上的第一个分区 |
| /dev/nvme0n2 | NVMe 0 上的第二个分区 |

表 D-2 示例 FreeBSD 分区

| 文件 | 描述 |
| :--- | :--- |
| /dev/ada0s1 | 根分区 |
| /dev/ada0s2 | 交换分区 |
| /dev/ada0s3 | 家目录分区
| /dev/nvme0n1 | 根分区 |
| /dev/nvme0n2 | 交换分区 |

## 附录 D 将你的 Linux 知识

与 macOS（在附录 C 中讨论过）一样，将 Linux 概念应用于 FreeBSD UNIX 操作系统并不困难。FreeBSD 是仅次于 macOS 的最流行的 Unix 系统，完全使用宽松的 BSD 开源许可证开发。本文写作时 FreeBSD 的最新版本为 13.1，并支持多种架构（Intel x86、ARM/ARM64、RISC-V 和 PowerPC）。你可以将 FreeBSD 配置为带有 X Windows 的工作站，并配备 GNOME 或 KDE 等桌面环境；由于 FreeBSD 的网络性能优于 Linux，它经常被那些提供跨互联网大规模数据服务的组织使用，例如 Netflix。

与 Unix 和 macOS一样，FreeBSD 使用文件系统层级标准 `FHS` 并使用相同的标准目录结构。然而，FreeBSD 使用 `/usr` 下的家目录而不是 `/home`。在默认情况下，普通用户使用简化的 BASH shell (`/bin/bash`)，而 root 用户使用 C shell (`/bin/sh`)。你可以在 FreeBSD 上安装和配置你熟悉的网络服务（例如 Apache、PostgreSQL、Samba、NFS、NTP、DHCP、DNS 和 SSH），以及许多相同的命令（例如 chmod、find、which、ps、nice、reboot、poweroff 和 ifconfig）。

## 安装 FreeBSD

与 Linux 类似，你可以通过包含 FreeBSD 安装介质的 CD 或 USB 驱动启动来开始裸 FreeBSD 安装，或者通过从 FreeBSD ISO 镜像启动开始 FreeBSD 虚拟安装。要获取安装 FreeBSD ISO 镜像以及如何将其写入 CD 或 USB 驱动的说明，请访问 freebsd.org。

## 系统配置

几乎所有的系统配置，包括系统主机、网络接口配置以及开机时启动的守护进程（服务），都存储在一个名为 `/etc/rc.conf` 的单个文件中。该文件中的行采用“参数-值”语法，可以使用文本编辑器或通过 `sysrc` 命令进行编辑（例如 `sysrc parameter=value`）。你也可以使用 `sysrc` 命令查看来自 `/etc/rc.conf` 的所有参数及其值。

FreeBSD 配置文件的参数存储在 `/etc/defaults` 目录下的文本文件中。例如，`/etc/rc.conf` 存储了系统配置参数，这些参数可以通过 `/etc/rc.conf` 中定义的相同参数进行覆盖；而 `/boot/loaders` 存储了引导加载程序配置参数，这些参数可以通过 `/boot/loader` 中的条目进行覆盖。需要系统默认值的软件包会在 `/etc/rc.conf.d` 目录下放置一个包含所需参数的文本文件。

## 内核配置

与 Linux 类似，FreeBSD 使用内核模块提供额外的功能和硬件支持。这些模块具有 `.ko` 扩展，并存储在 `/boot/kernel` 目录下。你可以使用 `kldstat` 命令插入模块，或使用 `kldunload` 命令移除模块。例如，你可以使用 `kldload` 命令将 Linux 文件系统模块加载到内核中。为了让这些模块在每次启动时自动加载，你可以将 `kldload /boot/kernel/lin_profs.ko` 行添加到 `/boot/loader.conf` 中。FreeBSD 内核还可以在启动期间查看和配置的属性和参数。要查看当前配置的所有内核参数，可以使用 `sysctl` 命令。例如，`sysctl kern.securelevel` 显示内核安全级别参数的值；而 `sysctl kern.securelevel=2` 则将其配置为 2（高安全性）。你还可以运行 `sysctl -a` 查看所有参数及其默认值。为了确保特定参数在启动时已配置，你可以修改或向 `/etc/sysctl.conf` 添加适当的行。

## 系统初始化

FreeBSD 具有交互式启动菜单，如图 D-1 所示。FreeBSD 启动会显示 10 秒菜单，允许你正常启动系统（多用户模式）、进入单用户模式进行系统维护或使用不同的内核或启动选项启动系统。

图 D-1 FreeBSD 引导程序

启动 FreeBSD 内核后，init 守护进程执行 `/etc/rc` 脚本，该脚本通过执行 `/etc/rc` 目录下的相应守护进程脚本，启动 `/etc/rc.conf` 中列出的其他守护进程。`/etc/rc` 脚本还会运行其他系统初始化，包括使用 `/etc/rc.conf` 指定参数连接网络接口的 `/etc/netstart`。要查看系统初始化期间 FreeBSD 内核检测到的硬件和加载的模块，可以查看 `/var/run/dmesg` 日志。或者，要查看由 init 启动的守护进程和组件（包括相关错误），可以查看 `/var/log/messages` 文件。

## 存储配置

如表 D-1 所示，FreeBSD 使用与 Linux 不同的设备文件来标识存储设备。对于物理存储设备，你可以使用 `geom` 命令。例如，运行 `geom disk show` 可以显示系统中可用设备列表。

表 D-1 常见 FreeBSD 存储设备文件

| 设备文件 | 描述 |
| :--- | :--- |
| /dev/ada0 | 第一个 SATA 驱动 |
| /dev/ada1 | 第二个 SATA 驱动 |
| /dev/da0 | 第一个 SCSI 驱动 |
| /dev/da1 | 第二个 SCSI 驱动 |
| /dev/md0 | 第一个虚拟磁盘 |
| /dev/s0 | 第一个 IDE 驱动 |
| /dev/nvme0 | 第一个 NVMe 驱动 |
| /dev/nvme0n1 | NVMe 0 上的第一个分区 |
| /dev/nvme0n2 | NVMe 0 上的第二个分区 |

表 D-2 示例 FreeBSD 分区

| 文件 | 描述 |
| :--- | :--- |
| /dev/ada0s1 | 根分区 |
| /dev/ada0s2 | 交换分区 |
| /dev/ada0s3 | 家目录分区 |
| /dev/nvme0n1 | 根分区 |
| /dev/nvme0n2 | 交换分区 |

## 启动环境

如果 FreeBSD 使用 ZFS 作为根，你可以使用 ZFS 快照将系统恢复到之前的状态。当对根目录进行快照时，后续的文件更改将存储在启动环境中。为了实现这一点，你必须首先使用 pkg 安装启动环境（pkg 见描述）。接下来，你可以运行 create 命令创建快照，并运行 zfs list 查看快照和关联的启动环境。要进行恢复，你需要运行 activate 并重启系统。或者，你可以重启系统，在引导程序界面按 e 并选择 July2 启动环境。

## 文件系统标志

虽然 Linux 和 FreeBSD 的大部分功能和命令是相同的，但配置文件系统的方法不同。在 FreeBSD 系统中，文件系统属性被称为文件标志，可以在系统或用户级别设置。例如，系统范围不可变标志（相当于 Linux 中的不可变属性），你可以运行 chflags alone filename。你可以使用 chflags -l filename 查看已设置的标志，或使用 chflags noshim filename 移除该系统范围不可变标志。

## 用户和组

在 Linux 中，使用 `/etc/group` 文件存储 FreeBSD 组信息。信息存储在 `/etc/passwd` 中转换为数据库格式 `/etc/passwd.db` 以供 FreeBSD 使用。由于 FreeBSD 没有 sudo 命令，用户必须属于 wheel 组才能使用 su 命令获取 shell。通过使用而不是 `/etc/shadow` 来存储密码信息，FreeBSD 将所有用户密码信息存储在 `/etc/master` 中，但将其转换为数据库格式 (`/etc/passwd.db`) 使用。

使用交互式界面创建用户账户，你可以运行 adduser 命令。默认情况下，新用户将获得 `/etc/adduser` 中的默认账户设置和默认家

# 662 CompTIA Linux+ 与 LPIC-1：Linux 认证指南

从 `/usr/share/kernel` 复制的目录文件。你也可以使用 `rmuser` 命令删除用户，并使用 `chpass` 命令修改用户设置。或者，你可以使用 `pw` 命令来添加、删除、修改、锁定和解锁用户账户。

## 安装软件

FreeBSD 软件包管理器是在 FreeBSD 系统上安装软件的主要方法。与 Linux 系统上的 Red Hat 和 Debian 管理器一样，它从在线软件仓库获取软件，包括依赖包。你使用 `pkg` 命令与 FreeBSD 软件包管理器交互，表 D-3 列出了示例命令。

### 表 D-3 FreeBSD 软件包管理器示例命令

| 命令 | 描述 |
|---|---|
| pkg update | 更新在线仓库中可用软件包列表 |
| pkg search apache | 在在线仓库中搜索名称或描述包含 apache 的包 |
| pkg install apache24 | 下载并安装 Apache Web 服务器 (apache24) 包 |
| pkg upgrade apache24 | 将 apache24 包升级到最新版本 |
| pkg info apache24 | 显示 apache24 包的详细信息 |
| pkg info -l apache24 | 显示 apache24 包的文件内容列表 |
| pkg check apache24 | 检查 apache24 包内容是否存在缺失或损坏的文件 |
| pkg lock apache24 | 防止修改或删除 apache24 包 |
| pkg remove apache24 | 卸载 apache24 包 |
| pkg clean |  /var/cache/pkg 目录下的任何缓存包文件 |
| pkg autoremove | 自动从系统删除未使用的依赖包 |
| pkg which /usr/local/sbin/httpd | 显示提供 /usr/local/sbin/httpd 文件的所属包 |

安装软件后，你还必须安装 apache24 包以便在启动时运行它。例如，要在安装后启动 Apache 服务器，你可以在 `/etc/rc.conf` 中添加 `apache24_enable=YES`。

系统中大多数软件的配置文件位于 `/etc` 或 `/usr/local/etc` 目录下。例如，用于配置 Apache Web 服务器的 httpd.conf 文件位于 `/usr/local/etc/apache24` 目录下。

## 管理服务

要管理 FreeBSD 系统上的服务，你可以使用 Linux 系统在实现 Systemd 之前使用的 `service` 命令。要启动 Apache 服务器，可以使用 `service apache24 start` 和 `service apache24 stop`；要显示启动时加载的服务及其顺序，可以运行 `service -e` 命令。

## 附录 D 将你的 Linux 知识应用于 FreeBSD

> 注意：如果服务未列在 `/etc/rc.conf` 中，你必须使用 `service servicename start` 命令来启动它。

## 监控工具

与 Linux 系统一样，你可以使用 `vmstat` 等命令监控 FreeBSD 系统的性能，或者使用 Linux 中的 `netstat` 和 `socket` 命令监控网络统计。要在 FreeBSD 上监控磁盘性能，可以使用 `gstat` 命令。

## 防火墙配置

FreeBSD 默认安装三种不同的防火墙系统：PF、IPFW 和 IPFILTER。PF 是最常用的；它将防火墙规则存储在 `/etc/pf.conf` 中并可以使用 `pfctl` 命令进行配置。此外，你可以使用 `blastctl` 命令配置黑名单进程，使用 `/etc/blacklist.conf` 文件拦截特定连接。

## 容器配置

FreeBSD 是最早实现容器的操作系统之一。然而，FreeBSD 容器被称为 jails，并不像 Docker 那样依赖于单一运行时容器。作为一个 FreeBSD jail，你从 FreeBSD 仓库下载一个包含文件系统（称为 userland）的 jail，将其提取到你选择的目录，并在 `/etc/jail.conf` 中配置 jail 的设置（例如名称、IP 地址）。接下来，你可以像管理 Docker 容器一样启动和管理你的 jail。

例如，如果你在 `/etc/jail.conf` 中创建了一个名为 jail1 的 jail，你可以使用 `service jail start jail1` 命令启动它。然后你可以使用 `jexec` 命令在 jail1 中执行命令，`jexec jail1 "ps aux"` 将显示 jail1 中运行的进程，而 `pkg -j jail1 install apache24` 将会在 jail 中启动 Apache Web 服务器。你也可以使用 `service jail stop jail1` 命令停止 jail1，或运行 `ls` 命令显示系统上运行的所有 jail。

## 关键术语

| adduser 命令 | pfctl 命令 |
|---|---|
| blacklist 命令 | gstat 命令 |
| 启动环境 | pkg 命令 |
| boot0 | pw 命令 |
| C shell | ruser 命令 |
| chpass 命令 | sysrc 命令 |
| filesystems 标志 | tunef 命令 |
| FreeBSD 软件包管理器 | UNIX 文件系统 `UFS` |
| geom 命令 | userland |
| gpart 命令 | ZFS 快照 |
| kenv 命令 | |
| kldstat 命令 | |
| kldload 命令 | newfs 命令 |

## 词汇表

- `sum` 命令：用于验证文件的校验和；** 代表校验和算法。例如，要验证 SHA1 校验和，可以使用 `shasum` 命令。

- /dev 目录：存储设备文件的目录。

- /etc/fstab：一个在启动时或向 mount 命令提供的参数不足时指定文件系统的文件。

- /etc/mtab：存储已挂载文件系统列表的文件。

- /proc/devices：包含当前正在使用的设备编号的文件。
