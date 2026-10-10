

![](img/3d310cc066dda6e2dfa67a650614076f_309_0.png)

https://installbuilder.bitrock.com/

## 11.2.1 什么是 InstallBuilder

Bitrock 公司的 InstallBuilder 能够创建多平台安装程序和原生设置包。它允许您将应用程序部署到任何环境中。它为每个操作系统提供可靠且专业的安装体验。

这款专业软件提供了原创工具，用于为您的应用程序开发坚固的多平台设置程序。

InstallBuilder 包含许多有用的功能：

- 使用设置脚本语言
- 设置调试器（带有专用脚本语言）。
- 自动更新集成。
- 多语言支持。
- 多语言支持。
- 优化器。
- 多种安装模式（GUI/控制台）。
- 在 Windows、ubuntu 和 macOS 上为您的设置程序提供原生外观和感觉。

InstallBuilder 提供了开发安装程序的完整环境。它允许开发者在不同平台之间保持设置程序的同步。作为商业产品，您将找到丰富的文档（见下文参考链接），关于如何满足您的特定设置约束。

由于该公司专注于设置程序制作领域，Bitrock 的客户支持也可以为您提供宝贵的帮助和建议，以开发您的多平台设置程序。

除了其深思熟虑的用户界面之外，该产品还使用 XML 文件格式来编写每个平台的安装过程脚本，从而允许复用来自 InstallBuilder 用户社区和支持团队的代码片段。

以下是 InstallBuilder 中使用的脚本语言的示例片段。

```xml
<folder>
  <description>OS X Files and scripts</description>
  <destination>${installdir}</destination>
  <name>osxfiles</name>
  <platforms>osx</platforms>
  <distributionFileList>
    <distributionFile>
      <origin>/path/to/osx.cpgz</origin>
    </distributionFile>
    <distributionFile>
      <origin>/path/to/osx-script.sh</origin>
    </distributionFile>
    <distributionFile>
      <origin>/path/to/</origin>
    </distributionFile>
  </distributionFileList>
</folder>
<folder>
  <description>Windows Files and scripts</description>
  <destination>${installdir}</destination>
  <name>windowfiles</name>
  <platforms>windows</platforms>
  <distributionFileList>
    <distributionFile>
      <origin>/path/to/windows.zip</origin>
    </distributionFile>
    <distributionFile>
      <origin>/path/to/windows.script.bat</origin>
    </distributionFile>
  </distributionFileList>
</folder>
```

此脚本片段针对 macOS 和 Windows 系统进行安装。

作为商业产品，一份完整且设计良好的开发者指南可免费获取，以便快速开发适用于每个目标桌面平台的专业外观设置程序（只需一个设置项目）。

- https://installbuilder.bitrock.com/
- https://docs.bitrock.com/

## 11.3 应用程序打包和部署工具的建议

打包对于 .NET Core 3 应用程序的顺利和谐部署至关重要。应用程序的打包将取决于：

- 您要发布的发行版类型：CLR、单个 EXE 或机器原生。
- 您的应用程序依赖的依赖项类型：GTK、QT 等（且您必须在安装程序中包含它们）。
- 您想要支持的平台。
- 部署的上下文：您的软件是商业应用程序？共享软件？还是仅部署在公司电脑上的工具？
- 您希望包含在包中的功能（多语言、自动更新、许可证保护等）。

此列表并不详尽，因为许多项目有其自身的约束条件。

为多平台应用程序选择设置工具的固有复杂性对于每个开发人员（或团队）来说都是一个很大的负担，不应在项目安装程序制作任务中被忽视。

在许多软件开发项目中，特别是在多平台环境中，这一阶段往往被低估，并产生有损已安装应用程序形象的工具体。

我们建议开发团队尽早介入 SDLC（软件开发生命周期），处理他们计划用于应用程序分发和部署的安装程序。

由于这是独立的项目，安装程序编码（是的，设置程序本身就是一个项目）可以在项目编码阶段同时进行。这种工作方式可以验证所选工具是否满足已开发软件的安装要求（依赖项设置、配置检查、环境等）。在专业环境中，可以专门分配资源以专门执行此任务。

在每个平台上使用免费可用的工具将使以原生格式打包的应用程序受益。用户将获得一个完整的解决方案，采用其熟悉的操作系统界面（用于安装程序和应用）。但此解决方案引入了使用多个不同的开发工具，每个操作系统一个，并使安装程序项目乘以目标操作系统的数量。

另一方面，使用工具（如 InstallBuilder）集中管理每个项目（每个目标操作系统一个）可以为项目本身提供更好的连贯性，并简化其管理。然而，此解决方案意味着需要为此特定任务投入不可忽略的预算。

但最重要的是，不要低估熟练的设置程序的价值，不要忘记该程序将是用户与应用程序的第一次接触，这可能产生对应用程序的积极或消极感知。

您必须确保安装程序解决方案为用户带来的效果与您希望用户在使用软件时获得的体验相符。

# .NET Core 3.0

![](img/3d310cc066dda6e2dfa67a650614076f_314_0.png)

## 第 12 章。对所审查解决方案的展望

正如我们在本书中看到的，.NET Core 第三版提供的多平台开发能力简直令人惊叹。尽管 .NET Core 3 不提供任何多平台桌面 GUI API，但现有可供开发者使用的工具已经能够满足其项目的每项要求。

这个新框架深思熟虑的架构提供了足够的灵活性，以应对任何类型的开发者应用需求。

长期以来仅向少数高技术人员开放的多平台开发领域，现在对 C# 开发者社区来说也是可及的。

.NET Core 3 为每个平台（Windows、Linux、macOS）生成原生可执行文件（通过 CoreRT）的能力，同时也提供了使用可执行文件压缩和优化工具的能力，这些工具长期只为精英开发者所专用。

前文中回顾的最新编码技术完美地说明了 .NET Core 3 可以使用的创新解决方案的丰富性。

每个介绍的技术都有其自身的开发历史和起源，这将部分决定其未来的使用和可维护性。

**Terminal.Gui** 在许多情况下可用于提供用户友好的体验，以替代控制台应用程序（控制台应用程序真的不够用户友好，特别是对于主要用户）。您还可以考虑使用它来开发容器化应用程序服务（在专用环境中持续运行），在那里它可以提供直接从执行该服务的容器进行的安全监控能力（在这种情况下，您应该能够访问该容器）。

**Electron.NET** 是 Electron 的一个包装器。Electron 是 Google 推广的工具，用于扩展其 NodeJS 开发环境和社区的应用领域。尚不确定 Google 是否会继续维护该工具，用于与 .NET 一起使用。

