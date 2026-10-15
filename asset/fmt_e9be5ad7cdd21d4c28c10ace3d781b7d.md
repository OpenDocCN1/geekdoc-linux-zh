
# 第 11 章 驱动程序与内核

## 驱动程序与内核

```
Feb 14 17:18:57 localhost kernel: BIOS-e820: [mem 0x0000000000000000-0x0000000000000ff] usable
Feb 14 17:18:57 localhost kernel: BIOS-e820: [mem 0x0000000000009f00-0x000000000000ffff] reserved
Feb 14 17:18:57 localhost kernel: Hypervisor detected: KVM
Feb 14 17:18:57 localhost kernel: AGP: No AGP bridge
Feb 14 17:18:57 localhost kernel: x86 PAT enabled: cpu 0, old 0x7049600070406, new 0x701060070106system.
Feb 14 17:18:57 localhost kernel: CPUTRS - virtualized
Feb 14 17:18:57 localhost kernel: e820: last_pfn = 0xdff0 max_arch_pfn 0x4000000
Feb 14 17:18:57 localhost kernel: found MP-table-at [ffff880000009ff0-0x0000ffff000ff]
Feb 14 17:18:57 localhost kernel: memory_mapping: [mem 0x00000000-0x000ffff]...
```

这些消息描述了内核检测到的处理器以及 RAM 如何映射。注意内核意识到它正在虚拟机中启动，而不是在裸机（bare hardware）上运行。

```
Feb 14 17:18:57 localhost kernel: ACPI: bus type registered
Feb 14 17:18:57 localhost kernel: aciphyp: ACPI Hot Plug Driver version: 0.5
Feb 14 17:18:57 localhost kernel: pci host bridge to bus 0000
Feb 14 17:18:57 localhost kernel: pci_bus 0000: root resource [bus 00-ff]
Feb 14 17:18:57 localhost kernel: pci_bus 0000: root resource [io 0x0000-xffff]
Feb 14 17:18:57 localhost kernel: pci_bus 0000: root resource [mem 0x00000000-0xffffffff]
Feb 14 17:18:57 localhost kernel: SCSI initialized
Feb 14 17:18:57 localhost kernel: ACPI: type USB registered
Feb 14 17:18:57 localhost kernel: usbcore: registered new interface usbfs
```

内核初始化系统的各种总线，包括 PCI 总线和 USB 子系统。

```
Feb 14 17:18:57 localhost kernel: Non-volatile memory driver v1.3
Feb 14 17:18:57 localhost kernel: Linux agpgart v0.13
Feb 14 17:18:57 localhost kernel: crash memory driver: version 1.1
Feb 14 17:18:57 localhost kernel: rdac: device handler registered
Feb 14 17:18:57 localhost kernel: hp_sw: device handler registered
Feb 14 17:18:57 localhost kernel: emc: device handler registered
Feb 14 17:18:57 localhost kernel: alua: device handler registered
Feb 14 17:18:57 localhost kernel: libphy: Fixed MDBus posted
Feb 14 17:18:57 localhost kernel: usberial: USB Serial support registered for generic
Feb 14 17:18:57 localhost kernel: i8042: PNP: PS/2 Controller [PNP0032:PS2K,PNP00F3:PS2M] at 0x60,0x64 irq 1,12
Feb 14 17:18:57 localhost kernel: serio: i8042 KBD port 0x60,0x64 irq 1
Feb 14 17:18:57 localhost kernel: serio: i8042 AUX port 0x60,0x64 irq 12
Feb 14 17:18:57 localhost kernel: input: Translated Set 2 keyboard dev/platform/i8042/serio0/input2
Feb 14 17:18:57 localhost kernel: rtc_cmos rtc_cmos: core registered ntc
Feb 14 17:18:57 localhost kernel: rtc_cmos rtc_cmos: setting system clock to2017-02-14 22:18:57 UTC (1487110737)
Feb 14 17:18:57 localhost kernel: cpuidle: using governor
Feb 14 17:18:57 localhost kernel: usbid: USB HID core driver
```

这些消息记录了内核检测到的各种设备，包括电源按钮、USB 集线器、鼠标以及实时时钟（RTC）芯片。内核的一些“设备”并非实际硬件；这些结构用于管理相关的硬件组。例如，`usbid`（USB 人机接口）驱动管理键盘、鼠标、平板电脑、游戏控制器和其他遵循 USB 标准的输入设备。

## 启动

```
Feb 14 17:18:57 localhost kernel: drop_monitor: Initializing network monitor
Feb 14 17:18:57 localhost kernel: TCP: cubic registered
Feb 14 17:18:57 localhost kernel: Netlink socket
Feb 14 17:18:57 localhost kernel: NET: Registered family 10
Feb 14 17:18:57 localhost kernel: NET: Registered family 17
```

在这个阶段，内核初始化了多种驱动程序。

`drop_monitor` 是一个 Red Hat 子系统，实现了对丢包的全面监控。“TCP cubic”是一种为高延迟、高带宽连接优化的拥塞控制算法。

```
Feb 14 17:18:57 localhost kernel: IMA: No TPM chip found, activating TPM-bypass!
Feb 14 17:18:57 localhost kernel: rtc_cmos rtc_cmos: setting system clock to2017-02-14 22:18:57 UTC (1487110737)
```

这里，内核报告它无法在系统中使用可信平台模块（TPM）。TPM 芯片是加密硬件设备，提供安全操作。当适当当时，它们可以使黑客变得困难。例如，TPM 可用于对内核代码签名，并拒绝执行任何签名匹配有助于避免执行恶意注入代码。期望拥有正常 TPM 的管理员看到此消息将是不开心的！

最后一条消息显示内核将电池备份的实时时钟设置为当前时间。这与我们之前看到的在识别为设备时提到的同一个 RTC。

```
Feb 14 17:18:57 localhost kernel: e1000: Intel(R) PRO/1000 Network Driver - version 7.3.21-K8-NAPI
Feb 14 17:18:57 localhost kernel: e1000: Copyright (c) 1999-2006 Intel Corporation.
```
