
+ 4. 此操作对 `/etc/gdm/gdm.conf-custom` 配置文件进行的更改会被集成到 GNOME 显示管理器。要设置并验证两个图形登录控制台，请执行以下步骤：

+ 1. 在文本编辑器中打开 `gdm.conf-custom` 配置文件。

+ 2. 在 `[servers]` 部分添加以下指令：

```
1=Standard device=/dev/console
2=Standard device=/dev/console
```

+ 3. 使用以下命令重新读取 GNOME 显示管理器配置文件：

```
$ sudo /etc/init.d/gdm reload
```

+ 4. 此操作对 `/etc/gdm/gdm.conf-custom` 配置文件进行的更改会被集成到 GNOME 显示管理器。要设置并验证两个图形登录控制台，请执行以下步骤：

+ 1. 在文本编辑器中打开 `gdm.conf-custom` 配置文件。

+ 2. 在 `[servers]` 部分添加以下指令：

```
1=Standard device=/dev/console
2=Standard device=/dev/console
```

+ 3. 使用以下命令重新读取 GNOME 显示管理器配置文件：

```
$ sudo /etc/init.d/gdm reload
```

# Lab 2

此实验旨在帮助你通过数据在用户主目录中的存储方式，理解 Evolution 邮件管理器的工作原理。

![](img/8521db60567337b3b9ca1b288c5d36b6_485_0.png)

# 关于光盘

# 468 Ubuntu 认证专家学习指南

本书附带的光盘包含了完整的 MasterExam 软件和本书的电子版。该软件可在任何 Windows 98/NT/2000/XP/Vista 电脑上轻松安装，必须安装后才能访问 MasterExam 功能。

虽然可以使用 WINE 软件在 Linux 上安装 MasterExam，但对此类安装不提供任何保证或保修，如果您选择这样做，将无法获得任何支持。众周知，与填空题相关的 Flash 代码会导致错误。Windows 是唯一推荐的安装系统。

MasterExam 无法识别命令的`粗体`格式。事实上，某些命令在大写显示时可能不准确。我们对 MasterExam 软件的这一局限性深表歉意。

光盘根目录下以 `.pdf` 格式包含了一份纸质笔版考试。如果您无法在 Windows 或 Linux 环境下运行 MasterExam，您仍然可以在电脑上查看该 `.pdf` 来获取考试内容。很抱歉，您将无法打印该 `.pdf`。

要注册第二个 MasterExam，只需点击主页上的“Online Training”链接，并按照指示进行免费在线注册。

# 系统要求

电子书需要 Adobe Acrobat Reader 或同等的 Linux 阅读器（如 Evince）。

# 安装和运行 MasterExam

在 Microsoft Windows 上，如果您的电脑光盘驱动器配置为“自动运行”（AutoRun），则在插入光片时光盘会自动启动。从启动界面，您可以点击 MasterExam 按钮来安装 MasterExam。这将开始安装过程并创建一个名为 LearnKey 的组。要运行 MasterExam，请选择“开始 | 所有程序 | LearnKey | MasterExam | LearnKey MasterExam”。如果自动运行功能没有启动光盘，请在 Windows 资源管理器中浏览到光盘并点击 `LaunchTraining.exe` 图标。然后点击 MasterExam 链接并按照提示操作。

如果尚未展开，点击“Ubuntu Certification Guide (Exam LPI 199)”旁边的加号以显示 Quiz 和 MasterExam 选项。如果您选择 Quiz，系统会提示您选择最多 48 个问题，并限制 90 分钟。

# 附录 A：关于光盘 469

如果您选择 MasterExam，您将看到一个只有 45 道题且限时两小时的考试。（实际上为考试分配了 75 分钟，但您阅读保密协议的时间也会计入在内。）

# 参加 MasterExam

