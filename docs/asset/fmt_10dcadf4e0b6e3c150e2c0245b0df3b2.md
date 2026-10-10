
# 外部总线控制器 (EBC) 设置

```c
#define CONFIG_SYS_FLASH CONFIG_SYS_FLASH_BASE

#define CONFIG_SYS_CPLD 0x08000000

/* 存储库 0 (NOR-FLASH) 初始化 */
#define CONFIG_SYS_EBC_PB0AP 0x03017300

#define CONFIG_SYS_EBC_PB0CR (CONFIG_SYS_FLASH | 0x0da00)

/* 存储库 2 (CPLD) 初始化 */
#define CONFIG_SYS_EBC_PB2AP 0x04814500

#define CONFIG_SYS_EBC_PB2CR (CONFIG_SYS_CPLD | 0x18000)

<...>
```

列表 7-4 展示了 U-Boot 如何为特定板卡配置。实际的板卡配置文件可能包含数百行类似于此处显示的内容。在此示例中，你可以看到 CPU（`CONFIG_440EF`）、板卡名称（`CONFIG_HOSTNAME`）、时钟频率以及 Flash 和 PCI 基础内存地址的定义。我们包含了配置变量（`CONFIG_XXX`）和配置设置（`CONFIG_SYS_XXX`）的示例。最后几行是初始化存储库 0 和 1 的外部总线控制器所需的实际处理器寄存器值。你可以看到，这些值只能通过对板卡和处理器的详细了解来获得。

U-Boot 的许多方面都可以使用这些机制进行配置，包括哪些功能被编译到 U-Boot 中（支持 DHCP、内存测试、调试支持等）。这种机制可以用于告诉 U-Boot 特定板上有多少以及什么类型的内存，以及这些内存映射在何处。你可以通过直接查看 U-Boot 代码获取更多信息，特别是非常优秀的 `README` 文件。

### 7.3.3 U-Boot 监控命令

U-Boot 支持超过 70 组标准命令集，通过 `CONFIG_CMD*` 可以启用超过 150 条唯一命令。U-Boot 通过配置设置宏（`CONFIG_*` 宏）启用宏命令。要查看来自近期 U-Boot 快照的完整列表，请参见附录 B，“U-Boot 可配置命令”。表 7-1 仅显示了其中几个，以便让你对可用功能有一个大致了解。

## 表 7-1 某些 U-Boot 可配置命令

| 命令集 | 命令描述 |
|---|---|
| `CONFIG_CMD_FLASH` | Flash 存储器命令 |
| `CONFIG_CMD_MEMORY` | 内存转储、填充、拷贝、比较等 |
| `CONFIG_CMD_DHCP` | DHCP 支持 |
| `CONFIG_CMD_PING` | Ping 支持 |
| `CONFIG_CMD_EXT2` | EXT2 文件系统支持 |

要启用特定命令，请定义与你想要启用的命令对应的宏。这些宏定义在你的板卡特定的配置文件中。列表 7-4 显示了在板卡特定的配置文件中启用的几条命令。你可以看到，如果板卡是 440EP，则会条件地定义 `CONFIG_CMD_USB`、`CONFIG_CMD_FAT` 和 `CONFIG_CMD_EXT2`。

与其在板卡特定的配置头文件中指定每个单独的 `CONFIG_CMD*` 宏，不如从 `.../include/config_cmd_all.h` 中定义的全量命令集开始。该头文件定义了所有可用的命令。第二个头文件 `.../include/config_cmd_default.h` 定义了一列表默认的 U-Boot 命令集，例如 `ftpboot`（从 ftp 服务器启动镜像）、`bootm`（从内存启动镜像）、如 `md`（显示内存）之类的内存工具等。要启用你特定的命令组合，你可以从默认设置开始，并根据需要添加或删除。列表 7-4 在默认基础上添加了 USB、FAT 和 EXT2 命令集。你也可以以类似的方式进行减法，从 `config_cmd_all.h` 开始：

```
#include "config_cmd_all.h"

#undef CONFIG_CMD_DHCP

#undef CONFIG_CMD_FAT

#undef CONFIG_CMD_FDOS

<...>
```
