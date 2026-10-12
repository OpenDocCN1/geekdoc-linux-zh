
Yu 澄清道，他并不是指内核开发者忽略警告，也不是他认为`BUG_ON`仅供VM开发者使用。他真正担心的是普通用户，他们可能更倾向于向内核开发者报告崩溃，而不仅仅是一个警告。对于Linux的观点，“我听到了，我并不是在争论什么，只是分享我的见解。’

同时，来自红帽的Justin Forbes解释了使用`CONFIG_DEBUG_VM`后的一些思路。他说：“我们主要将其分为三种情况：’

在实际上，我们对`rc`版本和`.0`版本运行标准的Fedora配置，但`git`快照是使用调试配置构建的。权衡是，无法关闭某些影响性能的选项，但我们确实获得了更多用户运行这些内核并暴露漏洞。快速内核遵循`Linus`的树，并在大多数工作日重新构建。由于Fedora不是默认配置，但在某些可以在不严重影响性能的情况下保持调试开启的情况下（例如`CONFIG_DEBUG_VM`的情况），我认为没有必要。当然，RHEL是一个保守得多的配置，其反应/回滚库也保守得多。’

他补充道：“保持选项开启会变得有问题，我们可以简单地将其关闭。Fedora的基础比典型的发行版更多样，也比大多数池更多样。无论是在硬件数组还是使用模式上，因此在其他情况下无法发现的问题会被发现。’

此外，对于报告而不是崩溃的愿望，Justin表示（此处可能是Justin said的笔误），‘我非常同意。我们收到了用户的警告，这些警告没有被忽视，其中一些用户愿意花时间彻底解决问题。他们可能不懂代码，但有很多[用户懂代码]。’

# OS 选项

# 封面故事

## Yocto

## 配方

Yocto项目提供了一套构建自定义Linux的工具。该项目提供了：

- 一个参考发行版，他们称之为`Pokey`
- `OpenEmbedded`构建系统，由Yocto和`OpenEmbedded`共同维护

Yocto的总体目标是为将Linux适配到嵌入式设备上运行提供一个完整的开发环境。环境包括模板、工具和工作代码。

Yocto最强大的功能之一是围绕层（layers）构建的模块化架构。层是……的集合

# OS 选项

任何项目开发中的一个关键点是操作系统的选择。系统的选择通常取决于项目的性质。

对于裸机环境（bare metal environment），不需要特殊的操作系统。相反，需要开发者将功能构建到应用程序中。为裸机系统开发需要实现一个硬件抽象层（HAL），以消除应用程序直接访问硬件驱动程序的需求。

其他项目需要实时操作系统（RTOS）。虽然Linux在环境中始终是实时的，但它在处理上一直有限制。RTOS系统在机器人领域很常见，如果不能满足反应时间，后果将是灾难性的。裸机Linux系统和RTOS经常将操作系统和内核集成。

第三类IoT项目需要一个更完整的操作系统。裸机Linux有利于较低的资源需求，但要求处理器具有内存管理单元（MMU）。另一方面，Linux作为操作系统允许访问大量的现成应用程序和服务，而这些服务在裸机系统和RTOS中是不可用的。

用于构建系统的文件和指令。用户可以根据需要进行混合组合，自定义各个层，同时保持整个系统的简单性。分层模型使得硬件供应商能够通过板级支持包（BSP）为操作系统开发者提供支持，BSP是一组用于构建硬件支持的分层文件集合。

配置环境，以便CPU能够加载并执行内核。这可能包括从`TFTP`服务器下载内核。IoT设备最常用的启动加载程序是`U-Boot`。

第三个组件是内核本身，它用于在设备上同时运行各种应用程序并提供硬件访问。第四个组件是设备树（DT），它是内核的一部分，用于告知CPU配置了哪些硬件。第五个也是最后一个组件由应用程序组成，它们通常位于根文件系统中。

# IoT 组件

