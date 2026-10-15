
# Python IDE（可选）

XBMC 或许是开源媒体中心领域有史以来最重要的事物。它起源于最初的 Xbox 游戏机，自那以后，它已成为多媒体爱好者的事实标准软件。它也被分支为许多其他成功的媒体中心应用，如 Boxee 和 Plex。XBMC 最终成长为一个非常强大的开源应用，背后有稳固的社区支持。它支持几乎所有主要平台，包括不同的硬件架构。它适用于 `Linux`、`Windows`、`Mac OS X`、`Android`、`iOS` 和 `Raspberry Pi`。

在这些页面中，我们将学习如何为 `XBMC` 构建扩展。扩展是一种向 `XBMC` 添加功能的方法，而无需学习 `XBMC` 的核心或以任何方式修改其核心。另一个额外优势是，`XBMC` 使用 `Python` 作为其脚本语言，这也用于构建扩展。由于 `Python` 与组成 `XBMC` 核心的 `C/C++` 等语言相比更容易学习，这真正帮助了新开发者参与该项目。

`XBMC` 支持各种类型的扩展（或插件）：插件、程序和皮肤。插件为 `XBMC` 添加功能。根据功能类型，插件将出现在 `XBMC` 的相应媒体部分。例如，`YouTube` 插件将出现在视频部分。脚本/程序就像 `XBMC` 的迷你应用程序。它们出现在程序部分。皮肤很重要，因为 `XBMC` 是一个完全可定制的应用程序——你可以改变该包几乎所有方面的外观和感觉。

根据你的扩展属于哪个类别，你必须相应地创建扩展目录。例如...

```text
**插件：**
plugin.audio.ludadi: 音频插件
plugin.video.ludadi: 视频插件
script.xxx.xxx: 程序
```

在本教程中，我们将构建一个名为 LUD Entertainer 的 `XBMC` 插件。该插件提供了一种在 `XBMC` 内观看 Reddit 视频的好方法。我们的插件将显示来自 Reddit 的各种内容，如预告片和文化纪录片。我们还允许用户添加自己的 Subreddit。然后，每个视频都可以归类为热门、最新、顶级、争议性等。通过这个插件，我们将展示如何轻松利用 `XBMC` 的内置方法来实现高质量的用户体验。

由于篇幅限制，我们无法在此打印完整代码。我们强烈建议探索封面光盘以访问完整代码，其中还有许多其他令人惊叹的功能。

## 使用 Python 为 XBMC 制作扩展

使用 `Python` 为 `XBMC` 创建新插件

![](img/dd9251551a61a36067892b1cc68615b0_56_0.png)

### 01 准备目录结构

正如我们之前提到的，每种 `XBMC` 扩展类型都遵循特定的目录命名约定。在这种情况下，我们要构建一个*视频*插件，因此插件目录名称将是 `plugin.video.ludlent`。但这只是根目录名称——我们还需要几个其他的文件夹和文件。

以下描述了 LUD Linux Entertainer 的目录结构：

```text
plugin.video.ludlent– 根插件目录
|-- addon.xml
|-- changelog.txt
|-- default.py
|-- icon.png
|-- LICENSE.txt
|-- README
|-- resources
|--- lib
|--- settings.xml
```

### 02 创建 addon.xml

需要在扩展目录的根目录中创建一个 `addon.xml` 文件。`addon.xml` 文件包含 `XBMC` 扩展的主要元数据。它包含关于扩展的概述、致谢、版本信息和依赖项信息。

`addon.xml` 的根元素是 `<addon>` 元素。其定义为：

```xml
<addon id="plugin.video.ludlent" name="LUD HSM Viewer"
version="0.0.1" provider_name="LUUK">
其余内容放置在这里
</addon>
```

