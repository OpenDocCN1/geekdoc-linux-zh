
FPSWA 驱动通常实现在名为 `fpswa.efi` 的文件中，并存储在易失性内存（例如 ROM）或 EFI 系统分区上。可以使用 EFI 启动服务将驱动加载到内存。一旦加载，为 FPSWA 定义的 GUID (`FPSWA_PROTOCOL`) (`struct fpswa_interface`) 就会生效。通过此指针，操作系统将拥有调用 FPSWA 处理器所需的所有内容。

### 432 启动 第10 章

| 内存类型 | 物理地址范围 | 页数 | 属性 |
| --- | --- | --- | --- |
| BootServicesData | 0x000000000000-0x000000fff | 1 | UC|WB |
| ConventionalMemory | 0x000000001000-0x0000088ff | 136 | UC|WB |
| BootServicesData | 0x000000008900-0x000009fff | 23 | UC|WB |
| RuntimeServicesCode | 0x00000000c000-0x00000ffff | 64 | WC|RT |
| ConventionalMemory | 0x0000010000-0x000308ff | 257921 | UC|WB |
| LoaderData | 0x00030f081000-0x00030866 | 66 | UC|WB |
| LoaderCode | 0x00030f087000-0x00030f8aa | 33 | UC|WB |
| LoaderData | 0x00030f09a000-0x00030cff | 35 | UC|WB |
| BootServicesData | 0x00030f03c000-0x00030cff | 1 | UC|WB |
| ConventionalMemory | 0x00030f03d000-0x00030dff | 4 | UC|WB |
| BootServicesData | 0x00030f031000-0x00030dff | 3 | UC|WB |
| ConventionalMemory | 0x00030f03d000-0x00030dff | | UC|WB |
| BootServicesData | 0x00030f0d6000-0x000307ff | 18 | UC|WB |
| RuntimeServicesCode | 0x00030f0e8000-0x00030effff | 2 | WC|RT |
| BootServicesData | 0x00030f0e9000-0x00030ebff | 2 | UC|WB |
| RuntimeServicesCode | 0x00030f0ec000-0x00031f56ff | 107 | UC|WB |
| BootServicesData | 0x00030f157000-0x00031b6ff | 98 | UC|WB |
| RuntimeServicesData | 0x00030f1b9000-0x00031b9ff | 1 | UC|WB |
| BootServicesData | 0x00030f1bba000-0x00031cdff | 20 | UC|WB |
| RuntimeServicesData | 0x00030f1ce000-0x000320f6ff | 57 | WC|RT |
| BootServicesData | 0x00030f207000-0x000324eff | 72 | UC|WB |
| BootServicesData | 0x00030f24f000-0x0003244ff | 1 | UC|WB |
| RuntimeServicesCode | 0x00030f250000-0x0003423ff | 468 | WC|RT |
| ACPIReclaimMemory | 0x00030f244000-0x00034255ff | 2 | UC|WB |
| BootServicesData | 0x00030f246000-0x000342dff | 8 | UC|WB |
| BootServicesData | 0x00030f248000-0x000342eff | 1 | UC|WB |
| RuntimeServicesCode | 0x00030f42f000-0x00037f3ff | 2833 | UC|WB |
| PalCode | 0x00030f34a000-0x00037e7ff | 59 | UC|WB |
| BootServicesData | 0x00030f37b000-0x000376cff | 2 | UC|WB |
| RuntimeServicesData | 0x00030f37d000-0x00037e4ff | 1 | UC|WB |
| BootServicesData | 0x00030f37e000-0x00037e0ff | 2 | UC|WB |
| RuntimeServicesData | 0x00030f380000-0x0003ffffff | 128 | WC|RT |
| RuntimeServicesData | 0x0000ffffc000-0x0000ffffff | 1024 | UC|RT |
| MemoryIOSpace | 0xffffffc000-0xffffffff | 16384 | UC|RT |

图10.10 空闲内存示例。表10.10 空闲内存。剩余的大多数项都是 `BootServicesData` 或 `RuntimeServicesData` 类型。两者唯一的区别是后者在EFI切换到运行时仍在使用。在映射末尾，我们看到一个 `PalCode` 项。该条目标记了 pal 代码占据的范围。如10.1节所述，该范围用于支持虚拟空间的PAL调用。注意最后一个条目是 `MemoryIOSpace`。该条目描述了用于访问 I/O 设备的（见第7章，*Device/O*）地址范围。由于它并不代表内存，我们可以更准确地说 `MemoryMap()` 返回的是地址映射，而不是内存映射。然而，为了与EFI规范保持一致，我们继续将其称为内存映射。

图10.11 Linux/ia64 提供的EFI运行时服务。

## 切换EFI到运行时

如前所述，启动服务程序 `ExitServices()` 可用于将EFI切换到运行时模式。这通常由加载程序在控制权移交给操作系统之前完成。该程序的成功返回意味着EFI启动服务不再可用，且EFI不再控制机器硬件（特别是内存）。运行时接受两个参数：第一个必须是作为 `efi_main()` 第一个参数传递的句柄，第二个必须是 `MemoryMap()` 返回的缓存。EFI检查此确保它与最新版本的映射对应。如果不是，则 `ExitServices()` 调用失败。也就是说，EFI在允许切换到运行时模式之前强制调用者获取最新版本的内存映射。这是一个防止意外使用状态内存映射的简单预防。EFI处于运行时模式，类型为 `BootServicesCode` 和 `BootServicesData` 的内存映射项可以被视为空闲内存。

## 内核内核接口

Linux/ia64内核通过接口（`include/asm-ia64/efi.h`）访问EFI运行时服务。该接口在图10.11中汇总。服务主要有三类：时间相关、环境变量相关和杂类。时间相关服务包括用于获取和设置挂钟时间的例程序。Linux内核使用 `get_time()`在启动时初始化日期和当天时间。另外两个程序提供了获取和设置唤醒时间的功能。在实现了这些功能的机器上，可以使用它们在指定时间自动开启机器。与环境变量相关的服务使得获取和设置EFI环境变量的内容成为可能。此外，`get_variable()`程序提供了读取环境变量的能力。杂类服务 `get_next_high_count()`单调计数器的高位，`reset_system()`提供了重启机器的能力。

```c
/* 时间服务: */
efi_status_t get_time(tm, tc);
efi_status_t set_time(tm);
efi_status_t get_wakeup(ena, pend, tm);
efi_status_t set_wakeup(ena, tm);

/* 环境变量服务: */
efi_status_t get_variable(nm, vattr, sz);
efi_status_t next_variable(sz, nm, vattr);
efi_status_t set_variable(nm, vattr, val);

/* 杂类服务: */
efi_status_t get_next_high_count(val);
efi_status_t reset_system(type, status, sz);
```

## 10.2 引导程序

![](img/6c68864a077d5b0dcc087ee4297a0609_472_0.png)
