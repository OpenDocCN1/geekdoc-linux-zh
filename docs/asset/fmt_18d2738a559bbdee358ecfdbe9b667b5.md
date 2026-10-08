
# Linux 发行版的创建

Linux 发行版的创建有许多原因。有些是因为对特定应用程序或环境的偏好而开发的；另一些是为了特定的任务，如革命、公共艺术、教育或安全而创建的。还有一些是为了兼容 Windows 或为了针对初学者而设计的。有些发行版坦率说是实验性的，或者是为了实干者设计的。

关于 EU OS 的公众辩论提醒了另一个更广泛的趋势：什么是可能接近我们的东西，其目标是使政府及其部门的 IT 结构标准化（图 1）。这一想法可以追溯到 Linux 的早期阶段，当时自由软件经常被推为弥合欧洲、北美技术民主化国家与发展中国家之间数字鸿沟的手段，但第一次政策发行版的尝试并没有被采纳，这在某种是因为它更多是政治考虑而非技术考虑，但主要是因为政策发行版的成功非常有限。

EU OS 是一个社区项目，希望被欧盟联盟（EU）采用。尽管离现实还远，但 EU OS 将自己描述为“概念验证”。挑战在于“证明管理团队可以在两年或更短时间内，在没有 Active Directory 和没有微软 Windows 的情况下管理用户及其数据、设备”。前者指的是 Linux，即从 2004 年开始的尝试将慕尼黑切换到自由软件的尝试。EU OS 的目标是产生一项正确的采用自由软件政策，该政策将被 Europa EU [2] 接受，这是欧盟机构共享的开源项目代码开发平台。项目还在未提供任何细节的情况下补充说，“正与成员国和层级的公共管理部门保持联系”。

EU OS 计划产生一种不可变的可启动容器技术，并从项目创始人 Robert Meijer 的个人带有各种发行版运行 Plasma 桌面。这些细节在媒体报道中往往受到关注，因为这正是受众感兴趣的，但 EU OS 并不打算作为人类的另一个发行版，EU 希望产生一个可以完全在欧洲内部维护的发行版。一个主要的担忧是，内核或 Wayland 等通用链接是否会遭受由于美国政府发起的当前关税战。欧盟的许多账户将对此类问题达成一致，这可能被识别为目标。项目还研究了 EU OS 如何与本地需求互动，至少这些关注点的优先级将高于技术。功能性需求已存在部分，但 EU OS 仍在开发中。

Bruce Byfield 是一位计算机记者、专从事自由和开源的自由职业作家和编辑。除了他的写作项目外，他还教授现场和在线学习课程。在他的博客中，他描写关于西海岸的一切（https://brucebyfield.wordpress.com）。他还是 PrenticePieces 的联合创始人，这是一个关于写作和幻想的博客（https://prenticepieces.com/）。

## 评测

### Latino Latino – 政策决策

政策已存在多年，但它们取得了参差不齐的成功。通常，它们始于取代政府使用的 Windows。在负担得起许可费用的发展中国家，当地政府对迁移到自由软件表现出浓厚兴趣，特别是本地开发或减少进口时。这可能起作用。其他还包括

- Bhoarat Operating Solutions (BOS) Linux：最近关于消除数字鸿沟和鼓励使用 Linux 的报告

- Astra Linux：最初为俄罗斯军队开发，Astra 已扩展为俄罗斯国家和核电站中 Linux 的替代品

- Kylin：为中国政府开发，Ubuntu Kylin 是其官方继任者

- Nova Linux：古巴尝试取代 Windows 的灵感源于

除了 Linux 之外，EU OS 还记录了十多个本地迁移努力，包括法国宪兵队的 Bantu，它取得了成功。EU OS 充分利用了这些例子。

（注：由于用户提供的原文中存在大量重复内容，上述译文已按原文结构进行完整翻译。）

## 评

### Lomiri

已安装。使用 UBports Installer [6]，它为每个设备提供了分步说明。

- postmarkOS - 可以通过 Lomiri [7] 的 wiki 页面访问 postmarkOS。

- Debian - 软件包在 Sid（Debian 不稳定版本）中可用，但目前没有可用的说明 [8]。

- Alpine - 软件包位于 Alpine 网站 [9] 上；

