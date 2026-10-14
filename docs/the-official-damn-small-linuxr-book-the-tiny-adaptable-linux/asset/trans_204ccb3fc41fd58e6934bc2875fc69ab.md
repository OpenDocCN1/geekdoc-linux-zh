

DSL 可以精确地实现你想要的功能。为此，本书各章节将指导你掌握调整 DSL 以满足需求的技术，并使 DSL 适应你的计算机设备。

以下是本书涵盖的一些主要主题。

## Booting DSL

只要有一台 PC 和一份 Damn Small Linux 拷贝（如本书光盘上的那样），大多数人都可以重新启动并在无需指导的情况下运行 DSL。如果某些硬件无法正常工作，按 F2 会显示启动选项，可帮助解决大多数简单问题。

启动 DSL 时，你可以向 DSL 传递其他启动选项来指导启动过程。其中一些选项可以使 DSL 更好地适用于你的特定硬件（如无法正确检测的显卡）。其他选项可让你以特殊方式运行 DSL（如完全从 RAM 运行 DSL）。还有其他选项可让你识别可拉入 DSL 系统的数据包位置（如你备份的桌面设置或已保存的应用程序）。

启动 DSL 时可能需要使用的启动选项包含在第 2 章“Booting DSL”中。有关识别个人设置备份位置和恢复位置的选项在第 4 章“Configuring and Saving DSL Settings”中介绍。有关在不同硬件环境中运行 DSL 的选项在第 8 章“Installing DSL in Alternate Ways”中介绍。

## Customizing the Desktop

Fluxbox 是 Damn Small Linux 默认使用的窗口管理器。尽管体积紧凑，但仍有许多方法可以调整 Fluxbox，使其外观和行为符合你的喜好。窗口管理器定义了菜单、鼠标操作、键盘导航、背景以及与图形界面外观和感觉相关的其他功能如何运行。

从 Fluxbox 桌面，大多数 DSL 活动都可通过单个桌面菜单进行控制（右键单击桌面即可看到 DSL 菜单）。选择 Desktop，Fluxbox Configuration 可查看可更改的桌面设置列表。图 1-2 显示了这些菜单的示例。

除了更改桌面的外观和感觉外，你还可以使用各种桌面实用程序来管理工作区、挂载和卸载文件系统以及管理任务。有关使用各种桌面工具和应用程序的说明在第 3 章中介绍。

### FIGURE 1-2 Customize your desktop settings from the DSL menu.

![](img/af53325d7f38f1cdafca9f44568e4ab8_36_0.png)

## Adding Applications with MyDSL

并非每个人都需要每一种可用的软件与他们的 live CD 一起运行，但几乎每个人都需要一些超出 DSL 所选软件的软件包。使用为 DSL 设计的 MyDSL 功能，你可以向 live 系统添加预打包软件，将这些软件包保存以便以后恢复，并在下次重新启动 DSL 时选择包含或不包含它们。

第 5 章包含对 MyDSL 功能的描述。MyDSL 的描述集中在图 1-3 所示的 MyDSL Extension 工具上。

### FIGURE 1-3 Customize your desktop settings from the DSL menu.

![](img/af53325d7f38f1cdafca9f44568e4ab8_36_1.png)

## Saving and Restoring Settings and Data

要使任何 live CD 长期有用，你需要在重新启动后保存数据文件、系统设置以及你经常使用的任何额外应用程序。DSL 在重新启动后保存个人文件的方式上提供了很大的灵活性。

DSL 的备份和恢复功能让你可以选择要备份的确切文件和数据目录，以及要将该数据存储在何处。如果你以特定方式保存该数据，DSL 会自动找到并恢复该数据

你可以学习如何重新制作自己的 DSL 映像，以包含你喜欢的任何应用程序或数据（无需在启动时合并额外的应用程序和数据）。

## What Is Damn Small Linux?

在继续之前，我们需要明确 Damn Small Linux 到底是什么。Damn Small Linux 是一种操作系统，设计为从 live 介质（如可启动的名片大小 CD）运行，其核心由 Linux 内核控制。它基于另一个名为 KNOPPIX 的 Linux live CD，而 KNOPPIX 本身则源自名为 Debian 的 Linux 发行版。

现在，我们需要理清所有这些。

## Understanding Operating Systems

操作系统是管理计算机硬件与你为使用该硬件而运行的应用程序之间交互的计算机软件。在专有个人计算世界中，你可能最熟悉 Microsoft Windows 和 Mac OS/X 操作系统。在自由和开源软件（FOSS）世界中，大多数操作系统都追溯到 UNIX。

Damn Small Linux 是众多以 Linux 命名的 FOSS 操作系统之一，因为它包含被称为内核的 Linux 软件。Linux 内核是操作系统的最关键部分，因为它提供最基本系统服务：进程管理、设备驱动框架、文件系统支持以及其他关键系统功能。随着新硬件、文件系统类型和其他组件连接到 Linux 系统，它们可以作为所谓的 loadable kernel modules 添加到内核中。

Linus Torvalds 创建了 Linux 内核，并至今仍领导 Linux 内核开发。该软件可从 Linux Kernel Archives（http://kernel.org）获得。大多数 Linux 发行版会添加来自 Free Software Foundation GNU 项目（www.gnu.org）的一组基本系统实用程序，其中包含许多最初在 UNIX 系统上可用的命令的克隆。

尽管最新可用的内核是 2.6 内核，但 DSL 选择继续使用 2.4 内核树。这主要是因为 2.6 内核明显更大。然而，随着安全漏洞被发现，从 2.6 内核回溯的修复程序会被包含在 DSL 使用的 2.4 内核中。改进的回溯也可以以同样的方式添加。

