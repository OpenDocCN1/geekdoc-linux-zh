# 精通 Linux Mint 22：安装、配置与高级功能完全指南



![](img/image_rsrc722.jpg)


![自动生成的 Logo 特写描述](img/image_rsrc723.jpg)


# 免责声明

《精通 Linux Mint 22》（以下简称“本书”）包含的信息仅供通用参考。作者和出版商已尽最大努力确保截至出版之日本书中信息的准确性和完整性。

然而，软件、技术和信息技术领域正在不断演进。因此，作者和出版者对于书中内容针对任何目的的完整性、准确性、可靠性、适用性或可用性不作任何明示或暗示的陈述或保证。读者对此类信息的任何依赖均须自担风险。

出版商和作者均不对因本文包含的信息或程序直接或间接导致（或声称导致）的任何损失或意外损害或后果性损害承担任何责任。

本书不作为具有适当资格和执照的专业人士或技术人员建议的替代。如果需要专业协助，应寻求胜任专业人士的服务。

已尽一切使本书书尽可能完整和准确，但不隐含任何保证或适用性。信息按“原样”提供。

作者和出版商对于因使用和应用本书的任何内容而直接或间接导致的任何责任、损失或风险（个人或其他），均不承担任何责任或法律责任。

# 致谢

感谢我的家人，没有他们，这一切将都不可能实现。

Linus Torvalds 是 Linux 的创建者和 Linux 商标的持有者，特此对此致谢，他并不支持或赞助这本自学类书籍。

Linux® 是 Linus Torvalds 在美国及其他国家的注册商标。

感谢 Linux Mark Institute 和社区开发并维护 Linux Mint。

感谢暴雪娱乐（Blizzard）开发并发布我真正热爱并享受的《魔兽世界》。

感谢 WINE（Wine Is Not An Emulator）提供的兼容层。

感谢 Lutris 让安装和运行游戏及软件变得更加方便。

感谢 Gabe Newell 和 Valve 公司（Valve）开发并发布 Steam 商店。

本书采用的阅读障碍友好版本使用的 OpenDyslexic 字体由 Abbie Gonzalez 制作，位于 `https://antijingoist.gumroad.com/l/OpenDyslexic` 和 `https://opendyslexic.org/`。

3. 选择 `FLATPAK` 并点击安装。

## 在终端通过 FLATPAK 安装 Mailspring：
```bash
flatpak install flathub com.getmailspring.Mailspring
```

## 在终端通过 SNAP 安装 Mailspring：
```bash
sudo snap install mailspring
```

# 图像编辑软件

图像编辑软件允许您通过裁剪、修饰和色彩调整来处理数字照片。它包含了矢量、位图和 3D 建模工具，用于增强或从零创建图像。它主要用于 2D 编辑，支持缩放大小和应用过滤器以调整属性或添加效果等任务，还方便了格式转换。

GIMP（GNU 图像处理程序）是一款用于照片编辑和图像合成的免费工具。它提供了绘画工具、图层支持以及具有全 Alpha 通道支持的高级处理功能。GIMP 可以通过插件和脚本进行扩展，可在多种平台上运行并支持许多文件格式，适用于简单和复杂的编辑需求。

Blender 是一款免费、开源的 3D 创作套件，用于建模、动画、特效和视频剪辑。它运行在 Linux、macOS 和 Windows 上，兼顾专业人士和爱好者的需求。凭借全面的工具，Blender 支持从游戏资产到电影的各种媒体制作。其由 `OpenGL` 驱动的界面确保了跨设备的一致体验，而其活跃的社区提供了广泛的支持和学习资源。

Pinta 是一款开源、跨平台的图像编辑器，类似于 Paint.NET，但功能更多。它为位图图像编辑提供了一个强大的工具箱，包括绘图工具、过滤器、色彩调整和用于复杂编辑的多个图层。它设计直观易用，包含无限次数的撤销历史、多语言支持和可自定义的工作区，成为一个既易于用又强大的编辑解决方案。

Krita 是一款专为数字艺术家和动画师设计的多功能、免费开源图形编辑器。它在 Linux、Windows 和 macOS 上提供用于 2D 动画和艺术创作的工具。Krita 具有 `OpenGL` 加速的画布、拥有 100 多种预载笔刷的高级笔刷引擎、非破坏性图层、矢量支持和可自定义界面。它还包含用于平滑笔触的笔刷稳定器、用于漫画的内置矢量工具以及用于共享或导入笔刷的管理器，是追求灵活性和精度的创者的强大工具。

Inkscape 是一款免费开源的矢量图形编辑器，运行在包括 Windows、macOS 和 Unix 类系统在多种平台上。得益于其矢量方法，它擅长创建清晰、可缩放的插图（如卡通、标志和图表），且没有像素限制。Inkscape 支持 `SVG` 作为主要格式，处理许多文件类型，并提供用于形状、文本、颜色和渐变的复杂设计工具，同时允许直接从位图源转换并编辑为矢量艺术。

Darktable 是一款免费开源的摄影应用和 RAW 开发工具，专注于非破坏性后期处理。它优化了工作流，可在各种平台上高效处理大量图像。通过实时调整、`GPU` 加速和对多种图像格式的支持等功能，Darktable 通过色彩校、效果和组织模块增强了图像编辑。它支持非破坏性编辑、`ICC` 配置和用于自定义的 `Lua` 脚本，其 UI 包含轻型模式和暗房模式以便于导航和编辑，此外还有快照和地图视图，可进行全面的图像管理。

Tux Paint 是一款专为 3 到 12 岁儿童设计的免费开源绘画软件。由 Bill Kendrick 于 2002 年创建，提供充满趣味特效和绘图工具的简单界面，以激发儿童的创造力。Tux Paint 支持 Windows、macOS 和 Android 等多个平台，在全球范围内可用。在吉祥物 Tux 的引导下，孩子们可以通过各种工具和效果探索艺术，而教师和家长可以使用额外内容自定义体验。Tux Paint 是培养计算机素养和艺术技能的理想选择，因其易用性和容性设计而闻名。

## Gnu 图像处理程序 (GIMP)

