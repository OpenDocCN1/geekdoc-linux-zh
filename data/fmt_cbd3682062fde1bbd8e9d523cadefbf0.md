
# 表 4.1 XFree86 文档

| 文件 | 说明 |
|---|---|
| `AccelCards` | 已测试的加速显卡列表 |
| `BUILD` | 如何从源码编译 XFree86 X 分发版 |
| `COPYRIGHT` | 版权声明 |
| `Devices` | 包含贡献的 X86Config 设备部分的旧文件 |
| `Monitors` | 包含贡献的 XF86Config 显示器部分的旧文件 |
| `QuickStart.doc` | 快速设置 XFree86 的快速入门指南 |
| `README` | 关于当前 XFree86 版本的通用信息 |
| `README.3DLabs` | 3DLabs 芯片组用户信息 |
| `README.Config` | 配置 XFree86 的详细分步指南 |
| `README.DECga` | 为 DEC 21030 用户的信息 |
| `README.DGA` | 如何为 XFree86 DGA 接口编程 |
| `README.I12B` | 关于 Number Nine 128 显的信息 |
| `README.LinkKit` | 关于如何从零开始构建 XFree86 的特定信息 |
| `README.Linux` | 在安装和使用 XFree86 后给 Linux 用户的有用信息 |
| `README.MGA` | 关于 Matrox Millennium 和 Mystique 显卡的信息 |
| `README.Mach32` | 关于 Mach32 XFree86 X 服务器的信息 |
| `README.Mach64` | 关于 Mach64 XFree86 X 服务的发布说明 |
| `README.NVIDIA` | 关于 Nvidia NV1, SGS-Thomson ST2000 和 Rival128 显卡的说明 |

## 配置 X 窗口系统第 11 版

### 第四章

仅限服务器：构建 XFree86 X 服务器时你的目录看起来应该是这样的

`VGADriver.Doc` 一个关于向 XFree86 添加 SVGA 或 VGA 驱动程序的 HOWTO；Eric S. Raymond 关于构建 xF86Config 模型的详尽论文

`xinput` XFree86 对输入设备（如摇杆）支持的通用信息

![](img/fbfff30e42d507bc7531108a281d6cf4_92_0.png)

# 红帽 Linux 的介绍与安装

## 第一部分

如果你是 X11 的新手，请先阅读 X 和 XFree86 的 man 页面以获取 X 的概述。在开始配置 X 之前，也请阅读 `quickstart.doc`。你需要了解关于关于电脑以及电脑显卡和显示器的技术细节。

这里是一些将会有帮助的信息：

- 你的电脑中安装的显卡类型、品牌、名称或型号
- 你的显卡的显存（而非系统内存）是如何安装的
- 你的电脑使用的时钟芯片类型
- 鼠标类型
- 显示器的类型、品牌、名称或型号
- 垂直频率
- 键盘

如果你是 X11 的新手，请先阅读 X 和 XFree86 的 man 页面以获取 X 的概述。在开始配置 X 之前，也请阅读 `quickstart.doc`。你需要了解关于电脑以及电脑显卡和显示器的技术细节。

这里是一些将会有帮助的信息：

- 电脑中安装的显卡类型、品牌、名称或型号
- 显存（而非系统内存）是如何安装的
- 电脑使用的时钟芯片类型
- 鼠标
- 显示器的类型、品牌、名称或型号
- 垂直频率
- 键盘

如果你是 X11 的新手，请先阅读 X 和 XFree86 的 man 页面以获取 X 的概述。在开始配置 X 之前，也请阅读 `quickstart.doc`。你需要了解关于电脑以及电脑显卡和显示器的技术细节。

...

## X86Config 文件

毫无疑问，XFree86 最重要的配置文件是 `X86Config`。该文件用于向选定的 X 服务器提供字体、鼠标、视频组和颜色深度设置。当你启动 X 会话时，服务器会搜索此文件。`X86Config` 通常位于 `/etc/X11`，也位于 `/usr/X11/lib/X11`；如果你以 root 身份运行 X，可以在 `/root` 下找到。

`X86Config` 是一个文本文件，由多个部分组成：

- 指定颜色、字体或特定软件模块的位置
- `Module`：指定应该加载哪些模块
- `ServerFlags`：允许或拒绝特殊操作的开关，例如核心转储、键盘关闭、视频模式切换、视频调优和鼠标配置
- `Keyboard`：告知 X 服务器预期的键盘以及使用哪些设置
- `Pointer`：告知 X 服务器使用什么指针以及如何处理按钮
- `Input`：用于输入设备（如图形板或触控笔）的特殊部分
- `Monitor`：针对显示器的特定细节和设置，如名称、水平同步、垂直同步范围和模型行（每个视频分辨率一个，例如 640x480、800x600、1024x768）
- `Device`：指定使用什么 X 服务器、颜色深度（例如每像素 8、16、24 或 32 位）、屏幕尺寸以及虚拟屏幕的大小

关于视频芯片组的细节，例如内存和时钟芯片

> 注意
> 不要使用与你的显卡和显示器不相同的 X86Config。错误的设置可能会损坏你的显示器。不要使用超出显示器规格的设置。你已经收到警告了！另一方面，如果你得到了一个很好的 X86Config，请将其记录并与他人分享。阅读 os.linux.x 或 comp.linux.portable 的发布，并查看 Linux 用户网页以获取提示、技巧和分享信息的地方。

在开始之前，请确保你已经阅读了 `README.Config`。

## Red Hat Linux 介绍与安装

## 使用 Xconfigurator

Red Hat 的 `Xconfigurator` 在探测您的系统并询问几个问题后会生成 `XF86Config` 文件。当您需要生成新的配置文件时（例如在更改电脑显卡之后），可以在控制台（无 X11）中使用此程序。您必须以 root 操作员身份运行此程序。从控制台的命令行或 X11 终端窗口启动 `Xconfigurator`，如下所示：

```
## su c Xconfigurator
```

屏幕会清空并出一个对话框，如图 4.1 所示。

![](img/fbfff30e42d507bc7531108a281d6cf4_95_0.png)

使用 Tab 键在屏幕上的不同按钮之间导航，当 OK 按钮变亮时按 Enter 键。`Xconfigurator` 首先检查从 `/usr/X11R6/lib/X11/XF86Config` 是否存在指向 `/etc/X11/XF86Config` 的符号链接。如果链接存在，`Xconfigurator` 将探测您的显卡并通过对话框报告，如图 4.2 所示。

图 4.2

`Xconfigurator` 用一个小对话框报告您的显卡信息。

![](img/fbfff30e42d507bc7531108a281d6cf4_95_1.png)

## 配置 X 系统第 11 版

第 4 章
