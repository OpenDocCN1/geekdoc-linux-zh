
列表 10.3，μC/OS 和 μC/OS-II 数据类型

μC/OS 的处理器特定代码（即端口）被放在文件名包含处理器名称的文件中。例如，Intel 80x86 实模式模型具有名为 `Ix86L.H`、`Ix86L_C.C` 和 `Ix86L_A.ASM` 的文件。表 10.1 显示了文件名称与旧名称的对应关系。

*(注：`OS_CPU.H`、`OS_CPU.C` 和可选的 `OS_CPU_A.ASM` 处已根据原文意图调整翻译)*

重新对应表 10.1

| `\SOFTWARE\uCOS\Ix86L` | `\SOFTWARE\uCOS-II\Ix86L` |
| --- | --- |
| `Ix86L.H` | `OS_CPU.H` |
| `Ix86L_A.ASM` | `OS_CPU_A.ASM` |
| `Ix86L_C.C` | `OS_CPU.C` |

作为起点，你必须将旧文件名（μC/OS 目录）复制到等效 μC/OS-II 目录中的名称。修改这些文件以从头创建它们是很容易的。表 10.2 显示了几个 μC/OS 端口文件的翻译示例。

| `\SOFTWARE\uCOS\I80251` | `\SOFTWARE\uCOS-II\I80251` |
| --- | --- |
| `I80251.H` | `OS_CPU.H` |
| `I80251.C` | `OS_CPU.C` |

| `\SOFTWARE\uCOS\M680x0` | `\SOFTWARE\uCOS-II\M680x0` |
| --- | --- |
| `M680x0.H` | `OS_CPU.H` |
| `M680x0.C` | `OS_CPU.C` |

| `\SOFTWARE\uCos\M68HC11` | `\SOFTWARE\uCos-II\M68HC11` |
| `M68HC11.H` | `OS_CPU.H` |
| `M68HC11.C` | `OS_CPU.C` |

| `\SOFTWARE\uCos\Z280` | `\SOFTWARE\uCos-II\Z280` |
| `Z80.H` | `OS_CPU.H` |
| `Z80_A.ASM` | `OS_CPU_A.ASM` |
| `Z80_C.C` | `OS_CPU.C` |

表 10.2，从 µC/OS 到 µC/OS-II 的文件重命名

μC/OS 的处理器特定代码（即端口）被放在文件名包含处理器名称的文件中。例如，Intel 80x86 实模式模型具有名为 `Ix86L.H`、`Ix86L_C.C` 和 `Ix86L_A.ASM` 的文件。表 10.1 显示了文件名称与旧名称的对应关系。
