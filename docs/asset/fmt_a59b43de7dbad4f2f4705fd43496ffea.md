
```
$ python vol.py -f klog.dump --profile=Win76 devicetree
DRV 0x01f89310 \Driver\klog
-- DEV 0x8d1d270 (?) FILE_DEVICE_KEYBOARD

DRV 0x2421770 \Driver\KbdClass FILE_DEVICE_KEYBOARD
-- DEV 0x81e96030 KeyboardClass
-- DEV 0x81926e31 53              PUSH EBP
0x81926e32 8bec            MOV EBP, ESP
0x81926e34 8b40c6            MOV EAX, [EBP+0xc]
0x81926e37 8b4d08            MOV ECX, [EBP+08]
0x81926e38 8e3c00            SUB ESP, ECX
0x81926e3d 53              PUSH EB
0x81926e3e 8b5860            MOV EBX, [EAX+060]
0x81926e41 31d803dff    MOV EAX, [0xffd0308]
0x81926e46 3a4808            CMP ECX, [EAX+08]
[snip]
```

此时，你已经知道 rootkit 的代码覆盖了 `0x81926e31` 附近的区域。请记住，它一直在运行。这一个程序的功能涉及挂钩 `IRP`，通过跟踪这些挂钩，你被直接带到了恶意机器的主体部分。

# Stuxnet 的恶意设备

```
$ python vol.py -f klog.dump devicetree
DRV 0x0255010 \System\vmfs
-- DEV 0x820f000 hKNOWN_FILE_fs
-- DEV 0x82a1030 hfs_fs
-- ATT 0x81f5020 -- \System\Flt

-- ATT 0x8123544 -- \\\netnet
```

Stuxnet 的恶意设备修改了系统：

```
$ python vol.py -f klog.dump devicetree
DRV 0x0255010 \System\vmfs
-- DEV 0x820f000 hKNOWN_FILE_fs
-- DEV 0x82a1030 hfs_fs
-- ATT 0x81f5020 -- \System\Flt
 
-- ATT 0x8123544 -- \\\\netnet
```

# 审计 SSDT

服务描述符表（`SSDT`）包含指向内核模式函数的指针。如图 13-7 所示，用户模式应用程序请求系统服务（如写入文件或创建进程），`ntdll.dll`（或其他用户模式库）中的小型存根代码协助调用线程以受控的方式进入内核模式。这种转换在 Windows 2000 中通过执行 `INT 0x2E` 指令完成，在 XP 中通过 `SYSCALL` 完成。两种方法最终都会进入名为 `KiSystemService` 的函数，该函数在 `SSDT` 中查找请求函数的地址。由于调用表是指针数组，因此查找是基于索引的。

**图 13-7:** 显示 `SSDT` 在分发系统调用中作用的高级示意图

## 内核取证与 Rootkits

`SSDT` 中函数的顺序和数量在不同的操作系统版本之间有所不同。例如，`NtUnloadDriver` 在 Windows 7 64位系统上位于 `0x184`，但在 Windows 8 64位系统上是 `0x1A1`。此外，请注意每个系统上都有多个调用表。第一个也是最为人知的表存储了内核执行模块（如 `nkrnl.exe` 等）提供的原生 API 函数。第二个表被称为影子 `SSDT`（shadow `SSDT`），存储由 `win32k.sys` 提供的 GUI 函数。如图 13-7所示，除非你正在运行 `IIS` 服务器，否则另外两个表默认是不使用的——在这种情况下，第三个表会被 `spud.sys`（`IIS` 服务驱动程序）使用。

### 数据结构

以下代码是 64 位 Windows 7 系统相关的数据结构。`nt:KeServiceDescriptorTable` 和 `nt:KeServiceDescriptorTableShadow` 都是 `_DESCRIPTOR_TABLE` 的实例，包含多达四个描述符（项）。每个描述符都有一个 `KiServiceTable` 成员指向一个函数数组，而 `ServiceLimit` 指定了数组中存在多少函数。

```
>>> dt("SERVICE_DESCRIPTOR_TABLE")
'_SERVICE_DESCRIPTOR_TABLE' (64 bytes)
0x0 : Descriptors ['array', 4, ['SERVICE_DESCRIPTOR_ENTRY']]

>>> dt("SERVICE_DESCRIPTOR_ENTRY")
'_SERVICE_DESCRIPTOR_ENTRY' (32 bytes)
0x0 : KiServiceTable ['pointer', ['void']]
0x8 : CounterTable ['pointer', ['unsigned long']]
0x10 : ServiceLimit ['unsigned long']
0x18 : ArgumentTable ['pointer', ['unsigned char*']]
```

## 枚举 SSDT

要在 Windows 内存转储中枚举 `SSDT`，可以使用 `ssdt` 插件。由于 32 位和 64 位版本之间的差异，该插件寻找 `SSDT` 数据的方式完全不同，但输出格式是一致的。具体来说，在 32 位 Windows 上，我们枚举所有线程对象并收集 `_THREAD.Tcb.ServiceTable` 成员的唯一值。该成员在 64 位平台上不存在，因此我们改为组装 `nt:KeAddSystemTable` 函数，并提取 `KeServiceDescriptorTable` 和 `KeServiceDescriptorTableShadow` 符号的相对虚拟地址（`RAs`），如图 13-8所示。

## 第二部分：Windows 内存取证

![](img/9e59079ff66884b5d70128a9edb02f4c_417_0.png)

图 13-8：跨 `KeAddSystemServiceTable` API 的 `SSDT` 和影子 `SSDT`。

以下是 `ssdt` 插件输出在 64 位 Windows 7 机器上的显示：

```
$ python vol.py -f memory.dump --profile=Win7Spx64 ssdt
Volatility Forensics Framework 2.4
```

[x64] 从 `KeAddSystemServiceTable` 获取所有引用的 `SSDTs`...

正在为内核查找适当地址空间...

| SSDT[0] at 0ffff88002dc300 有 401 项 |

| Entry 0000: 0ffff88002ceca90 (NtMapUserSmi) 属于 nkrnl.exe |

| Entry 0001: 0ffff88002bd1e8c (WaitForSingleObject) 属于 nkrnl.exe |

| Entry 0002: 0ffff88002d3a1a (NtKernelReturn) 属于 nkrnl.exe |

| Entry 0003: 0ffff88002c4a80 (ReadFile) 属于 nkrnl.exe |

| Entry 0004: 0ffff88002bf6a7d (NtDeviceIoControlFile) 属于 nkrnl.exe |

| Entry 0005: 0ffff88002bed9a0 (WriteFile) 属于 nkrnl.exe |

| Entry 0006: 0ffff88002b7c90 (NtRemoveIoCompletion) 属于 nkrnl.exe [截取] |

| SSDT[1] at 0ffff966001ab50 有 827 项 |

| Entry 0000: 0ffff9660019597a (NtThreadState) 属于 win32k.sys |

| Entry 0001: 0ffff96600192a50 (NtPeekWithMessage) 属于 win32k.sys |

| Entry 0002: 0ffff966001a2f6c (NtCallNoParam) 属于 win32k.sys |

| Entry 0003: 0ffff966001b211c (NtGetKey) 属于 win32k.sys |

| Entry 0004: 0ffff966001ab500 (NtInvalidateRequest) 属于 win32k.sys |

| Entry 0005: 0ffff966001a4164 (NtCallNoParam) 属于 win32k.sys |
