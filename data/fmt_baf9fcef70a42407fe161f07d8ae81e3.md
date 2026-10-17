
```
* Code maturity level options
  * Prompt for development and/or incomplete code/drivers (CONFIG_EXPERIMENTAL)
[Y/n/?]
```

在此示例中，询问你是否希望被提示开发和/或不完整的代码/驱动程序。你有以下选项：`Y` 表示是，现在的默认值；`n` 表示否；`?` 表示该选项的帮助。

### 6. 通过回答问题继续配置内核

完成后，通过按正确顺序执行几个命令继续编译内核。你可以一个一个输入，也可以将它们全部放在一行中用分号 (`;`) 分隔，然后等待完成。正确的顺序命令如下：

- `make dep`—此命令检查你是否拥有编译内核所需的所有文件。
- `make clean`—此命令删除之前编译的所有痕迹，这会减慢编译过程，但能确保基于 solely 你的配置的干净内核。
- `make bzImage`—此命令编译实际的内核。
- `make bzlilo`—此命令将内核安装为默认内核。请谨慎使用！如果你不确定是否要安装此内核，不要运行它。继续阅读以了解如何为测试目的安装新内核。
- `make modules`—如果你有一些组件是模块，则需要运行此命令来编译它们。
- `make modules_install`—如果你有模块，运行此命令来安装它们。

或者作为一行命令，输入以下命令：

```
root@linux:/usr/src/linux > make dep; make clean; make bzImage; make bzlilo;
make modules; make modules_install
```

现在可能是你去倒杯咖啡的好时机，因为这是一个漫长的过程。根据你的硬件配置，可能需要七分钟到一个多小时。当它完成时，如果你已执行 `make bzlilo` 命令，则需要重新启动才能加载新内核。否则，继续阅读以了解如何在将其作为默认安装之前测试新内核。

## Testing a Kernel Before Installing It

这是一个重要问题，因为如果你不确定新内核是否能正确启动，就没有必要在未先测试的情况下将其安装为默认内核！这实际上是一个简单的过程。不要执行 `make bzlilo` 步骤，而是将其替换为 `make bzdisk` 并确保你的 A: 驱动器中有软盘。

这将把内核安装到磁盘上以便你可以测试它。重新启动计算机，它将从该磁盘启动。如果一切顺利且内核运行正常，你可以通过运行 `make bzlilo` 来安装它。如果出现问题，取出磁盘并重新启动计算机以启动旧内核。

但如果没有磁盘驱动器怎么办？没问题——你可以配置 `LILO` 以启动多个内核。跳过 `make bzlilo` 步骤并使用 `YaST` 设置 `LILO` 以具有加载测试内核的选项。以 root 身份运行 `YaST`：

```
root@linux:/ > yast
```

接下来，从菜单中选择 `System Administration`, `Kernel and Boot Configuration`, `LILO Configuration`。或者，要直接进入 `LILO` 配置，可以这样运行 `YaST`：

```
root@linux:~> yast --mask lilo
```

现在你准备好配置 `LILO` 了（见 Figure 8.9）。按照以下步骤操作：

FIGURE 8.9

使用 `YaST` 配置 `LILO` 非常容易。

![](img/659f91d9da7b29976c0625e2e9628511_199_0.png)

- 1. 你需要做的第一件事是为测试内核创建新的配置。按 `F4`。
- 2. 对于配置名称，输入 `test` 并按 `Tab` 移动到下一个字段。
- 3. 选择 `Boot Linux` 作为 `Which Operating System` 选项。`YaST` 然后应自动在 `(Root) Partition to Boot` 选项中填入正确的分区；只需检查以确保。
- 4. 对于 `Kernel to be Booted by LILO Option`，按 `F3` 以获取文件选择框。
- 5. 浏览到 `/usr/src/linux/arch/i386/boot/` 并选择 `bzImage`（见 Figure 8.10）。

FIGURE 8.10

选择要启动的内核。

![](img/659f91d9da7b29976c0625e2e9628511_199_1.png)

- 6. 保存并退出。
- 7. 你现在应该有一个名为 `test` 的新条目。按 `Enter` 保存 `LILO` 配置并退出。

