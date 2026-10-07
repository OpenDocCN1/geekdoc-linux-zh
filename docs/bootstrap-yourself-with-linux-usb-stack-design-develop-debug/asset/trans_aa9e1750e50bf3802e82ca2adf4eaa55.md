

## 第 3 章：Linux USB 子系统概览

![](img/779a74a6577501a55983f193067274a3_58_0.png)

**图 3.10**
USB gadget 子系统架构图。

![](img/779a74a6577501a55983f193067274a3_58_1.png)

**图 3.11**
menuconfig 中的 USB gadget 支持。

设备驱动程序、USB 支持、USB gadget 支持。你可以在 menuconfig 的 USB Gadget 选项中找到 USB Gadget Support 选项，如图 3.11 所示。

```
menuconfig USB_GADGET
tristate "USB Gadget Support"
```

# Linux USB Gadget 子系统

Linux 内核选择菜单。使用 <Enter> 选择项目……，高亮的字母是快捷键。按 <T> 包含，按 <M> 排除，按 <B> 将功能模块化。按 <Esc><Esc> 退出，按 <Help> 搜索。图例：[*] 内置 [ ] 排除 [*] 模块可更改

```
*> USB Gadget Support
  [*] Debugging messages (DEVELOPMENT)
  <*> Debugging information files (DEVELOPMENT)
  (*) Debugging information files in debugfs (DEVELOPMENT)
  [*] USB Peripheral Controller (M306657 USB Peripheral Controller) ---
    <*> USB Peripheral Controller
    Gadget Drivers
      <*> Ethernet Gadget (with CDC Ethernet support)
      [*] Ethernet Emulation Mode (ECM) support
      [*] Gadget Filesystem (EXPERIMENTAL)
      File-backed Storage Gadget testing version
      [*] USB Gadget
      Serial Gadget (with ACM and CDC OBEX support)
      [*] Function Gadget
      [*] Composite Device (Ethernet and ACM)
      [*] Function Composite gadget (EXPERIMENTAL)
      [*] NDIS + CDC Serial + Storage configuration (NEW)
      USB Ethernet + CDC Serial + Storage configuration (NEW)
```

![](img/779a74a6577501a55983f193067274a3_59_0.png)

图 3.12

menuconfig 中的各种 USB gadget 选项。

接下来的章节详细介绍了 gadget 框架中的一些主要配置选项。与 USB host 配置相比，gadget 配置更为简单且具有功能性。图 3.12 展示了 gadget 子系统的配置选项。

配置 gadget 驱动框架的第一步是为平台支持的设备控制器选择驱动程序。与 USB host 框架不同，gadget 框架仅支持一个设备控制器。你可以从 USB Peripheral Controller Support 菜单选项中选择设备控制器驱动，后续代码允许你选择一个设备控制器。

# USB 外设控制器支持

# 此处的顺序按字母排序，但集成控制器位于离散控制器之前，因此它们将成为初始/默认值：

- 集成/SOC 控制器优先
- 同时在 SOC 和离散版本中使用的许可 IP

![](img/779a74a6577501a55983f193067274a3_60_0.png)

图 3.13
menuconfig 列出的内核中提供的各种外设控制器驱动程序。

- 离散控制器（包括所有仅限 PCI 的控制器）
- debug/dummy gadget+hcd 在最后。

```
choice prompt "USB Peripheral Controller"
depends on USB_GADGET
```

当你选择 USB Peripheral Controller Support 菜单选项时，menuconfig 会弹出图 3.13 所示的菜单选项，列出了内核支持的 USB 控制器驱动程序。选择此菜单选项为平台支持的控制器设置 USB 设备控制器驱动程序。

拥有一个提供 gadget 驱动活动洞察的调试机制是非常重要的。gadget 框架驱动程序通过普通打印提供调试信息，可以通过以下选项启用。

```
config USB_GADGET_DEBUG
  boolean "Debugging messages (DEVELOPMENT)"
  depends on DEBUG_KERNEL
```

# Linux USB Gadget 子系统

某些 USB 设备控制器使用 PROC_FS 为用户导出调试信息。如果你的设备控制器驱动程序使用基于 PROC_FS 的调试解决方案，请尝试以下选项。

```
config USB_GADGET_DEBUG_FILES
    boolean "Debugging information files (DEVELOPMENT)"
    depends on PROC_FS
```

某些 USB 控制器使用 DEBUG_FS 向用户导出调试信息。如果你的设备控制器驱动使用基于 DEBUG_FS 的调试解决方案，请尝试以下选项。

```
config USB_GADGET_DEBUG_FS
    boolean "Debugging information files in debugfs (DEVELOPMENT)"
    depends on DEBUG_FS
```

```
config USB_GADGETFS
    tristate "Gadget Filesystem (EXPERIMENTAL)",
```

功能性驱动程序是 gadget 子系统的下一个特性。它们是类驱动的实现。这还包括对复合框架的支持，该框架实现了多功能 USB 设备。作为 gadget 框架一部分实现的、主要的 USB 类规范见表 3.2。

复合驱动框架以不同的组合存在，并主要由特定特定需求驱动。在 gadget 配置文件中，你可以看到各种复合功能，主要用于诺基亚、三星和 Google Android 的设备。

```
config USB_COMPOSITE
    tristate "Composite Device (Ethernet and ACM)"
depends on NET
```

```
config USB_KIA
    tristate "Nokia gadget"
depends on PHET
```

## 表 3.2 USB 类配置

| 配置选项 | 描述 | 依赖 |
| :--- | :--- | :--- |
| config USB_MULTI | "Multunction gadget (EXPERIMENTAL)" | BLOCK & NET |
| config USB_MULTI_RNDIS | "RNDIS + CDC Serial + Storage configuration" | USB_MULTI |
| config USB_MULTI_CDC | "CDC Ethernet + CDC Serial + Storage configuration" | USB_MULTI |

