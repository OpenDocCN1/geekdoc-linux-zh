
| 正在发送: | `D:\work\dr\application\basic1.srec` |

| 数据包: | 25 | 错误检查: CRC | 文件大小: 64K |

| 重试次数: | 0 | 总重试次数: 0 | 文件: 1 / 1 |

| 上次错误: | | | |

| 文件: | | 23k / 64K |

| 已用时间: | 00:00:11 | 剩余: 00:00:19 | 吞吐量: 21020 bps |

图 12.10 HyperTerminal 传输状态对话框。

应用程序到目标硬件的传输进度和信息（包括吞吐量和剩余时间）如图 12.10 所示。

当代码关闭且 RedBoot 输出消息时。RedBoot 输出消息的示例如代码列表 12.6 所示。

- 1 入口点: `0x00180000`，地址范围: `0x00180000-0x0011aba0`
- 2 `xyzModem`: CRC 模式，2(SOH)/215(STX)/0(CAN) 数据包，4 次重试

代码列表 12.6 我们的应用程序传输完成后 RedBoot 输出的消息。

在代码列表 12.6 的第 1 行，显示了我们加载的镜像的内存信息。这些信息包括入口点和应用程序使用的内存范围。第 2 行总结了传输统计数据。

# 第 6 步

现在我们准备好运行我们的示例应用程序了。由于 RedBoot 知道我们应用程序的加载地址，我们不需要为 RedBoot `go` 命令指定入口点。要运行应用程序，在 RedBoot 提示符下输入以下命令：

```
RedBoot> go
```

随着 `basic1` 应用程序的运行，代码列表 12.7 中的输出将出现在 Hyper-Terminal 屏幕上。应用程序将一直运行。

- 1 Hello eCosWorld!!!
- 2
- 3 Thread A, count: 1 message: 75
- 4 Thread A, count: 2 message: 75
- 5 Thread B, message: 68
- 6 Thread A, count: 3 message: 75
- 7 Thread B, message: 68
- 8 Thread A, count: 4 message: 68

代码列表 12.7 Basic1 应用程序输出。

### 12.5.3 调试应用程序

RedBoot 为调试应用程序提供了一些基础设施，例如查看位置，而 GDB 提供了更广泛的调试功能。接下来，我们将使用 GDB 连接到目标硬件，下载示例应用程序，然后运行该应用程序。关于 GDB 的更多文档可以在网上找到：

http://sources.redhat.com/gdb

在宿主机开发工具的设置过程中，我们构建了 GDB 并包含了 Insight GUI；详情请参见第 10 章。可以在命令行模式下运行 GDB，即使带有 Insight GUI 也可以进入 GDB。关于 Insight 的更多信息可以在网上找到：

http://sources.redhat.com/insight

在这一步中，我们将简要介绍使用命令行模式下的 GDB 以及 Insight 界面。调试环境图如图 12.11 所示。

> 调试优化过的代码可能是不可靠的，因为编译器可能会做出与源代码不完全匹配的更改。在这种情况下，在调试源代码时禁用编译器优化可能更好。

要禁用编译器优化，你可以从全局编译器标志 (`CYGBLD_GLOBAL_CLAG`) 中删除 `-O2` 选项，或使用 `-O0` 选项将优化级别设置为零。然后需要重新构建 eCos 库和应用程序代码。

# 第 12 章 使用 eCos 的示例应用程序

![](img/185e30b232edb8183f2482fa0071447a_324_0.png)

**图 12.11** 我们示例的调试环境，在宿主机上运行 GDB，在目标上运行 RedBoot。

如图 12.11 所示，带有 Insight GUI 的 GDB 运行在宿主机开发系统上。我们可以通过串口或以太网端口连接到目标。目标硬件运行着 RedBoot，其中包含 GDB stub。GDB stub 为我们的目标提供了通信协议。

在继续后续步骤之前，确保 RedBoot 已在控制台目标硬件上启动并运行。

# 第 7 步

要启动带有 Insight GUI 的 GDB，我们运行 `i386-elf-gdb.exe`。如果你不想使用 Insight GUI，可以使用 windows 选项运行 GDB；例如，`i386-elf-gdb.exe -nw`。