- NixOS - 将以下行添加到 `/etc/nixos/configuration.nix`：

![](img/5d8ea078bd95ce53a498c7a527477ee9_30_0.png)

```
services.desktopManager?
lomiri.enable = true;

services.desktopManager?
defaultSession = "lomiri";
```

图 1：带有搜索和文件管理器的 Lomiri 桌面面。

然后运行 `nixos-rebuild switch`。只要系统完全安装完成，它将启动到 Lomiri 桌面面。

![](img/5d8ea078bd95ce53a498c7a527477ee9_30_1.png)

## Lomiri 桌面

如果你在 2010-2017 年的 Unity 时代使用过 Ubuntu 系统， Lomiri 界面的初印象会很熟悉。Lomiri 显示了搜索和文件管理器。搜索工具是一个为 Unity 创建并现在已转型的独特且强大的应用程序。你可以搜索任何文件、应用程序、视频和照片。你也可以搜索设置和应用程序。事实上，搜索工具可以按日期、类别和最后更改类型进行过滤。搜索功能快速且实用，是 Lomiri 中最优秀的应用程序之一。默认管理器名为 Nautilus。如果你用过 Ubuntu，你将熟悉它及其功能。

“设置”应用提供了各种功能和微调。Unity Tweak（Unity 调整工具）为配置 Lomiri 启动器、搜索和面板提供了多个选项。启动器隐藏功能也值得花时间。你可以轻松更改面板的透明度级别。带有经典“文件”、“编辑”、“查看...”菜单的面板还提供了带有自定义主题的自动隐藏选项。

![](img/5d8ea078bd95ce53a498c7a527477ee9_30_2.png)

图 2：左侧的系统设置和右侧的 Tweak 工具。

我几乎忘了提到 Lomiri 的平视显示（HUD）功能。HUD 是一个控制面板，允许通过快捷键访问顶层菜单项，让你无需碰鼠标即可选择。默认菜单快捷键是 Alt+F，你可以通过点击打开它。

窗口管理器设置比 Genome 更丰富，允许你为可用窗口中的许多事件设置不同的动画。反向窗格关注你在用户界面中使用过的应用程序。例如，当接收到消息时，通知将快速弹出以引起用户的注意力。

- 左上、顶部、底部 - 调整大小到显示器的左部分

- 右下、底部 - 调整大小到显示器的右部分

热边缘角（Hot corners）是一个非常实用的选项：移动到显示位置即可触发操作。Genome 有类似的选项，但 Lomiri 提供了更多热边缘角：顶部、中间和右侧；三个位置，中间显示器上的两个，以及左侧和右侧。可能的操作包括：切换桌面、窗口展开、窗口平铺、所有窗口平铺。

在管理大量按键时，可以使用热边缘角进行窗口和工作空间管理。

窗口管理器提供了更多值得关注的功能：

- 极快速深色/白色主题切换：你也可以更改颜色代理，尽管可用的颜色有限：深色、黑色、

- 顶角 - 最大化

LOMIRI-LINUX.COM

第 296 期

31

## 评

Lomiri

### 全局菜单

经典的应用程序菜单通常包含“文件”、“编辑”、“选择”和“查找”选项。全局菜单意味着这些选项从应用程序窗口裁剪并移动到顶部。全局菜单在 GNOME 中是禁用的，引起了争议。在 Lomiri 上你可以放松：全局菜单是稳固且稳定的，就像 macOS 一样。启用全局菜单：聚焦应用程序，将光标移动到顶部面板，并

### 系统设置

![](img/5d8ea078bd95ce53a498c7a527477ee9_31_0.png)

![](img/5d8ea078bd95ce53a498c7a527477ee9_31_1.png)

## Lomiri 移动端

Unity 的整个目标是支持桌面和移动系统的融合。Lomiri 的移动版本 (3) 针对触摸屏进行了优化，并且快速流畅。界面 (4) 比相同设备上的 Android 快。

![](img/5d8ea078bd95ce53a498c7a527477ee9_31_2.png)

图 5：日历和系统设置。

![](img/5d8ea078bd95ce53a498c7a527477ee9_31_3.png)

图 3：Ubuntu 上的 Lomiri 移动版本。

