
`common` 子目录包含适用于所有 HAL 架构的通用包配置文件，包括通用中断配置、虚拟内存布局和 HAL 调试控制的文件。该子目录中包含了函数封装器，用以在所有 HAL 实现之间建立通用性。

`arch` 子目录位于 `powerpc` 架构 HAL 目录下，包含对 PowerPC 处理器的通用支持文件。该通用支持包含的功能包括异常初始化、ROM 和 RAM 启动配置、通用异常和异常处理、线程上下文切换、一个通用的链接器脚本文件以及调试函数。

`mbx` 子目录包含 Motorola MBX860 的源文件。MBX 包的描述（CDL 脚本格式）位于 `cdl` 子目录下的 `hal_powerpc_mbx.cdl` 文件中。

`include` 子目录包含 MBX 平台的所有头文件。`include` 子目录下有 `pkgconfig` 包，内存布局文件位于此处。

`misc` 子目录包含 RedBoot 最小配置文件，这些文件可以导入到配置工具（Configuration Tool）中以建立配置选项和包的基准。

`src` 子目录包含 MBX 平台的主源文件 `mbx.S`。该文件包含 `hal_hardware_init` 程序中的硬件设置代码，该程序配置了所有必要的处理器寄存器，并初始化了 MBX 平台的芯片组配置。`tests` 子目录包含 MBX 平台的测试。

`mpc86x` 和 `quiec` 子目录之所以存在，是因为它们是 MBX 平台使用的 MPC860 架构的变体。我们需要注意我们作为基准的平台所使用的变体，以防我们需要修改或扩展变体包中提供的支持。

随着我们进行平台移植工作，我们还需要关注 MBX 平台包中包含的包。这些包可能也需要修改以支持新硬件。

# 步骤 1：让新平台被识别

平台移植的第一步是让配置工具识别我们的新硬件，这样我们就可以为新硬件构建软件了。

我们在 PowerPC HAL 目录下创建一个 `martini` 目录，因为我们的-硬件使用了 PowerPC MPC860T 处理器。

由于我们使用 MBX 平台作为基准，我们将 `hal\powerpc\mbx\current` 子目录复制到我们的新硬件子目录 `hal\powerpc\martini\current` 中。

> 注意：如果新硬件平台下的文件是只读的，将这些文件改为读/写会更方便，这样我们就可以进行适当修改。当使用光盘中的 Martini 示例时，文件被标记为只读。当将它们复制到工作目录时，请确保根据需要标记为读/写。

接下来，我们需要将文件名从 MBX 平台更改为代表我们的 Martini 平台。表 13.1 显示了 Martini 包所需的文件名更改示例，这些更改适用于新子目录 `hal\powerpc\martini\current` 中的文件。表 13.1 中也给出了文件的子目录位置。

# HAL 移植文件名更改

| MBX 平台文件名 | Martini 平台文件名 |
|---|---|
| `hal_powerpc_mbx.cdl` | `hal_powerpc_martini.cdl` |
| Subdirectory `include\pkgconf` |  |
| `mlt_powerpc_mbx_ram.h` | `mlt_powerpc_martini_ram.h` |
| `mlt_powerpc_mbx_ram.ldi` | `mlt_powerpc_martini_ram.ldi` |
| `mlt_powerpc_mbx_ram.mlt` | `mlt_powerpc_martini_ram.mlt` |
| `mlt_powerpc_mbx_rom.h` | `mlt_powerpc_martini_rom.h` |
| `mlt_powerpc_mbx_rom.ldi` | `mlt_powerpc_martini_rom.ldi` |
| `mlt_powerpc_mbx_ram.mlt` | `mlt_powerpc_martini_rom.mlt` |
| Subdirectory `src` |  |
| `mbx.s`^a | `martini.s`^a |

a 在这种情况下，汇编文件的扩展名为大写的 "S" 而不是小写的 "s" 是关重要的。大写的"S"允许 GNU C 编译器对汇编文件进行预处理。

# 平台移植示例

现在，我们需要修改新的 CDL 脚本文件 `hal_powerpc_martini.cdl`（位于 `hal\powerpc\martini\current\cdl` 子目录下），以反映我们的 Martini 平台。Martini 硬件平台所需的修改包括由我们的新 Martini 平台替换 MBX 箱，这可以通过查找和替换完成。

代码列表 13.1 显示了为新的 Martini 包所做的更改示例。Martini 平台的文件 `hal_powerpc_martini.cdl`：

```
packagePGK_HAL_POWERPC_MARTINI (
2      display "Martini board"
3      parent hal_powerpc
4      requires MPC860
5      define_header hal_powerpc_martini.h
6      include_dir pkgconf

      description
        The MARTINI package provides the support
9        needed to run Ecos on a Martini board
10       equipped with a PowerPC processor.

     compile martini.S




)
```

如第 1 行，我们将包命令名称从 `CYPGK_HAL_MBX` 更改为 `CYPGK_HAL_MARTINI`。我们还更改了第 2 行的 CDL 显示。你可以为显示选择任何名称。第 3 行和第 4 行保持不变。第 5 行引用我们新的头文件 `hal_powerpc_martini.h`。在第 12 行，CDL 命令将 `mbx.S` 更改为 `martini.S`。

在两个源文件中存在我们需要为新平台更改的位置。第一个位于 `include` 子目录下的文件。。我们需要更改这一行：

```
#include <pkgconf/hal_powerpc_mbx.h>
```

```
#include <pkgconf/hal_powerpc_martini.h>
```

我们需要对 `src` 目录下的 `martini.S` 文件执行相同的修改。在进行修改期间，使用 `grep` 工具查找 `mbx` 字符串可能会很有帮助。

> 注意：如果使用不同的 HAL 平台作为基准，你可能会发现各种源文件需要额外的修改。

接下来，我们需要让配置工具识别我们的 Martini 平台。为了实现这一，我们将新平台包添加到 `packages` 子目录下的 `ecos.db` 文件中。

> 注意：在编辑文件之前，备份原始 `ecos.db` 文件是一个好习惯，以防你需要引用它或恢复原始文件。

正如我们在第 11 章“Ecos Toolkit”中所，`ecos.db` 使用 CDL 并包含了组件框架中所有包的高级描述。列表 13.2 显示了为了让配置工具识别我们的 Martini 平台而在 `ecos.db` 文件中添加的 CDL 描述。

```
package CYPGK_HAL_POWERPC_MARTINI {
  alias "Martini board" hal_powerpc martini_powerpc_martini
  directory hal/powerpc/martini
  script hal/powerpc_martini.cdl
  description
    The MARTINI HAL package provides the support
    needed to run Ecos on a Martini board
    equipped with a PowerPC processor.
}
target martini {
  alias "Martini board" martini860
  packages CYPGK_HAL_POWERPC
}
```

# 迁移示例

- 17 `CYPGKG_HAL_POWERPC_MPC8xx`

- 18 `CYPGKG_HAL_POWERPC_MARTINI`

- 19 `CYPGKG_HAL_QUICC`

- 20 `CYPGKG_IO_SERIAL_POWERPC_QUICC_SMC`

- 21 `CYPGKG_DEVS_ETH_POWERPC_QUICC`

- 22 `CYPGKG_DEVS_FLASH_MBX`

- 23

- 24 `CYPGKG_DEVS_FLASH_AM29XXXXX`

Martini 目标提供了在 Martini 板卡上运行 Eco 所需的软件包。

## 代码行 13.2 ecos 仓库文件，ecos.db，针对 Martini 平台的更改。