带有 Insight 的 GDB 如图 12.12 所示。

图 12.12 显示了处于前景的 Insight GUI 窗口和背景中的 Console 窗口。可以通过选择 View -> Console 显示 Console 窗口。

第一步是加载我们的示例应用程序。使用 Insight，我们选择 File -> Open，然后浏览到示例应用程序的位置。使用 Insight 加载示例应用程序后 `basic1.exe`。

# 第 8 步

接下来，连接到目标。通过串口或以太网端口连接到目标，如图 12.13 所示。

![](img/185e30b232edb8183f2482fa0071447a_325_0.png)

# 目标选择

| 连接 | |

| --- | --- |

| 目标: | 串口 |

| 波特率: | 3840 |

| 端口: | COM1 |

# 第 9 步

连接后，我们通过 Run -> Download 下载应用程序。在下载期间，Insight 窗口右上角会出现进度条。下载状态显示在底栏。

# 第 10 步

如果 Console 窗口未打开，选择 View -> Console。这允许我们查看应用程序的输出。

# 应用程序

启动应用程序，选择 Control -> Continue。`basic1` 程序的输出如代码 12.7，显示在 Console 窗口中。

你现在可以熟悉 GDB 的功能，例如单步执行、设置断点和观察变量。

# 12.5.1 使用 GDB 命令行界面

如所述，如果不需要 Insight GUI，也可以从命令行运行 GDB。让我们通过命令行加载并运行应用程序。在使用 Insight 时，这些命令也可以在 Console 窗口中输入。表 12.2 列出了使用串口和以太网运行 GDB 的命令行。这些命令显示在 GDB 提示符 `(gdb)` 之后。

# 表 12.2 串口和以太网 GDB 命令

| 串口 | 以太网 |

| --- | --- |

| 第 1 步：切换到应用程序目录。 | 第 1 步：切换到应用程序目录。 |

| `(gdb) cd d:/wdir/application` | `(gdb) cd d:/wdir/application` |

| 第 2 步：设置串口波特率。 | 第 2 步：通过以太网连接到目标。ᵃ |

| `(gdb) select remotebaud 3840` | `(gdb) target remote 192.168.0.10:9000` |

| 第 3 步：通过串口连接到目标。 | 第 3 步：加载应用程序 |

| `(gdb) target remote compl` | `(gdb) load basic1.exe` |

| 第 4 步：加载应用程序。 | 第 4 步：运行应用程序。 |

| `(gdb) load basic1.exe` | `(gdb) continue` |

| 第 5 步：运行应用程序。 | |

| `(gdb) continue` | | |

ᵃ 使用构建 RedBoot 时配置的静态 IP 地址。

## 12.6 ECos 测试

ECos 存储库为各种包提供了测试套件。这些测试旨在彻底测试不同包中的各种功能，以确保其正常运行。这些测试在模块、组件和系统层级执行，并包括压力测试和性能测试。

ECos 存储库包含了内核、各种设备驱动程序以及 I/O 子系统的测试。内核部分包含了测试不同同步机制、各种线程相关函数以及使用不同锁功能的测试。I/O 子系统包含了各种串口测试。此外还有针对不同目标硬件平台的测试。

测试源代码包含在 ECos 源码仓库中，位于包目录结构下的 `tests` 目录；通用目录结构的插图请参阅图 11.1。测试源代码是如何在应用程序中实现功能的极佳范例。这些测试可以引导你理解不同的 ECos API。

现在，让我们关注如何使用配置工具（Configuration Tool）在 ECos 框架中构建和运行测试。通过选择 `Build` -> `Tests`，可以使用配置工具来构建测试。测试过程过程的输出文件位于安装树下的 `tests` 目录。输出文件为 ELF 格式文件。

> 注意：某些测试（例如包含在 Basic Networking 工作包中的测试）包含一个必须启用才能构建特定测试的配置选项。启用 `Build Networking Tests (Demo Programs) (CYPOS_NET_BUILD_TESTS)` 配置选项允许构建额外的网络测试。