访问官方网站 [`www.gimp.org/`](https://www.gimp.org/) 获取有关 GIMP 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 Gnu 图像处理程序 (GIMP)：

1. 打开软件管理器并搜索 Gnu 图像处理程序 (GIMP)。
2. 点击 Gnu 图像处理程序 (GIMP)，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Gnu 图像处理程序 (GIMP)：
```bash
sudo apt install gimp
```

### 在终端通过 FLATPAK 安装 Gnu 图像处理程序 (GIMP)：
```bash
flatpak install flathub org.gimp.GIMP
```

### 在终端通过 SNAP 安装 Gnu 图像处理程序 (GIMP)：
```bash
sudo snap install gimp
```

## Blender

访问官方网站 [`www.blender.org/`](https://www.blender.org/) 获取关于 Blender 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 Blender：

1. 打开软件管理器并搜索 Blender。
2. 点击 Blender，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Blender：
```bash
sudo apt install blender
```

### 在终端通过 FLATPAK 安装 Blender：
```bash
flatpak install flathub org.blender.Blender
```

### 在终端通过 SNAP 安装 Blender：
```bash
sudo snap install blender --classic
```

## Pinta

访问官方网站 [`www.pinta-project.com/`](https://www.pinta-project.com/) 获取关于 Pinta 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 Pinta：

1. 打开软件管理器并搜索 Pinta。
2. 点击 Pinta，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。





## Pinta

### 通过终端通过 APT 安装 Pinta：
```bash
sudo apt install pinta
```

### 通过终端通过 FLATPAK 安装 Pinta：
```bash
flatpak install flathub com.github.PintaProject.Pinta
```

### 通过终端通过 SNAP 安装 Pinta：
```bash
sudo snap install pinta
```

## Krita

访问 Krita 官方网站 [`krita.org/en/`](https://krita.org/en/) 了解关于 Krita 的所有信息。

### 通过软件管理器通过系统软件包/FLATPAK 包安装 Krita：
1. 打开软件管理器并搜索 Krita。
2. 点击 Krita，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Krita：
```bash
sudo apt install krita
```

### 通过终端通过 FLATPAK 安装 Krita：
```bash
flatpak install flathub org.kde.krita
```

### 通过终端通过 SNAP 安装 Krita：
```bash
sudo snap install krita
```

## Inkscape

访问 Inkscape 官方网站 [`inkscape.org/`](https://inkscape.org/) 了解关于 Inkscape 的所有信息。

### 通过软件管理器通过系统软件包/FLATPAK 包安装 Inkscape：
1. 打开软件管理器并搜索 Inkscape。
2. 点击 Inkscape，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Inkscape：
```bash
sudo apt install inkscape
```

### 通过终端通过 FLATPAK 安装 Inkscape：
```bash
flatpak install flathub org.inkscape.Inkscape
```

### 通过终端通过 SNAP 安装 Inkscape：
```bash
sudo snap install inkscape
```

## Darktable

访问 Darktable 官方网站 [`www.darktable.org/`](https://www.darktable.org/) 了解关于 Darktable 的所有信息。

### 通过软件管理器通过系统软件包/FLATPAK 包安装 Darktable：
1. 打开软件管理器并搜索 Darktable。
2. 点击 Darktable，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Darktable：
```bash
sudo apt install darktable
```

### 通过终端通过 FLATPAK 安装 Darktable：
```bash
flatpak install flathub org.darktable.Darktable
```

### 通过终端通过 SNAP 安装 Darktable：
```bash
sudo snap install darktable
```

## Tuxpaint

访问 Tuxpaint 官方网站 [`tuxpaint.org/`](https://tuxpaint.org/) 了解关于 Tuxpaint 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Tuxpaint：
1. 打开软件管理器并搜索 Tuxpaint。
2. 点击 Tuxpaint，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

### 通过终端通过 FLATPAK 安装 Tuxpaint：
```bash
flatpak install flathub org.tuxpaint.Tuxpaint
```

# 音频编辑软件

音频编辑软件允许您编辑和创建音频、导入和导出文件、录制声音以及调整时间和音量。它还允许混合轨道、应用混响和均衡等效果，并在文件格式之间进行转换。数字音频工作站提供了具有用户友好界面的全面音乐制作软件，能够非线性编辑以及实时和离线处理以实现专业音质。

Audacity 是一款适用于 Windows、macOS、Linux 和 Unix 类系统的免费开源音频编辑器和录音器。自 2015 年以来下载量超过 11.4 亿次，因其对主流系统的兼容性、对各种音频格式的支持以及配合 `VST3` 等插件的能力而广受欢迎。Audacity 采用 `GPL-2.0-or-later` 许可，还提供深度频率可视化工具，是音频编辑和录制的理想选择。

Ardour 是一款用于在 Linux、macOS 和 Windows 上进行录音、编辑和母带数字音频工作站。由 Paul Davis 创建，根据硬件提供无限可能，包括延迟校正、各种监控选项和插件效果。Ardour 支持无限轨道、总线和灵活的路由。其编辑功能包括高精度的拖放、裁剪、分割和时间拉伸。Ardour 在母带方面表现出色，与 `JACK` 集成用于高级处理，并支持导出音频 CD 文件。

Mixxx 是一款免费开源 DJ 软件，用于创造性地混合数字音乐文件，适用于所有水平的 DJ。它具有用于轨道匹配的 BPM 和键位检测功能，支持最多四首歌同步，支持各种 DJ 控制器并允许自定义映射。使用音效增加趣味并进行链以发挥创意。使用时间码胶片获得经典感。Mixxx 由一个专注的社区开发，是对于渴望免费进行数字混合的 DJ 来说完美选择。

## Audacity

访问 Audacity 官方网站 [`www.audacityteam.org/`](https://www.audacityteam.org/) 了解关于 Audacity 的所有信息。

### 通过软件管理器通过系统软件包/FLATPAK 包安装 Audacity：
1. 打开软件管理器并搜索 Audacity。
2. 点击 Audacity，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Audacity：
```bash
sudo apt install audacity
```

### 通过终端通过 FLATPAK 安装 Audacity：
```bash
flatpak install flathub org.audacityteam.Audacity
```

### 通过终端通过 SNAP 安装 Audacity：
```bash
sudo snap install audacity
```

## Ardour

访问 Ardour 官方网站 [`ardour.org/`](https://ardour.org/) 了解关于 Ardour 的所有信息。

### 通过软件管理器通过系统软件包/FLATPAK 包安装 Ardour：
1. 打开软件管理器并搜索 Ardour。
2. 点击 Ardour，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Ardour：
```bash
sudo apt install ardour
```

### 通过终端通过 FLATPAK 安装 Ardour：
```bash
flatpak install flathub org.ardour.Ardour
```

## MIXXX

访问 Mixxx 官方网站 [`mixxx.org/`](https://mixxx.org/) 了解关于 Mixxx 的所有信息。

### 通过软件管理器通过 RPM/FLATPAK 包安装 MIXXX：
1. 打开软件管理器并搜索 MIXXX。
2. 点击 MIXXX，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

### 通过终端通过 FLATPAK 安装 MIXXX：
```bash
flatpak install flathub org.mixxx.Mixxx
```

### 通过终端通过 SNAP 安装 MIXXX：
```bash
sudo snap install mixxx-community
```

# 视频编辑软件

视频编辑软件是处理视频片段、添加音乐和调整时间的本质工具。它对于制作电影、电视节目、广告和视频随笔至关重要，使得编辑过程在个人电脑上变得可行。该软件支持将视频切割成部分、叠加音轨并将最终产品导出为视频文件。从专业人士到爱好者，它都允许用户精炼他们的视频作品，实现广泛的风格和应用。

OpenShot 是一款适用于 Linux、macOS、Windows 和 ChromeOS 的免费开源视频编辑器，由 Jonathan Thomas 于 2008 年发布。它提供了跨平台编辑功能并通过 `FFmpeg` 支持各种格式。OpenShot 支持无限数量的轨道和层，能够应对复杂项目。关键特性包括用于平滑过渡的基于曲线的关键帧动画、易于使用的拖放功能以及适应不同项目比例的剪辑缩放。此外，它还提供了视频转场、合成、结合 Blender 的 3D 标题、高级时间线控制、帧精确度、速度更改、音频混合以及用于绿幕效果的色度键等数字效果。

Kdenlive 是另一款开源视频编辑器，始于 2003 年。它支持多轨道编辑并使用 `FFmpeg` 提供广泛的格式支持。其界面和快捷键可以自定义以增强用户体验。Kdenlive 包含一个用于创建字幕和标题的标题器、许多效果和转场以增添专业感。它提供代理编辑以提高工作流效率、防止数据丢失的自动备份、用于额外支持的在线资源、用于实时编辑的时间线预览、用于动态变化的关键帧效果，以及用于个性化的可主题界面。Kdenlive 由一个小型而专注的团队开发，适用于基础和专业的视频编辑任务。





Shotcut 是一款适用于 FreeBSD、Linux、macOS 和 Windows 的免费开源视频编辑器，由 Dan Dennedy 于 2011 年创建。它通过 `FFmpeg` 支持广泛的格式并提供多轨道编辑。Shotcut 具有 GPU 加速处理功能以提高渲染速度、视频和音频过滤器以增强效果，并支持摄像头和音频捕捉进行直接录制。它可以处理网络流播放，并提供高级编辑工具，如用于调整视频色调和氛围的调色、用于动画效果的关键帧、用于跟踪对象的运动跟踪，并支持 Blackmagic Design 等专业硬件输入。Shotcut 的多功能性批量编码选项（确保输出一致）以及维护质量的完整性检查使其成为初学者和专业人士的理想选择。

Pitivi 是一款适用于 Linux 的免费开源视频编辑器，为新手和专业人士提供了直观且高效的编辑体验。它支持无限视频和音频轨道，允许处理复杂项目。Pitivi 包含完整的撤销/重做功能以便轻松纠正错误、用于动态变化的关键帧效果，并通过 `GStreamer` 导入各种格式以实现广泛的兼容性。Pitivi 遵循 `GNOME` 指南设计，通过用于精确编辑的帧进、用于删除不需要部分的剪辑以及平衡音频的混音等功能确保了易用性。它是社区驱动的，强调可用性和多媒体创新，提供了一个强大的编辑平台。

## OpenShot

访问 OpenShot 官方网站 [`www.openshot.org/`](https://www.openshot.org/) 了解有关 OpenShot 的所有信息。

### 通过软件管理器通过系统安装包/FLATPAK 包安装 OpenShot：
1. 打开软件管理器并搜索 OpenShot。
2. 点击 OpenShot，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 OpenShot：
```bash
sudo apt install openshot-qt
```

### 在终端通过 FLATPAK 安装 OpenShot：
```bash
flatpak install flathub org.openshot.OpenShot
```

### 在终端通过 SNAP 安装 OpenShot：
```bash
sudo snap install openshot-community
```

## Kdenlive

访问 Kdenlive 官方网站 [`kdenlive.org/en/`](https://kdenlive.org/en/) 了解有关 Kdenlive 的所有信息。

### 通过软件管理器通过系统安装包/FLATPAK 包安装 Kdenlive：
1. 打开软件管理器并搜索 Kdenlive。
2. 点击 Kdenlive，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Kdenlive：
```bash
sudo apt install kdenlive
```

### 在终端通过 FLATPAK 安装 Kdenlive：
```bash
flatpak install flathub org.kde.kdenlive
```

### 在终端通过 SNAP 安装 Kdenlive：
```bash
sudo snap install kdenlive
```

## Shotcut

访问 Shotcut 官方网站 [`www.shotcut.org/`](https://www.shotcut.org/) 了解有关 Shotcut 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Shotcut：
1. 打开软件管理器并搜索 Shotcut。
2. 点击 Shotcut，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

### 在终端通过 FLATPAK 安装 Shotcut：
```bash
flatpak install flathub org.kde.Shotcut
```

### 在终端通过 SNAP 安装 Shotcut：
```bash
sudo snap install shotcut
```

## Pitivi

访问 Pitivi 官方网站 [`www.pitivi.org/`](https://www.pitivi.org/) 了解有关 Pitivi 的所有信息。

### 通过软件管理器通过系统安装包/FLATPAK 包安装 Pitivi：
1. 打开软件管理器并搜索 Pitivi。
2. 点击 Pitivi，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Pitivi：
```bash
sudo apt install pitivi
```

### 在终端通过 FLATPAK 安装 Pitivi：
```bash
flatpak install flathub org.pitivi.Pitivi
```

# 集成开发环境 (IDE)

集成开发环境 (IDE) 是某种软件工具，通过结合代码编辑器、调试器和构建自动化工具来简化软件开发。流行的 IDE（如 `IntelliJ IDEA` 和 `Eclipse`）通常包含编译器或解释器，简化了开发过程。它们还集成了版本控制和 GUI 构建工具，通过统一的界面提高了生产力。IDE 支持多种编程语言，其中某些是针对特定语言定制的。现代 IDE 通常是图形化的，尽管过去存在过文本版本。

Visual Studio Code 由微软创建，是一款适用于 Windows、Linux 和 macOS 的多功能源代码编辑器。它提供调试、语法高亮和智能代码补全，支持许多编程语言。可以通过中心存储库中的主题、快捷键和扩展进行个性化。尽管它会收集使用数据，但其开源性质确保了透明度。它在没有传统项目系统的情况下运行，允许将目录打开并保存为工作区，支持广泛的语言扩展。

VSCodium 是微软 VS Code 编辑器的社区驱动开源版本，没有遥测和品牌标识。它在保留相同功能的同时，通过移除跟踪功能尊重了用户的隐私和自由。VSCodium 简化了获取 VS Code 优势的途径，无需从源码编译，并在 `MIT` 许可证下二进制文件。它解决了对软件自由和隐私的担忧，确保所有人都能获得最新、干净的 VS Code 版本。

Atom 是 GitHub 开发的一款适用于 macOS、Linux 和 Windows 的免费开源文本和源代码编辑器。它于 2015 年发布，因其使用 HTML、CSS 和 JavaScript 的自定义能力而受到赞誉。它构建在 `Electron` 框架上，支持 JavaScript 插件并嵌入 Git 控制。尽管已退役，Atom 作为为开发者提供的多功能且易用编辑器的遗产依然存在。

Geany 是一款免费开源的轻量级文本编辑器，具有基本的 IDE 功能，为速度设计，依赖项极少。它支持许多编程语言和标记语言，提供语法高亮、代码折叠、自动补全和项目管理。Geany 跨操作系统工作，包括 BSD、Linux、macOS、Solaris 和 Windows，尽管其 Windows 版本除非用户添加，否则缺少某些 Unix 的工具。与传统的 Unix 编辑器不同，Geany 类似于 `Notepad++` 等 Windows 编辑器，使用 `Scintilla` 和 `GTK` 构建界面。

Bluefish 是一款面向程序员和 Web 开发人员的强大编辑器，支持多种编程和标记语言。它在 `GNU GPL` 许可证下开源，运行在 Linux、macOS 和 Windows 等多个平台上。Bluefish 以其速度、轻量设计和高效处理大量文档的能力而出。它提供项目支持、多线程远程文件编辑、强大的搜索和替换、快速代码片段以及与外部程序的集成。此外，它具有可自定义的语言支持、行内拼写检查、自动恢复和站点管理工具，是编码和 Web 开发的全面工具。

## Visual Studio Code

要探索有关 Visual Studio Code 的所有信息，请访问其官方网站 [`code.visualstudio.com/`](https://code.visualstudio.com/)。

### 通过软件管理器通过 FLATPAK 包安装 Visual Studio Code：
1. 打开软件管理器并搜索 Visual Studio Code。
2. 点击 Visual Studio Code，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Visual Studio Code：
```bash
sudo apt install wget gpg apt-transport-https
wget -qO- https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > packages.microsoft.gpg
sudo install -D -o root -g root -m 644 packages.microsoft.gpg /etc/apt/keyrings/packages.microsoft.gpg
```





## Visual Studio Code

```bash
echo "deb [arch=amd64,arm64,armhf signed-by=/etc/apt/keyrings/packages.microsoft.gpg] https://packages.microsoft.com/repos/code stable main" |sudo tee /etc/apt/sources.list.d/vscode.list > /dev/null

sudo apt update && sudo apt install code
```

### 通过终端通过 FLATPAK 安装 Visual Studio Code：
```bash
flatpak install flathub com.visualstudio.code
```

### 通过终端通过 SNAP 安装 Visual Studio Code：
```bash
sudo snap install code --classic
```

### 通过图形界面通过 .deb 安装 Visual Studio Code：
访问发布页面：[`code.visualstudio.com/download`](https://code.visualstudio.com/download)

滚动到带有 Linux 企鹅 Tux 的部分。

点击 `.deb` 下载链接以获取 Debian 包文件。

下载后，进入你的 `Downloads` 目录：
找到下载的 Debian 包文件，文件名类似于 `code_1.90.1-1718141439_amd64.deb`。

双击 `.deb` 包文件启动安装过程。
按照屏幕上的说明操作，并在提示时点击“Install”（安装）。

## VSCodium

访问 VSCodium 官网 [`vscodium.com/`](https://vscodium.com/) 了解关于 VSCodium 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 VSCodium：
1. 打开 `Software Manager`（软件管理器）并搜索 `VSCodium`。
2. 点击 `VSCodium`，然后点击 `Source Selection Box`源选择框）。
3. 选择 `FLATPAK` 并点击 `Install`安装）。

### 通过终端通过 APT 安装 VSCodium：
```bash
wget -qO - https://gitlab.com/paulcarroty/vscodium-deb-rpm-repo/raw/master/pub.gpg \
| gpg --dearmor \
| sudo dd of=/usr/share/keyrings/vscodium-archive-keyring.gpg

echo 'deb [ signed-by=/usr/share/keyrings/vscodium-archive-keyring.gpg ] https://download.vscodium.com/debs vscodium main' \
| sudo tee /etc/apt/sources.list.d/vscodium.list

sudo apt update && sudo apt install codium
```

### 通过终端通过 FLATPAK 安装 VSCodium：
```bash
flatpak install flathub com.vscodium.codium
```

### 通过终端通过 SNAP 安装 VSCodium：
```bash
sudo snap install codium --classic
```

### 通过图形界面通过 .deb 安装 VSCodium：
访问发布页面：[`github.com/VSCodium/vscodium/releases`](https://github.com/VSCodium/vscodium/releases)

滚动到最新版本部分。

点击 `amd64.deb` 下载链接以获取 Debian 包文件。

下载后，进入你的 `Downloads` 目录：
找到下载的 Debian 包文件，文件名类似于 `codium_1.90.1.24165_amd64.deb`。

双击 `.deb` 包文件启动安装过程。
按照屏幕上的说明操作，并在提示时点击“Install”（安装）。

## Atom

访问 Atom 官网 [`atom-editor.cc/`](https://atom-editor.cc/) 了解关于 Atom 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Atom：
1. 打开 `Software Manager`（软件管理器）并搜索 `Atom`。
2. 点击 `Atom`，然后点击 `Source Selection Box`源选择框）。
3. 选择 `FLATPAK` 并点击 `Install`安装）。

### 通过终端通过 FLATPAK 安装 Atom：
```bash
flatpak install flathub io.atom.Atom
```

### 通过图形界面通过 .deb 安装 Atom：
访问发布页面：[`github.com/atom/atom/releases/tag/v1.60.0`](https://github.com/atom/atom/releases/tag/v1.60.0)

滚动到最新版本部分。

点击 `amd64.deb` 下载链接以获取 Debian 包文件。

下载后，进入你的 `Downloads` 目录：
找到下载的 Debian 包文件，文件名类似于 `atom-amd64.deb`。

双击 `.deb` 包文件启动安装过程。
按照屏幕上的说明操作，并在提示时点击“Install”（安装）。

## Geany

访问 Geany 官网 [`geany.org/`](https://geany.org/) 了解关于 Geany 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Geany：
1. 打开 `Software Manager`（软件管理器）并搜索 `Geany`。
2. 点击 `Geany`，然后点击 `Source Selection Box`源选择框）。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击 `Install`安装）。

### 通过终端通过 APT 安装 Geany：
```bash
sudo apt install geany
```

### 通过终端通过 FLATPAK 安装 Geany：
```bash
flatpak install flathub org.geany.Geany
```

### 通过终端通过 SNAP 安装 Geany：
```bash
sudo snap install geany --channel=latest/edge
```

## Bluefish

访问 Bluefish 官网 [`bluefish.openoffice.nl/index.html`](https://bluefish.openoffice.nl/index.html) 了解关于 Bluefish 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Bluefish：
1. 打开 `Software Manager`（软件管理器）并搜索 `Bluefish`。
2. 点击 `Bluefish`，然后点击 `Source Selection Box`源选择框）。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击 `Install`安装）。

### 通过终端通过 APT 安装 Bluefish：
```bash
sudo apt install bluefish
```

### 通过终端通过 FLATPAK 安装 Bluefish：
```bash
flatpak install flathub nl.openoffice.bluefish
```

# 直播软件

直播软件允许你在线广播实时视频和音频，捕捉来自摄像头、麦克风或屏幕的内容。与将文件保存到设备的下载不同，流媒体在不进行本地存储的情况下实时播放媒体，使用数据包进行流畅播放。这节省了空间并提供了视频和音乐的即时访问，使其成为在线娱乐和直播分享的热门。

OBS Studio 是一款 Windows 和 macOS 的免费开源直播和录屏软件。它支持多种视频编码方法，并与 YouTube 和 Twitch 等平台集成。用户可以混合音频、无缝切换场景并自定义过渡效果。其友好的界面包含多场景画布、音频混音器和简单的设置，以便于配置。OBS 还支持插件和脚本以增强功能，迎了初学者和寻求专业级制作的高级用户。

Owncast 是一个自托管、可自定义的直播和聊天平台，对内容和社区拥有完全控制权。它与流行的直播软件集成，并具有内置聊天功能用于观众互动、自定义表情和聊天机器人。它为寻求独立于大型平台的主播设计，提供了无跟踪的体验。兼容 Linux 和 macOS 服务器，只需少量设置即可开始直播。Owncast 还可以连接到 Fediverse，扩大受众范围。对于那些想要没有主流服务限制的自定义无广告直播的人非常完美。

## OBS Studio

访问 OBS Studio 官网 [`obsproject.com/`](https://obsproject.com/) 了解关于 OBS Studio 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 OBS Studio：
1. 打开 `Software Manager`（软件管理器）并搜索 `OBS Studio`。
2. 点击 `OBS Studio`，然后点击 `Source Selection Box`源选择框）。
3. 选择 `RPM` 或 `FLATPAK` 并点击 `Install`安装）。

### 通过终端通过 APT 安装 OBS Studio：
```bash
sudo apt install obs-studio
```

### 通过终端通过 FLATPAK 安装 OBS Studio：
```bash
flatpak install flathub com.obsproject.Studio
```

### 通过终端通过 SNAP 安装 OBS Studio：
```bash
sudo snap install obs-studio
```

## Owncast

访问 Owncast 官网 [`owncast.online/`](https://owncast.online/) 了解关于 Owncast 的所有信息。

### 通过终端通过 APT 安装 Owncast：
```bash
sudo apt update
curl -s https://owncast.online/install.sh | bash
```

# 个人数据隐私

个人数据隐私是一项基本权利，涉及控制如何共享姓名、位置或在线行为等个人详情。随着数字交互的增加，保护这些信息对于维护在线信任至关重要。滥用可能导致欺诈、不希望的营销或限制自由表达，这使得数据保护法对于防止隐私受泄露和滥用至关重要。这关乎确保负责任地使用我们的信息，在连接的世界中维护自由和安全。





Searx 是一个免费的开源元搜索引擎，它通过不共享 IP 地址或搜索历史来优先保护用户隐私。它阻止跟踪 Cookie 并使用 `HTTP POST` 进行查询以增强隐私。灵感源自 Seeks，Searx 提供了网站的直接链接，并带有缓存或代理视图的选项。它支持跨多个领域的搜索，并允许用户运行私有实例或使用公共实例（包括 Tor 服务）。Searx 从 80 多个引擎获取结果，自定义设置保存在 cookie 中。它还支持用于特殊搜索操作符进行定制化查询。

OpenStego 是一个免费的基于 Java 的隐写工具，它可以在图像中隐藏数据并提供水印功能以保护版权，适用于多种平台。它支持加密以增加额外的安全性，使其成为在不改变数字文件外观的情况下隐藏信息或验证所有权的全面解决方案。

Tor，全称为洋葱路由（The Onion Router），是一种免费软件，通过通过全球志愿者中继网络引导互联网流量来实现匿名通信。它最初是为美国情报部门的安全通信而开发的，现在为数百万用户服务，从监控中隐藏用户的位置和互联网使用情况。尽管初衷是为了隐私和自由，但 Tor 的用途涵盖了合法活动到非法交易以及信息泄露，引发了关于隐私与安全之间影响的争议。

i2pd 是一个用于访问 I2P 的 C++ 工具，I2P 是一种通过隐藏用户 IP 地址确保匿名通信的加密网络。与 Java I2P 不同，i2pd 专门专注于路由，不需要 Java，并且具有更好的性能和更低资源。它支持从文件共享到消息的各种应用程序，同时保持在线的匿名性和安全性。

## Searx

访问 Searx 官方网站 [`github.com/searx/searx`](https://github.com/searx/searx) 获取有关 Searx 的所有信息。

### 在终端通过 APT 安装 Searx

首先，更新您的软件包列表：

```bash
sudo apt update
```

接下来，安装必要的包：

```bash
sudo apt install git rsync make gcc libc6-dev libssl-dev zlib1g-dev libpcre2-dev libevent-dev build-essential zlib1g-dev libpcre2-dev libsqlite3-dev libssl-dev libevent-dev libsystemd-dev curl wget git libxslt-dev python3-dev python3-babel python3-venv python3-pip
```

安装并使用 Node.js 版本 16 的 Node 版本管理器 (NVM)：

```bash
nvm install 16
nvm use 16
```

准备 Searx 环境：

```bash
cd ~/
git clone https://github.com/searx/searx.git
cd searx
python3 -m venv venv source venv/bin/activate
```

打开 `requirements.txt` 并将任何 `werkzeug` 条目替换为：

```text
werkzeug==2.2.2
```

然后保存更改。

安装 Python 依赖项：

```bash
pip install -r requirements.txt
```

复制默认设置文件并自定义：

```bash
cp searx/settings.yml searx/settings_custom.yml
gedit searx/settings.yml
```

根据您的喜好编辑 `settings.yml`，包括更改密钥。

在 `preferences.py` 中通过将 `advanced_search` 设置为 `True` 来启用高级搜索：

```bash
gedit searx/preferences.py
```

找到 `settings['ui'].get('advanced_search', False)` 并将 `False` 改为 `True`。保存所有更改并退出编辑器。

激活虚拟环境：

```bash
deactivate
```

启动 Searx：

```bash
sh -c '/home/username/searx/venv/bin/python /home/username/searx/searx/webapp.py'
```

将 `username` 替换为您的实际用户名。此指南确保 Searx 已安装并配置供个人使用，增强了对搜索数据的隐私保护和控制。

要为 Searx 创建桌面快捷方式，打开终端并导航到应用程序目录：

```bash
cd /usr/share/applications
```

然后，使用您喜欢的文本编辑器打开名为 `searx1.desktop` 的新文件：

```bash
sudo gedit searx1.desktop
```

在 `searx1.desktop` 文件中输入以下内容，将 `username` 替换为实际系统用户名：

```ini
[Desktop Entry]
Type=Application
Name=Searx
Comment=Searx - 尊重隐私的开源元搜索引擎
Exec=sh -c '/home/username/searx/venv/bin/python /home/username/searx/searx/webapp.py'
Icon=terminal
Terminal=false
Categories=Network;WebBrowser;
```

输入细节后，保存进度。最后，退出编辑器。此设置提供了一个从桌面直接启动 Searx 的便捷快捷方式。

## OpenStego

访问 OpenStego 官方网站 [`www.openstego.com/`](https://www.openstego.com/) 获取有关 OpenStego 的所有信息。

### 在 GUI 中通过 DEB 包安装 OpenStego

导航到发布页面：
[`github.com/syvaidya/openstego/releases`](https://github.com/syvaidya/openstego/releases)。

1. 点击最新的 `openstego_.deb` 下载 OpenStego。
2. 进入您的 `Downloads` 文件夹。
3. 双击 `openstego_0.8.6-1_all.deb`。
4. 点击 `Install`。

## Tor Browser Launcher

访问 Tor Browser Launcher 官方网站 [`www.torproject.org/`](https://www.torproject.org/) 获取有关 Tor Browser Launcher 的所有信息。

## 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 Tor Browser Launcher

1. 打开 `Software Manager` 并搜索 `Tor Browser Launcher`。
2. 点击 `Tor Browser Launcher`，然后点击 `Source Selection Box`。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击 `Install`。

## 在终端通过 APT 安装 Tor Browser Launcher

```bash
sudo apt install torbrowser-launcher
```

## 在终端通过 FLATPAK 安装 Tor Browser Launcher

```bash
flatpak install flathub org.torproject.torbrowser-launcher
```

## I2pd

访问 I2pd 官方网站 [`i2pd.website/`](https://i2pd.website/) 获取有关 I2pd 的所有信息。

## 通过软件管理器通过 FLATPAK 包安装 I2pd

1. 打开 `Software Manager` 并搜索 `I2pd`。
2. 点击 `I2pd`，然后点击 `Source Selection Box`。
3. 选择 `FLATPAK` 并点击 `Install`。

## 在终端通过 FLATPAK 安装 I2pd

```bash
flatpak install flathub website.i2pd.i2pd
```

## 在终端通过 SNAP 安装 I2pd

```bash
sudo snap install i2pd
```

## Hyphanet

访问 Hyphanet 官方网站 [`www.hyphanet.org/`](https://www.hyphanet.org/) 获取有关 Hyphanet 的所有信息。

## 在终端和 GUI 中 APT 和 Java 安装 Hyphanet

```bash
sudo apt update
```

导航到发布页面：
[`www.hyphanet.org/pages/download.html`](https://www.hyphanet.org/pages/download.html)

1. 点击 "Download Hyphanet for GNU/Linux & POSIX。"
2. 打开终端并使用以下命令安装必要的项：
```bash
sudo apt install default-jre default-jdk libcanberra-gtk-module libcanberra-gtk3-module libcanberra-gtk-module:i386 gtk2-engines-murrine xapp*
```
3. 进入 `Downloads` 文件夹：
```bash
cd ~/Downloads
```
4. 使用 Java 执行安装程序：
```bash
java -jar new_installer_1497.jar
```
5. 在语言选择菜单中，选择 "English”（或您的常用语言）。点击 `OK`，然后点击 `Next`。
6. 选择您的安装路径并点击 `Next`。点击 `OK` 确认创建目标目录。
7. 确保选择了 "Base" 选项，然后点击三次 `Next`。
8. 通过切换旁边的开关选择将这些设置应用于“current user”。
9. 点击 `Next`，然后点击 `Done` 完成安装。

## ZeroNet

访问 ZeroNet 官方网站 [`zeronet.io/`](https://zeronet.io/) 获取有关 ZeroNet 的所有信息。

## 在终端通过 APT 安装 ZeroNet

```bash
sudo apt update && sudo apt upgrade
wget https://github.com/HelloZeroNet/ZeroNet-linux/archive/dist-linux64/ZeroNet-py3-linux64.tar.gz
tar xvpfz ZeroNet-py3-linux64.tar.gz
cd ZeroNet-linux-dist-linux64/
./ZeroNet.sh
```

要为 ZeroNet 创建桌面快捷方式，请打开终端并导航到应用程序目录：

```bash
cd /usr/share/applications
```

创建一个名为 `zeronet1.desktop` 的新文件：

```bash
sudo gedit zeronet1.desktop
```

在文本编辑器中向文件中填充以下细节：

```ini
[Desktop Entry]
Name=ZeroNet
Comment=Access decentralized websites
Exec=./Downloads/ZeroNet-linux-dist-linux64/ZeroNet.sh
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```




将 `/path/to/` 替换为 ZeroNet 在你系统上的实际路径。点击“保存”保存更改，或前往“文件” > “保存”，或者点击 ☰ 图标，选择“另存为”，然后点击“保存”。完成后关闭编辑器。

## Web 浏览器

Web 浏览器是允许我们从网络或本地存储获取内容并显示在设备上以访问网站的工具。无论是在电脑还是手机上，当我们输入 URL 时，像 `Google Chrome` 和 `Safari` 等浏览器会连接到网络服务器，允许我们通过 `HTTPS` 安全地浏览页面。它们与搜索引擎不同，其作用是渲染网页、存储用于个性化和追踪的 cookie，并使用缓存加速重复访问。隐私功能有助于管理这些 cookie，确保获得更安全的浏览体验。

Chromium 是 Google 推出的一个开源浏览器项目，旨在构建更安全、更快速的网络。与 `Chrome` 不同，它是完全开源的，缺少了自动更新和某些解码器等功能。它是许多浏览器（包括 `Chrome` 和 `Edge`）的基础，通过其多进程架构和各大科技巨头的贡献来关注安全性。

Ungoogled-Chromium 是 Chromium 的一个版本，经过修改消除了对 Google Web 服务的依赖，同时保持原始体验。它增强了隐私性和控制力，需要手动激活某些功能。它阻止了内部 Google 请求，并借鉴了来自 `Inox` 和 `Bromite` 等项目的调整，以提供注重隐私的浏览体验。

Google Chrome 于 2008 年发布，是 Google 的一款流行 浏览器。它基于 `Apple WebKit` 和 `Mozilla Firefox` 的免费软件构建，适用于多个平台，包括 Windows、Linux、macOS、iOS 和 Android。它以性能强大著称，具有极简的界面和独特的工具，如用于 URL 和搜索的 `omnibox`，以及用于扩展和主题的完善 `Chrome 应用商店`。

Microsoft Edge 由微软于 2015 年发布，从其最初的 `EdgeHTML` 基础演变为 2020 年的 Chromium 基础。这一变化增强了跨设备的兼容性和性能。`Edge` 具有 PDF 读取、`WebAssembly` 支持以及用于兼容的 `Internet Explorer` 模式。它与微软的服务无缝集成，提供语音控制、搜索功能和清爽的`阅读模式`。

Thorium Browser 是 Chromium 的一个高性能变体，针对现代 CPU 进行了优化。它镜像了 Google Chrome 的功能，但引入了改进速度和隐私的增强和补丁。它排除了 Google 的遥测数据，并默认集成了替代搜索引擎，迎合技术丰富的群体。

Vivaldi 由 Vivaldi Technologies 于 2015 年发布，面向追求丰富功能和定制化的技术爱好者以及前 Opera 用户。它提供了独特的 UI 定制、内置的广告和追踪器拦截、邮件支持以及创新的标签页管理，支持 `Chrome` 和 `Firefox` 扩展。

Brave 是一款注重隐私的免费开源浏览器，默认阻止大多数广告和追踪器。它通过观看可选广告向用户发放`基础注意力代币 (BAT)`。Brave 包含内置 `VPN`、加密钱包和自己的搜索引擎，优先考虑用户知情和隐私。

Firefox 由 Mozilla 开发，是一款免费开源 Web 浏览器，以速度、隐私功能和灵活性闻名。它支持多个平台，并使用 `Gecko` 引擎遵循网络标准。功能包括标签页浏览、隐私浏览和各种开发者工具。Firefox 因其对用户隐私和网络标准的承诺而保持流行。

Firefox ESR 专为不需要频繁更新的稳定 Web 部署组织设计。它专注于安全性和修复而非最新功能，提供无比拟的数据保护和灵活的部署，是企业和大学的理想选择。

Waterfox 是 Firefox 的分支，专注于伦理、用户隐私和性能。它支持 Firefox 插件，并通过禁用遥测来强调隐私。Waterfox 确保在不牺牲速度或功能的情况下提供安全的浏览体验。

LibreWolf 是一个独立的 Firefox 变体，专注于隐私、安全和自由。它增强了针对追踪和指纹识别的防护，排除了遥测，并预装了 `uBlock Origin` 以实现无广告浏览。

Pale Moon 是一款针对现代处理器优化的免费开源浏览器。它基于自己的 `Goanna` 引擎构建，专注于效率、定制和隐私，支持经典插件和广泛的定制。

Mullvad Browser 与 Tor 项目共同开发，增强了在线隐私。它默认开启隐私浏览，不留下任何 cookie 或历史记录，并反指指纹。它针对隐私进行了微调，最大限度地减少追踪和指纹识别。

Basilisk 基于 `Goanna` 引擎和 `UXP` 平台，提供稳定、抗更改的浏览体验。它支持现代网络标准和各种插件，提供熟悉的浏览体验。

## Chromium

访问 Chromium 官网 [`www.chromium.org/chromium-projects/`](https://www.chromium.org/chromium-projects/) 了解所有关于 Chromium 信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 Chromium：

1. 打开软件管理器并搜索 `Chromium`。
2. 点击 `Chromium`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Chromium：

```bash
sudo apt install chromium
```

### 在终端通过 FLATPAK 安装 Chromium：

```bash
flatpak install flathub org.chromium.Chromium
```

### 在终端通过 SNAP 安装 Chromium：

```bash
sudo snap install chromium
```

## Ungoogled-Chromium

访问 Ungoogled-Chromium 官网 [`github.com/ungoogled-software/ungoogled-chromium`](https://github.com/ungoogled-software/ungoogled-chromium) 了解所有关于 Ungoogled-Chromium 信息。

### 通过软件管理器通过 FLATPAK 包安装 Ungoogled-Chromium：

1. 打开软件管理器并搜索 `Ungoogled-Chromium`。
2. 点击 `Ungoogled-Chromium`，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

### 在终端通过 FLATPAK 安装 Ungoogled-Chromium：

```bash
flatpak install flathub io.github.ungoogled_software.ungoogled_chromium
```

## Google Chrome

访问 Google Chrome 官网 [`www.google.com/intl/en_uk/chrome/`](https://www.google.com/intl/en_uk/chrome/) 了解所有关于 Google Chrome 信息。

### 在终端通过 APT 安装 Google Chrome：

```bash
sudo apt update && sudo apt upgrade
wget -qO - https://dl.google.com/linux/linux_signing_key.pub | gpg --dearmor | sudo tee /etc/apt/keyrings/google-chrome.gpg
sudo sh -c 'echo "deb [arch=amd64 signed-by=/etc/apt/keyrings/google-chrome.gpg] http://dl.google.com/linux/chrome/deb/ stable main" > /etc/apt/sources.list.d/google-chrome.list'
sudo apt update
sudo apt install google-chrome-stable
```

### 在 GUI 中通过 .deb 安装 Google Chrome：

1. 导航至发布页面：[`www.google.com/chrome/`](https://www.google.com/chrome/)
2. 点击“下载 Chrome”。
3. 点击“64 位 .deb (适用于 Debian/Ubuntu)”旁边的圆圈。
4. 点击“接受并安装”下载 Chrome。
5. 进入你的“下载”文件夹。
6. 双击 `google-chrome-stable_current_amd64.deb`。
7. 点击“安装”。

## Microsoft Edge

访问 Microsoft Edge 官网 [`www.microsoft.com/en-us/edge`](https://www.microsoft.com/en-us/edge) 了解所有关于 Microsoft Edge 信息。

### 在终端通过 APT 安装 Microsoft Edge：

```bash
curl -sSL -O https://packages.microsoft.com/config/<distribution>/<version>/packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb
sudo apt update
sudo apt install microsoft-edge-stable
```

[文件名将根据所使用的 Microsoft edge 浏览器版本而异]。

### 在 GUI 中通过 .deb 安装 Microsoft Edge：





[`www.microsoft.com/en-us/edge/download?form=MA13FJ`](https://www.microsoft.com/en-us/edge/download?form=MA13FJ)。

点击“接受并下载”下载 Microsoft Edge。

前往你的“下载”文件夹。

双击 `microsoft-edge-stable_125.0.2535.92-1_amd64.deb`。

点击“安装”。

## Thorium

访问 Thorium 官方网站 [`thorium.rocks/`](https://thorium.rocks/) 获取关于 Thorium 的所有信息。

### 通过 GUI 通过 .rpm 安装 Thorium：

访问发布页面：

[`github.com/Alex313031/thorium/releases`](https://github.com/Alex313031/thorium/releases)

点击最新的 `thorium-browser_AVX2.rpm` 下载 Thorium。

前往你的“下载”文件夹。

双击 `thorium-browser_124.0.6367.218_AVX2.deb`。

点击“安装”。

## Vivaldi

访问 Vivaldi 官方网站 [`vivaldi.com/`](https://vivaldi.com/) 获取关于 Vivaldi 的所有信息。

### 通过终端通过 APT 安装 Vivaldi：

```bash
sudo apt update
sudo apt install wget
wget -qO- https://repo.vivaldi.com/archive/linux_signing_key.pub | gpg --dearmor | sudo dd of=/usr/share/keyrings/vivaldi-browser.gpg
echo "deb [signed-by=/usr/share/keyrings/vivaldi-browser.gpg arch=$(dpkg --print-architecture)] https://repo.vivaldi.com/archive/deb/ stable main" | sudo dd of=/etc/apt/sources.list.d/vivaldi-archive.list
sudo apt update && sudo apt install vivaldi-stable
```

### 通过 GUI 通过 .deb 安装 Vivaldi：

访问下载页面：

[`vivaldi.com/download/?platform=linux`](https://vivaldi.com/download/?platform=linux)

点击“Vivaldi for Linux DEB” 下载 Vivaldi。

前往你的“下载”文件夹。

双击 `vivaldi-stable_6.7.3329.41-1_amd64.deb`。

点击“安装”。

## Brave

访问 Brave 官方网站 [`brave.com/`](https://brave.com/) 获取关于 Brave 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Brave：

1. 打开软件管理器并搜索 Brave。
2. 点击 Brave，然后点击源选择框。
3. 选择 FLATPAK 并点击安装。

## 通过终端通过 APT 安装 Brave：

```bash
sudo apt update && sudo apt upgrade
sudo apt install curl
sudo curl -fsSLo /usr/share/keyrings/brave-browser-archive-keyring.gpg https://brave-browser-apt-release.s3.brave.com/brave-browser-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/brave-browser-archive-keyring.gpg] https://brave-browser-apt-release.s3.brave.com/ stable main"|sudo tee /etc/apt/sources.list.d/brave-browser-release.list
sudo apt update && sudo apt install brave-browser
```

## 通过终端通过 FLATPAK 安装 Brave：

```bash
flatpak install flathub com.brave.Browser
```

## 通过终端通过 SNAP 安装 Brave：

```bash
sudo snap install brave
```

## Firefox

访问 Firefox 官方网站 [`www.mozilla.org/en-GB/firefox/new/`](https://www.mozilla.org/en-GB/firefox/new/) 获取关于 Firefox 的所有信息。

### 通过软件管理器通过系统软件包/FLATPAK 包安装 Firefox：

1. 打开软件管理器并搜索 Firefox。
2. 点击 Firefox，然后点击源选择框。
3. 选择 SYSTEM PACKAGE 或 FLATPAK 并点击安装。

## 通过终端通过 APT 安装 Firefox：

```bash
sudo apt install firefox
```

## 通过终端通过 FLATPAK 安装 Firefox：

```bash
flatpak install flathub org.mozilla.firefox
```

## 通过终端通过 SNAP 安装 Firefox：

```bash
sudo snap install firefox
```

## Firefox ESR

访问 Firefox ESR 官方网站 [`www.mozilla.org/en-GB/firefox/enterprise/`](https://www.mozilla.org/en-GB/firefox/enterprise/) 获取关于 Firefox ESR 的所有信息。

### 通过 GUI 通过 .tar.xz 安装 Firefox：

访问发布页面：

[`www.mozilla.org/en-GB/firefox/all/#product-desktop-esr`](https://www.mozilla.org/en-GB/firefox/all/#product-desktop-esr)

点击“你想下载哪个浏览器？”并选择“Firefox Extended Support Release”。
点击“选择你偏好的安装程序”并选择“Linux 64-bit”。
点击“选择你偏好的语言”并选择“English (British)”。
点击“立即下载”下载 Firefox ESR。

前往你的“下载”文件夹。

双击 `firefox-115.11.0esr.tar.bz2`。

选择 `firefox` 并点击“提取”。

前往 `~/Downloads/firefox`。

双击 `firefox`。

要为 Firefox ESR 创建桌面快捷方式，打开终端并输入以下命令：

```bash
cd /usr/share/applications
sudo gedit firefoxesr1.desktop
```

使用以下内容更新 `firefoxesr1.desktop` 文件：

```ini
[Desktop Entry]
Name=Firefox ESR
Comment=Firefox ESR
Exec=./Downloads/firefox/firefox
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

要保存更改，点击“保存”，或前往“文件”并选择“保存”，或点击 ☰ 图标，选择“另存为”，然后点击“保存”。完成后，退出编辑器。确保 `Exec=` 路径正确指向系统上 Firefox ESR 可执行文件的位置。

## Waterfox

访问 Waterfox 官方网站 [`www.waterfox.net/`](https://www.waterfox.net/) 获取关于 Waterfox 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 Waterfox：

1. 打开 GNOME 软件并搜索 Waterfox。
2. 点击 Waterfox，然后点击源选择框。
3. 选择 FLATPAK 并点击安装。

## 通过终端通过 FLATPAK 安装 Waterfox：

```bash
flatpak install flathub org.mozilla.firefox
```

### 通过 GUI 通过 .tar.xz 安装 Waterfox：

访问发布页面：

[`www.waterfox.net/download/`](https://www.waterfox.net/download/)

在 Linux 64-bit GTK3 同一行点击“Download tarball”下载 Waterfox。

前往你的“下载”文件夹。

双击 `waterfox-6.0.16.tar.bz2`。

选择 `waterfox` 并点击“提取”。

前往 `~/Downloads/firefox`。（注：原文此处可能有误，已按原文翻译）

双击 `firefox`。

要为 Waterfox 创建桌面快捷方式，打开终端并输入以下命令：

```bash
cd /usr/share/applications
sudo gedit waterfox1.desktop
```

使用以下内容更新 `waterfox1.desktop` 文件：

```ini
[Desktop Entry]
Name=Waterfox
Comment=Waterfox
Exec=./Downloads/firefox/waterfox
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

要保存更改，点击“保存”，或前往“文件”并选择“保存”，或点击 ☰ 图标，选择“另存为”，然后点击“保存”。完成后，退出编辑器。确保 `Exec=` 路径正确指向系统上 Waterfox 可执行文件的位置。

## LibreWolf

访问 LibreWolf 官方网站 [`librewolf.net/`](https://librewolf.net/) 获取关于 LibreWolf 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 LibreWolf：

1. 打开软件管理器并搜索 LibreWolf。
2. 点击 LibreWolf，然后点击源选择框。
3. 选择 FLATPAK 并点击安装。

## 通过终端通过 APT 安装 LibreWolf：

```bash
sudo apt update && sudo apt install -y wget gnupg lsb-release apt-transport-https ca-certificates
distro=$(if echo " una bookworm jammy bullseye vera " | grep -q " $(lsb_release -sc) "; then lsb_release -sc; else echo focal; fi)
wget -O- https://deb.librewolf.net/keyring.gpg | sudo gpg --dearmor -o /usr/share/keyrings/librewolf.gpg
sudo tee /etc/apt/sources.list.d/librewolf.sources << EOF > /dev/null
Types: deb
URIs: https://deb.librewolf.net
Suites: $distro
Components: main
Architectures: amd64
Signed-By: /usr/share/keyrings/librewolf.gpg
EOF
sudo apt update && sudo apt install librewolf
```

## 通过终端通过 FLATPAK 安装 Firefox：

```bash
flatpak install flathub io.gitlab.librewolf-community
```

## Pale Moon

访问 Pale Moon 官方网站 [`www.palemoon.org/`](https://www.palemoon.org/) 获取关于 Pale Moon 的所有信息。

### 通过 GUI 通过 .tar.xz 安装 Pale Moon：

访问发布页面：

[`www.palemoon.org/download.shtml`](https://www.palemoon.org/download.shtml)

在 Linux 64-bit GTK3 同一行点击“Download tarball”下载 Pale Moon。

前往你的“下载”文件夹。

双击 `palemoon-33.1.1.linux-x86_64-gtk3.tar.xz`。

选择 `palemoon` 并点击“提取”。

前往 `~/Downloads/palemoon`。

双击 `palemoon`。





## Pale Moon

要为 Pale Moon 创建桌面快捷方式，打开终端并输入以下命令：

```bash
cd /usr/share/applications
sudo gedit palemoon1.desktop
```

使用以下内容更新 `palemoon1.desktop` 文件：

```
[Desktop Entry]
Name=Pale Moon
Comment=Pale Moon
Exec=./Downloads/palemoon/palemoon
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

要保存更改，请点击“保存（Save）”，或前往“文件（File）”并选择“保存”，或者点击 ☰ 图标，选择“另存为（Save As）”，然后点击“保存”。完成后，退出编辑器。确保 `Exec=` 路径正确指向您系统中 Pale Moon 可执行文件的位置。

## Mullvad Browser

访问 Mullvad Browser 官方网站 [`mullvad.net/en/browser`](https://mullvad.net/en/browser) 获取所有关于 Mullvad Browser 的信息。

## 在图形界面中通过 .tar.xz 安装 Mullvad Browser

1. 导航至发布页面：[`mullvad.net/en/download/browser/linux`](https://mullvad.net/en/download/browser/linux)
2. 点击 Linux 标签页。
3. 点击“下载（Download）”下载 Mullvad Browser。
4. 进入您的 `Downloads` 文件夹。
5. 双击 `mullvad-browser-linux-x86_64-13.0.16.tar.xz`。
6. 选择 `mullvad-browser` 并点击“提取（Extract）”。
7. 进入 `~/Downloads/mullvad-browser/Browser`。
8. 双击 `mullvadbrowser.real`。

为 Mullvad Browser 创建桌面快捷方式，打开终端并输入以下命令：

```bash
cd /usr/share/applications
sudo gedit mullvad-browser1.desktop
```

使用以下内容更新 `mullvad-browser1.desktop` 文件：

```
[Desktop Entry]
Name=Mullvad Browser
Comment=Mullvad Browser
Exec=./Downloads/mullvad-browser/Browser/mullvadbrowser.real
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

要保存更改，请点击“保存（Save）”，或前往“文件（File）”并选择“保存”，或者点击 ☰ 图标，选择“另存为（Save As）”，然后点击“保存”。完成后，退出编辑器。确保 `Exec=` 路径正确指向您系统中 Mullvad Browser 可执行文件的位置。

## Basilisk

访问 Basilisk 官方网站 [`www.basilisk-browser.org/`](https://www.basilisk-browser.org/) 获取所有关于 Basilisk 的信息。

## 在图形界面中通过 .tar.xz 安装 Basilisk

1. 导航至发布页面：[`www.basilisk-browser.org/download.shtml`](https://www.basilisk-browser.org/download.shtml)
2. 在 United States（美国）下，找到 Linux x86_64 压缩包所在行，点击 `x86 64-bit GTK3` 下载 Basilisk。
3. 进入您的 `Downloads` 文件夹。
4. 双击 `basilisk-20240510185247.linux-x86_64-gtk3.tar.`。
5. 选择 `basilisk` 并点击“提取（Extract）”。
6. 进入 `~/Downloads/basilisk`。
7. 双击 `basilisk`。

为 Basilisk 创建桌面快捷方式，打开终端并输入以下命令：

```bash
cd /usr/share/applications
sudo gedit basilisk1.desktop
```

使用以下内容更新 `basilisk1.desktop` 文件：

```
[Desktop Entry]
Name=Basilisk
Comment=Basilisk
Exec=./Downloads/basilisk/basilisk
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

要保存更改，请点击“保存（Save）”，或前往“文件（File）”并选择“保存”，或者点击 ☰ 图标，选择“另存为（Save As）”，然后点击“保存”。完成后，退出编辑器。确保 `Exec=` 路径正确指向您系统中 Basilisk 可执行文件的位置。

# 密码管理器

密码管理器是安全的应用程序，它们将您所有的登录详情存储在一个地方，消除了记忆每个帐据的需求。在当今的数字世界中，它们至关重要，通过生成强力密码和防止身份盗窃提供了便利性并提升了安全性。凭借加密和云存储等功能，它们是跨设备管理个人和工作帐户的极佳选择。虽然有免费版本，但投资付费服务可以确保最高的安全性和功能，使其成为保护数字生活的宝贵工具。

LastPass 由 `GoTo` 管理，是一款强大的密码管理器，旨在安全地存储和处理密码。它提供了 Web 界面、浏览器扩展和移动端应用，确保密码在设备间可以轻松访问和同步。通过 `AES-256` 加密，LastPass 保护用户数据，提供自动填充表单、密码生成和安全备注存储等功能。它支持带有 `LastPass Authenticator` 等选项的双重身份验证，增强了安全性。LastPass 适用于主流浏览器和手机，即使在离线状态下也能无缝管理密码，并包含用户设置的密码提示以供应急访问。

Bitwarden 是一款多功能的开源密码管理器，将安全性与易用性相结合，为多个平台上的凭据和敏感数据提供加密存储。它支持各种设备，提供桌面、浏览器和移动端应用，以及 `CLI` 工具，确保您的数据安全且随处可访问。凭借双重身份验证、无密码登录和安全共享等功能，它满足了从个人到企业的各类需求。它对隐私的承诺通过零知识加密以及云端或自托管选项得到了体现。除了密码，它还可以管理备注、卡片等。

KeePassXC 是一款免费的开源密码管理器，起源于 `KeePassX` 社区分支，为 Windows、macOS、Linux 和 BSD 等平台提供了安全的密码存储地。它支持 `KeePass 2.x` (`.kdbx`) 格式，可以导入旧数据库，并通过密钥文件和 `YubiKey` 增加安全性。KeePassXC 因隐私隐私受到 EFF 的赞誉，具有加密、不依赖云端和跨平台兼容等特点，让您掌控数据。其浏览器扩展通过自动填充密码增强了用户体验。

Buttercup 是一款免费的开源密码管理器，为您的凭据提供安全的 `256-bit AES` 加密。它为简单而设计，易于存储和查找登录详情。它支持所有主流桌面平台和移动设备，实现跨设备无缝集成。凭借自动锁定、自定义条目和内置垃圾箱等功能，管理密码变得简单直观。Buttercup 还提供了 Chrome 扩展，增强了它的实用性。

## LastPass

访问 LastPass 官方网站 [`www.lastpass.com/`](https://www.lastpass.com/) 获取所有与 LastPass 相关的信息。

## 在终端和图形界面中通过 .sh 安装 LastPass

1. 导航至发布页面：[`lastpass.com/lplinux.php`](https://lastpass.com/lplinux.php)
2. 点击下载最新的 Linux 版本（Latest Linux Release）。
3. 进入 `~/Downloads`。
4. 双击 `lplinux.tar.bz2`。
5. 选择“提取（Extract）”并将文件提取到 `~/Downloads`。
6. 在 `~/Downloads` 中右键点击空白处，并选择“在终端中打开（Open in Terminal）”。
7. 在终端输入以下命令：

```bash
chmod +x install_lastpass.sh
```
8. 输入以下内容运行脚本：

```bash
./install_lastpass.sh
```

## Bitwarden

访问 Bitwarden 官方网站 [`bitwarden.com/`](https://bitwarden.com/) 获取所有关于 Bitwarden 的信息。

## 通过软件中心通过 FLATPAK 软件包安装 Bitwarden

1. 打开软件中心（Software Manager）并搜索 Bitwarden。
2. 点击 Bitwarden，然后点击来源选择。
3. 选择 `FLATPAK` 并点击安装。

## 在终端通过 FLATPAK 安装 Bitwarden

```bash
flatpak install flathub com.bitwarden.desktop
```

## 在终端通过 SNAP 安装 Bitwarden

```bash
sudo snap install bitwarden
```





访问 Buttercup 官方网站 [`buttercup.pw/`](https://buttercup.pw/) 了解关于 Buttercup 的所有信息。

## 通过 GUI 使用 AppImage 安装 Buttercup：

导航至发布页面：
[`buttercup.pw/`](https://buttercup.pw/)

点击 "Linux (AppImage)" 下载 Buttercup。

将文件下载到你的 `~/Downloads` 文件夹。

在 `Downloads` 文件夹中找到 `Buttercup-linux-x86_64.AppImage` 文件，右键点击它并选择“属性（Properties）”。

在属性菜单中，切换到“权限（Permissions）”选项卡，并勾选“允许程序执行（Set as executable）”。

双击 `Buttercup-linux-x86_64.AppImage` 文件开始安装过程。

要创建一个 Buttercup AppImage `.desktop` 快捷方式，请在终端中执行以下步骤：

使用命令导航到应用程序目录：
```
cd /usr/share/applications
```

运行以下命令打开一个新的 `.desktop` 文件进行编辑：
```
sudo gedit buttercup1.desktop
```

在 `buttercup1.desktop` 文件中输入以下细节：
```
[Desktop Entry]
Name=Buttercup
Comment=Buttercup
Exec=./Applications/Buttercup.AppImage
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

点击“保存（Save）”保存进度。或者，你可以点击“文件（File）”、“保存”，或点击 ☰ 图标选择“另存为（Save As）”，最后点击“保存”。保存后关闭编辑器。

# 媒体播放器

媒体播放器无论是软件还是硬件，都能从存储设备、光盘或互联网等源播放音频视频文件。某些格式可能需要解码器，可以流播放在线内容，并且对 DVD 和蓝光支持的支持不相同。播放器的选择会影响媒体质量，为不同的格式使用多个播放器是常见做法。与存储和共享文件的媒体服务器不同，播放器并非为编辑设计，但通常支持字幕、更新和皮肤。开源播放器提供了广泛的格式支持和自定义。播放列表有助于组织媒体，某些播放器还可以转换文件格式或流播放网络电台。轻量级播放器占用资源极少，是配置较低的系统的理想选择。

VLC 是一款功能强大、免费开源的媒体播放器，适用于桌面及 Android 和 iOS 等移动设备。它由 VideoLAN 项目开发，支持各种音频、视频和流格式，包括 DVD。它可以流播放媒体并转码文件，内置了 `libavcodec` 库的解码器。VLC 在 Linux 和 macOS 上通过 `libdvdcss` 支持加密 DVD 播放，并可在各大应用商店下载，但由于 DVD 解密，其法律状态在不同地区有所异。

Parole 媒体播放器为 Xfce 桌面设计，使用 `GStreamer` 框架播放各种媒体类型，包括本地文件、DVD 和流。它非常轻量、通过插件可扩展，且资源利用率高。它支持拖放播放列表和基础播放控制，但缺少高级配置选项，并在处理损坏文件和高分辨率显示器时较为吃力，通用性不如 `mpv` 或 `VLC` 等播放器。

SMPlayer 是适用于 Windows 和 Linux 的免费开源播放器，通过内置适用于任何视频和音频格式的解码器提供无缝体验。它会记住每个文件的播放设置，确保你以相同的设置继续播放。作为 `MPlayer` 的图形界面程序，它支持 YouTube 播放、字幕下载，并提供多种皮肤和高级功能，无需外部解码器。SMPlayer 支持超过 30 种语言，让跨平台的媒体播放变得简单且可定制。

Haruna 是一款适用于 KDE Plasma 的开源视频播放器，提供了通过 `youtube-dl` 播放在线视频、YouTube 播放列表、自动播放列表和自定义快捷键等功能。它直观的设计和对各种视频格式的兼容性使其成为 Linux 用户的首选。通过自动跳过章节和可调字幕设置，Haruna 增强了观看体验。可在 Flathub 和 Ubuntu 仓库获取，是寻求全面媒体播放器的人的必备尝试。

Dragon Player 是 KDE 桌面的多媒体播放器，专注于简单性，提供没有过度功能的直接体验。它基于 `Codeine` 开发于 KDE 3，现在适用于 KDE SC 4，使用 `Phonon` 进行多媒体框架支持。它的功能包括简洁的界面、视频续播、字幕支持、可调的视频显示设置以及 CD/DVD 播放。Dragon Player 免费开源，是那些看重易用性而非复杂性的人的理想选择。

## VLC

访问 VLC 官方网站 [`www.videolan.org/`](https://www.videolan.org/) 了解关于 VLC 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 VLC：

1. 打开软件管理器并搜索 VLC。
2. 点击 VLC，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端中使用 APT 安装 VLC：
```
sudo apt install vlc
```

### 在终端中使用 FLATPAK 安装 VLC：
```
flatpak install flathub org.videolan.VLC
```

### 在终端中使用 SNAP 安装 VLC：
```
sudo snap install vlc
```

## SMPlayer

访问 SMPlayer 官方网站 [`www.smplayer.info/`](https://www.smplayer.info/) 了解关于 SMPlayer 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 SMPlayer：

1. 打开软件管理器并搜索 SMPlayer。
2. 点击 SMPlayer，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端中使用 APT 安装 SMPlayer：
```
sudo apt install smplayer
```

### 在终端中使用 FLATPAK 安装 SMPlayer：
```
flatpak install flathub info.smplayer.SMPlayer
```

### 在终端中使用 SNAP 安装 SMPlayer：
```
sudo snap install smplayer
```

## Haruna

访问 Haruna 官方网站 [`apps.kde.org/en-gb/haruna/`](https://apps.kde.org/en-gb/haruna/) 了解关于 Haruna 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 包安装 Haruna：

1. 打开软件管理器并搜索 Haruna。
2. 点击 Haruna，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端中使用 APT 安装 Haruna：
```
sudo apt install haruna
```

### 在终端中使用 FLATPAK 安装 Haruna：
```
flatpak install flathub org.kde.haruna
```

### 在终端中使用 SNAP 安装 Haruna：
```
sudo snap install haruna
```

## Dragon Player

访问 Dragon Player 官方网站 [`apps.kde.org/en-gb/dragonplayer/`](https://apps.kde.org/en-gb/dragonplayer/) 了解关于 Dragon Player 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE 安装 Dragon Player：

1. 打开软件管理器并搜索 Dragon Player。
2. 点击 Dragon Player，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 并点击安装。

### 在终端中使用 APT 安装 Dragon Player：
```
sudo apt install dragon
```

### 在终端中使用 SNAP 安装 Dragon Player：
```
sudo snap install dragon
```

# 系统工具

系统工具是帮助管理和优化计算机系统或应用程序软件的软件程序。它们在后台运行，执行如数据备份、磁盘压缩和文件管理等任务。这些工具可以是操作系统的一部分，也可以单独安装以增强或替换默认工具。它们在确保安全、优化性能和保持计算机运行良好方面起着至关重要的作用。例如反病毒软件、磁盘碎片整理程序、调试器、诊断程序和网络工具。它们对于普通用户和 IT 专业人员都是必重要的，根据其对系统的影响需要不同的用户权限。

`QDirStat` 是一款用于管理磁盘空间的图形化工具，通过传统的树形结构和彩色树图提供目录和文件的双重视图。它引入了多选、自定义清理操作和详细错误报告等功能。它易于用且多功能，方便按类型识别和管理文件。





Psensor 是一个基于 GTK+ 的软件，用于实时监控硬件温度和 CPU 风扇转速。它还可以监控远程服务器并显示 Linux CPU 使用率。Psensor 会自动检测支持的硬件，以文本和详细图表的形式呈现数据。它包含了针对关键温度和风扇问题的可配置报警和提醒。

Stacer 是一个适用于 Linux 的开源系统优化器和应用程序监控器。它允许用户管理启动应用、清理不需要的文件、处理系统服务和进程，以及卸载应用程序。Stacer 还提供了实时资源使用监控和 APT 仓库管理器，方便编辑软件包仓库。

BleachBit 是一个用于在 Linux 和 Windows 上释放磁盘空间和保护隐私的工具。它可以清理不需要的文件，并可以对文件进行粉碎以防止恢复。BleachBit 支持广泛的应用，并包含诸如清理 Firefox 以提高速度等高级功能，使其对于维护系统性能和安全性至关重要。

SoundConverter 是适用于 GNOME 桌面面的音频文件转换器，支持 Ogg Vorbis、AAC、MP3 和 FLAC 等格式。它提供快速的多线程转换，并可以从视频文件中提取音频。用户可以根据标签轻松重命名文件并组织文件夹，从而简化音频转换任务。

Converseen 是一款适用于 Windows、Linux、macOS 和 FreeBSD 的多功能图像处理器。它支持超过 100 种格式，允许对图像进行转换、调整大小、旋转和翻转。用户还可以将 PDF 文转换为图像并批量重命名文件。Converseen 用户友好，适用于任何图像处理需求。

GParted 是一个使用 GNU Parted 管理磁盘分免费应用程序。它简化了创建、调整大小、移动和复制分区等任务，对于设置新操作系统和重新组织磁盘空间非常有用。GParted 支持各种文件系统和存储设备，满足新手和高级用户的需求。

HardInfo 是 Linux 的系统分析和基准测试工具，提供了对硬件和软件组件的详细洞察。它提供 HTML 或纯文本格式的报告，并允许基准比较。HardInfo 以易访问的格式组织数据，便于诊断和分析系统性能以及硬件规格。

gpustat 是一个监控 NVIDIA 图形设备的命令行实用。它提供实时 GPU 状态查询，具有内置监听模式、详细的 GPU 属性、运行进程名称和功耗等功能。对于需要深入了解 NVIDIA GPU 性能的人来说，这是一个非常有用的工具。

Czkawka 以波兰语中的“打嗝”命名，是一款快速且免费的应用程序，旨在通过删除不需要的文件来清理电脑。它用 Rust 构建，因速度快而脱颖，使用高级算法和多线程高效地执行任务。这款开源工具无广告，可在 Linux、Windows、macOS 和 FreeBSD 上使用。它提供 CLI 和 GUI 前端，其中 GUI 使用 GTK 4 或 Slint 框架以适应不同的用户偏好。Czkawka 通过不访问互联网或收集数据来确保隐私。它支持多种语言，并有各种工具来查找重复文件、空文件夹、大文件等。它还可以搜索相似图像、视频和音乐，并识别无效的符号链接、损坏的文件以及文件内容与扩展之间的不匹配。

## QDirStat

访问 QDirStat 官方网站 [`github.com/shundhammer/qdirstat`](https://github.com/shundhammer/qdirstat) 获取有关 QDirStat 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE 软件包安装 QDirStat：

1. 打开软件管理器并搜索 `QDirStat`。
2. 点击 `QDirStat`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 并点击安装。

### 通过终端通过 APT 安装 QDirStat：

```
sudo apt install qdirstat
```

## Psensor

访问 Psensor 官方网站 [`github.com/chinf/psensor`](https://github.com/chinf/psensor) 获取有关 Psensor 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE 软件包安装 Psensor：

1. 打开软件管理器并搜索 `Psensor`。
2. 点击 `Psensor`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 并点击安装。

### 通过终端通过 APT 安装 Psensor：

```bash
sudo apt install psensor
sudo sensors-detect
sensors
```

## Stacer

访问 Stacer 官方网站 [`oguzhaninan.github.io/Stacer-Web/`](https://oguzhaninan.github.io/Stacer-Web/) 获取有关 Stacer 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE 软件包安装 Stacer：

1. 打开软件管理器并搜索 `Stacer`。
2. 点击 `Stacer`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 并点击安装。

### 通过终端通过 APT 安装 Stacer：

```bash
sudo apt install stacer
```

## Bleachbit

访问 Bleachbit 官方网站 [`www.bleachbit.org/`](https://www.bleachbit.org/) 获取有关 Bleachbit 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 软件包安装 Bleachbit：

1. 打开软件管理器并搜索 `Bleachbit`。
2. 点击 `Bleachbit`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Bleachbit：

```bash
sudo apt install bleachbit
```

### 通过终端通过 FLATPAK 安装 Bleachbit：

```bash
flatpak install flathub org.bleachbit.BleachBit
```

## SoundConverter

访问 SoundConverter 官方网站 [`soundconverter.org/`](https://soundconverter.org/) 获取有关 SoundConverter 的所有信息。

### 通过终端通过 FLATPAK 安装 SoundConverter：

```bash
flatpak install flathub org.soundconverter.SoundConverter
```

## Converseen

访问 Converseen 官方网站 [`converseen.fasterland.net/`](https://converseen.fasterland.net/) 获取有关 Converseen 的所有信息。

### 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 软件包安装 Converseen：

1. 打开软件管理器并搜索 `Converseen`。
2. 点击 `Converseen`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 通过终端通过 APT 安装 Converseen：

```bash
sudo apt install converseen
```

### 通过终端通过 FLATPAK 安装 Converseen：

```bash
flatpak install flathub net.fasterland.converseen
```

### 通过终端通过 SNAP 安装 Converseen：

```bash
sudo snap install converseen
```





# 通过软件管理器通过 FLATPAK 软件包安装 Czkawka

1. 打开软件管理器并搜索 `Czkawka`。
2. 点击 `Czkawka`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 并点击安装。

# 在终端中通过 FLATPAK 安装 Czkawka

```bash
flatpak install flathub com.github.qarmin.czkawka
```

# 在终端中通过 SNAP 安装 Czkawka

```bash
sudo snap install czkawka
```

# 通讯

即时通讯软件允许用户通过网络上的文本进行即时通信。与电子邮件不同，对话是实时发生的，并且通常带有表情符号、语音聊天、视频聊天和文件共享等功能。它对于快速交流非常有用，但依赖于中央服务器，这引发了隐私担忧。某些服务包括聊天室和移动消息，增强了连接性。然而，用户可能面临服务停用和隐私问题。

Discord 是一个用于即时消息、语音和视频通话的社交平台。它通过服务器支持社区，用户可以在其中聊天、分享媒体和闲逛。由于拥有适用于各大平台的应用程序，它在玩家和各种兴趣小组中非常流行。Discord 提供了私信和群聊工具、无缝交互的低延迟技术以及自定义审核功能。它将日常对话的便利性与大型社区的兴奋感相结合，使数字聚会变得简单且包容容。更多信息请访问 [`discord.com`](https://discord.com/)。

来自微软的 Skype 提供免费的视频、语音通话和消息服务。它可以在各种设备上运行，且基础功能免费，电话通话和短信提供付费选项。Skype 连接了商业世界，增强了协作。它提供即时消息、语音聊天等功能，并为用户提供唯一 ID。尽管它不支持紧急电话，但它提供了视频聊天背景模糊等功能。最近，Skype 集成了 Bing AI 聊天机器人。更多信息请访问 [`skype.com`](https://skype.com/)。

Session 是由 Oxen Project 开发的一款注重隐私的聊天应用。它适用于 macOS、Windows、Linux、iOS 和 Android，使用区块链网络进行安全通信，无需手机号码或电子邮箱。相反，用户拥有一个唯一的 66 位 ID。尽管缺乏双重身份验证且协议不断演进，但其加密经过独立验证。Session 提供了一种交换消息、语音备注和媒体的安全方式。更多信息请访问 [`getsession.org`](https://getsession.org/)。

Pidgin 是一个免费的开源即时客户端，支持许多协议。它允许用户通过一个界面连接到各种服务。它以带有 Off-the-Record Messaging 插件的强加密而闻名，在隐私爱好者中非常流行，并包含在 Tails OS 中。Pidgin 拥有友好的 GTK+ 界面，适用于多个操作系统，并支持通过插件扩展以增加额外功能。更多信息请访问 [`pidgin.im`](https://pidgin.im/)。

Ferdium 是一款桌面应用程序，将你喜爱的服务整合到一个平台中以便于访问。它支持同一服务的多个账户，提供工作空间以区分个人和职业生活，并包含一个待办事项面板。添加自定义服务非常简单，确保了灵活性。Ferdium 优先考虑隐私，提供跨设备云同步，并休眠未使用的服务以节省资源。它源自 Franz，通过额外的功能和对 Franz 账户的兼容增强了体验。更多信息请访问 [`ferdium.org`](https://ferdium.org/)。

Signal 是一款采用顶尖加密的安全消息应用。它提供免费的文本、语音消息、照片、视频和通话，即使是长途也是免费的。Signal 包含加密贴纸和群聊，没有广告、追踪器或与大型科技公司的关联。作为一个由捐赠支持的非营利组织，它代表了隐私和可访问性。更多信息请访问 [`signal.org`](https://signal.org/)。

Telegram 是一款结合了通信和社交网络的讯工具应用。它于 2013 年发布，支持端到端加密的消息、媒体共享以及语音或视频通话。用户可以享受故事（Stories）、大型小组和用于广播的频道。Telegram 的开放 API 允许自定义机器人和微应用，丰富了用户交互。它在各大平台上均可用，以其安全性、易于使用的界面和丰富的功能而脱颖而出。更多信息请访问 [`telegram.org`](https://telegram.org/)。

## Discord

访问 Discord 官方网站 [`discord.com/`](https://discord.com/) 获取关于 Discord 的所有信息。

# 通过软件管理器通过 FLATPAK 软件包安装 Discord

1. 打开软件管理器并搜索 `Discord`。
2. 点击 `Discord`，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

# 在终端中通过 FLATPAK 安装 Discord

```bash
flatpak install flathub com.discordapp.Discord
```

# 在终端中通过 SNAP 安装 Discord

```bash
sudo snap install discord
```

## Skype

访问 Skype 官方网站 [`www.skype.com/en/`](https://www.skype.com/en/) 获取关于 Skype 的所有信息。

# 通过软件管理器通过 FLATPAK 软件包安装 Skype

1. 打开软件管理器并搜索 `Skype`。
2. 点击 `Skype`，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

# 在终端中通过 APT 安装 Skype

```bash
sudo apt update
sudo apt install software-properties-common apt-transport-https curl ca-certificates
curl -fsSL https://repo.skype.com/data/SKYPE-GPG-KEY | sudo gpg --dearmor | sudo tee /usr/share/keyrings/skype.gpg > /dev/null
echo deb [arch=amd64 signed-by=/usr/share/keyrings/skype.gpg] https://repo.skype.com/deb stable main | sudo tee /etc/apt/sources.list.d/skype.gpg
```

# 通过 FLATPAK 安装 Skype（继续）

```bash
sudo apt update
sudo apt install skypeforlinux
```

# 在终端中通过 FLATPAK 安装 Skype

```bash
flatpak install flathub com.skype.Client
```

# 在终端中通过 SNAP 安装 Skype

```bash
sudo snap install skype
```

# 在 GUI 中通过 .deb 安装 Skype

导航至发布页面：[`repo.skype.com/SYSTEM PACKAGE/pool/main/s/skypeforlinux/`](https://repo.skype.com/rpm/pool/main/s/skypeforlinux/)

点击最新的 `skypeforlinux__amd64.deb` 下载 Skype。

进入“下载下载文件夹。

双击 `skypeforlinux__amd64.deb`。

点击安装。

# Session

访问 Session 官方网站 [`getsession.org/`](https://getsession.org/) 获取关于 Session 的所有信息。

# 在终端中通过 FLATPAK 安装 Session

```bash
flatpak install flathub network.loki.Session
```

## Pidgin

访问 Pidgin 官方网站 [`www.pidgin.im/`](https://www.pidgin.im/) 获取关于 Pidgin 的所有信息。

# 通过软件管理器通过 SYSTEM PACKAGE/FLATPAK 软件包安装 Pidgin

1. 打开软件管理器并搜索 `Pidgin`。
2. 点击 `Pidgin`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

# 在终端中通过 APT 安装 Pidgin

```bash
sudo apt install pidgin
```

# 在终端中通过 FLATPAK 安装 Pidgin

```bash
flatpak install flathub im.pidgin.Pidgin
```

## Ferdium

访问 Ferdium 官方网站 [`ferdium.org/`](https://ferdium.org/) 获取关于 Ferdium 的所有信息。

# 通过软件管理器通过 FLATPAK 软件包安装 Ferdium

1. 打开软件管理器并搜索 `Ferdium`。
2. 点击 `Ferdium`，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

# 在终端中通过 FLATPAK 安装 Ferdium

```bash
flatpak install flathub org.ferdium.Ferdium
```

# 在终端中通过 SNAP 安装 Ferdium

```bash
sudo snap install ferdium
```





# 安装 Signal

## 通过终端通过 FLATPAK 安装 Signal：

```
flatpak install flathub org.signal.Signal
```

## 通过终端通过 SNAP 安装 Signal：

```bash
sudo snap install signal-desktop
```

## Telegram

访问 Telegram 官方网站 [`telegram.org/`](https://telegram.org/) 了解关于 Telegram 的所有信息。

## 通过软件管理器通过 FLATPAK 软件包安装 Telegram：

1. 打开软件管理器并搜索 Telegram。
2. 点击 Telegram，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

## 通过终端通过 FLATPAK 安装 Telegram：

```bash
flatpak install flathub org.telegram.desktop
```

## 通过终端通过 SNAP 安装 Telegram：

```bash
sudo snap install telegram-desktop
```

# 远程办公

远程办公软件允许员工在任何地方进行协作、通信和任务管理，减少了对物理办公室的需求。这项技术自 20 世纪 70 年代以来不断进化，并在互联网和云计算的兴起下蓬勃，支持居家办公和混合办公模式。它提供了成本效益、灵活性并能够接触更广泛的人才池，但挑战包括面对面互动减少以及潜在的孤立感。

Zoom 是一款视频会议应用，在新冠肺炎期间通过在虚拟会议中使用视频、音频和聊天连接数百万用户而广受欢迎。它是免费下载的，并提供付费和免费计划。免费计划支持最多 100 人、时长 40 分钟的会议。用户可以共享屏幕、文件并进行私聊。加入会议不需要账户，但主持会议需要。它的易用性以及即使在免费版中也能聚集大型群体的能力，使其成为许多人的首选。访问官方网站 [`zoom.us/`](https://zoom.us/)。

Slack 是一款业务消息传递应用，旨在增强团队通信与协作。它提供专用通道，无论位置或时区如何，都能在团队之间进行无缝信息共享和交互。Slack 支持灵活的异步工作，允许在需要时访问信息和同事。它通过让每个人平等地访问共享、可搜索的信息来促进包容性，并加速决策制定。通过集成生成式 AI 和各种应用程序，Slack 简化了工作流。无论是通过消息、音频、视频还是实时聚会（huddles），Slack 都能适应多种工作偏好，在安全环境中将大小团队团结在一起。访问官方网站 [`slack.com/`](https://slack.com/)。

Citrix Workspace 应用为用户生产力提供了对所有基本资源的安全且即时访问，整合了虚拟桌面、应用程序和网络服务，并具有单点登录等功能。它是适用于云环境和本地环境的通用客户端，通过 `HDX` 等技术取代了 Citrix Receiver，在所有主流操作系统和浏览器上提供高定义体验。该应用确保了应用程序和桌面的安全、高效管理，并通过高级搜索和无缝网络浏览增强用户体验。访问官方网站 [`www.citrix.com/`](https://www.citrix.com/)。

## Zoom

访问 Zoom 官方网站 [`zoom.us/`](https://zoom.us/) 了解关于 Zoom 的所有信息。

## 通过终端通过 APT 安装 Zoom：

```bash
sudo apt update
sudo apt install gdebi libglib2.0-0 libxcb-shape0 libxcb-shm0 libxcb-xfixes0 libxcb-randr0 libxcb-image0 libfontconfig1 libgl1-mesa-glx libxi6 libsm6 libxrender1 libpulse0 libxcomposite1 libxslt1.1 libsqlite3-0 libxcb-keysyms1 libxcb-xtest0 ibus libegl1-mesa libxcb-cursor0
```

## 到发布页面：

[`zoom.us/download?os=linux`](https://zoom.us/download?os=linux)

1. 点击与 Linux 类型同一行的框。
2. 选择 `Debian`。
3. 点击与 OS 架构同一行的框。
4. 选择 `64-bit`。
5. 点击 `Download` 下载 Zoom。
6. 进入你的“下载”文件夹。
7. 双击 `zoom_amd64.deb`。
8. 点击 `Install`。

## Slack

访问 Slack 官方网站 [`slack.com/intl/en-gb/`](https://slack.com/intl/en-gb/) 了解关于 Slack 的所有信息。

## 通过软件管理器通过 FLATPAK 软件包安装 Slack：

1. 打开软件管理器并搜索 Slack。
2. 点击 Slack，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

## 通过终端通过 FLATPAK 安装 Slack：

```bash
flatpak install flathub com.slack.Slack
```

## 通过终端通过 SNAP 安装 Slack：

```bash
sudo snap install slack
```

## Citrix Workspace

访问 Citrix Workspace 官方网站 [`www.citrix.com/products/receiver.html`](https://www.citrix.com/products/receiver.html) 了解关于 Citrix Workspace 的所有信息。

## 在 GUI 中通过 .deb 安装 Citrix Workspace：

1. 进入发布页面 [`www.citrix.com/downloads/workspace-app/`](https://www.citrix.com/downloads/workspace-app/)。
2. 点击 `Workspace app for Linux`。
3. 点击 `Citrix Workspace app for Linux`。
4. 点击 `Debian Packages`。
5. 点击 `Full Packages (Self-Service Support)`。
6. 点击 Citrix Workspace app for Linux (x86_64) 下的 `Download File` 下载 Citrix Workspace。
7. 进入你的“下载”文件夹。
8. 双击 `icaclient_24.5.0.76_amd64.deb`。
9. 点击 `Install`。

# 云办公套件

云办公套件是在线工具，通过提供对协作和生产力应用的移动访问来增强业务敏捷性。这种向云端的转变在 Linux 桌面等设备的支持下，使远程工作人员能够实时连接并共享信息。

## Google Docs 编辑器

Google Docs 套件是 Google Drive 的一部分，提供了基于 Web 的生产力工具，包括 `Docs`、`Sheets`、`Slides`、`Drawings`、`Forms`、`Sites` 和 `Keep`。可以通过在线或移动设备访问，支持修订历史、机器学习增强和多种格式支持，实现实时协作。该套件简化了文档的创建和共享，促进了跨环境的团队协作。

## Microsoft 365

Microsoft 365 是微软的一套套件，融合了生产力工具、协作功能和云服务。它包含了熟悉的应用程序，如 `Word`、`Excel` 和 `PowerPoint`，以及 `Outlook.com`、`OneDrive` 和 `Microsoft Teams`。它专为个人和企业使用设计，为 `Windows`、`macOS` 和移动设备提供程序，以及 Web 版本。Microsoft 365 还具有如 `Exchange Server` 和 `SharePoint` 等企业级解决方案，以及提供访问桌面版软件、托管电子邮件和内网服务的订阅计划。

## Zoho Office 套件

Zoho Office 套件是一套为现代团队协作和生产力设计的全面 Web 端套件。它结合了广泛的应用程序，包括文字处理、电子表格、演示文稿、数据库、笔记等，并集成了用于 `CRM`、项目管理和发票的级工具。该平台通过支持随地办公、提供无缝共享以及通过云文档管理确保移动性来鼓励协作。





访问 Microsoft 365 官网 [https://www.microsoft.com/en-gb/microsoft-365/] 了解有关 Microsoft 365 的所有信息。

## 通过图形界面浏览器访问 Microsoft 365
导航至网页：
[https://www.microsoft.com/en-gb/microsoft-365/]
登录以访问 Microsoft 365。

## Zoho Office Suite
访问 Zoho Office Suite 官网 [https://www.zoho.com/officesuite/] 了解有关 Zoho Office Suite 的所有信息。

## 通过图形界面浏览器访问 Zoho Office Suite
[https://www.zoho.com/officesuite/]
登录以访问 Zoho Office Suite。

## AI 内容生成
AI 内容生成使用 transformers 和大语言模型等先进 AI 技术来创建文本、图像等内容。尽管最初存在偏见和不准确等问题，但这项技术正在改变我们生产和与媒体互动的方式。它的潜力正在改变业务和创意流程，标志着数字创新的新纪元。

Easy Diffusion 通过针对所有平台的一键安装简化了 Stable Diffusion 的使用。它不需要技术设置，并具有用户友好的界面。它支持 ControlNet、SDXL、多个 LoRA、简单的嵌入、无缝平铺、重绘、更快处理、更低的 VRAM 占用、WebP 格式、撤销操作、新采样器以及改进的放大功能。这让每个人都能使用先进的文本生成图像 AI。

oobabooga 是一个通 Gradio Web UI，用于与大语言模型交互，包括 Transformers、GPTQ 和 Llama。它有三种界面模式——默认、笔记本和聊天，并支持 ExLlamaV2 和 AutoGPTQ 等多个后端。用户可以通过下拉菜单切换模型，并通语音输入/输出、翻译等扩展增强体验。它支持与自定义角色聊天、精确的聊天模板，并集成 Transformers 库以实现高效的模型加载和 CPU 推理。此外，它具有兼容 OpenAI 的 API 服务器，是文本生成任务的全面工具。

Stable Diffusion 中的负面提示词（Negative prompt）允许用户指定图像中不想要的元素，例如“模糊”或“重复”，帮助模型避免这些元素。这种技术通过精炼细节和准确性来提高图像质量，无需复杂的指令。

Upscayl 是一款免费开源的 AI 图像放大工具，利用深度学习增强低分辨率照片。它由 TGS963 和 Nayam Amarshe 创建，可在多个平台上运行，并将图像放大高达 4 倍而不丢失细节。它使用先进的 AI 技术锐化图像、增强质量并减少伪影。其简单的界面和快速处理使其适用于需要高质量图像放大的普通用户和专业人士。

Stable Diffusion Web UI 简化了 Stable Diffusion 的使用，具有易于安装、通过文本生成和修改图像，以及外扩（outpainting）和内绘（inpainting）模式。它包括用于精确结果的注意力调整、用于迭代处理的循环以及用于提高图像质量的各种放大选项。用户可以训练自定义嵌入，使用 AI 增强的工具进行面部和图像修复，并探索样式应用和提示词编辑等创意控制。它支持在适中的硬件上高效运行，与流行扩展集成，并提供带有进度跟踪和实时预览的直观界面。

## Easy Diffusion
访问 Easy Diffusion 官网 [https://easydiffusion.github.io/] 获取更多信息。

### 在终端中通过 APT 安装 Easy Diffusion
```bash
sudo apt update
```
导航至发布页面：
[https://github.com/easydiffusion/easydiffusion/releases]
下载最新的 `Easy-Diffusion-Linux.zip`。
进入 `~/Downloads` 并双击 `Easy-Diffusion-Linux.zip`。
选择 `easy-diffusion` 并点击 `Extract`（提取）。
导航至 `~/Downloads/easy-diffusion`。
右键点击空白处并在终端中打开。
运行命令：
```bash
./start.sh
```

### 为 Easy Diffusion 创建桌面快捷方式
打开终端并输入：
```bash
cd /usr/share/applications
```
运行：
```bash
sudo gedit easy-diffusion1.desktop
```
使用以下内容更新：
```ini
[Desktop Entry]
Name=Easy Diffusion
Comment=Easy Diffusion
Exec=./Downloads/easy-diffusion/start.sh
Icon=terminal
Terminal=true
Type=Application
Categories=Utility;Game;
```
保存并退出编辑器。

## oobabooga (Text Generation GUI)
访问 oobabooga (Text Generation GUI) 官网 [https://github.com/oobabooga/text-generation-webui] 获取更多信息。

### 在终端中通过 .sh 安装 oobabooga (Text Generation GUI)
导航至发布页面：
[https://github.com/oobabooga/text-generation-webui]
下载 `text-generation-webui-main.zip`。
进入 `~/Downloads` 并双击 `text-generation-webui-main.zip`。
选择 `text-generation-webui-main` 并点击 `Extract`（提取）。
导航至 `~/Downloads/text-generation-webui-main`。
右键点击空白处并在终端中打开。
运行命令：
```bash
./start_linux.sh
./update_linux.sh
```
### 为 oobabooga 创建桌面快捷方式
打开终端并输入：
```bash
cd /usr/share/applications
```
运行：
```bash
sudo gedit easy-diffusion.desktop
```
使用以下内容更新：
```ini
[Desktop Entry]
Name=oobabooga (Text Generation GUI)
Comment=oobabooga (Text Generation GUI)
Exec=./Downloads/text-generation-webui-main/start_linux.sh
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```
保存并退出编辑器。

## Stable Diffusion 的负面提示词
使用以下负面提示词来避免不想要的元素：
`((((extra fingers))))`, `(((poorly hands))))`, `(((poorly drawn face))))`, `(((mutation))))`, `(((deformed))))`, `(((bad proportions))))`, `(((extra limbs))))`, `(((glitchy))))`, `(((extra hands))))`, `(((mangled fingers))))`, `(((portrait))))`, `(((text))))`, `(((words))))`, `(((copyright))))`, `(((realism))))`, `(((2girl))))`, `(((3girl))))`, `(((4girl))))`, `(((helmet))))`, `(((multiple_breasts))))`, `(((flowers))))`, `(((blur))))`, `(((terrible))))`, `(((awful))))`, `(((copyright))))`, `((trademark)))), `(((watermark))))`, `((((censorship))))`, `(((censored))))`, `(((deformed face))))`, `(((bad anatomy))))`, `(((deformed face))))`, `(((ugly))))`, `(((deformed hands))))`, `(((blurry))))`, `(((multiple_breasts))))`, `(((multiple_nipples))))`, `(((jpeg artifacts))))`, `(((signature))))`, `(((username))))`, `(((blurry))))`, `(((monochrome))))`, `(((asymmetrical breasts))))`, `(((cropped))))`, `(((worst quality))))`, `((((low quality))))`, `(((normal quality))))`, `(((extra digit))))`, `(((fewer digits))))`, `(((lowres))))`, `(((artist name))))`, `(((poorly draw))))`, `(((messy drawing))))`, `(((extra ears))))`, `(((broken legs))))`, `(((puffy nipples))))`, `(((disformed))))`, `((((long neck))))`, `(((out of frame))))`, `(((crossed eyes))))`, `(((bad hands))))`, `(((error))))`, `(((missing fingers))))`, `(((normal quality))))`, `(((mutated))))`, `(((broken legs))))`, `(((hands inside body))))`, `(((extra leg))))`, `(((third leg))))`, `(((amputee))))`, `(((extra breasts))))`, `(((fused hands))))`, `(((claws))))`, `(((more than 2 nipples))))`, `(((lineart))))`, `(((simple background))))`, `(((floating limbs))))`, `(((disconnected limbs))))`, `(((out of focus))))`, `(((conjoined))))`, `(((blended))))`.





`fused`, `pathetic`, `sloppy`, `liquid collarbone`, `disappearing arms`, `missing breasts`, `short arm`, `missing arms`, `more than 2 legs`, `extra arms`, `fused fingers`, `malformed hands`, `missing hand`, `missing hands`, `one hand with more than 5 fingers`, `one hand with less than 5 fingers`, `one hand with less than 5 digit`, `fused digit`, `bad digit`, `liquid digit`, `bad gloves`, `poorly drawn gloves`, `fused gloves`, `more than 1 left hand`, `more than 1 right hand`, `asymmetrical body`, `missing extremities`, `walleyed`, `eye bags`, `duplicate`, `dehydrated`, `cloned face`, `malformed limbs`, `blind`, `dead eyes`, `out of shot`, `logo`, `writing`.

## Stable Diffusion Web UI

访问 Stable Diffusion Web UI 官方网站 [`github.com/AUTOMATIC1111/stable-diffusion-webui`](https://github.com/AUTOMATIC1111/stable-diffusion-webui) 获取更多信息。

## 通过终端中的 `.sh` 安装 Stable Diffusion Web UI：

导航至发布页面：

[`github.com/AUTOMATIC1111/stable-diffusion-webui`](https://github.com/AUTOMATIC1111/stable-diffusion-webui)

下载最新的源代码 (zip)。

进入 `~/Downloads` 并双击 `stable-diffusion-webui-1.9.4.zip`。

选择 `stable-diffusion-webui-1.9.4` 并点击提取。

导航至 `~/Downloads/stable-diffusion-webui-1.9.4`。

右键点击空白处并选择在终端中打开。

运行命令：

```bash
./webui.sh
```

### 为 Stable Diffusion Web UI 创建桌面快捷方式：

打开终端并输入：

```bash
cd /usr/share/applications
```

运行：

```bash
sudo gedit stablediffusionwebui1.desktop
```

使用以下内容更新文件：

```ini
[Desktop Entry]
Name=Stable Diffusion Web UI
Comment=Stable Diffusion Web UI
Exec=./Downloads/stable-diffusion-webui-1.9.4/webui.sh
Icon=terminal
Terminal=true
Type=Application
Categories=Utility;Game;
```

保存并退出编辑器。

# 系统设置

Linux Mint 22 上的系统设置提供了计算机硬件、软件和配置细节的完整概述。无论是在进行故障排除、升级，还是对内存、处理器速度或操作系统版本等细节感兴趣，通过终端命令或`System Monitor`和`系统设置`等图形界面访问这些设置都能获得价值的见解。这些工具允许性能调整、安全配置和驱动程序更新，增强你对系统能力的理解和优化。

## 夜间模式
GNOME 桌面环境减少屏幕的蓝光发射，使眼睛在深夜更加舒适。此功能位于显示设置下，可以开启或关闭，并允许调整屏幕色温以减少眼劳。自动设置为从日落到日出激活，非常适合晚上工作或休息，并可以在看电影等活动期间临时禁用。此工具增强了用户晚上使用电脑的舒适度和健康。

## Redshift
Cinnamon 桌面环境上的 Redshift 根据一天的时间调整屏幕色温，减少眼睛疲劳和潜在的失眠。该工具在晚上在暖色调（2000–4000 K）和白天的冷色调（5500–6500 K）之间切换，以匹配自然光，帮助你的眼睛逐渐适应。Redshift 可配置为连续或固定设置，需要你的位置来准确跟踪太阳高度，支持 Linux 和 BSD 系统上的多显示器。此应用程序模拟你环境的周围光，以获得更舒适的屏幕体验。

## PipeWire
PipeWire 旨在通过提供低延迟、基于图形的处理引擎来增强 Linux 对音频视频的处理。它支持以前由`PulseAudio`和`JACK` 管理的各种多媒体用例，并包含一个健壮的安全模型，以便像`Flatpak`这样的容器化应用程序与音视频设备交互。作为 Linux 演进的应用开发生态系统的一部分，PipeWire 与`Wayland`和`Flatpak` 旨在成为基础组件，实现最小延迟的捕和播放、实时处理，以及跨`PulseAudio`、`JACK`、`ALSA`和`GStreamer` 应用程序的无缝集成，并支持沙箱环境。

## 环境变量
Linux Mint 22 系统变量或环境变量是用于存储信息并控制命令行应用程序和系统操作行为的动态命名值。这些变量由一个名称和一个值组成，格式为 `KEY=value`，`=` 符号周围没有空格。包含空格的值必须括在引号中，可以使用冒号（`":"`）分隔符分配多个值。变量名区分大小写，通常使用大写字母。环境变量是全局可的并被子进程继承，而 shell 变量仅局限于当前的 shell 实例。它们为自定义 Linux Mint 22 的系统和应用程序行为提供了一个多功能的工具。

## Cinnamon 背景
在 Cinnamon 中将图像设置为背景可以让你通过选择任何图像或颜色来个性化你的桌面。右键点击桌面，选择“更改桌面背景”，并通过“桌面背景偏好”对话框添加新壁纸。你还可以调整其外观以适应或填充屏幕。对于纯色，选择“无壁纸”并选择颜色。更改是即时的，对于系统级设置，管理员可以使用`dconf` 设置默认值、锁定配置并为所有用户添加额外的背景，确保设备之间统一的外观或品牌形象。

## Mount_options.conf
`Mount_options.conf` 是系统管理员的 UDisks 功能，允许自定义各种文件系统的挂载选项以确保安全和数据一致性。它在 UDisks 2.9.0 中引入，允许通过配置文件或`udev` 规则进行系统级覆盖，专门针对可移动介质等动态挂载点，优先考虑安全可靠的访问而不损害系统。它区分了文件系统类型和驱动程序，完善了对数据管理的控制，防止未经授权的访问和数据丢失，成为安全高效存储处理的关键工具。

### 启动应用程序
在 Linux Mint 22 的 Cinnamon 桌面中，“启动应用程序”允许你管理启动时启动的程序。按下 Super 键进行搜索并调整你的启动过程以提高效率。禁用默认项时要小心，因为它们通常至关重要。轻松添加新应用或调整现有应用（包括启动延迟），确保在控制运行内容和时间的情况下实现更流畅的启动，而不会让系统负载过重。

### 自动挂载卷
Linux Mint 22 启动时的自动挂载卷确保你的驱动器在系统启动时自动连接。使用许多 Linux 发行版中的`GNOME Disks` 工具，你可以轻松地设置此项。启动“磁盘”，选择你的驱动器，然后选择分区，并调整挂载选项以启用系统启动时挂载。此工具简化了向 `/etc/fstab` 文件添加条目的过程，使分区无需手动编辑配置文件即可系统范围内可用。只需重启机器，你选择的分区将自动挂载，简化了你以便即时访问的设置。

在 Linux Mint 22 中，快捷键和截图是捕捉屏幕内容的必要手段，对于分享见解、解决问题或保留记忆至关重要。它们确认了你的经历，归档了信息，并通过视觉上下文增强了文档。`Screenshot`等工具使得截图对于各种任务的高效通信和文档记录变得无足可贵。





默认的 systemd 超时时间通常设置为 90 秒，它决定了 systemd 在认为操作失败之前等待服务启动或停止的持续时间。此超时机制通过防止服务无限挂起来确保系统的响应能力。然而，为了更具灵活性，systemd 允许根据特定需求调整此超时时间，使服务能够偏离默认设置的自定义超时配置。

不可变文件和文件夹是创建后就无法修改或删除的数字资产。这一特性确保了数据的完整性和安全性，特别是在保持历史准确性和防止未经授权的更改至关重要的环境中。虽然这个概念看起来很死板，但它是防止数据篡改和丢失的屏障，让你在关键信息保持未被触动时获得可靠性和安心。

FFmpegthumbnailer 是一款轻量级工具，旨在快速生成视频缩略图，提高文件管理效率。它利用强大的 `ffmpeg` 库来解码视频帧，其功能与 `ffmpeg` 的配置绑定。FFmpegthumbnailer 以其速度快和资源占用少而闻名，对于文件管理器至关重要，它简化了为视频文件创建视觉信息缩略图的过程，有助于更快地识别和访问视频内容。

Linux `.desktop` 文件是简单的文本文件，为桌面环境提供有关软件应用程序的基本信息。它们定义了程序如何启动、其名称以及使用的图标。这些文件通过允许创建快捷方式，使用户更容易通过图形界面与应用程序交互。

在 Linux Mint 22 中，电源设置允许用户管理计算机能量消耗，这对于延长电池寿命和效率至关重要。这些设置包括屏幕亮度、睡眠模式以及笔记本盖子关闭时的行为的选项。用户可以通过系统设置面板轻松地自定义这些偏好，确保设备在节电的同时保持最佳运行。

## 夜光模式 (GNOME)

访问夜光模式 (GNOME) 官网 [`foundation.gnome.org/`](https://foundation.gnome.org/) 获取有关夜光模式 (GNOME) 的所有信息。

### 通过 GUI 设置夜光模式 (GNOME)：

1. 打开应用程序菜单并选择“设置 (Settings)”。
2. 进入左侧边栏的“显示 (Displays)”选项卡，然后点击“夜光模式 (Night Light)”。
3. 打开“夜光模式”旁边的开关将其启用。
4. 在“计划 (Schedule)”行中，点击下拉框并选择“手动计划 (Manual Schedule)”。
5. 设置激活时间为 21:00 到 06:00。
6. 调整色温度滑块，使其处于第三条和第四条白线中间点略下方的位置。

## 夜光模式 (Cinnamon & Redshift)

访问夜光模式 (Cinnamon & Redshift) 官网 [`github.com/linuxmint/cinnamon`](https://github.com/linuxmint/cinnamon) 和 [`github.com/jonls/redshift`](https://github.com/jonls/redshift) 获取有关夜光模式 (Cinnamon & Redshift) 的所有信息。

### 通过终端和 GUI 安装并设置夜光模式 (Cinnamon & Redshift)：

```bash
sudo apt install redshift redshift-gtk wayland*
```

通过以下命令进入配置目录：

```bash
cd ~/.config
```

通过输入编辑 Redshift 配置：

```bash
nano redshift.conf
```

输入以下设置：

```ini
[redshift]
temp-night=2250
transition=1
brightness=1.0
gamma=1.0

[location]
adjustment-method=vidmode
location-provider=manual
```

使用 `CTRL + S` 保存更改并使用 `CTRL + X` 退出。

# PipeWire 音频杂音与爆破声修复

访问 PipeWire 官网 [`pipewire.org/`](https://pipewire.org/) 获取有关 PipeWire 的所有信息。

### 通过命令行和 GUI 修复 PipeWire 潜在的杂音或爆破声等音频问题：

禁用音频节能功能：

```bash
echo "options snd_hda_intel power_save=0" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf
echo "options snd_hda_intel power_save_controller=N" | sudo tee -a /etc/modprobe.d/audio_disable_powersave.conf
```

验证更改：

```bash
cat /sys/module/snd_hda_intel/parameters/power_save
cat /sys/module/snd_hda_intel/parameters/power_save_controller
```

编辑 PipeWire 配置以优化性能：

```bash
sudo gedit /usr/share/pipewire/pipewire.conf
```

调整量子（quantum）设置：
- 将 `#default.clock.quantum = 1024` 修改为 `default.clock.quantum = 2048`。
- 将 `default.clock.min-quantum = 16` 修改为 `default.clock.min-quantum = 2048`。
- 将 `#default.clock.max-quantum = 2048` 更新为 `default.clock.max-quantum = 4096`。

保存更改并重启 PipeWire 服务：

```bash
systemctl --user restart pipewire.service pipewire-pulse.service pipewire-media-session.service
systemctl --user restart pipewire-multi.service
```

通过编辑增强音频优先级：

```bash
sudo gedit /etc/security/limits.conf
```

添加：

```text
@audio   -  nice      -20
```

保存并退出。

通过清除 speech-dispatcher 消除潜在冲突：

```bash
sudo apt remove speech-dispatcher
```

确保所有 PipeWire 配置中的更改保持一致。保存并备份必要文件，然后重启电脑。

# Linux Mint 22 系统变量

### 通过命令行和 GUI 设置 Linux Mint 22 系统变量：

编辑系统级 Bash 配置文件：

```bash
sudo gedit /etc/bash.bashrc
```

添加以下设置：

```bash
# Environment Variables
#export STAGING_WRITECOPY='1'
#export DXVK_ENABLE_NVAPI='1'
#export WINEESYNC='1'
#export WINEDEBUG='-all'
#export __GL_SHADER_DISK_CACHE_SKIP_CLEANUP='1'
#export __GL_THREADED_OPTIMIZATION='1'
#export STAGING_SHARED_MEMORY='1'
#export WINE_SIMULATE_WRITECOPY='1'
#export DXVK_STATE_CACHE_PATH='/home/username/.wine/drive_c/Program Files (x86)/Battle.net'
#export __GL_SHADER_CACHE='/home/username/.wine/drive_c/Program Files (x86)/Battle.net'
#export VKD3D_SHADER_CACHE_PATH='/home/username/.wine/drive_c/Program Files (x86)/Battle.net'
#export VKD3D_CONFIG='dxr'
#export exclude_processes='Agent.exe "Battle.net Helper.exe
```

在适用处将 `username` 替换为您的实际用户名。点击“保存”或通过文件菜单保存更改。

# 在 Gnome & Cinnamon 中设置图像背景

访问 Cinnamon 官网 [`github.com/linuxmint/cinnamon`](https://github.com/linuxmint/cinnamon) 获取有关 Cinnamon 的所有信息。

### 将图像设置为背景：

1. 右键点击图像文件并选择“设置为壁纸”。

# mount_options.conf

访问 udisks 官网 [`www.freedesktop.org/wiki/Software/udisks/`](https://www.freedesktop.org/wiki/Software/udisks/) 获取有关 udisks 的所有信息。

### 通过命令行和 GUI 设置 `mount_options.conf`：

```bash
sudo apt update
sudo gedit /etc/udisks2/mount_options.conf
```

添加以下内容：

```ini
[defaults]
ntfs_defaults=uid=$UID,gid=$GID
ntfs_allow=uid=$UID,gid=$GID,nls,umask,dmask,fmask,nohidden,sys_immutable,discard,force,sparse,showmeta,prealloc,no_acs_rules,acl,noatime
```

点击“保存”或通过文件菜单保存。

## Cinnamon 中的启动项

### 在 Cinnamon 中通过 GUI 添加启动项：

1. 使用 Super 键应用程序菜单。
2. 导航到“启动项”，点击 + 号并选择“选择应用程序”。
3. 输入要启动的应用程序名称，选择它并点击“添加”。

对于添加自定义命令：
1. 使用 Super 键从菜单打开“启动项”。
2. 点击 + 号并选择“自定义命令”。
3. 输入命令名称、命令本身（例如 `discord` 以启动 Discord）、详细注释，并在需要设置启动延迟。
4. 点击“保存”。

### 通过命令行添加启动项：

1. 打开终端。
2. 进入包含应用程序快捷的目录：
   ```bash
   cd /usr/share/applications
   ```
3. 列出所有文件：
   ```bash
   dir
   ```
4. 识别应用程序的 `.desktop` 文件（例如 `firefox.desktop`）。
5. 将此文件复制到启动目录：
   ```bash
   sudo cp firefox.desktop /etc/xdg/autostart
   ```

# GNOME 中的启动项

通过 GUI 在 GNOME 中添加启动项：





按下 `Super` 键打开应用程序菜单并启动“微调 (Tweaks)”。

导航到“启动应用程序 (Startup Applications)”选项卡并点击 `+` 按钮。

输入您想要自动启动的应用名称并选择“添加”。

# 使用 GNOME Disks 自动挂载分区

访问 GNOME Disks 官方网站 [`apps.gnome.org/en-GB/DiskUtility/`](https://apps.gnome.org/en-GB/DiskUtility/) 了解有关 GNOME Disks 的所有信息。

## 通过 GUI 界面自动挂载分区：

1. 从应用程序菜单启动“磁盘 (Disks)”。
2. 选择包含您想要挂载卷的磁盘。
3. 选择该磁盘上的特定卷并点击齿轮图标。
4. 选择“编辑挂载选项 (Edit Mount Options)”。
5. 将“用户会话默认 (User Session Defaults)”旁开关切换到左侧。
6. 点击“确定”确认更改。

# Cinnamon 截图快捷键

### 通过命令行和 GUI 更改闪光颜色属性：

1. 打开“文件 (Files)”应用程序并按 `CTRL + L` 启用“位置输入”模式。
2. 输入 `/usr/share/themes/` 并导航到 `Mint-Y-Dark-Red` 文件夹。
3. 在文件夹内部进入 `cinnamon` 目录。
4. 在空白处右键点击并选择“在终端打开”。
5. 执行：
```bash
sudo gedit cinnamon.css
```
6. 搜索 `flashspot` 元素并将其值更改为 `"#00FFFFFF"`。
7. 保存并退出。
8. 按 `ALT + F2` 打开 cinnamon 运行命令框，输入 `r` 并回车重启 cinnamon。

### 通过 GUI 创建“截图 (Screenshots)”文件夹：

1. 打开“文件 (Files)”应用程序并导航到 `~/Pictures` 目录。
2. 在空白处右键点击并选择创建新文件夹选项。
3. 将其重命名为“Screenshots”。

### 通过 GUI 拍摄活动窗口截图：

1. 从应用程序菜单打开“设置 (Settings)”。
2. 导航到“键盘 (Keyboard)”并选择“快捷键 (Shortcuts)”。点击“添加自定义快捷键”。
3. 命名为“Focused Window Screenshot”并输入：
```bash
bash -c "cd ~/Pictures/Screenshots && gnome-screenshot -w -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"
```
4. 添加命令并为其分配键盘快捷键，例如 `F10`。

### 通过 GUI 拍摄全屏截图：

1. 从应用程序菜单打开“设置 (Settings)”。导航到“键盘 (Keyboard)”并选择“快捷键”。
2. 点击“添加自定义快捷键”。
3. 命名为“Fullscreen Screenshot”并输入：
```bash
bash -c "cd ~/Pictures/Screenshots && gnome-screenshot -f screenshot_$(date +%d-%m-%y-%H-%M-%S).png"
```
4. 添加命令并为其分配键盘快捷键，例如 `F11`。

# GNOME 概览与 Windows 键

### 通过 GUI 更改“显示概览 (Show the Overview)”快捷键：

1. 打开应用程序菜单并选择“设置 (Settings)”。导航到“键盘 (Keyboard)”选项卡并选择“查看和自定义快捷键”。
2. 搜索“Show the overview”。
3. 按 `Super + TAB` 设置新的快捷键。

### 通过 GUI 更改“切换窗口 (Switch Windows)”快捷键：

1. 打开应用程序菜单并选择“设置 (Settings)”。
2. 导航到“键盘 (Keyboard)”选项卡并选择“查看和自定义快捷键”。
3. 搜索“Switch windows”。按 `ALT + TAB` 设置新的快捷键。

# GNOME 截图快捷键

### 通过 GUI 更改“截图 (Take a Screenshot)”快捷键：

1. 打开应用程序菜单并选择“设置 (Settings)”。
2. 导航到“键盘 (Keyboard)”选项卡并选择“查看和自定义快捷键”。
3. 搜索“Take a screenshot”。
4. 按 `F10` 设置新的快捷键。

### 通过 GUI 更改“窗口截图 (Take a Screenshot of a Window)”快捷键：

1. 打开应用程序菜单并选择“设置 (Settings)”。
2. 导航到“键盘 (Keyboard)”选项卡并选择“查看和自定义快捷键”。
3. 搜索“Take a screenshot of a window”。
4. 按 `F11` 设置新的快捷键。

### 通过 GUI 更改“交互式窗口截图 (Take a Screenshot of a Window Interactively)”快捷键：

1. 打开应用程序菜单并选择“设置 (Settings)”。
2. 导航到“键盘 (Keyboard)”选项卡并选择“查看和自定义快捷键”。
3. 搜索“Take a screenshot of a window interactively”。
4. 按 `F9` 设置新的快捷键。

#  Systemd 超时

访问 Systemd 官方网站 [`systemd.io/`](https://systemd.io/) 了解有关 Systemd 的所有信息。

### 通过命令行和 GUI 设置默认 Systemd 超时：

```bash
sudo apt update
cd /etc/systemd/
sudo gedit system.conf
```

更改：
`#DefaultTimeoutStartSec=90s`
为：
`DefaultTimeoutStartSec=30s`

点击“保存”或通过文件菜单保存进度。
运行：
```bash
sudo systemctl daemon-reload
```

# 使文件和文件夹变为不可变

访问不可变文件和文件夹官方网站 [`www.linux.org/docs/man1/chattr.html`](https://www.linux.org/docs/man1/chattr.html) 了解有关不可变文件和文件夹的所有信息。

### 通过命令行使文件和文件夹变为不可变：

```bash
sudo apt update
cd ~/Downloads
sudo chattr +i -RV CurseForge-1.251.0-17831.AppImage
```

# ffmpegthumbnailer

访问 ffmpegthumbnailer 官方网站 [`github.com/dirkvdb/ffmpegthumbnailer`](https://github.com/dirkvdb/ffmpegthumbnailer) 了解有关 ffmpegthumbnailer 的所有信息。

### 在终端通过 APT 安装 ffmpegthumbnailer：

```bash
sudo apt update
sudo apt install ffmpeg ffmpegthumbnailer gstreamer1.0-libav
rm -r ~/.cache/thumbnails/
```

# 删除 .desktop 文件

访问 .desktop 文件官方网站 [`specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html`](https://specifications.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html) 了解有关 .desktop 文件的所有信息。

### 通过终端删除 .desktop 文件：

```bash
cd /usr/share/applications
dir
sudo cp uget-gtk.desktop uget-gtk1.desktop
sudo rm -r uget-gtk.desktop
sudo update-desktop-database
```

# 电源设置

### 通过 GUI 调整电源设置：

1. 从应用程序菜单打开“设置 (Settings)”。
2. 导航到“电源 (Power)”部分。
3. 将“屏幕屏 (Screen Blank)”设置为“5 分钟”。
4. 通过选择“关闭”关闭“自动暂停 (Automatic Suspend)”。

# GNOME 扩展

GNOME Shell 扩展由第三方开发，通过允许窗口管理微调或应用启动修改等自定义功能来增强 GNOME 界面。您可以在专用网站上查找并管理这些扩展，它们带有唯一的标识符 (UUID) 以确保安全安装。虽然它们提供了从细微到重大的界面变化的各种功能增强，但用户应保持谨慎。扩展与操作系统深度集成，可能会导致系统问题或安全风险。然而，它们在提供下载之前会经过严格的安全审查，以确保创新与安全之间的平衡。访问 GNOME 官方网站 [`foundation.gnome.org/`](https://foundation.gnome.org/) 获取更多信息。

GNOME Shell Extension Manager 简化了 GNOME 扩展的安装和管理。该工具允许用户直接从 `extensions.gnome.org` 网站浏览、安装、删除、启用或禁用扩展，而无需网络浏览器。这在 Ubuntu 21.10 及更高版本中特别有用，因为默认的 Firefox 由于 Snap 格式无法安装扩展。由于从 GNOME 43 起支持应用内更新以及管理已安装扩展（包括系统扩展）的能力，它提供了一种精简的体验。它可以通过 Flathub 以 Flatpak 形式获取，是增强 GNOME 桌面环境的重要工具。访问官方网站 [`extensions.gnome.org/`](https://extensions.gnome.org/) 了解更多详情。

GNOME Shell Integration Chrome 扩展和 Firefox 加载程序有助于 GNOME 桌面环境与相应网络浏览器之间的无缝交互。它们允许用户直接从浏览器中安装、管理和应用 GNOME Shell 扩展，而无需使用终端或其他工具。这种集成简化了 GNOME 桌面体验的自定义和增强，使得对于倾向于图形界面而非命令行操作的用户来说更易使用。更多信息可以在 [`extensions.gnome.org/extension/19/user-themes/`](https://extensions.gnome.org/extension/19/user-themes/) 找到。





Linux Mint 22 上的 GNOME 桌面环境 User Themes 扩展允许用户自定义 GNOME Shell 的外观。默认情况下，`GNOME Tweaks` 无法更改 GNOME Shell 主题。安装此扩展可以克服这一局限性，直接在环境中提供更多个性化选项。

ArcMenu 是一款顶级的 GNOME Shell 扩展，提供传统的应用菜单体验，具有从简单到新奇的多种布局。它具有内置的 `GNOME search`、快速系统快捷键访问，以及样式化的更新（例如可调整的搜索框圆角）。最新版本包含了错误修复和改进，例如针对类别和应用程序的独立图标大小设置，以及 Windows 11 风格的按钮子菜单。更多信息请访问 [`extensions.gnome.org/extension/1228/arcmenu/`](https://extensions.gnome.org/extension/1228/arcmenu/)。

Dash to Panel 是一款多功能 GNOME Shell 扩展，它将启动栏转换为统一的主面板，将应用程序启动器和系统托盘合并，提供类似于 KDE Plasma 和 Windows 7+ 的流畅体验。它消除了对独立 dock 栏的需求，可以轻松访问运行中和收藏的应用程序。它具有高度可定制性，允许用户调整面板的外观、行为和功能，包括运行指示器、窗口预览和智能隐藏（intellihide）。自定义运行指示器、悬停实时预览、启动应用的键盘快捷键以及多显示器支持等功能增强了可用性，让您的工作区感觉更加个性化且高效。更多信息请访问 [`extensions.gnome.org/extension/1160/dash-to-panel/`](https://extensions.gnome.org/extension/1160/dash-to-panel/)。

Desktop Icons (NG) 是 GNOME Shell 的增强扩展，作为官方 Desktop Icons 扩展的修订版。它引入了跨桌面、应用程序和 Nautilus 窗口的直观拖放功能，以及针对多个文件的多功能“用...打开”选项。它确保即使图标名称过长，在悬停或点击时也能显示完整全名，并在桌面活动频繁时保持保持合成器的稳定性。更多详情请访问 [`extensions.gnome.org/extension/2087/desktop-icons-ng-ding/`](https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/)。

Tray Icons: Reloaded 是一款 GNOME Shell 扩展，通过将托盘图标返回顶部面板来重振您的桌面活力，并丰富了新功能。它引入了带有“三点”图标的溢出模式、可自定义的托盘位置、图标限制和大小设置。用户可以微调图标的颜色饱和度、对比度和亮度，以及可调整的托盘、图标边距和内边距。更多信息请访问 [`extensions.gnome.org/extension/2890/tray-icons-reloaded/`](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)。

# GNOME Shell Extension Manager

访问 GNOME Shell Extension Manager 官方网站 [`github.com/mjakeman/extension-manager`](https://github.com/mjakeman/extension-manager) 了解关于 GNOME Shell Extension Manager 的所有信息。

### 通过软件管理器通过 FLATPAK 包安装 GNOME Shell Extension Manager

1. 打开软件管理器并搜索 `GNOME Shell Extension Manager`。
2. 点击 `GNOME Shell Extension Manager`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 GNOME Shell Extension Manager

```
sudo apt update
sudo apt install gnome-shell-extension-manager
```

### 在终端通过 FLATPAK 安装 GNOME Shell Extension Manager

```bash
flatpak install flathub com.mattjakeman.ExtensionManager
```

# GNOME Shell Integration

有关 GNOME Shell 扩展集成的所有信息，请访问 GNOME Shell Integration 官方网站：

- [`chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep`](https://chrome.google.com/webstore/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)
- [`addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/`](https://addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/)

### 通过 GUI 安装 GNOME Shell Integration Chrome 扩展

导航至发布页面：
[`chromewebstore.google.com/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep`](https://chromewebstore.google.com/detail/gnome-shell-integration/gphhapmejobijbbhgpjhcjognlahblep)

点击“添加至 Chrome”，然后点击“添加扩展”进行确认。

### 通过 GUI 安装 GNOME Shell Integration Firefox 插件

导航至发布页面：
[`addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/`](https://addons.mozilla.org/en-GB/firefox/addon/gnome-shell-integration/)

点击“添加到 Firefox”，然后点击“添加”进行确认。

请务必勾选“允许此扩展在无密窗口中运行”，以确保在所有会话中可用。

# User Themes

访问 User Themes 官方网站 [`gitlab.gnome.org/GNOME/gnome-shell-extensions`](https://gitlab.gnome.org/GNOME/gnome-shell-extensions) 了解关于 User Themes 的所有信息。

### 通过 GUI 安装 User Themes GNOME 扩展

导航至发布页面：
[`extensions.gnome.org/extension/19/user-themes/`](https://extensions.gnome.org/extension/19/user-themes/)

点击“安装”并确认添加 User Themes。

# ArcMenu

访问 ArcMenu 官方网站 [`gitlab.com/arcmenu/ArcMenu`](https://gitlab.com/arcmenu/ArcMenu) 了解关于 ArcMenu 的所有信息。

### 通过 GUI 安装 ArcMenu GNOME 扩展

导航至发布页面：
[`extensions.gnome.org/extension/3628/arcmenu/`](https://extensions.gnome.org/extension/3628/arcmenu/)

点击“安装”并确认添加 ArcMenu。

# Dash to Panel

访问 Dash to Panel 官方网站 [`github.com/home-sweet-gnome/dash-to-panel`](https://github.com/home-sweet-gnome/dash-to-panel) 了解关于 Dash to Panel 的所有信息。

### 通过 GUI 安装 Dash to Panel GNOME 扩展

导航至发布页面：
[`extensions.gnome.org/extension/1160/dash-to-panel/`](https://extensions.gnome.org/extension/1160/dash-to-panel/)

点击“安装”并确认添加 Dash to Panel。

### 通过 GUI 调整 Dash to Panel 托盘字体大小

1. 右点击 `Dash to Panel` 打开右键菜单。
2. 选择 `Dash to Panel Settings`。在设置窗口中，导航到 `Fine-Tune` 标签页。
3. 调整 `Tray Font Size` 滑块到 `21px`。

# Desktop Icons (NG)

访问 Desktop Icons (NG) 官方网站 [`github.com/rastersoft/gnome-shell-extension`](https://github.com/rastersoft/gnome-shell-extension) 了解关于 Desktop Icons (NG) 的所有信息。

### 通过 GUI 安装 Desktop Icons (NG) GNOME 扩展

导航至发布页面：
[`extensions.gnome.org/extension/2087/desktop-icons-ng-ding/`](https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/)

点击“安装”并确认添加 Desktop Icons (NG)。

# Tray Icons: Reloaded

访问 Tray Icons: Reloaded 官方网站 [`github.com/MartinPL/Tray-Icons-Reloaded`](https://github.com/MartinPL/Tray-Icons-Reloaded) 了解关于 Tray Icons: Reloaded 的所有信息。

### 通过 GUI 安装 Tray Icons: Reloaded GNOME 扩展

导航至发布页面：
[`extensions.gnome.org/extension/2890/tray-icons-reloaded/`](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)

点击“安装”并确认添加 Tray Icons: Reloaded。

# Cinnamon Applets




Cinnamon 插件通过提供实用工具来增强您的 Linux Mint 22 体验，例如“强制退出”插件，它允许您通过点击来关闭无响应的窗口。要创建一个插件，需要分配一个唯一的 ID，创建一个包含 `metadata.json` 文件的文件夹用于存储插件信息，以及一个用于代码的 `applet.js` 文件。插件存储在本地或系统范围的 Cinnamon 插件目录。通过简单的 API，插件可以适应各种面板方向和尺寸，确保在多个实例中的功能可用性。请访问 Cinnamon 官方网站 [`github.com/linuxmint/cinnamon`](https://github.com/linuxmint/cinnamon) 获取更多详情。

Cinnamon 中的分组窗口列表（Grouped Window List）插件在面板中按应用程序组织打开的窗口，与其他操作系统的任务栏功能。它通过将同一应用程序的多个实例归类到单个图标下，简化了它们之间的导航，提供悬停预览，并允许快速切换或管理窗口。该插件增强了效率和工作区的组织，使管理已打开的应用并保持桌面环境整洁变得更加容易。可以在 [`cinnamon-spices.linuxmint.com/applets/view/27`](https://cinnamon-spices.linuxmint.com/applets/view/27) 了解更多。

Cinnamon Windows Alt-Tab 切换器提供多种样式，如图标、缩略图或组合，通过更大的图标和详细预览使导航更加容易。用户可以从系统设置调整图标大小和样式。Cinnamon-Alt-Tab-Enhanced 项目增加了诸如支持多个工作区、更大的缩略图视图以及全面的键盘鼠标支持等功能，增强了用户体验。可以在 [`github.com/linuxmint/cinnamon-screensaver`](https://github.com/linuxmint/cinnamon-screensaver) 找到更多信息。

Cinnamon 菜单插件简化了访问系统上安装的应用程序。只要有相应的 `.desktop` 文件，用户就可以通过输入名称或别名轻松启动应用程序。该插件还将应用程序组织分类分类，使导航和发现更加直观。它弥补了用户便利与系统功能之间的鸿沟，确保查找和运行任何应用程序都是一个流畅且直接的过程。可以在 [`github.com/linuxmint/Cinnamon`](https://github.com/linuxmint/Cinnamon) 找到更多详情。

Cinnamon 桌面环境的日历插件提供了类似于 Windows XP 的时间显示，Windows XP 是微软广受好的操作系统。此功能允许用户模拟 Windows XP 的外观和氛围，同时避免其编程限制。此外，它还支持 12 小时制，与军事风格的 24 小时制形成对比，提供了一种友好的计时方法。访问 [`github.com/linuxmint/cinnamon-spices-applets`](https://github.com/linuxmint/cinnamon-spices-applets) 获取更多信息。

## 分组窗口列表

通过图形用户界面设置分组窗口列表，首先从应用程序菜单启动 `Firefox`。

打开后，最小化该程序。

右键点击面板上的 `Firefox` 图标并选择“配置”。

导航到“面板”（Panel）选项卡。

在“按钮标签”（Button label）选项中，点击框框并选择“窗口标题”（Window Title）。

## Cinnamon Windows Alt-Tab 切换器

通过图形用户界面设置 Cinnamon Windows Alt-Tab 切换器，请遵循以下步骤。

打开应用程序菜单并运行 `Windows` 命令。

导航到 `Alt-Tab` 区域并找到“Alt-Tab 切换器样式”（Alt-Tab switcher style）选项。

点击旁边的复选框并从下拉菜单选择“仅缩略图”（Thumbnails only）。

## Cinnamon 菜单插件

通过图形用户界面设置 Cinnamon 菜单插件，右键点击菜单按钮并选择“配置”。

导航到“面板”（Panel）选项卡。通过向右滑动开关启用“使用自定义图标和标签”（Use a custom icon and label）选项。

在“文本”（Text）字段中，按 `CTRL` + `A` 选择所有文本，然后按 `DEL` 清空。

输入“ Start”作为新标签。对于图标，点击同一行中的框框。

在搜索框中，按 `CTRL` + `A` 选择所有文本，然后按 `DEL` 清空。

在搜索中输入 `start-here`，当它出现时选择 `start-here` 图标，并点击“选择”完成选择。

## Cinnamon 日历插件

要通过 GUI 在 Cinnamon 日历插件中设置自定义日期格式，右键点击通常位于屏幕右下角的 `Calendar` 插件。

从插件中选择“配置”。

```
%I:%M
```




使用方向键找到 GNOME 并按下 `SPACEBAR` 选择它，它会用星号标记它。

使用方向键移动到 "Ok" 并按下 `Enter` 开始安装。

# Tasksel

访问 Tasksel 官方网站 [`github.com/ParrotSec/tasksel`](https://github.com/ParrotSec/tasksel) 了解关于 Tasksel 的所有信息。

在终端中通过 APT 安装 Tasksel：

```
sudo apt update
sudo apt install tasksel
```

# KDE Plasma

访问 KDE Plasma 官方网站 [`kde.org/plasma-desktop/`](https://kde.org/plasma-desktop/) 了解关于 KDE Plasma 的所有信息。

在终端中通过 APT 安装 KDE Plasma：

```bash
sudo apt update
sudo apt install kde-full
```

在终端中通过 Tasksel 安装 KDE Plasma：

输入 `tasksel`。

使用方向键找到 KDE Plasma 并按下 `SPACEBAR` 选择它，它会用星号标记它。

使用方向键移动到 "Ok" 并按下 `Enter` 开始安装。

# LXDE

访问 LXDE 官方网站 [`www.lxde.org/`](https://www.lxde.org/) 了解关于 LXDE 的所有信息。

在终端中通过 APT 安装 LXDE：

```bash
sudo apt update
sudo apt install lxde
```

在终端中通过 Tasksel 安装 LXDE：

输入 `tasksel`。

使用方向键找到 LXDE 并按下 `SPACEBAR` 选择它，它会用星号标记它。

使用方向键移动到 "Ok" 并按下 `Enter` 开始安装。

# XFCE

访问 XFCE 官方网站 [`www.xfce.org/`](https://www.xfce.org/) 了解关于 XFCE 的所有信息。

在终端中通过 APT 安装 XFCE：

```bash
sudo apt update
sudo apt install xfce
```

在终端中通过 Tasksel 安装 XFCE：

输入 `tasksel`。

使用方向键找到 XFCE 并按下 `SPACEBAR` 选择它，它会用星号标记它。

使用方向键移动到 "Ok" 并按下 `Enter` 开始安装。

# 编程语言

编程语言是编写软件的系统，通过类型和错误处理等特性平衡了形式（语法）和意义（语义）。受计算机架构的影响，它们已从特定硬件的形式演变为更抽象的形式，增强了简单性。从命令式到面向对象的类型，它们在满足各种需求的同时，平衡了优势与权衡（例如简单性与性能的平衡）。这种演变体现在计算机科学的动态研究和分类中，使编程成为充满活力的领域。

Zig 由 Andrew Kelley 创建，是一种紧凑的静态类型编译语言，旨在系统编程，定位为 C 语言的现代继任者。Zig 追求简单高效，避免了宏和预处理器，拥抱流控制、易于函数调用和直接库导入。它通过编译时泛型和反射暗示借鉴了新语言，增强了灵活性。Zig 优先考虑安全性但不要求运行时检查，提供可选类型和内置测试框架在没有垃圾回收的情况下管理手动内存，使其与 `Go`、`Rust` 和 `Carbon` 等对手区别开来。

`Go` 由 Google 的 Robert Griesemer、Rob Pike 和 Ken Thompson 创建，是一种高级静态类型语言，与 C 类似但增加了内存安全、垃圾回收和并发特性。它在简单和安全上蓬勃发展，是可扩展系统的理想选择。在 Google 的支持下，`Go`（或 `Golang`）拥有强大的标准库、内置并发和活跃的生态系统。其主要实现包括用于各种平台和 WebAssembly 的 `gc` 编译器，以及通过 `gofrontend` 的 `gccgo` 或 `gollvm`。`GopherJS` 甚至通过将 `Go` 编译为 JavaScript 引入网络。

`Rust` 由 Graydon Hoare 于 2006 创建并由 Mozilla 支持，是一种多功能编程语言，以强调性能、类型安全和并发著称，不需要垃圾回收。它独特的“借用检查器”有助于管理内存和数据竞态。Amazon 和 Google 等科技巨头采用了 Rust，甚至集成到 Linux 内核开发中，Rust 以其快速普及和对系统编程的影响脱颖而出，融合了函数式编程的思想来创建稳健、高效的软件。

`Lua` 是一种 1993 年诞生于巴西的多功能编程语言，以高效和轻量级闻名。它是嵌入式使用的理想选择，运行在跨平台解释器上，并提供简单的 `C API` 进行集成。得益于动态类型、自动内存管理和对多种编程范式的支持，在脚本、配置和快速原型开发方面表现出色。由 PUC-Rio 开发的 Lua 强调速度、可移植性和易嵌入性。它的名字在葡萄语中意为“月亮”，强调了它的独特身份。Lua 免费开源，以其性能、小内存占用和跨平台、跨设备的适应性而脱颖而出。

`OpenJDK` 是 Java 平台标准版的免费开源版本，由 Sun Microsystems 于 2006 年发起，根据 `GPL-2.0` 许可并带有链接的特殊例外。它是爱好者和开发者汇聚以推进 Java SE 及其相关项目的地方，提供了各种操作系统的最新 `OpenJDK JDK 21` 二进制文件。参与活跃的 OpenJDK 社区以探索、下载或贡献于 Amber、`Loom`、`Panama`、`Valhalla` 以及 Java 的未来。对于性的 Java 应用，`dev.java` 是你的首选。无论是学习、下载还是贡献，`OpenJDK` 都体现了 Java 演进中的协作与创新。

## Zig

访问 Zig 官方网站 [`ziglang.org/`](https://ziglang.org/) 了解关于 Zig 的所有信息。

在终端中通过 SNAP 安装 Zig：

```bash
sudo snap install zig --beta --classic
```

## Go

访问 Go 官方网站 [`go.dev/`](https://go.dev/) 了解关于 Go 的所有信息。

在终端中通过 GUI 和命令行安装 Go：

导航到发布页面：[`go.dev/dl/`](https://go.dev/dl/)

点击下载的 `go.linux-amd64.tar.gz` 下载 Go。

在终端中运行以下命令：

```bash
cd ~/Downloads
tar -xvf go1.22.4.linux-amd64.tar.gz
sudo chown -R root go
sudo mv go /usr/local
```

## Rust

访问 Rust 官方网站 [`www.rust-lang.org/`](https://www.rust-lang.org/) 了解关于 Rust 的所有信息。

在终端中通过 curl 安装 Rust：

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
source "$HOME/.cargo/env"
```

## Lua

访问 Lua 官方网站 [`www.lua.org/home.html`](https://www.lua.org/home.html) 了解关于 Lua 的所有信息。

在终端中通过 APT 安装 Lua：

```bash
sudo apt update
sudo apt install build-essential libreadline-dev wget cd
mkdir lua_build
cd lua_build
wget https://www.lua.org/ftp/lua-5.4.6.tar.gz
tar -xvf lua-5.4.6.tar.gz
cd lua-5.4.6
make linux test
sudo make install
```

## OpenJava

访问 OpenJava 官方网站 [`openjdk.org/`](https://openjdk.org/) 了解关于 OpenJava 的所有信息。

在终端中通过 APT 安装 OpenJava：

```bash
sudo apt update && sudo apt upgrade
sudo apt install default-jre default-jdk
```

# Imageboards

Imageboards（图片看板）是图片优先于文本的在线论坛，起源于日本。它们允许用户通过发布图片参与各种讨论，功能类似于公告板，但更关注临时内容。用户可以匿名发布，并通常使用口令（tripcodes，哈希密码）来识别身份而无需存储个人数据。与在线图库不同，图片看板上的内容主要来自外部来源。4chan 等平台提供“安全”口令来增强匿名性，使其这些论坛在视觉内容和匿名交互的结合上脱颖而出。



YChanEx 是一款旨在从 4chan 和 8chan 等留言板下载帖子和图片的工具。它可以在带有 .NET 4.5 的 Windows 上运行，也可以通过 WINE 在 Linux 上运行，具有独特的“ychanex:” 浏览器协议以方便下载。该软件仍在开发中，支持多种留言板，并包含代理支持、brotli 解压缩和帖子历史等功能。最近的更新改进了可靠性和用户界面，并计划了更多增强。YChanEx 旨在简化留言板内容的存档，使其更容易保存这些论坛的讨论和图片。

# YChanEx

访问 YChanEx 官方网站 [`github.com/murrty/YChanEx`](https://github.com/murrty/YChanEx) 了解有关 YChanEx 的所有信息。

## 通过终端或 GUI 中的 APT 安装 YChanEx：

更新包管理器元数据：

```
sudo apt update
```

启用 32 位架构支持：

```bash
sudo dpkg --add-architecture i386
sudo apt update
```

下载并添加 WineHQ 仓库密钥：

```bash
sudo mkdir -p /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources
```

安装 WineHQ：

```bash
sudo apt update
sudo apt install winehq-staging
```

导航到发布页面：

[`github.com/murrty/YChanEx/releases/tag/2.0`](https://github.com/murrty/YChanEx/releases/tag/2.0)

下载最新的 `YChanEx.exe`。

进入 `~/Downloads` 并双击 `YChanEx.exe` [如果此操作不起，请右键点击并将 `WINE` 设置为默认程序]。

要为 YChanEx 创建 `.desktop` 快捷方式，请在终端中执行以下步骤：

使用命令进入应用程序目录：

```bash
cd /usr/share/applications
```

运行以下命令打开并编辑一个新的 `.desktop` 文件：

```bash
sudo gedit ychanex1.desktop
```

在 `ychanex1.desktop` 文件中输入以下详情：

```ini
[Desktop Entry]
Name=YChanEx
Comment=YChanEx
Exec=/bin/bash -c "cd ~/Downloads && wine YChanEx.exe"
Icon=terminal
Terminal=false
Type=Application
Categories=Utility;Game;
```

点击“保存”保存进度。或者，您也可以点击“文件”，然后“保存”，或者点击 ☰ 图标选择“另存为”，最后点击“保存”。保存后关闭编辑器。

# 电子书阅读器

电子书软件将您的设备转换为数字书籍，允许在计算机、平板电脑或手机上阅读。它支持 EPUB、PDF 和 Word 等多种格式，每个格式都有独特的功能和兼容性。了解这些格式有助于您根据阅读偏好选择合适的格式，确保在不同设备上获得流畅愉悦的体验。

Calibre 是一款免费开源的电子书套件，允许用户跨多种格式组织、显示、编辑、创建和转换电子书。它支持与许多电子阅读器同步。您可以直接编辑 EPUB 和 AZW3 格式，而其他格式需要转换。Calibre 提供了大量的插件，支持元数据管理，并允许导入电子书（包括无线同步）。尽管它不支持原生移除 DRM，但可以使用插件来启用此功能。从 6.0 版本开始，全文搜索增强了其库功能，并通过基于 Python 的配方方便了内容转换。

Bookworm 是一款适用于 Windows 的多功能免费电子书阅读器，支持 PDF、EPUB、MOBI 等格式。它为可访问性而设计，提供纯文本和完整格式视图。功能包括文本转语音、针对扫描文档的 OCR 以及用于快速查找术语的维基百科集成。用户可以轻松地导航文档、做注释，甚至从网页中提取文章。无论是使用屏幕阅读器还是享受朗读功能，Bookworm 都增强了每个人的阅读体验。

# Calibre

访问 Calibre 官方网站 [`calibre-ebook.com/`](https://calibre-ebook.com/) 了解有关 Calibre 的所有信息。

## 通过软件管理器通过系统软件包/FLATPAK 包安装 Calibre：

1. 打开软件管理器并搜索 `Calibre`。
2. 点击 `Calibre`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

## 通过终端通过 APT 安装 Calibre：

```bash
sudo apt install calibre
```

## 通过终端通过 FLATPAK 安装 Calibre：

```bash
flatpak install flathub com.calibre_ebook.calibre
```

## 通过终端通过二进制安装安装 Calibre：

```bash
sudo -v && wget -nv -O- https://download.calibre-ebook.com/linux-installer.sh | sudo sh /dev/stdin
```

# Bookworm

访问 Bookworm 官方网站 [`getbookworm.com/`](https://getbookworm.com/) 了解有关 Bookworm 的所有信息。

## 通过软件管理器通过系统软件包/FLATPAK 包安装 Bookworm：

1. 打开软件管理器并搜索 `Bookworm`。
2. 点击 `Bookworm`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

## 通过终端通过 APT 安装 Bookworm：

```bash
sudo apt install bookworm
```

## 通过终端通过 FLATPAK 安装 Bookworm：

```bash
flatpak install flathub com.github.babluboy.bookworm
```

# 虚拟化

虚拟化软件称为虚拟机管理程序（hypervisor），允许一台计算机充当多台虚拟机，允许不同的操作系统在单台 PC 上同时运行。这项技术优化了资源利用，简化了备份，并允许各种操作系统和过时的应用程序无缝运行。它通过将潜在威胁与恶意软件和浏览器漏洞隔离来增强安全性。除了个人用途外，虚拟化还支持基础设施服务（IaaS），提高了企业的扩展性和效率，降低了成本并改进了灾难恢复和测试。它体现了灵活、高效的计算，以少胜多。

Oracle VirtualBox 是一款多功能的虚拟化工具，适用于企业和个人使用，支持 Windows、Linux 和 macOS 等多种操作系统。它提供了丰富的功能来实现高性能，能够适应许多客操作系统，包括不同的 Windows 版本和 Linux 发行版。作为 GPL v3 下的开源软件，VirtualBox 在保持专业质量的同时邀请社区贡献，并由 Oracle 支持。定期更新扩展了支持的系统和功能，并包含了开发人员所需的预构建虚拟机等资源。

Virt-manager 主要由红帽开发，是一个通过 `libvirt` 管理虚拟机（VM）的桌面工具。它允许用户创建、编辑、启动和停止虚拟机，并查看其性能和控制台。自 2014 年以来，它支持 KVM、Xen、QEMU、LXC 容器以及 FreeBSD 的 bhyve 虚拟机管理程序。该套件包含了用于轻松设置虚拟机的 `virt-install`、用于虚拟机显示交互的 `virt-viewer`、用于克隆虚拟机的 `virt-clone`、用于编辑虚拟机配置的 `virt-xml` 以及为基于 libvirt 的容器设置根文件系统的 `virt-bootstrap`。

# Oracle VirtualBox

访问 Oracle VirtualBox 官方网站 [`www.virtualbox.org/`](https://www.virtualbox.org/) 了解有关 Oracle VirtualBox 的所有信息。

## 通过终端通过 APT 安装 Oracle VirtualBox：

```bash
sudo apt update && sudo apt upgrade
cd
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | rpm --import -
sudo apt update
sudo apt install virtualbox-7.0
```

## 通过 GUI 通过 DEB 安装 Oracle VirtualBox：

1. 导航到发布页面：[`www.virtualbox.org/wiki/Linux_Downloads`](https://www.virtualbox.org/wiki/Linux_Downloads)
2. 点击最新的 Ubuntu 24.04 软件包链接下载 Oracle VirtualBox。
3. 进入您的下载文件夹：双击 `virtualbox-7.0_7.0.18-162988~Ubuntu~noble_amd64.deb`。
4. 点击“安装”完成安装。

## 将用户添加到 vboxusers 组：

切换到 root 用户：

```bash
su -
```

将您的用户名添加到 `vboxusers` 组（将 "username" 替换为实际用户名）：

```bash
sudo usermod -aG vboxusers username
```

退出 root 用户：

```bash
exit
```

重启系统以应用更改：

```bash
sudo reboot
```

Virt-manager





访问 Virt-manager 官方网站 [`virt-manager.org/`](https://virt-manager.org/) 获取有关 Virt-manager 的所有信息。

### 通过软件管理器通过“系统软件包”包安装 Virt-manager：

1. 打开软件管理器并搜索 `Virt-manager`。
2. 点击 `Virt-manager`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 并点击安装。

### 在终端通过 APT 安装 Virt-manager：

```bash
sudo apt install virt-manager
```

# 游戏

在 Linux Mint 22 上玩游戏提供了从传统游戏平台的激动转变，充分利用了 Linux Mint 22 稳健且稳定的环境。通过利用 `Steam Proton` 和 `Lutris` 等工具，你可以在一个传统上认为不适合游戏的平台上流畅地运行从独立独立游戏到 AAA 大作的各种游戏。这种演变凸显了社区的共同努力，使 Linux 成为一个对游戏玩家友好的操作系统，展示了在性能和硬件支持方面的显著改进。虽然驱动程序兼容性等挑战仍然存在，但这种进步是不可否认的，为 Windows 游戏提供了一个耳一新的替代方案，并专注于开源原则和用户控制。

`Wine-Staging` 可于 [`www.winehq.org/`](https://www.winehq.org/)，它是 `Wine` 的一个测试场，包含了尚未进入开发分支的错误修复和功能。它加快了用户和开发者访问实验性功能。`Wine-Staging` 作为 `Wine` 开发版本的补丁集，允许维护者选择性地包含补丁。一个专门团队从错误报告开始审查并维护这些补丁，以提高 `Wine` 的性能，特别是对于游戏和应用程序。区别包括用于测试的 `winehq-staging`、用于稳定版本的 `winehq-stable`、用于开发头文件的 `winehq-devel` 以及用于额外调试工具的 `wine-development`。

`Lutris` 是一个用于 Linux 的免费开源游戏管理器，它与 `Steam`、`GOG`、`Humble Bundle` 和 `Epic Games Store` 等平台集成。它简化了跨各种硬件和软件玩游戏体验，支持超过 20 多个模拟器和 `Wine` 的社区脚本，确保新旧游戏的流畅运行。`Lutris` 由 Mathieu Comandon 和社区开发，促进了视频游戏的保护，允许用户使用他们的 PC 构建一个开源游戏机。它是一个由 `Linux` 和 `Vulkan` 驱动的稳定平台，让你的游戏收藏保持活力并易于访问。

`ProtonUp-Qt` 位于 [`github.com/DavidoTek/ProtonUp-Qt`](https://github.com/DavidoTek/ProtonUp-Qt)，是一个 GUI 工具，用于简化 Linux 和 Steam Deck 上 `Steam`、`Heroic` 和 `Lutris` 游戏的安装和管理 `GE-Proton`、`Luxtorpeda` 和 `Wine-GE`。它增强了兼容性，当 Valve 的 `Proton` 不或运行经典游戏升级版时提供解决方案。最新更新 `2.9.1` 包含了 `Steam 快捷方式编辑器`，切换到 `Ph42oN’ssDxvk-Async` 并改进了 `Wine-GE` 的处理，以及 UI/UX 增强和配置改进，以获得更流畅的游戏设置。

`Steam` 是领先的 PC 游戏数字平台，提供自动游戏更新、第三方标题分发、匹配机制和社交功能。它为开发者提供 `Steamworks`，支持 `macOS`、`Linux` 和移动平台，并销售其他数字内容和如 `Valve Index` 等硬件。2013 年以 75% 的份额主导市场，到 2021 年，`Steam` 拥有超过 34000 款游戏和 1.32 亿用户，引领了如 `Steam Deck` 等创新。

`DXVK` 是一个基于 `Vulkan` 的层，通过 `Wine` 为 Linux 上的 3D 翻译 `Direct3D 9/10/11`，通过桥接 `DirectX` 和 `Vulkan` 增强游戏体验，减少开销并提升性能。这一创新标志着 Linux 游戏的关键转折，提供了与 Windows 相当甚至优的体验，使 Linux 成为游戏玩家更有竞争力的选择。

`VKD3D` 设计用于在 `Vulkan` 上完全实现 `Direct3D 12` API，主要用于 `Proton's-Direct3D 12` 支持。它优先考虑性能和游戏兼容性，利用现代的 `Vulkan` 特，尽管这意味着旧系统可能不受支持。最新版本 `2.12` 引入了 `NVIDIA Reflex` 支持、如 `D3D12 render pass API` 等增强，以及针对特定游戏问题的各种修复和变通。它还包含了 `NVIDIA GPU` 上的性能改进以及用于开发者的调试工具，使其成为支持 `Vulkan` 平台游戏的重要工具。

# Wine-Staging

访问 `Wine-Staging` 官方网站 [`wiki.winehq.org/Wine-Staging`](https://wiki.winehq.org/Wine-Staging) 获取有关 `Wine-Staging` 的所有信息。

更新包管理器元数据：

```bash
sudo apt update
```

启用 32 位架构支持：

```bash
sudo dpkg --add-architecture i386
sudo apt update
```

下载并添加 `WineHQ` 仓库密钥：

```bash
sudo mkdir -p /etc/apt/keyrings
sudo wget -O /etc/apt/keyrings/winehq-archive.key https://dl.winehq.org/wine-builds/winehq.key
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources
```

安装 `WineHQ-Staging`：

```bash
sudo apt update
sudo apt install winehq-staging gamemode winbind protobuf-compiler libprotobuf-dev libopusfile0 winetricks
```

# Lutris

访问 `Lutris` 官方网站 [`lutris.net/`](https://lutris.net/) 获取有关 `Lutris` 的所有信息。

### 通过软件管理器通过“系统软件包/FLATPAK”包安装 Lutris：

1. 打开软件管理器并搜索 `Lutris`。
2. 点击 `Lutris`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Lutris：

```bash
sudo apt install lutris
```

### 在终端通过 FLATPAK 安装 Lutris：

```bash
flatpak install flathub net.lutris.Lutris
```

# ProtonUp-Qt

访问 `ProtonUp-Qt` 官方网站 [`davidotek.github.io/protonup-qt/`](https://davidotek.github.io/protonup-qt/) 获取有关 `ProtonUp-Qt` 的所有信息。

### 通过软件管理器通过“RPM/FLATPAK”包安装 ProtonUp-Qt：

1. 打开软件管理器并搜索 `ProtonUp-Qt`。
2. 点击 `ProtonUp-Qt`，然后点击源选择框。
3. 选择 `FLATPAK` 并点击安装。

### 在终端通过 FLATPAK 安装 ProtonUp-Qt：

```bash
flatpak install flathub net.davidotek.pupgui2
```

# Steam

访问 `Steam` 官方网站 [`store.steampowered.com/`](https://store.steampowered.com/) 获取有关 `Steam` 的所有信息。

### 通过软件管理器通过“RPM/FLATPAK”包安装 Steam：

1. 打开软件管理器并搜索 `Steam`。
2. 点击 `Steam`，然后点击源选择框。
3. 选择 `SYSTEM PACKAGE` 或 `FLATPAK` 并点击安装。

### 在终端通过 APT 安装 Steam：

```bash
sudo apt update
sudo apt install steam
```

### 在终端通过 FLATPAK 安装 Steam：

```bash
flatpak install flathub com.valvesoftware.Steam
```

### 在终端通过 SNAP 安装 Steam：

```bash
sudo snap install steam
```

# DXVK

访问 `DXVK` 官方网站 [`github.com/doitsujin/dxvk`](https://github.com/doitsujin/dxvk) 获取有关 `DXVK` 的所有信息。

### 在终端和 GUI 通过 .sh 安装 DXVK：

导航至发布页面：
[`github.com/doitsujin/dxvk/releases`](https://github.com/doitsujin/dxvk/releases)

1. 下载最新的 `dxvk-tar.gz`。
2. 进入 `~/Downloads`，双击 `dxvk-2.3.1.tar.gz`，选择 `dxvk-2.3.1` 并点击解压。
3. 右键点击空白处选择“在终端中打开”。

运行这些命令：

```bash
cd ~/Downloads/dxvk-2.3.1
cp x64/*.dll ~/.wine/drive_c/windows/system32
cp x32/*.dll ~/.wine/drive_c/windows/syswow4
```

`winecfg`

配置 Wine：

1. 点击 `Libraries`。
2. 选择 `dxgi` 并点击 `Edit`。
3. 将 `Native` 旁边的开关切换到 `Builtin` 并点击 `OK`。
4. 对 `d3d9`、`d3d11` 和 `d3d10core` 重复此操作。
5. 点击 `Apply` 并点击 `OK`。

# Vkd3d-proton





[`github.com/HansKristian-Work/vkd3d-proton/releases`](https://github.com/HansKristian-Work/vkd3d-proton/releases)

下载最新的 `vkd3d-proton`。

前往 `~/Downloads`，双击 `vkd3d-proton`，选择 `vkd3d-proton-2.12` 并点击解压。

右键点击空白处并选择“在终端中打开”。

运行以下命令：

```bash
cd ~/Downloads/vkd3d-proton-2.12
./setup_vkd3d_proton.sh install
winecfg
```

### 配置 Wine：

1. 点击 **Libraries**（库）。
2. 将 `d3d12core` 和 `d3d12` 添加并配置为 `native`（原生）优于 `builtin`（内置）。

# 魔兽世界

《魔兽世界》是一款迷人的在线游戏，邀请玩家探索艾泽之地广阔的土地。随着《地心之战》等新扩展内容的推出，它提供了地下世界、盟族种族以及待征服的远古邪。经典版本和如《巨龙时代》之类的更新通过地下和独特的挑战焕发了游戏活力。无论是重新开始、回归还是拥抱硬核模式，WoW 都承诺与朋友一起开启无尽的冒险，通过游戏获得奖励，并加入冒险者社区。现在加入参与史诗级的任务、战斗和一个充满活力且不断变化的世界。访问魔兽世界官方网站：[`worldofwarcraft.com/`](https://worldofwarcraft.com/)。

战暴客户端是一款桌面应用程序，旨在通过在一个地方管理所有战暴网游戏来简化你的游戏体验。它允许你方便地安装、更新和启动游戏，并访问战暴商店和游戏新闻。它取代了之前的游戏启动器，是通往当前及未来游戏的门户。通过单点登录功能，登录一次即可访问所有游戏，如果选择需要，登录状态可保持长 30 天。该客户端还支持游戏的后台补丁，并提供暂停或禁用自动更新的选项，确保你随时畅畅游戏而无需担心。对于任何问题，都有直接支持和故障排除建议。访问战暴网官方网站：[`battle.net/`](https://battle.net/)。

Lutris 魔兽世界游戏内商店黑屏问题出现在玩家通过 Lutris 运行魔兽世界时，访问游戏内商店遇到黑屏，导致他们无法查看或购买物品。此问题也可能发生在选择物品后的结算阶段。本节提供了处理和解决此漏洞的实用解决方案，旨在恢复游戏的商店功能并增强游戏体验。

WINE-Staging 魔兽世界游戏内商店黑屏问题出现在玩家通过 WINE-Staging 运行魔兽世界时，访问游戏内商店遇到黑屏，导致他们无法查看或购买物品。此问题也可能发生在选择物品后的结算阶段。本节提供了处理和解决此漏洞的实用解决方案，旨在恢复游戏的商店功能并增强游戏体验。访问 Wine-Staging 官方网站 [`wiki.winehq.org/Wine-Staging`](https://wiki.winehq.org/Wine-Staging) 获取更多信息。

魔兽世界中的 DirectX 12 错误可以通过将 Nvidia 图形驱动程序从版本 525 更新到 545 来解决。这个问题通常发生在游戏被设置为使用 DirectX 12 而不是 DirectX 11 时。你可以通过更改战暴客户端和魔兽世界本身的设置来修复此问题。

正式版魔兽世界原版插件套件是一个经过仔细挑选的模组集合，旨在为玩家融合《军团盟约》的现代风味与 WoW 原版时代的怀旧感。它通过受早期 RPG 启发的便利功能丰富游戏，包括从 `Accountant Classic` 到 `XToLevel` 的 UI 增强，旨在通过结合两个世界的优点提升你的游戏体验。该套件涵盖了从属性跟踪到任务管理的所有内容，确保在艾泽之地的之旅更加顺畅、愉快。

CurseForge 是一个游戏中心，玩家可以在这里下载魔兽世界、我的世界和星际争霸 2II 等游戏的模组和插件。它还是一个创意平台，提供制作新模组的模板，并通过下载量为作者奖励积分。CurseForge 应用增强了插件管理，通过快速响应的功能和自动更新选项简化了更新。通过支持模组作者（他们获得应用收入的 70%），用户直接为他们喜欢的创作者的成功贡献力量，可以选择免费的广告支持版本或订阅以移除广告并进一步支持社区。访问 CurseForge 官方网站：[`www.curseforge.com/`](https://www.curseforge.com/)。

在命令行中运行战暴网涉及在 Linux Mint 22 的 Cinnamon 环境上设置 WINE-Staging、安装必要的包并配置图形 API 转换层。为了实现这一点，必须首先安装先决包以确保兼容性和最佳性能。启动战暴客户端最有效的方法是通过命令行，然后通过“自定义命令”功能将其集成到 Linux Mint 22 的启动选项中。访问战暴网官方网站 [`battle.net/`](https://battle.net/) 获取更多详情。

# 战暴网

访问战暴网官方网站 [`eu.shop.battle.net/en-gb?from=root`](https://eu.shop.battle.net/en-gb?from=root) 了解所有关于战暴网的信息。

[需要已安装 WINE-Staging]

### 通过终端和 GUI 使用 .exe 安装战暴网：

1. 导航至发布页面：[`download.battle.net/en-gb/?product=bnetdesk`](https://download.battle.net/en-gb/?product=bnetdesk)
2. 点击“再次尝试”下载战暴网。
3. 前往 `~/Downloads`。
4. 右键点击空白处。
5. 点击“在终端中打开”。
6. 运行以下命令：

```bash
sudo apt update && sudo apt upgrade
gamemoderun wine Battle.net-Setup.exe --disable-software-rasterizer
```
7. 按照屏幕上的说明操作。

### Lutris 魔兽世界游戏内商店黑屏问题的可能修复

访问魔兽世界和 Lutris 官方网站：
[`worldofwarcraft.blizzard.com/`](https://worldofwarcraft.blizzard.com/)
[`lutris.net/`](https://lutris.net/)

#### 通过命令行和 GUI 修复：

1. 从应用程序菜单中打开 Lutris。
2. 选择 Blizzard Battle.net，点击酒杯图标旁边的箭头，然后选择“Wine Configuration”（Wine 配置）。
3. 在 Wine 配置窗口中，找到“Windows Version”（Windows 版本）下拉菜单并选择 Windows 11 或 Windows 10。
4. 导航到“Graphics”（图形）选项卡，启用“CSMT for improved graphic performance”和“VAAPI as backend for DXVA2 GPU”。
5. 转到“Drives”（驱动器）选项卡，按添加按钮并分配一个新的驱动器号。
6. 并选择魔兽世界目录，包含 `retail`、`classic` 和 `classic_era` 文件夹。点击“OK”。
7. 点击“Apply”应用这些设置并再次点击“OK”确认。
8. 确保未设置 `WINEESYNC` 变量且没有正在运行 `esync` 实例。
9. 如果问题持续，考虑将你的图形驱动程序更新到最新版本，例如 NVIDIA 的 555 驱动。

### WINE-Staging 魔兽世界游戏内商店黑屏问题的可能修复

访问魔兽世界和 WINE-Staging 官方网站：
[`worldofwarcraft.blizzard.com/`](https://worldofwarcraft.blizzard.com/)
[`wiki.winehq.org/Wine-Staging`](https://wiki.winehq.org/Wine-Staging)

#### 通过命令行和 GUI 修复：

在终端中运行以下命令：

```bash
winecfg
```

1. 选择 Blizzard Battle.net，点击酒杯图标旁边的箭头，然后选择“Wine Configuration”（Wine 配置）。





找到并选择《魔兽世界》目录，该目录包含 `retail`、`classic` 和 `classic_era` 文件夹。点击“确定”。

点击“应用”应用这些设置并再次点击“确定”确认。

确保未设置 `WINEESYNC` 变量且没有 esync 实例正在运行。如果问题仍然存在，考虑将您的显卡驱动更新到最新版本，例如 NVIDIA 的 555 驱动。

## DirectX 12 错误可能的解决方案

访问 DirectX 官方网站 [`www.microsoft.com/en-gb/download/details.aspx?id=35`](https://www.microsoft.com/en-gb/download/details.aspx?id=35) 获取所有 DirectX 相关信息。

### 通过 GUI 修复：

1. 从应用程序菜单打开 Battle.net。
2. 点击大蓝色“游戏”或“更新”按钮旁边的齿轮图标。
3. 选择“游戏设置”，并找到你想要玩的《魔兽世界》版本部分。
4. 勾选“额外命令行参数”，并在相邻的框中输入 `-d3d11`。点击“完成”。
5. 启动《魔兽世界》，进入“选项”菜单，选择“系统”下的“图形”选项卡，并滚动到“高级”下的“图形 API”。确保已选择 DirectX 11。
6. 如果没有，从“图形 API”旁边的下拉菜单中选择 DirectX 11，并重启《魔兽世界》以应用更改。

## 巨服版魔兽世界怀旧版插件包

以下是一份精心编写的插件目录，旨在复制一个类似于《军团之会》以及《魔兽世界》经典/怀旧版的用户界面。这些修改整合了若干灵感源自早于或同期《魔兽世界》旧版发布的 RPG 游戏的质量提升（QOL）增强。

* `Accountant Classic`
* `Cheugy_Mission_Reports`
* `ClassicFCT`
* `ClassicFrames`
* `ClassicGuildFrame`
* `ClassicLevelUp`
* `ClassicQuestText`
* `ClassicUI`
* `ClassicalFps`
* `ClockHider`
* `CovenantMissionHelper`
* `CTMOD`
* `DejaCharacterStats`
* `ExtraQuestButton`
* `GarrisonCommander`
* `IcyVeinsStatPriority`
* `Misspelled`
* `MyRolePlay`
* `NeatPlates`
* `NPCRPGossip`
* `Notes`
* `OldCastbars`
* `OrderHallCommander`
* `PixelPerfectAlign`
* `QuestCompletist`
* `Storyline`
* `UnlimitedMapPinDistance`
* `VenturePlan`
* `WarPlan`
* `XToLevel`

这一系列插件经过精心挑选，旨在增强您的游戏体验，镜像了《军团之会》和经典/怀旧版《魔兽世界》时代的审美与功能，同时从早于或同时发布旧版的 RPG 改进中汲取灵感。

## Linux Mint 22 命令参考

字体 文件和目录管理的必备系统命令

#### 列出目录内容
命令：`sudo ls directory`
描述：列出指定目录的内容。

#### 切换目录
命令：`cd directory`
描述：将当前工作目录更改为指定的目录。

#### 返回上一级目录
命令：`cd ..`
描述：将当前工作目录更改为父目录，在目录层次结构中向上移动。

#### 列出所有非隐藏文件和文件夹
命令：`dir`
描述：列出当前工作目录下所有非隐藏的文件和文件夹。

#### 列出所有文件和文件夹（包括隐藏）
命令：`ls -a`
描述：列出当前目录下所有的文件和文件夹，包括隐藏文件。

#### 创建目录
命令：`sudo mkdir directory`
描述：在当前工作目录下创建一个新目录。

#### 删除文件
命令：`sudo rm filename`
描述：从文件系统中删除指定的文件。

#### 递归删除文件和文件夹
命令：`sudo rm -r directory`
描述：删除指定的目录及其内容，包括所有文件和子目录。

#### 将文件拷贝到目的地
命令：`sudo cp filename destination`
描述：将指定的文件复制到指定的目的地。

#### 将文件夹拷贝到目的地
命令：`sudo cp -R folder destination`
描述：将指定的文件夹及其内容复制到指定的目的地。

#### 将文件或文件夹移动到目的地
命令：`sudo mv filename destination`
描述：将指定的文件或文件夹移动到指定的目的地。

#### 重命名文件或文件夹
命令：`sudo mv filename newfilename`
描述：将指定的文件或文件夹重命名为新的名称。

#### 显示文件内容
命令：`sudo cat filename`
描述：在终端中显示指定文件的内容。

#### 列出父目录内容
命令：`ls ..`
描述：列出当前工作目录父目录的内容。

### 精通 APT：高级包管理技术

#### 更新包列表
命令：`sudo apt update`
描述：通过从软件仓库获取最新信息更新本地软件包数据库。

#### 升级已安装包
命令：`sudo apt upgrade`
描述：将所有安装的应用程序升级到仓库中的最新版本，处理任何所需的依赖关系。

#### 完全升级已安装包
命令：`sudo apt full-upgrade`
描述：对系统上的所有包进行完全升级到最新版本，必要时可能删除包。

#### 搜索包
命令：`sudo apt search package`
描述：搜索匹配关键词的软件包。

#### 显示包信息
命令：`sudo apt show package`
描述：提供特定软件包的详细信息。

#### 安装包
命令：`sudo apt install package`
描述：从软件仓库安装软件包，包括任何所需的依赖。

#### 移除包
命令：`sudo apt remove package`
描述：从系统中移除软件包，但保留与其相关的配置文件。

#### 彻底移除包
命令：`sudo apt purge package`
描述：从系统中移除软件包，包括其配置文件。

#### 自动移除无用包
命令：`sudo apt autoremove`
描述：从系统中移除任何未使用的包及其依赖关系。

#### 列出已安装包
命令：`sudo apt list`
描述：显示系统中当前安装的所有软件包列表。

#### 添加仓库
命令：`sudo add-apt-repository repository`
描述：向系统添加新的软件仓库。

#### 移除仓库
命令：`sudo add-apt-repository -r repository`
描述：从系统中移除之前添加的仓库。

#### 编辑源文件
命令：`sudo apt edit-sources`
描述：用默认文本编辑器打开 `sources.list` 文件，以手动编辑软件仓库源。

#### 修复损坏的依赖关系
命令：`sudo apt install -f`
描述：通过安装缺失或冲突的包尝试解决并修复任何损坏的包依赖关系。

#### 获取包的源码
命令：`sudo apt source package`
描述：从仓库下载包的源代码。

#### 升级系统
命令：`sudo do-release-upgrade`
描述：启动发行版升级过程，将操作系统移动到新版本。

#### 清理包
命令：`sudo apt clean`
描述：清除本地包缓存以释放磁盘空间。

#### 自动清理包
命令：`sudo apt autoclean`
描述：通过删除不需要的文件自动清理本地包缓存。

#### 锁定 APT 包
命令：`sudo apt mark-hold package`
描述：防止软件包在升级期间被更新。

#### 解锁 APT 包
命令：`sudo apt mark-unhold package`
描述：取消对包的锁定，允许其在升级期间进行更新。

#### 显示已锁定的包
命令：`sudo apt-mark showhold`
描述：显示系统当前所有被锁定的软件包列表。

#### 包验证
命令：`sudo apt-key verify`
描述：验证软件包仓库密钥的完整性和真实性。




# 精通 Flatpak：安装、管理及其他

## Flatpak 安装
命令：`flatpak install flatpak`
描述：从远程仓库安装 Flatpak。

### 列出已安装的 Flatpak
命令：`flatpak list`
描述：提供系统上当前安装的所有 Flatpak 应用程序的概述。

### 更新 Flatpak
命令：`flatpak update`
描述：将所有安装的 Flatpak 升级到最新版本。

### 运行 Flatpak
命令：`flatpak run flatpak`
描述：启动已安装的 Flatpak 应用程序。

### 卸载 Flatpak
命令：`flatpak uninstall flatpak`
描述：从系统中移除指定的 Flatpak 软件包。

### Flatpak 远程仓库列表
命令：`flatpak remote-list`
描述：列出已添加到系统的 Flatpak 远程仓库名称。

### 添加 Flatpak 远程仓库
命令：`flatpak remote-add --if-not-exists name url`
描述：向系统添加新的 Flatpak 远程仓库。

###  Flatpak 远程仓库
命令：`flatpak remote-delete name`
描述：从系统的配置中移除指定的 Flatpak 远程仓库。

# Snap 操作：安装、管理和探索 Snap 应用程序全面指南

## 安装 Snap
命令：`sudo snap install <snap>`
描述：从 Snapcraft 数据库安装 snap 应用程序。

### 列出已安装的 Snap
命令：`sudo snap list`
描述：列出系统上安装的 snap。

### 更新 Snap
命令：`sudo snap refresh`
描述：将所有 snap 升级到最新版本。

### 运行 Snap
命令：`snap run <snap>`
描述：运行已安装的 snap。

### 移除 Snap
命令：`sudo snap remove <snap>`
描述：从系统中移除已安装的 snap。

### 搜索 Snap
命令：`sudo snap find <search_term>`
描述：在 Snapcraft 数据库中搜索匹配搜索词的 snap。

### 列出 Snap 信息
命令：`sudo snap info <snap>`
描述：提供有关已安装 snap 的详细信息。

### 查看 Snap 连接
命令：`sudo snap connections <snap>`
描述：显示已安装的 snap 所建立的连接。

# 精通文件所有权修改

## 文件所有权修改
命令：`sudo chown user filename`
描述：将文件或文件夹的所有者更改指定的用户。

### 递归修改所有权
命令：`sudo chown -R user filename`
描述：递归地将文件或文件夹及其内容的所有者更改指定的用户。

### 指定用户组的所有权修改
命令：`sudo chown user:group filename`
描述：更改文件或文件夹关联的所有者和组。

### 静默所有权修改
命令：`sudo chown -f user filename`
描述：修改所有权，如果操作未成功则抑制错误消息。

### 详细所有权修改
命令：`sudo chown -v user filename`
描述：更改所有权的同时提供有关该过程的详细信息。

### 交互式所有权修改
命令：`sudo chown -i user filename`
描述：更改文件或文件夹所有权时请求确认。

### 保留时间戳的所有权修改
命令：`sudo chown --preserve-timestamps user filename`
描述：修改文件所有权的同时保留与文件相关的时间戳。

# 精通文件权限：访问控制和安全设置全面指南

## 更改文件权限
命令：`sudo chmod permissions filename`
描述：修改文件或文件夹的权限以控制访问和安全设置。

### 递归更改权限
命令：`sudo chmod -R permissions filename`
描述：递归地修改文件或文件夹及其内容的权限。

### 使用数字更改文件权限
命令：`sudo chmod numbers filename`
描述：使用数字代码（例如 755）调整文件或文件夹的权限。

### 递归更改数字权限
命令：`sudo chmod -R numbers filename`
描述：使用数字代码递归更新文件或文件夹及其子项的权限。

### 详细更改权限
命令：`sudo chmod -v permissions filename`
描述：更改文件或文件夹权限的同时，提供有关已权限更改的详细信息。

### 确认更改权限
命令：`sudo chmod -i permissions filename`
描述：更改文件或文件夹权限的同时，对每次单独的权限修改请求确认。

### 参考文件更改权限
命令：`sudo chmod --reference=reference-file filename`
描述：将文件或文件夹的权限设置为指定参考文件的权限。

# 探索 dpkg：软件包管理全面指南

## 安装 .deb 软件包
命令：`sudo dpkg -i file.deb`
描述：在系统上安装指定的 .deb 文件。

### 移除已安装的 .deb 软件包
命令：`sudo dpkg -r package_name`
描述：卸载已安装的 .deb 软件包并保留其配置文件。

### 移除包含文件的 .deb 包
命令：`sudo dpkg -P package_name`
描述：完全移除已安装的 .deb 软件包，包括其配置文件。

### 列出已安装软件包
命令：`sudo dpkg -l`
描述：列出主机系统安装的所有软件包，以及版本和描述信息。

### 列出软件包安装的文件
命令：`sudo dpkg -L package_name`
描述：提供指定软件包安装的文件完整列表。

### 检查软件包依赖
命令：`sudo dpkg -I package_name.deb`
描述：验证并列出 .deb 软件包所需的依赖项。

### 重新配置已安装软件包
命令：`sudo dpkg-reconfigure package_name`
描述：允许修改已安装软件包的配置设置。

### 修复损坏的安装
命令：`sudo dpkg --configure -a`
描述：通过重新配置未正确安装或配置的软件包来修复损坏的安装。

# 使用 wget 高效获取文件

## 下载文件
命令：`wget url`
描述：从指定的 URL 下载文件。

### 更改输出文件名
命令：`wget -o filename url`
描述：修改要下载的文件名。

### 后台下载文件
命令：`wget -b url`
描述：在下载文件的同时允许不中断地使用命令行。

