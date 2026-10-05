

# 文本模式

## 基础命令

| | |
|---|---|
| Ctrl+Enter | 换行 (在 LaTeX 中为 \) |
| Alt+Enter | 创建相同布局的新段落 |
| Ctrl+Alt | 软连字符 - 在 LaTeX 中 |
| Ctrl+Shift | 直引号 |
| Ctrl+Spacebar | 插入不换空格 |
| Ctrl+C | 复制文本 |
| Shift+Ctrl+C | 复制段落布局 |
| Ctrl+D | DVI 预览 |
| Shift+Ctrl+D | 更新 DVI 预览 |
| Ctrl+F | 查找和替换 (查找) |
| Ctrl+I | 打开上下文对话框 (插入) |
| Ctrl+L | LaTeX 模式 |
| Ctrl+M | 新文档 |
| Ctrl+O | 打开文件 |
| Ctrl+P | 打印文件 |
| Ctrl+Q | 退出 LyX |
| Ctrl+R | 重新加载文件 (reload) |
| Ctrl+S | 保存文件 |
| Shift+Ctrl+S | 另存为文件 |
| Ctrl+T | PostScript 预览 |
| Shift+Ctrl+T | 更新 PostScript 预览 |
| Ctrl+V | 插入文本 |
| Shift+Ctrl+V | 应用段落布局 |
| Ctrl+W | 关闭文件 |
| Ctrl+X | 剪切文本 |
| Ctrl+Z | 撤销 |
| Shift+Ctrl+Z | 重做 |
| Alt+C | 选择字体（见下文） |
| Alt+M | 数学函数（见下文） |
| Alt+P | 选择段落类型（见下文） |
| Alt+S | 选择字体大小（见下文） |
| Alt+X | 执行 LyX 命令 |

## 快捷键 655

| | |
|---|---|
| F2 | 保存文件 |
| F3 | 打开文件 |
| Ctrl+F4 | 关闭文件 |
| Alt+F4 | 退出 LyX |
| F7 | 拼写检查 |
| F10 | 打开菜单（目前仅支持英文菜单） |

## 段落格式

| | |
|---|---|
| Shift+Ctrl+C | 复制段落布局 |
| Shift+Ctrl+V | 应用段落布局 |
| Alt+P, Spacebar | 段落类型下拉菜单（抱歉，KLyX 中不支持） |
| Alt+P, 1-4 | 段落类型 *章节，节，小节*, 小节 |
| Alt+P, 1-4 | 段落类型 *章节*,节*, 小节*, 三级小节 |
| Alt+P, I | 段落类型项目列表 |
| Alt+P, S | 标准 |

## 字体格式

| | |
|---|---|
| Ctrl+B | 粗体 |
| Ctrl+E | 斜体 (强调) |
| Ctrl+K | 小型大写 |
| Shift+Ctrl+P | 打字字体 (程序代码) |
| Ctrl+U | 下划线 |
| Alt+C, Spacebar | 无格式（默认字体） |
| Alt+C, B | 粗体 (bold) |
| Alt+C, E | 斜体 (italic) |
| Alt+C, M | 公式 (数学模式) |
| Alt+C, P | 打字字体 (程序代码) |
| Alt+C, R | 罗马字体 |
| Alt+C, S | 无衬线字体 |
| Alt+C, T | LaTeX 模式 |
| Alt+C, U | 下划线 |

## 656 LYX - 让 LaTeX 简单

| | | | | |
|---|---|---|---|---|
| Alt+S | 1 | 2 | 3 | 0 | 从极小到巨大 (S ... 普通) |
| Alt+S | T | 极小 | | |
| Alt+S | Shift+S | 较小 |
| Alt+S | S | 小 |
| Alt+S | N | 大 |
| Alt+S | Shift+L | 更大 |
| Alt+S | H | 巨大 |
| Alt+S | Shift+H | 极大 |
| Alt+S | + | 更大 |
| Alt+S | - | 更小 |

## 数学模式

在特性方面，LyX 比许多其他公式编辑器（如 Word）具有巨大优势：公式几乎完全可以通过键盘输入。特别是 LaTeX 专业人士会松一口气——只要按下空格键，LyX 就会将命令替换为相应的符号或结构。例如，在数学模式下输入 `\frac` 和空格，LyX 会生成分式，你可以继续所见即所得的操作。