MasterExam 为您提供了真实考试的模拟。尽管存在上述问题，但问题的数量、题类型以及允许的时间旨在准确反映考试环境。您可以选择开卷考试（包含提示、参考资料和答案）、闭卷考试（90 分钟）或计时（120 分钟）的 MasterExam 模拟。当您启动 MasterExam 时，屏幕右下角会出现一个数字时钟。除非在时间过期之前选择结束考试，否则时钟将一直倒计时到零。

对于“填空”题，您需要输入精确的答案。在现实生活中，单词拼写错误和命令拼写错误一样。

# 卸载安装

在 Microsoft Windows 中，为了获得最佳卸载效果，请使用“开始 | 所有程序 | LearnKey Uninstall | Uninstall LearnKey MasterExam”选项来卸载 MasterExam。

# LearnKey 技术支持

有关软件 Windows 版安装（安装、操作和卸载）的技术问题，以及有关在线注册的问题，请访问 www.learnkey.com 或发送电子邮件至 techsupport@learnkey.com。我们不对软件的 Linux安装提供支持。

# 获取内容支持

有关电子书或 MasterExam 技术内容方面的问题，请访问 www.mhprofessional.com 或发送电子邮件至 customer.service@mcgraw-hill.com。对于美国以外的客户，请发送电子邮件至 international_cs@mcgraw-hill.com。

![](img/8521db60567337b3b9ca1b288c5d36b6_488_0.png)

# 附录 B：关于光盘

# 测试 Linux

UCP 考试是为初级 Linux 管理员设计的，许多候选人可能至少部分使用 Microsoft Windows。这可能是许多候选人在工作或家里唯一的可用操作系统。在本节中，我将演示

# 474 Ubuntu 认证专家学习指南

在带有 Service Pack 2 的 Microsoft Windows XP Media Center 上安装 VMware Server。我没有在任何其他 Microsoft 操作系统上测试过 VMware Server 的安装，因此步骤可能会有所。

要在 Microsoft Windows 上安装 VMware Server，请按照以下步骤操作：

- 1. 导航到下载 VMware Server 可执行文件的目录，并运行该 VMware Server 文件。

- 2. 可执行文件在一段时间后将启动安装向导。点击“Next”，阅读并接受许可协议，然后点击“Next”。

- 3. 除非你的磁盘空间紧张，否则选择“Complete”以安装所有 VMware Server 和客户端组件，并点击“Next”。

- 4. 如果你看到关于 VMware 管理界面仅支持某些操作系统的警告，请记下并点击“OK”。

- 5. 接受 VMware Server 安装的默认位置，或者如果偏好其他位置则进行更改。如果你安装了不同的产品，你可能想在不同的目录下安装 VMware Server。否则，点击“Next”。

- 6. 点击“Install”开始安装。此过程可能需要几分钟。在提示时点击“Finish”。

- 7. 现在你应该可以打开已安装的 VMware Server。点击 Start | All Programs | VMware | VMware Server | VMware Console。

- 8. 若要继续，请阅读附录后部分的“为 Linux 安装准备 VMware”中的步骤。安装 Ubuntu Linux 所所需的步骤是相同的。

# 在 Ubuntu Hardy Heron 上安装 VMware Server

本节展示了如何从上述 tarball 包在 Ubuntu Hardy Heron 系统上安装 VMware Server。本节假设你已经安装了带有内核模块的最新内核和源码或内核开发包。它还假设你已经为你的发行版安装了 GNU C 编译器包。你应该知道如何打开另一个虚拟控制台以根据需要运行其他命令。如果你以前运行过注的安装脚本，你可能不需要查看本节列出的所有步骤。

# 附录 B：使用 VMware 475 测试 Linux

你还需要确保使用如下命令安装了必要的先决条件包：

```bash
$ sudo apt-get install build-essential linux-kernel-devel \
linux-headers-generic xinetd
```

要在 Ubuntu Hardy Heron 系统上安装 VMware Server，请按照以下步骤操作：
