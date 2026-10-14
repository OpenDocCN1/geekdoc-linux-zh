
现在你有所有这些数据进来，你要怎么做？你需要能够移动世界中的执行器并产生实际的效果。这可能是用于轮子或履带的电机，用于移动物体的杠杆，或者潜在的完整肢体，如手臂或腿。虽然你可以尝试直接通过计算机的输出端口驱动这些类型的电子设备，但通常没有足够的电流来提供所需的功率。因此，你需要有一些板外的“大脑”能够处理向这些设备供电。Arduino 是承担这一任务的最受欢迎的候选者之一。

幸运的是，Arduino 设计为连接到计算机的串行端口，因此你可以简单地使用 `pySerial` 与它对话。你可以向你编写并上传到 Arduino 的代码发送指令，以处理各种执行器的实际操作。然而，Arduino 可以回应。这意味着你可以读取反馈数据，看看你的动作产生了什么效果。你的轮子转动到你想要的程度了吗？这意味着你还可以将 Arduino 用作你的传感器和计算机之间的接口，从而进一步简化你的 Python 代码。也有大量的附加模块可用，它们可能能够直接提供你所需的感知功能。此外，还有几种型号的 Arduino，因此你可能会找到最适合你需求的专用型号。

现在你有所有这些数据进来以及在实际世界中行动的能力，最后一步是给你的机器人一些“大脑”。不幸的是，目前的技术水平并未达到 R2-D2 或 C-3PO 的幻想。你大部分实际的创新编码工作很可能会发生在机器人的这一部分。这个术语通常称为人工智能。目前有几个正在进行的项目，你可以将它们作为起点，赋予你的机器人一些真正的推理能力，如 `SimpleAI` 或 `PyBrain`。

## 绕过 GIL

对于机器人工作，你可能需要在多个 CPU 上真正并行运行一些代码。Python 目前有 GIL，这意味着解释器中内置了一个根本性的瓶颈。绕过它的一种方法是实际运行多个 Python 解释器，每个执行线程一个。另一个选项是从 Python 转向 Jython 或 IronPython，因为它们都没有 GIL。

![](img/e016e192a91ffc1a9e474690a590742f_73_0.png)

## 使用 Python 为 XBMC 制作扩展

Python 是全球最流行的易用的开源语言。学习如何使用它来构建 XBMC 的功能，XBMC 是全球最受喜爱的 FOSS（自由及开源软件）媒体中心

## 资源

- XBMC: www.xbmc.org/download
- Python 2.7x
- Python IDE（可选）
- Code on FileSilo（位于 FileSilo 的代码）

XBMC 也许是开源媒体中心领域发生过的重要事件中最关键的一个。它最初诞生于初代 Xbox 游戏机，自那以后，它已成为多媒体爱好者的事实标准软件。它也被分支为许多其他成功的媒体中心应用程序，如 Boose 和 Plex。最终，XBMC 发展成为一个非常强大的开源应用程序，背后有一个坚实的社区支持。它支持几乎所有主要平台，包括不同的硬件架构。它可用于 Linux、Windows、mac OS、Android、iOS 和 Raspberry Pi。

在这些页面中，我们将学习如何为 XBMC 构建扩展。扩展是一种在不学习 XBMC 核心或不以任何方式修改该核心的情况下，为 XBMC 添加功能的方法。一个额外的优势是 XBMC 使用 Python 作为其脚本语言，而这也同样可用于构建扩展。由于与 C/C++（XBMC 核心的编程语言）相比，Python 更容易学习，这真的有助于新开发人员参与到该项目中。

XBMC 支持各种类型的扩展（或 Add-ons）：插件（Plugins）、程序（Programs）和皮肤（Skins）。插件为 XBMC 添加功能。根据功能类型，插件将出现在 XBMC 的相关媒体部分。例如，YouTube 插件将出现在视频部分。脚本/程序就像 XBMC 的迷你应用程序。它们出现在程序部分。皮肤非常重要，因为 XBMC 是一个完全可定制的应用程序——你可以改变软件包几乎每个方面的外观和感觉。根据你的扩展所属的类别，你需要相应地创建扩展目录。例如...

