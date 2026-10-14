
| SyscallTable | 222 | 0xffffff7f80fff4 | getdirentattr | HOOKED |

| SyscallTable | 344 | 0xffffff7f80ffee | getdirent64 | HOOKED |

| SyscallTable | 397 | 0xffffff7f80fa7 | write_nancel | HOOKED |

对于每个系统调用，都会打印索引、处理器地址、符号名和状态。被挂钩的函数状态为 `HOOKED`。在之前的输出中，挂钩的函数有 `getdirentattr`（目录条目）、`getdirent64`（目录条目）和 `write_nancel`（write）。挂钩这些函数允许 rootkit 隐藏文件和目录。作为插件调用的 `syscall.master` 文件来自内核的 `bsd`。你可以从 https://opensource.apple.com/source/xnu/ 下载所有 Mac 源码。`mac_check_trap` 插件不需要额外的文件，因为所有条目都定义在内核的 `mach_syscall_name_table` 变量中。

## 影子系统调用表

你必须执行的第二个检查是验证影子调用表的使用。在这种攻击中，内核中所有引用系统调用表的代码都被改为引用“影子”表。影子表是合法表的拷贝，恶意软件的目的是为了取证检查让运行的系统看起来不存在。我们不要将其与 Windows 上的影子表（例如 `ServiceDescriptorTable`）混淆——它们是完全不同的概念。

在 NoSuch2013 的演讲中，Pedro Vila 展示了绕过 Volatility 插件检查的攻击，包括 `mac_check_syscalls`（见 http://reverse-engineering.info/wp-content/uploads/2013/05/D3_04_Revisiting_MacOS_Rootkits.pdf）。作为回应，Cem Guruk 在 2013 Volatility 插件提交中检查了影子调用表。这项工作已包含在 Volatility 2.4 的 `mac_check_syscall` 中。

## IOKit 通知

IOKit 子系统（https://developer.apple.com/library/mac/documentation/devicedrivers/conceptual/IOKitFundamentals/Introduction/Introduction.html）是 Mac 用于开发设备驱动和与硬件进行结构化交互的工具和 API 集合。数字取证分析师关注 IOKit 是因为它暴露了许多内核扩展可以滥用的接口。例如，允许为硬件事件注册回调的通知接口。

你可以使用 Volatility `mac_plugins` 列出所有注册的通知回调。对于每个回调，它还会呈现处理函数的地址和交付的服务：

```
$ python vol.py -f clean.mem --profile=MacLion_10_8_1_AMD64 mac_notifiers
Volatility Foundation Framework 2.4
```

| Status | Key | Handler | Matches |

| :--- | :--- | :--- | :--- |

| OK | IOServicePublish | 0xffffff8007962aa | IOServiceConnect |

| OK | IOServicePublish | 0xffffff80079be4a | IO,Apple,State |

| OK | IOServicePublish | 0xffffff800065ac | IOSWrangler |

| OK | IOServicePublish | 0xffffff8000a2aa0 | IOHideDevice |

| OK | IOServicePublish | 0xffffff8000a2aa0 | IOHIDEventService |

| OK | IOServicePublish | 0xffffff8000a2aa | IOSWrangler |

| OK | IOServicePublish | 0xffffff8000a2ac38 | AppleKeyswitch |

| OK | IOServicePublish | 0xffffff80007c7a02 | IOSWrangler |

| OK | IOServicePublish | 0xffffff8000627c0 | AppleSMC |

| OK | IOServicePublish | 0xffffff8000796298 | IOdisplay |

| OK | IOServicePublish | 0xffffff8000a1aa452 | IOSWrangler |

| OK | IOServicePublish | 0xffffff80ad5c6 | IOHIDEventService, |

## 检测 Logtext

Logtext (https://code.google.com/p/logtext) 是一个开源 rootkit，滥用 IOKit 接口来实现内核模式键盘记录器。以下代码显示了 Logtext 如何注册以实现其回调函数：

```
notify = addNotification(gIOPublishNotification, serviceMatching("IOHIDKeyboard"), (IOServiceNotificationHandler),
```

# 834 第四部分：Mac 内存取证

&com_fsb_iokit_logKext::myNotificationHandler,this,

0);

此代码使用 `addNotification` 例程来注册类型为 `GIOPublishNotification` 的回调。每当匹配第二个参数（`IOKeyboard`）的服务发布事件时，它会触发给定的回调。在这种情况下，函数的第二个参数用于过滤键盘服务。此行代码的作用是：每当按下键时，攻击者的回调函数 `com_fsb_iokit_logKext::myNotificationHandler` 就会被执行。处理函数可以将用户输入的按键转换为字符并保存到日志中。以下输出显示了针对 `logKext` 感染内存样本的 `mac_notifiers` 结果。

```
$ python.py --file=MacION_10_7_AMD64 -f logKext
mac_notifiers | grep IOKeyboard
IOService IOKeyboard 0xffffff801ddc800 com.fsb.fkext OK
IOServiceFirstPublish IOKeyboard 0xffffff801f50f980 __kernel OK
IOServiceTerminate IOKeyboard 0xffffff801bba400 com.fsb.fkext OK
```

同样发现了之前提到的发布者通知（publisher notice）以及终止通知器（termination notifier）。当键盘被移除时，会触发终止通知，这允许 `logKext` 停止监控已不存在的设备。你还可以看到在内核中注册的回调。

## TrustedBSD

TrustedBSD 子系统实现了对系统资源基于策略的访问控制。它通过允许策略规定哪些进程可以访问资源（如文件、目录、网络等）来实现。这些策略通过一个通知系统强制执行，该系统在特定事件发生时执行回调。每个被监控事件的回调借此可以决定是否允许该操作。

通过 `IOKit`，TrustedBSD 回调也可以被滥用。为了证明这一点，Pedro Vilaça 发布了一个概念证明根内核（rootkit），它为 `mpo_proc_check_task` 策略钩子注册了回调。当用户应用程序调用 `task_pid` 时，该钩子会被触发。在它的概念证明根内核中，恶意回调提升了与恶意软件相关的进程的权限。根内核可以滥用策略回调来阻止文件或目录被发现、阻止网络数据发送等。

要检测 TrustedBSD 回调，你可以使用 `mac_trustedbsd` 插件。该插件会枚举每个策略注册的回调，并验证它们是否在已知的内核模块中实现。在干净的系统中，你应该预期看到为 `TMASafetyNet`（时光机器）、`Sandbox`（沙盒）和 `Quarantine`（隔离）注册的策略：

```
$ python.py -f clean.vmem --profile=MacLion_10_7_5_AMD64_mac_trustedbd
```

Volatility Foundation Volatility Framework 2.4

| | 名称 | 指针 | 状态 |

|---|---|---|---|

| mpo_vnode_check_name_to | TMSafetyNet | 0xffff7f8f0d69b80 | OK |
