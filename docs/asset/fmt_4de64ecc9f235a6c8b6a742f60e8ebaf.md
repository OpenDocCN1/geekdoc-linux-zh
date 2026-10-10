
| GPFUD0 | 0 | | (31-24) 映射到 GPIO31 (若 GPFUD0=1 电平为低) | 仅读 |

| GPFUD1 | 4 | | (23-16) 映射到 GPIO23 (若 GPFUD1=1 电平为低) | 仅读 |

| 寄存器 | 偏移量 | | | 功能 |

|---|---|---|---|---|

| GPFUDCK0 | 0 | | (31-24) 映射到 GPIO31 (若 clock=1) + 无影响 | |

| GPFUDCK1 | 4 | | (23-16) 映射到 GPIO23 (若 clock=1) + 无影响 | |

| 寄存器 | 偏移量 | | | 功能 | PUD |

|---|---|---|---|---|---|

| ALT0 | 0 | | | | 00 上拉/下拉 |

| ALT1 | 4 | | | | 01 下拉 |

| ALT2 | 8 | | | | 10 上拉 |

| ALT3 | 12 | | | | 11 |

| | | | | | | | | | |

|---|---|---|---|---|---|---|---|---|

| | (31-24) | | | [24] | [23] | [22] | [21] | [20] | |

| | | | | ? | ? | ? | ? | |

| | 不要使用 | | | | | | | | |

图-6：用于内存映射 GPIO 操作的可用寄存器示例

注意差值是 `0x20000`，在二进制中为 `10000000000000000000`（即 17 个 0，或 `1<<17`）。`GPIO17` 位于第一个地址库中。对于 `GPIO32` 到 `GPIO53`，你需要读取 `GPVL1` 寄存器。上面的输出表示这是 `GPVL0` 寄存器第一次禁用，以及第六次禁用。

你可以使用 `devmem2` 程序通过设置 `GPCLR (0x02)` 寄存器上的第 17 位来关闭 LED，通过设置 `GPFSET0 (0x1c)` 寄存器上的第 17 位来开启 LED：

```
pi@pi /sys/class/gpio/gpio17 $ cat value
1
pi@pi /sys/class/gpio/gpio17 $ sudo -devmem2 0x3F200028 0x20000
/dev/mem. 内存映射到地址 0x7F677000.
地址 0x3F200028 (0x7F677028) 的值: 0x67706f
写入 0x20000，回读 0x67706f
pi@pi /sys/class/gpio/gpio17 $ sudo -devmem2 0x3F20001c 0x20000
/dev/mem. 内存映射到地址 0x7F677000.
地址 0x3F20001c (0x7F67701c) 的值: 0x67706f
写入 0x20000；回读 0x67706f
pi@pi /sys/class/gpio/gpio17 $ cat value
1
```

你可以看到这些位对 `gpio17` 的 `sysfs` 值有直接影响。注意还有其他寄存器用于设置和检测事件（例如下降/上升沿）。请参见 BCM2835 文档表 6-1。

## 使用 C 和 devmem 控制 GPIO

图 6-14 提供了配置引脚模式的细节和示例。所有 GPIO 都可以设置为输入或输出模式，如图 6-14 左下所示。

## C/C++ 中的位操作

本节使用位运算高效地操作内存。为了确保你熟悉这些操作，完整的示例位于 `chapter6/bits/Test.cpp`。`uint8_t`（无符号 8 位整数）类型和 `display()` 函数用于创建一个简洁的示例：

```cpp
#include <iostream>
#include <sstream>
#include <bitset>
#include <iomanip>

string display(uint8_t a) {
    stringstream ss; // 设置宽度并将位设为二进制
    ss << setw(3) << (int)a << " " << bitset<8>(a);
    return ss.str();
}

int main() {
    uint8_t a = 25, b = 5; // 无符号范围为 0 到 255
    cout << "A = " << display(a) << " and B = " << display(b) << endl;
    cout << "A & B " << display(a & b) << endl; // 与运算
    cout << "A | B " << display(a | b) << endl; // 或运算
    cout << "A ^ B " << display(a ^ b) << endl; // 异异运算
    cout << "A << 1 " << display(a << 1) << endl; // 左移
    cout << "B >> 1 " << display(b >> 1) << endl; // 右移
    cout << "1 << 8 " << display(1 << 8) << endl; // 左移！警告！
    return 0;
}
```

当此代码被编译并执行时，得到如下输出：

```
pi@pi ~/exploringpi6/bits ./bits
A is 25 (00011001) and B is 5 (00000101)
A & B is 1 (00000001)
A | B is 29 (00011101)
-A is 230 (11100110)
A ^ B is 28 (00011100)
A << 1 is 50 (00110010)
B >> 1 is 2 (00000010)
```

注意，位移 1 位（`(1<<1)`）导致结果 0（并产生编译器警告），因为发生了溢出，你可以使用数据类型的大小简化计算；此原理用于本章中的校验和（在列表 6-14 中）。

你应该写入 3 位模式的位置位于图 6-14 顶部。例如，为了将 `GPIO17` 设置为输出，你可以向 `FSEL17` 值写入 001，即 `GPIOSEL` 寄存器中的第 21、22 和 23 位。重要的是，你需要确保在更改 `FSEL17` 时只操作特定的 3 位，更改任何其他位都将影响 `GPIO10-GPIO19`，可能会改变它们的引脚。

列表 6-9 提供了一个代码示例，将 `GPIO17` 设置为输出并快速闪烁 LED（约 11.8 MHz）。它还将 `GPIO27` 设置为输入以控制 LED。代码列表中的命令描述了所使用的操作。

### 列表 6-9: chapter6/memoryGPIO/LEDflash.c