- 应用程序备份

- root 权限和 SSH

- 云端/本地设置软件包

- Lomiri 值得探索。

橄榄绿、紫色、红色、鼠尾。

- 通知：Lomiri 桌面没有隐藏单个应用程序的选项，但在移动版本中可用。

- 字符映射：当你需要输入特殊字符时，字符映射非常好。

## 信息

- 1) Unity: https://unity.org/

- 2) Lomiri: https://github.com/lomiri/lomiri

- 3) Ubuntu: https://en.wikipedia.org/wiki/Ubuntu_linux

- 4) Ubuntu: https://www.ubuntu.com/

- 5) Ubuntu Supported Devices: https://devices.ubuntu.com/

- 6) Ubuntu Installer: https://github.com/ubuntu/ubuntu-installer

- 7) postmarkos: https://postmarkos.org/postmarkos/wiki/lomiri

- 8) Lomiri in Debian: https://packages.debian.org/lomiri

- 9) Lomiri in Alpine: https://pkgs.alpinelinux.org/package/edge/x86_64

Morph 浏览器是默认浏览器。Firefox 在 Store [10] 中不可用，它是 GitHub 的 Google Play 非官方替代品。浏览器的移动版本与桌面版本不同，并针对触摸屏进行了良好优化。

设置工具类似于 OS 等且更加简单（图 5）。可以通过 UT Twe Tool [12] 实现高级系统调优。日历和事件允许使用 CalDAV 协议进行同步。

## LINUX

社区在学习和改进 Lomiri 方面做得出色。Lomiri 运行良好，具有响应式界面且易于使用。

Unity 是为了融合而创建的，Lomiri 维护了这些原则，桌面、移动或平板电脑使用相同的 shell。手势支持良好，允许你在窗口之间快速导航。

## 作者

Paul Neiser 自 00 年代后期以来一直是 Linux 用户和 FOSS 倡导者。他热衷于隐私、安全、网络和社区驱动。在 Mastodon 上找到 Paul：https://mastodon.social/paulneiser

Lomiri 看起来非常，并且允许移动设备。功能包括：

- 电话

![](img/5d8ea078bd95ce53a498c7a527477ee9_31_4.png)

图 4：运行中的 Morph 浏览器。

## 评

### GNOME 会议

GUADEC 是 GNOME 的主要活动。自 2000 年以来，它汇聚了来自全球自由软件爱好者和专业人士。加入 2025 年在布雷西亚或在线举办的 GUADEC，听取技术发展，参加讲座，参与工作坊并庆祝 GNOME！

## 了解更多

GUADEC.ORG

![](img/5d8ea078bd95ce53a498c7a527477ee9_32_0.png)

## 深度解析

### Nushell

### 数据管道

Nushell 的功能之一是能够在 shell 中原生处理结构化数据。传统的 shell 运行在

作者 Marcin Gastol 

Nushell 的数据优先方法将脚本提升到了清晰和精确的新水平。Nushell 用结构化管道取代了[缺失]，它用 Rust 构建，并且类似于

# 在 Ubuntu 上安装和配置

Nushell 可以通过多种方式安装在 Ubuntu 上（Apt 仓库、Snap 或源码）。这里是 Apt 方法，它简单且能保持 Nushell 更新。

要使用官方仓库在 Ubuntu 上安全地安装 Nushell，首先添加 GPG 密钥，以确保软件包的真实性。Apt 系统需要此密钥来验证下载的软件包来自：

```
curl --fsSL https://apt.io/nushell/nushell.gpg | sudo apt --dearmor -o /etc/apt/trusted.gpg.d/dury-nushell.gpg
```

接下来，将仓库 URL 添加到系统的 Apt 列表中：

```
echo "* https://apt.io/nushell/ main" | sudo tee /etc/apt/sources.list.d/dury.list
```

最后，使用 apt 安装命令安装 Nushell：

```
sudo apt install nushell
```

这将从仓库拉取 Nushell 二进制及其所有依赖项

## 基础配置

安装 Nushell 后，你可能需要配置环境。Nushell 的配置通常通过两个文件完成（位于你的配置目录/ ubuntu）：