| | |
|---|---|
| Ctrl+M | 切换到数学模式 |
| Esc | 退出数学模式，在元素末尾插入 |
| Spacebar | 公式（例如分式或括号） |
| Ctrl+Spacebar | 元素之间的空格 |
| \code | 替换相应的符号（见第 612 页） |
| | 上标 |
| Alt+M, 8 | 无穷大符号 (∞) |
| Alt+M, or | 插入括号 |
| Alt+M,= | 不等符号 (≠) |
| Alt+M=+ | 加减号 (±) |
| Alt+M, F | 分式 |
| Alt+M, G, letter | 希腊字母（例如） |
| G, B | β |

## 快捷键 657

| | |
|---|---|
| Alt+M,I | 积分 |
| Alt+M,P | 偏导符号 (∂) |
| Alt+M,S | 根号 (square) |
| Alt+M,V | 矢量箭头 (\vec{i}) |

最后，两个例子：

```
\int_a^b x Ctrl+M, Spacebar, beta, alpha, Ctrl+Spacebar, dx
```

```
\sin(\frac{\pi}{2}) Ctrl+M, cursor down, pi
```

# imp – Photoshop 的替代品

imp (GNU Image Manipulation Program) 是一个图像处理程序，在许多方面提供了与商业程序 Photoshop 相似甚至更好的功能。本质区别在于：imp 是免费软件 (GPL)。它的主要作者是 Matt 和 Spencer Kimball，并得到了许多帮助调试、优化或编写众多插件（扩展模块）的人的支持。

本章对 imp 1.0 进行初步介绍。尽管由于空间限制，无法尝试描述 imp 的所有功能，但至少将提供所有功能的详细信息。图形文件的简单转换、图像处理的执行以及截图的制作见第 15 章（第 491 页）。

## 20.1 简介

### imp 是什么？

imp 是一个图像处理程序——从引言中你就知道这一点。如果你没有 Photoshop 或类似程序的经验，这个术语可能仍然模糊。通过 imp，你可以：

- 读取和写入各种格式的位图文件；支持的格式包括 GIF、PNG 和 TIFF
- 导入 PostScript 文件 (EPS/PS) 和 Photoshop 文件 (PSD)
- 从零开始创作绘画
- 更改图像的颜色和亮度分布（例如，调节亮度、增加对比度等；此类操作主要用于提高扫描的质量）
- 为图像应用各种滤，例如检测并突出边缘、实现视觉效果等
- 选择并裁剪图像部分，对其单独处理，并将它们组合成新图像（照片管理）
- 将新的图形元素整合图像（线条、图案、渐变色、文本等）
- 创建动画 *.gif 文件（例如制作震撼的网页）
- 将 imp 操作自动化（要做到这一点，你必须熟悉 GIMP 集成的 Script-Fu 语言）
- 对文件集批量应用 imp

> imp 不包含任何扫描功能。Linux 下控制扫描器的丰富功能由 SANE (Scanner Access Next) 包提供，它是许多发行版的组成部分。正确安装后，可以通过插件从 imp 直接使用 SANE——见 xscanimage 文。关于 SANE 的最新信息可以在 www.mastang.com/sane 找到。

> imp 不包含照片 CD 文件（扩展名 PCD）的导入过滤器。如果你想从照片 CD 读取图像，可以采用非常易用的 xpcd 程序——见第 517 页。

## 梦想与现实

imp 是一个功能极其丰富且强大的程序（而本章只描述了前 5%！）。尽管如此，很大可能你在进行第一次实验后，就会放弃所有希望并从硬盘上删除该程序。主要有两个原因：

- imp 是一个强大的工具，但在高效使用它之前，你需要深入熟悉。偶尔在主页上摆弄一个 *.gif 文件对该程序的适用性非常有限。（这不只是 imp 的错。通常，专业的图像处理是一项比看起来困难得多的活动。）
- imp 对硬件有很高要求。imp 手册也是如此，它通常使用 acroread 阅读。作为一个合理的工作环境，你需要足够的内存（至少 64 MB）、快速的 CPU、大屏幕、高分辨率鼠标以及支持真色的显卡（即 24 位）。

错误的预期也源于 imp 经常被描述为免费但在其他方面等同于 Adobe Photoshop 的变体。这目前有些夸大（但 imp 正在积极开发中）。以下点总结了主要的限制和差异：

## 在线文档

尽管 imp 提供了编写整本书所需的材料，但打印文档仍然少得惊人。然而，有一份 600 页的手册（imp 用户手册，简称 GUM），通常随 imp 一提供。GUM 有多个版本：

- *.pdf 文件（Adobe Acrobat 文档，13 Mbytes）