现在你可以测试你的新内核了。重新启动计算机，并在 `LILO` 提示符下输入单词 `test`。这将加载你的新内核。如果一切正常，运行 `make bzImage` 命令将新内核安装为默认内核。否则，重新启动并像往常一样加载 Linux 以恢复到之前的内核。

## 了解各种重要的配置参数

现在你已经知道如何编译内核，让我们来看看可用的配置参数。熟悉最常见的参数将会非常有帮助。

### 代码成熟度级别选项

内核的某些部分仍在开发中；因此，它们还不够稳定供所有人使用。这甚至在稳定内核中也会发生。开发人员喜欢鼓励测试，所以如果你想查看仍在开发中因此不完全稳定的那些选项和驱动程序，你应该对该选项说 yes。说 no 会使它们不可见。大多数人这里选择 no，但如果你真的想要一个仍处于实验阶段的特定驱动程序，那么说 yes 以便能够选择它。但要小心，它可能无法按预期工作——这就是为什么它被称为实验性的。

### 处理器类型和特性

这里是你为处理器选择参数的地方：

| Option | Description |
|---|---|
| Processor Family: | 这里你会看到支持的各种处理器家族列表，例如 386、486/Cx486、Pentium 等等。如果你拥有 Pentium II 或更高版本，你应该选择 Ppro/6x86MX 选项。 |
| Maximum Physical Memory: | 此选项使你能够设置系统的最大内存大小。你可以将其设置为 1GB 或 2GB 的 RAM。 |
| Math Emulation | 如果你的处理器没有数学协处理器，你可以让内核为你模拟一个。所有 486 DX 及以上的处理器都有数学协处理器，因此你可能不需要内核模拟。 |
| MTRR (Memory Type Range Register) Support | 此功能仅适用于 P-II 和 AMD-K6-2 Stepping 8 及以上。这些是特殊的寄存器，可能用于控制处理器对内存范围的访问。如果你拥有 PCI/AGP VGA 卡，这非常有用。通过启用此选项并配置 X-Windows 使用它，你可以将图形速度提高 2.5 倍。如果你处理器支持此功能，请启用它。 |
| Symmetric Multi-processing Support | 如果你的机器中有多个 CPU，启用此选项以使内核使用所有可用处理器。 |

### 可加载模块支持

可加载模块是内核的一部分，但不是内置在内核中；它作为单独的对象构建，并在需要时加载。模块在效率方面非常出色，因为它们使内核的大小变小。模块使设备驱动程序能够在加载时动态配置，而无需重新编译整个内核来重新配置其中一个设备驱动程序。

这里是你选择模块支持的地方：

| Option | Description |
|---|---|
| Enable Loadable Modules Support | 要启用模块的使用，请说 Y。此选项是推荐的。 |
| Set Version Information on All Symbols for Modules | 如果你在这里说 Yes，模块将随内核版本一起构建。这样模块必须与内核版本匹配才能被加载。说 No 会放宽此限制，但在模块为特定内核版本设计的情况下可能不太安全。这里说 No 是安全的。 |
| Kernel Modules Loader | 启用此功能将按需自动加载模块。禁用此功能将导致模块手动加载。这里选择 Yes 是个不错的选择。 |

### 通用设置

本节包括适用于大多数机器的常见选项。让我们来看一些重要选项：

| Option | Description |
|---|---|
| Networking Support | 即使你没有网络，也应该在这里说 Yes。一些程序即使在独立机器上运行也需要使用网络服务。只有在你真的知道自己在做什么时才说 No。 |
| PCI Support | 如果你有 PCI 总线，请说 Yes。 |
| System V IPC | IPC 代表进程间通信。此选项非常重要，因为许多程序都使用 System V IPC 进行通信。请说 Yes。 |
| Kernel Support for a.out Binaries | a.out 是可执行文件的旧格式。它已被新的 ELF 格式取代。你最好将 a.out 的支持作为模块构建，因为你不太可能在日常使用中需要它。 |
| Kernel Support for ELF Binaries | 在这里说 Yes。这非常重要，因为所有程序现在都是 ELF 格式。 |