在这里，`id` 是插件的标识符，因此它应在所有 `XBMC` 扩展中是唯一的，并且 `id` 也用作目录名称；`version` 告诉 `XBMC` 扩展的版本号，这有助于其提供自动更新的能力——`XBMC` 遵循 Major.Minor.Patch 的版本约定；`name` 是插件的英文标题。

**注意：** 步骤 3 到 5 涵盖了需要在 `addon.xml` 文件内添加的条目。

### 03 添加依赖项信息

扩展内部的依赖项使用 `<requires>` 元素进行管理。

```xml
<import addon="xbmc.python" version="2.1.0"/>
<import addon="plugin.video.youtube" version="3.0.0"/>
<import addon="plugin.video.vimeo" version="2.3.0"/>
<import addon="plugin.video.dailymotion_com" version="1.0.0"/>
</requires>
```

在上面的代码中，我们添加了一个名为 `xbmc.python` 版本 2.1 的库的依赖项。目前，它是作为强制依赖项添加的。要使依赖项变为可选，你需要添加 `optional="true"`；例如 `<import addon="kumal.special" version="0.1.0" optional="true"/>`

在上例中，我们将核心依赖项 `xbmc.python` 添加为 2.1.0，因为这是随 `XBMC` 版本 Frondo 12.0 和 12.1 一起发布的版本。如果你将 `xbmc.python` 添加为 2.0，那么它仅在 `XBMC` Eden 11.0 中有效，而在最新版本中无效。

对于当前版本的 `XBMC` 12.1，随附的核心 `XBMC` 组件版本如下：

```text
xbmc.python 2.1.0
xbmc.gui 4.0.0
xbmc.json 6.0.0
xbmc.metadata 2.1.0
xbmc.addon 12.0.0
```

除了 `xbmc.python` 之外，我们还添加了一些第三方插件作为依赖项，例如 `plugin.video.youtube`。当我们安装 `plugin.video.ludlent` 时，这些插件将自动安装。

### 04 设置提供者和入口点

我们的扩展旨在为 `XBMC` 提供视频内容。为了传达这一点，我们必须设置以下元素：

```xml
<extension point="xbmc.plugin.source" library="default.py">
<provides>video</provides>
</extension>
```

在这里，`library` 属性设置了插件的入口点。在这个例子中，当用户激活插件时，`default.py` 将被执行。`<provides>` 元素设置了它提供的媒体类型。这也反映在插件的放置位置上。由于我们的是一个视频插件，它将显示在 `XBMC` 的视频部分。

### 05 设置插件元数据

关于插件的元数据在 `<extension point="xbmc.addon.metadata">` 中提供。以下是重要元素...

- **<platforms>:** 大多数时候，`XBMC` 扩展都是跨平台兼容的。然而，如果你依赖于仅在特定平台上可用的原生平台库，那么你需要在这里设置支持的平台。平台的接受值为：all, linux, osx, osx32, osx64, ios (Apple iOS), win32 (Windows DirectX), win64 (Windows OpenGL) 和 android。

- **<summary lang="en">:** 这提供了插件的简要描述。我们的示例将语言属性设置为英文，但你也可以使用其他语言。

- **<description>:** 插件的详细描述。

- **<website>:** 托管该插件的网页。

- **<source>:** 源代码仓库 URL。如果你在 GitHub 上托管你的插件，可以在这里提及仓库 URL。

- **<forum>:** 你的插件的讨论论坛 URL。

- **<email>:** 作者电子邮件。你可以直接输入电子邮件，或使用对机器人友好的电子邮件地址，例如 **max** at domain dot com。

### 06 设置更新日志、图标、扇形艺术和许可证

我们需要在插件目录中额外添加几个文件...

- **changelog.txt:** 你应该列出你的插件在不同版本之间所做的更改。更新日志可从 `XBMC` UI 中查看。

  更新日志示例：

  - 初始发布

  - 修复视频缓冲问题

- **icon.png:** 这将在 `XBMC` UI 中代表该插件。它必须是一个非透明的 **PNG** 文件，大小为 256x256。
