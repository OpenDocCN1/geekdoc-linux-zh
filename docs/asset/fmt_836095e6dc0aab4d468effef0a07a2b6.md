
# 虚拟机内存取证

## 104 第一部分：内存取证简介

为了完全匹配，Sebastian Bourne-Rich 最近注意到 VMware 产品通常会创建一个 `.vmem` 和一个结构化文件（分割架构/split schema）。Volatility 需要编写一个全新的空间来支持这种架构，因为 `.vmem` 包含物理内存，但元数据指示了如何重新选取这些内容，以创建客机内存的准确表示。换句话说，当从 VMware 系统获取数据时，请确保恢复所有带有 `.vmem`、`.vmms` 和 `.vmss` 扩展的文件——因为在其中一个（或多个文件包含所需的证据之前，恢复是非常困难的。

在元数据文件的偏移处，你将找到一个类似于所示的 `_VMWARE_HEADER` 结构：

```
>>> dt(_VMWARE_HEADER)
'_VMWARE_HEADER' (12 bytes)
0x0    Magic               ['unsigned int']
0x8    GroupCount          ['unsigned int']
0xc    Groups              ['array', lambda x :x.GroupCount, '_VMWARE_GROUP']
```

为了使文件有效，`Magic` 值必须为 `0xbed2bed0`、`0xbad1bed2` 或 `0xbed3bed3`。这些成员指定了一个 `_VMWARE_GROUP` 结构数组，其如下所示：

```
>>> dt(_VMWARE_GROUP)
'_VMWARE_GROUP' (80 bytes)
0x0    Name                ['String', 'length': 64, 'encoding': 'utf8']
0x40   TagsOffset          ['unsigned long long']
```

每个组都有一个 `Name`，允许对元数据组件进行分类，以及一个 `TagsOffset`，它指定了你可以在哪里找到 `_VMA_TAG` 结构列表。一个标签看起来如下所示：

```
>>> dt(*VMWARE_TAG)
  _VMWARE_TAG * (None bytes)
0x0 : Flags [unsigned char]
0x1 : NameLength [unsigned char]
0x2 : Name 'String',
  {'length': lambda x: x.NameLength, 'encoding': 'utf-8'}
```

这些标签是在元数据文件中寻找物理内存数据的关键。如果虚拟机的 RAM 超过 4GB，单次物理内存运行存储在一个名为 `"memory"` 的组和一个名为 `"Memory"` 的标签中。对于 RAM 超过 4GB 的系统，会有多个运行记录，它们同样位于名为 `"memory"` 的组中，但包含了名为 `"Memory"`、`regionPPN`、`regionpageNum` 和 `regionSize` 的标签。Volatility 内的地址空间（参见 `volatility/plugins/addrspaces/vmware.py`）解析这些标签以重建物理内存视图。

### VirtualBox

当你挂起或暂停虚拟机时，VirtualBox 不会自动将全 RAM 保存到磁盘（与其他虚拟化产品不同）。相反，你必须使用以下技术之一创建内存转储：

- `vboxmanage` 命令。这种方法创建一个带有自定义段的 ELF64 核心转储二进制文件，其中这些段代表客机物理内存。有关更多信息，请参阅 http://www.virtualbox.org/manual/ch08.html#vboxmanage-debugvm
- 在启动虚拟机时使用 `--dbg` 切换，然后使用 `.pgmffile` 命令。这种方法输出原始内存转储。更多信息，请参阅 https://www.virtualbox.org/ticket/10222。
- 使用 VirtualBox API（`vboxapi`）创建你自己的内存转储工具。我还在上述工单 `#10222` 中附带了一个名为 `vboxdump.py` 的 Python 脚本，展示了示例。

第二和第三种方法产生原始内存转储，Volatility 原生支持。然而，第一种方法生成 ELF64 核心转储，需要特殊支持。Philippe Teeuwen（参见 http://www.yobi.be/wiki/RAM_analysis）对这种格式进行了初步分析，并创建了支持这些格式的 Volatility 地址空间。因此，Cuckoo Sandbox 能够集成了以 ELF64 核心转储格式保存 VirtualBox 虚拟机内存转储的能力。

ELF64 文件有几个自定义程序头段。其中之一是 `PT_NOTE`（`elf64_note`），其名称为 `VCORE`。该标记段包含一个 `DBGFOREDESCRIPTOR` 结构，如下所示所示：

```
>>> dt*(DBGFOREDESCRIPTOR)
'DBGFOREDESCRIPTOR' (24 bytes)
0x0			u32Magic		['unsigned int']
0x4			u32FmVersion		['unsigned int']
0x8			u32Self		['unsigned int']
0xC			u32Version		['unsigned int']
0x10			u32Revision		['unsigned int']
0x14			u32CPUs		['unsigned int']
```

该结构包含了 VMware magic、版本和 CPU 数量。如果你想遍历 ELF64 头（`elf64_phdr`），`p_addr` 是起始地址。`p_offset` 成员告诉你内存的位置。最后，`p_sz` 告诉你块的大小。

### 注意事项

关于 VirtualBox ELF64 转储的更多信息，请查看：

- ELF64 格式：http://virtualbox.org/ch12
- VirtualBox 源码：http://virtualbox.org/trunk/include/vmm.h
- 创建转储的 C++ 代码：http://virtualbox.org/trunk/src

### QEMU

QEMU 与 VirtualBox 非常相似，以 ELF64 格式保存内存。事实上，主要的区别在于 `PT_NOTE` 名称是 `CORE` 而不是 `VCORE`。你可以使用 `virsh` 创建这些转储，它是 `libvirt`（http://libvirt.org/）的命令行界面。这里还有一个 Python API，Cuckoo Sandbox（http://www.cuckoosbox.org/）目前使用它来创建 QEMU 的转储。

## 105 内存获取

### Xen/KVM

LibVMI 项目（https://github.com/bdpayne/libvmi）是一个支持 Xen 和 KVM 虚拟机管理器的虚拟机入侵库。换句话说，你可以在不执行虚拟机内部代码的情况下对运行中的虚拟机进行分析。这是一种强大的能力。作为额外奖励，该项目包含一个 Python API（`pyvmi`）和 Volatility 地址空间（`pyVmSpace`）。

### Microsoft Hyper-V

要从 Hyper-V 获取内存，你首先需要在虚拟机目录下保存 `.bin`（物理块）和 `.vsv`（元数据）文件。遗憾的是，Volatility 目前不支持 Hyper-V 格式，因此你需要使用 `vm2dump.exe` 工具（http://archive.msdn.microsoft.com/vm2dump）将 `.bin` 和 `.vsv` 文件转换为转储。然后可以使用 WinDbg 或 Volatility 进行分析。有关此过程的更多信息，请参考 Wyatt Roersma 的《Analyzing Hyper-V Saved Files》（http://www.wyattroersma.com/?p=77）。Wyatt 的主要观察之一是，`vm2dump.exe` 在内存超过 4GB 的虚拟机上失效。

> 注意事项
>
> 你也可以使用 Sysinternals LiveKD 或 Monsools LiveKD（http://monsools.com/2010/08/12）从运行中的 Hyper-V 获取内存。