### 插件。

- `plugin.audio.ludiaudi`：音频插件
- `plugin.video.ludvidi`：视频插件
- `script.xxx.xxx`：程序

在本教程中，我们将构建一个名为 LUD Entertainer 的 XBMC 插件。该插件提供了一种从 XBMC 内部观看 Reddit 视频的绝佳方式。我们的插件将显示来自 Reddit 的各种内容，如预告片 và 纪录片。我们还将允许用户添加他们自己的 Subreddit。然后，每个视频都可以归类为 Hot（热门）、New（最新）、Top（置顶）、Controversial（争议）等。通过这个插件，我们将演示如何轻松地接入 XBMC 内置的方法，以实现非常高质量的用户体验。

由于篇幅限制，我们无法在此处打印完整代码。我们建议从 FileSilo 下载完整代码。

## 01 准备目录结构

正如我们之前提到的，每种 XBMC 扩展类型都遵循特定的目录命名约定。在这种情况下，我们正在构建一个视频插件，因此插件目录名称应为 `plugin.video.luddent`。但这只是根目录的名称——我们还需要其他几个文件夹和文件。

以下描述了 LUD Linux Entertainer 的目录结构：

```text
plugin.video.luddent – 根插件目录
├── addon.xml
├── changelog.txt
├── default.py
├── icon.png
├── LICENSE.txt
├── README
├── resources
├── lib
└── settings.xml
```

## 02 创建 addon.xml

需要在扩展目录的根目录下创建一个 `addon.xml` 文件。`addon.xml` 文件包含 XBMC 扩展的主要元数据。它包含有关扩展的概述、credits（致谢）、版本信息和依赖信息。

`addon.xml` 的根元素是 `<addon>` 元素。它定义为：

```xml
<addon id="plugin.video.luddent" name="LUD HSW Viwer" version="0.0.1" provider:name="LUDD">其余内容放置在这里</addon>
```

在这里，`id` 是插件的标识符，因此它应在所有 XBMC 扩展中保持唯一，并且也用于目录名称；`version` 告知 XBMC 扩展的版本号，这有助于其提供自动更新的能力——XBMC 遵循 Major.Minor.Patch（主.次.补丁）的版本命名约定；`name` 是插件的英文标题。

**注意：** 步骤 3 到 5 涵盖了需要添加到 `addon.xml` 文件中的条目。

## 03 添加依赖信息

扩展内部的依赖关系使用 `<requires>` 元素进行管理。

```xml
<requires>
<import addon="xbmc.python" version="2.1.0"/>
<import addon="plugin.video.youtube" version="3.0.0"/>
<import addon="plugin.video.version="2.3.0"/>
<import addon="plugin.video.dailymotion.com" version="1.0.0"/>
</requires>
```

在上面的代码中，我们添加了对版本为 2.1 的名为 `xbmc.python` 的库的依赖。目前，它被添加为强制依赖项。要使依赖项变为可选，你需要添加 `optional="true"`，例如 `<import addon="kunal.special" version="0.1.0" optional="true"/>`

在上面的示例中，我们将核心依赖 `xbmc.python` 设置为 2.1.0，因为这是随 XBMC 版本 Frodo 12.0 和 12.1 一起发布的版本。如果你将 `xbmc.python` 设置为 2.0，那么它只在 XBMC Eden 11.0 中有效，而在最新版本中无效。

对于当前版本的 XBMC 12.1，发布的 XBMC 核心组件版本如下：`xbmc.python` 2.1.0, `xbmc.gui` 4.0.0, `xbmc.json` 6.0.0, `xbmc.python` 2.1.0, `xbmc.metadata` 12.0.0

除了 `xbmc.python`，我们还添加了一些第三方插件作为依赖项，例如 `plugin.video.youtube`。当我们安装 `plugin.video.luddent` 时，这些插件将自动安装。

## 04 设置提供者和入口点

我们的扩展旨在为 XBMC 提供视频内容。为了传达这一点，我们必须设置以下元素：

```xml
<extension point="xbmc.python.pluginsource" library="default.py">
<provides>videos</provides>
</extension>
```
