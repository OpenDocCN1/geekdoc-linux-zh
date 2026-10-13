
在本章中，我描述了如何访问 OpenBoot 以及可用于测试和提供硬件信息的各种命令。

我描述了 OpenBoot 体系。我解释了 OpenBoot 如何控制许多硬件设备。通过 OpenBoot 中的可编程用户界面，系统管理员可以设置若干控制系统硬件和外围设备的参数。

本章还解释了设备名称。在整本书中，我将引用 Solaris 中使用的设备名称。理解它们中的每一个都关重要。我将在第 16 章重新讨论这个主题，该章将深入介绍设备和设备驱动。除了设备名称，我还解释了如何设置临时和永久设备别名。

最后，我描述了如何保护 OpenBoot 环境免受未经授权的访问，并深入探讨了上一章讨论的话题——引导和加载内核。

本章和第一章假设操作系统已安装并配置。在下一章中，我将描述如何从 OpenBoot PROM 安装 Solaris 操作系统。

## 第 2 章 OPENBOOT 91

### 应用知识

### 练习

#### 2.1 使用 OpenBoot 命令

在以下练习中，您将停止系统并使用以下 OpenBoot 命令设置参数并收集系统的基本信息。

**预计时间：** 15 分钟

- 1. 执行正确的 OpenBoot 命令显示 banner：

  `banner`
- 2. 按照如下设置将参数设置为默认值：

  `reset-all`
- 3. 按照如下格式显示 OpenBoot 帮助列表：

  `help`
- 4. 使用 `banner` 命令从您的系统中获取以下信息：

  ROM 版本：

  已安装内存 (MB)：

  系统类型：

  系统序列号：

  以太网地址：

  主机 ID：
- 5. 使用 `printenv` 命令显示以下 OBP 参数列表：

  `output-device`

  `input-device`

  `auto-boot?`

  `boot-device`
- 6. 设置以下参数以防止系统在重置后自动引导。

  从 OpenBoot `ok` 提示符输入以下内容：

  `setenv auto-boot? false`
- 7. 输入以下内容验证其已设置：

  `printenv auto-boot?`
- 8. 现在，从 UNIX 提示符，按照如下方式将 `auto-boot?` 参数设回 true：

  `eeprom auto-boot? true`
- 9. 将系统恢复到 0 级，并验证 `auto-boot?` 参数已设置为 true。
- 10. 使用以下命令显示连接到系统的磁盘设备列表：

  `probe-scsi`

  `probe-scsi-all`

  `probe-ide`

  解释这些命令之间的主要区别。

  > 注意：如果这些命令中的任何一个返回了继续操作将挂起的消息，请输入 `n` 以避免该命令。在运行 `probe` 之前运行 `reset-all`，然后响应 `y`。

### 应用知识

- 8. 使用第 7 步中的 OpenBoot 命令列出连接到系统的每个 SCSI 设备的目标数和设备类型。
- 9. 从 OpenBoot 提示符，按照如下方式识别您的默认引导设备：

  ```
  printenv boot-device
  ```
- 10. 使用 `show-disks` OpenBoot 命令获取系统中磁盘驱动器的列表，如下：

  ```
  show-disks
  ```

  按照如下格式显示 `disk4` 别名的完整设备路径：

  ```
  dealias disk4
  ```

  按照如下方式创建一个指向 SCSI 目标 4 的永久性设备别名 `disk4`：

  ```
  nalias disk4=/iommu/sbus/esdma@,400000/esp8,000000/sd4
  ```

  重置系统，并输入以下内容验证 `dealias` 仍然设置：

  ```
  dealias
  ```
- 11. 启动系统，以 root 身份登录，并使用 `eeprom` 命令列出所有 NVRAM 参数。
- 12. 使用 `eeprom` 命令按照如下方式显示 `boot-device` 设置：

  ```
  eeprom
  ```
- 13. 从 OpenBoot 提示符按照如下方式将 `boot-device` 设置为默认值：

  ```
  set-default
  ```
- 14. 从 OpenBoot 提示符，按照如下方式移除 alias `disk4`：

  ```
  nalias
  ```
