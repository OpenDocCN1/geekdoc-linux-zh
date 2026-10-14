
```
$ python.py -f injartarget.lime --profile=LinuxDebian3_286 linux_malfind

Volatility Foundation Framework 2.4

Process: Target PID: 1629 Address: 0x110000 File: Anonymous Mapping

Protection: VM_READ|VM_WRITE|VM_EXEC

Flags: VM_READ|VM_WRITE|VM_EXEC

0x010100 31c0
0x010101 01 c3 31 d1 39 d2 86 63 01 56 04 06 6a 1.1.1..Qj.j
0x010102 01 6a 02 89 e1 cd 80 89 c6 b6 80 52 52 56 68 zifs..j.....f
0x010103 7a 69 66 53 89 e1 cd 6a 10 56 51 58 89 e1 cd 80 66 80 .j..V.RRV
0x010104 03 6a 04 01 56 89 e1 cd 80 66 83 05 52 52 56

0x010100 31c0 XOR EAX, EAX
0x010102 31db8 XOR EBX, EBX
0x010104 31c9 XOR ECX, ECX
0x010105 31d2 XOR EDX, EDX
0x010106 b066 MOV AL, 0x66
0x01010a b301 MOV BL, 01
0x01010c 51 PUSH ECX
0x01010d 6a06 PUSH EBX
0x01010f 6a01 PUSH 01
0x010111 6a02 PUSH 02
0x010113 89e1 MOV ECX, ESP
0x010115 cd80 INT 0x80
0x010117 89c6 MOV ESI, EAX
0x010119 b066 MOV AL, 0x66
0x01011b b302 MOV BL, 02
0x01011d 52 PUSH EDX
0x01011e 66687a69 PUSH WORD 0x697a
```

如输出所示，目标进程（PID 16929）在地址 0x10110000 处有一个可读、可写且可执行的内存区域。`mmap` shellcode 初始分配了该区域。你也可以使用 `linux_netstat` 查看 shellcode 成功创建的后门套字：

```
$ python vol.py -f target.lime --profile=LinuxDebian3_x86 linux_netstat -p 16929

Volatility Foundation Volatility Framework 2.4
TCP 0.0.0.0:31337 0.0.0.0 LISTEN target/16929
```

在调查中，你现在可以开始研究 shellcode 的反汇编，以确定它为攻击者提供了哪些功能。

## 进程空（Process Hollowing）

进程空是用恶意代码覆盖内存中的进程或进程部分。攻击者经常使用进程空在列出合法进程状态的系统工具中隐藏恶意软件的存在。此外，内核数据结构将报告原始进程二进制文件的路径（例如 `/usr/bin/apache2`），而不是恶意软件文件。这种不匹配会导致防病毒软件和其他主机保护工具扫描磁盘上的无辜文件而忽略恶意软件。在 Windows 上，著名的恶意软件样本如 Stuxnet 曾使用进程空来逃避检测。

## 检测算法

进程空检测依赖于拥有一个良好的指令副本与内存中的指令进行对比。虽然你可以信任内核的文件缓存，但所需的文件可能是不完整的（由于交换引起）。此外，你不能信任受损系统上的文件。由于这些问题，Volatility 依赖于来自基线镜像（或安装包）的文件副本。因此，只要你有获取可能受感染文件的可信副本，就可以使用 `linux_process_hollow` 插件来执行检查。该插件需要：

- 可信二进制文件的路径
- PID (s)
- 应用程序映射到内存的地址

插件通过读取可信文件的符号表开始，并将每个函数与内存中的实际代码进行比较。除了直接重定位（不使用 GOT/PLT 地址）的情况外，应用程序的代码不应该改变。目前的实现一次只操作一个进程。但请记住 Volatility 是开源且可扩展的。你可以更新代码，使其与加载的进程、共享库和内核模块对应的文件进行自动对比。

## 检测示例

以下场景涉及一个被恶意软件感染的系统，该软件执行了进程空（以及库注入，我们将在下一节中讨论）。目标进程是 `bash` 的实例，其 PID 为 18550，如第一个命令所示：

```
$ python vol.py -f shared.lime --profile=LinuxDebian3_286 linux_pid | grep bash

Volatility Foundation Volatility Framework 2.4

Offset Name Uid Gid Start
0x7f6164 bash 18550 0 0x3acd00 24-25
```

下一个命令确定了 ELF 文件在进程内存中的加载地址。根据输出，可执行区域 (r-x) 从 0xb400 开始。你也可以看到磁盘上的路径 (`/bin/bash`)。

```
$ python vol.py -f shared.lime --profile=LinuxDebian3_286 linux_maps -p 18550 | grep bash

Volatility Foundation Volatility Framework 2.4

Pid Start End Flags Go Inode Path
18550 0x80400 0x80400 r-x 0x0 1 /bin/bash
18550 0x804900 0x80a00 rw- 0x0 1 /bin/bash
```

然后我们将这些信息传递给 `linux_process_hollow`，并提供可执行文件的可信副本路径 (`/mnt/sharedlib/bin/bash`)。插件报告主函数已被更改：

```
$ python vol.py -sharedlib.lib --profile=LinuxDebian3_286 linux_process --p 18550 -b 0x80400 -P /mnt/sharedlib/bin/bash

Volatility Foundation Volatility Framework 2.4

Task PID Symbol Address
bash 18550 name 0x8045bc
```

如果我们使用 `linux_volshell` 调查该地址，会发现一段指令和一个对 `/tmp/.XICE` 的字符串引用：

```
$ python vol.py -sharedlib.lib --profile=LinuxDebian3_286 linux_volshell

Volatility Foundation Volatility Framework 2.4

Current context: process init, pid=1 DTB=0x370bf00
Welcome to volshell!
To get help, type 'hh('
>> cc(pid=18550)
Current context: process bash, pid=18550 DTB=0x35acd00
>> db(0x8045bc, 48)
0x8045bc eb17 57 58 09 24 c7 44 24 04 01 00 00 00 bb 00 e0
0x8045cc 3a 75 57 ff d3 83 04 c4 cc e4 e8 ef ff ff 22 7f 74
0x8045dc 6d 70 2f 2e 58 49 43 45 27 2e 6e 78 00 00 00 mp./XICE-unix-....
>> di(0x8045bc)
0x8045bc eb17 JMP 0x804d5
```