- `config.nu`：用于交互式 Nushell 设置的主脚本（类似于 Bash 的 .bashrc）。

- 你可以设置 Nushell 特定选项、别名、自定义并在启动时运行任何命令。

- `env.nu`：为 Nushell 设置变量的脚本（并导出到由 Nushell 运行的命令）。这用于设置环境变量：

## 结构化数据处理

Nushell 的功能之一是能够在 shell 中原生处理结构化数据。传统的 shell 处理

```
echo "* https://apt.io/nushell/ main" | sudo tee /etc/apt/sources.list.d/dury.list
```

34

2025年7月

* Nushell *

LINUX-MAGAZINE.COM

所有命令的输出均为文本，需要你使用 `grep`、`awk` 或 `jq` 等工具进行解析。而 Nushell 命令从结构上返回表格和列表类数据类型，你可以轻松地找到并对其进行操作。

```bash
nushell --config
Config file created at: /home/marcin/config/nushell.env
Config file created at: /home/marcin/config/nushell.nu
```

-O*: 欢迎来到 Nushell，一种所有数据都是结构化的 Shell 语言！版本：0.83.0 (x86_64-linux-mus)

请通过 https://discord.gg/nushell 加入我们的社区

在 Twitter 上关注我们：https://github.com/nushell

我们的文档位于：https://nushell.sh

查看我们的博客：https://nushell.sh/blog/

在 https://nushell.sh/book/configuration/welcome-message 学习如何使用它

距离 Nushell 首次提交已经过去有一段时间了：启动时间：58ms 412ms

## 将数据视为文件系统

Nushell 中的 `ls` 命令返回一个包含文件的表格，其中包含名称、类型、大小和修改时间等列。你可以直接对其进行查询。例如，你可以按修改时间列出当前文件夹中的目录（见图 3）：

```bash
ls | type == "dir" | sort-by modified reverse
```

## 结构化系统信息

`ps` 和 `sys` 命令是 Nushell 内置的，能够很好地返回结构化数据。例如，`ps` 会提供一个包含 PID、名称、CPU、内存等列的表格。你可以找到占用最高的进程（见图 4）：

```bash
ps | sort --mem last
```

## 打开并解析文件

Nushell 的 `open` 命令是从文件中引入数据的强大方式。它能自动检测包括 JSON、CSV、TOML、YAML、XML 等在内的类型，并将其转换为表格或记录。例如，图 5 中的表格是通过以下命令生成的

## 处理流水线数据

一旦你在 Nushell 流水线中拥有数据（无论来自内部命令还是你解析的外部命令），你就可以使用一组命令来处理它：

```bash
open stack.yaml
```

此文件用于覆盖 Nushell 设置、定义环境变量或任何其他任务。以前，环境变量在 `env.nu` 中配置。通常，大多数配置可以在 `config.nu` 中完成，并且它在 `env.nu` 之前加载。你可以用默认编辑器打开此文件。图 2：`config.nu` 和 `env.nu` 文件在首次启动时自动创建。

## 深度 Nushell

### 文件和目录管理

Nushell 可以像 Bash 一样运行标准文件操作（复制、移动和删除）。它根据需要使用内置或 `cp`、`mv` 和 `rm` 的等效命令。你可以像往常在 Nushell 中使用 `mv`、`rm` 和其他命令。优势是将这些与结构化查询结合。例如，过滤目录中所有大于 100MB 的文件（小心操作！）：

| pid | ppid | name | status | cpu | mem | virtual |

|---|---|---|---|---|---|---|

| 0 | 334 | dockerd | Sleeping | 0.00 | 88.3 MB | 2.4 GB |

| 1 | 773 | systemd | Sleeping | 0.00 | 10.7 MB | 30.7 MB |

| 2 | 1931 | systemd | Sleeping | 0.00 | 11.6 MB | 29.9 MB |

| 3 | 998 | snapd | Sleeping | 0.00 | 12.1 MB | 31.8 MB |

| 4 | 526 | snapd | Sleeping | 0.00 | 13.8 MB | 22.7 MB |

| 5 | 128 | snapd | Sleeping | 0.00 | 14.5 MB | 23.6 MB |

| 6 | 115 | journald | Sleeping | 0.00 | 15.3 MB | 24.8 MB |
