
# Embedded Linux 嵌入式系统构建指南

![](img/20a8a1dba21eed48c328710bf57d85d0_0_0.png)
![](img/20a8a1dba21eed48c328710bf57d85d0_0_1.png)
![](img/20a8a1dba21eed48c328710bf57d85d0_0_2.png)

# 引言

我们将尝试理解 `Linux` 的一些基本概念，并看看为什么需要 `Linux` 以及使用 `Linux` 相比 `Windows` 有什么优势。让我们开始吧，`Linux` 是一个开源操作系统。开源意味着如果你在进行开发，就可以免费获得源代码。与授权软件不同，你不需要为它付费。它由 `Linus Torvalds` 基于 `Unix` 开发。人们可以免费使用 `Linux`，而不像 `Windows` 那样。这意味着与 `Windows` 不同，我们不需要购买许可证。你可以轻松地从任何 `Linux` 服务器下载并使用它。在 `Linux` 中，大部分操作系统都是免许可的。你可以轻松地下载……并使用它。它运行在大多数平台上，如电脑、移动设备、服务器等。例如，如果你正在运行 `Ubuntu` 或 `Android`，这意味着你直接或间接地正在使用 `Linux`。`Android` 基本上基于你的 `Linux`，只是 `Android` 中的 GUI 前端是用 `Java` 编写的。但底层结构是你的 `Linux` 内核，根文件系统概念等都是基于 `Linux` 环境的。根据大小和口味，我们会有灵活性选择许多选择，而且非常强大。人们甚至可以在不向电脑安装系统的情况下，通过 `CD/DVD` 或 `U` 盘运行 `Linux`。

- `Linux` 是一个开源操作系统。
- 开源意味着如果你在进行开发，就可以免费获得源代码。
- 与授权软件不同，你不需要为它付费。
- 它由 `Linus Torvalds` 基于 `Unix` 开发。
- 人们可以免费使用 `Linux`，而不像 `Windows` 那样。
- 这意味着与 `Windows` 不同，我们不需要购买许可证。
- 你可以轻松地从任何 `Linux` 服务器下载并使用它。
- 在 `Linux` 中，大部分操作系统都是免许可的。
- 你可以轻松地下载……并使用它。
- 它运行在大多数平台上，如电脑、移动设备、服务器等。
- 例如，如果你正在运行 `Ubuntu` 或 `Android`，这意味着你直接或间接地正在使用 `Linux`。
- `Android` 基本上基于你的 `Linux`，只是 `Android` 中的 GUI 前端是用 `Java` 编写的。
- 但底层结构是你的 `Linux` 内核，根文件系统概念等都是基于 `Linux` 环境的。
- 根据大小和口味，我们会有灵活性选择许多选择，而且非常强大。
- 人们甚至可以在不向电脑安装系统的情况下，通过 `CD/DVD` 或 `U` 盘运行 `Linux`。

## 目录

- 构建嵌入式系统
- 释放嵌入式 Linux 冒险、设计、开发与部署
- 带有示例代码
- 引言
- 为什么我们使用 Linux
- Linux 是一个开源操作系统
- 开源意味着
- 免费使用
- 许可证
- 相比 Windows 优势
- 虚拟机基础
- 安装
- 安装 VirtualBox
- 在虚拟机中安装 Ubuntu-16.04 X64
- Linux 终端
- 示例代码
- Linux Shell (BASH 和 SH)
- 示例代码
- 基础 Linux 命令
- 文本编辑器 (GEDIT)
- 文本编辑器 (NANO)
- 文本编辑器 (VI)
- 文本编辑器 (VIM)
- 版本控制 (GIT)
- 示例代码
- 使用 CTAGS 进行代码解析
- 示例代码
- 使用 SCOPE 进行代码解析
- 示例代码
- 嵌入式平台基础
- 低预算嵌入式板
- 串口通信 (MINICOM, PUTTY, TERATERM)
- 网络通信 (SSH, SCP, WINSCP, TFTP)
- 示例代码
- 从源码编译 QEMU
- 在 QEMU 中运行 ARM 编译的代码
- 带网络支持的 QEMU
- 构建块简介
- 工具链
- 引导加载程序概念
- U-BOOT 概念
- 为真实的 RPI 构建 U-BOOT
- 为 QEMU 构建 U-BOOT
- 在 QEMU 上运行 U-BOOT
- Linux 内核简介
- Linux 内核目录结构
- 板级支持包 (BSP)
- 在 QEMU 上启动 RPI