每个Linux用于IoT设备由五个主要组件组成（见图2）。首先是启动加载程序，它在开发者的PC上编译成源代码，稍后将在设备上执行。第二个是在上电后立即由启动加载程序在CPU的ROM中执行。ROM知道可以从哪里找到启动加载程序，是从`MMC`、`MicroSD`卡还是CPU的状态引脚。

ROM中的代码随后配置启动介质，并在预设地址搜索启动加载程序。如果找到了启动加载程序，ROM将代码传输到`RAM`，由CPU对其进行处理。启动加载程序负责设置

尽管桌面Linux用户习惯于将`ISO`文件下载到`USB`闪存器并用它在PC上安装Linux，但IoT系统的处理方式有所不同。为了创建我刚才描述的所有五个基本组件，需要一个框架。

该框架由系统模块（SoM）的硬件制造商选择，该模块包含CPU以及电源管理和信号调理所需的所有电路。如果一家公司为其IoT产品指定了特定的SOM，你将受益于SoM在BSP层提供的框架。

![](img/527ef1a4e6443ad30b67df9e58b510e1_16_0.png)

![](img/527ef1a4e6443ad30b67df9e58b510e1_16_1.png)

**图 1**: 裸机、RTOS 和 Linux 嵌入系统在系统资源的需求上存在差异。

**图 2**: IoT 设备的 Linux 镜像由五个主要组件组成。

# 封面故事

## Yocto

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
  <meta name="sync" version="-8" revision="gatherspath"/>
  <meta name="meta-digi" src="https://github.com/Digi-embedded"/>
  <meta name="meta-freescale" src="https://github.com/Freescale"/>
  <meta name="meta-bsp" src="https://github.com/freescale/external_imx"/>
  <meta name="meta-yocto" src="https://github.com/yooproject/meta-yocto"/>
  <meta name="meta-embedded" src="local"/>
  <meta name="meta-swupdate" src="https://github.com/digi"/>
  <meta name="meta-user" src="https://github.com/digi"/>
  <meta name="meta-poky" src="https://github.com/yooproject/poky"/>
</manifest>
```

**图 3:** `manifest`文件列出了所有层的仓库。

## 层

`BSP`由不同的层组成，每个层都有自己的仓库。提供者通常以存档文件的形式授予第三方访问BSP的权限。然后解压该文件，并列出每个层仓库的`manifest`文件。下面是一个示例：这是一个`Digi`系统模块（SoM）的BSP。

文件3指向要下载的所有层。每一层由特定组织创建并维护。该仓库作为整个BSP的基础，提供了使用`BitBake`和`OpenEmbedded`项目构建BSP的配置以及其他层所依赖的参考实现。在这种情况下，由于`Freescale`CPU的广泛普及和频繁使用，Yocto项目采用了这一层。然而，还有一个由`NXP`提供的名为`meta-imx`的仓库。该层包含了`iMX`CPU的配置、配方和应用程序。你还会发现由SoM提供的层，例如`meta-digi`和`meta-digi-dualboot`。最后，你可以看到`Digi`还包含了其他仓库，如`meta-yocto`和`meta-swupdate`。`Digi`将这些内容添加到BSP中，以包含框架、服务和应用程序。

每一层都包含一个名为`config`的目录。该目录反过来包含至少一个配置文件，告诉Yocto项目如何处理由该层带来的配方，并且与Yocto版本兼容。每一层都包含一组配方。例如，所有配方都包含了如何构建内核模块或镜像的指令，或者是组织系统特定部分的规则。

![](img/527ef1a4e6443ad30b67df9e58b510e1_17_0.png)

**图 4:** 典型层的结构：除了配置文件，主要用于`BitBake`构建的配方。

# 封面故事

## Yocto

| 表 1: 开发计算机 |
|---|
| 处理器 | 64位，8核心 |
| 操作系统 | `Ubuntu 18.04 LTS` |
| 内存 | `8GB` |
| 存储媒体 | `250GB` 空间 |