- 15. 重置系统，并输入以下内容验证 `disk4` 不再设置：

  ```
  printenv
  ```
- 16. 按照如下格式设置所有 OpenBoot 参数：

  ```
  set-defaults
  ```

### 复习题

- 1. 操作系统启动之前看到的硬件级接口被称为：

  A. OpenBoot

  B. EEPROM

  C. Firmware

  D. Boot
- 2. 哪里存储 `hostid` 等信息？

  A. Firmware

  B. OpenBoot

  C. NVRAM
- 3. OpenBoot 执行哪些任务？（选两个）

  A. POST

  B. Bootblock

  C. ufsboot

  D. Kernel

## 第 2 章 OPENBOOT 93

### 应用知识

- 4. 下列哪项不是 固件的任务？

  A. 测试和初始化系统硬件

  B. 加载内核

  C. 从存储设备或网络启动操作系统

  D. 允许修改启动配置，如 NVRAM 参数
- 5. 下列哪项通过互连总线连接到主机？

  A. SBUS 卡

  B. SCSI 外设

  C. 插件设备驱动

  D. Nodes
- 6. `/pci/1f,0/pci@1,1/ide@3` 是什么类型的设备？

  A. 全设备路径

  B. 物理设备

  C. 逻辑设备

  D. 实例
- 7. 下列哪项用于在 OpenBoot 中获取设备并显示路径？

  A. show-devs

  B. dmesg

  C. pwd

  D. sysdef
- 8. 哪个命令创建名为 `disk3` 的临时设备别名？

  A. `setenv disk3 /iommu/sbus/espdfma@,400000/esp8f,800000/sd3@0,sd@0`

  B. `setenv disk3 /iommu/sbus/espdfma@,400000/esp8f,800000/sd3@0,sd@0`

  C. `naliases disk3 /iommu/sbus/espdfma@,400000/esp8f,80000/sd@0`

  D. `dealias disk3 /iommu/sbus/espdfma@,400000/sd3@0`
- 9. 如果你想在 NVRAM 中创建永久别名（重启后仍存在），你应该使用下列哪个命令？

  A. dealias

  B. naliases

  C. setenv

  D. eeprom
- 10. 哪个 NVRAM 变量指定了从哪个设备启动？

  A. `boot-device`

  B. `boot-file`

  C. `output-device`

  D. `input-device`
- 11. 哪个命令不能用于修改 NVRAM 变量？

  A. `set-defaults`

  B. `setenv`

  C. `naliases`

  D. `set-default`

## 运用你所学的知识

- 12. 如果系统由于错误的 NVRAM 变量无法启动，在 OpenBoot 提示符下执行以下哪项操作可以将 NVRAM 变量重置为默认设置？

  - A. `set-default <variable>`

  - B. Stop-N

  - C. `set-defaults`

  - D. Ctrl-N
- 13. 下列选项可以限制用户在 OpenBoot 提示符下允许执行的操作？

  - A. `security-password`

  - B. `security-mode`

  - C. `set-secure`

  - D. `set-security`
- 14. 下列哪项用于 OpenBoot 中测试指定设备节点下方所有具有内置自检方法的设备？

  - A. diag

  - B. `probe-scsi`

  - C. test-all

  - D. test
- 15. 在 OpenBoot 命令中使用以下哪个选项时，系统会提示你输入要加载的独立程序名称？

  - A. -v

  - B. -f

  - C. -s

  - D. -a
- 16. 启动设备的块 1–15 中驻留了什么？

  - A. bootblk

  - B. superblock

  - C. kernel

  - D. fsboot
- 17. 下列哪项用于加载操作系统内核？

  - A. fsboot

  - B. openBoot

  - C. bootblk

  - D. init
- 18. 下列哪个命令列出所有硬件设备、系统设备、可加载模块以及选定内核调优参数的值？

  - A. `/var/adm/messages`

  - B. adb

  - C. dmesg

  - D. sysdef
- 19. 哪个目录存储物理设备名称？

  - A. `/var`

  - B. `/dev`

  - C. `/kernel`

  - D. `/devices`

  - E. `/etc`

## 运用你所学的知识
