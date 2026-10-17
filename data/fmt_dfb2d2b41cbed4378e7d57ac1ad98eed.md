
打开生成的反汇编文件，查找 `main` 函数。而不是直接调用 `printf` 的地址，有一个调用名为 `printf@plt` 符号的调用：

```asm
00048348 <main>:
...
80483f5: e8 06 ff ff ff    call  8048306 <printf@plt>
80483fa: 68 00 00 00 00    mov $0x0, %eax
```

转到该偏移量，即 `0048300`。你可以清楚地看到有一个跳入 GOT。`push $0x0` 将设置 `printf` 的实际地址，进入第一个可用于共享符号的 GOT 条目，即 `GOT[3]`：

![](img/628186dda7facdc011bf39c938de3975_33_0.png)

```asm
00048300 <printf@plt>:
8048300: ff 25 98 94 04 08  jmp    *0x0894998
8048306: 68 00 00 00 00    push $0x0
804830b: e9 e0 ff ff ff    jmp    80482f0 <.init+0x34>
```

在 `gdb` 会话中运行可执行文件以分析 GOT。因为 `_got.plt` 表是这个 ELF 二进制文件中的一个段，你可以向 `gdb` 询问其确切地址：

```bash
$ gdb ./relro
(gdb) info sections _got.plt
0x089495c >0x0894964  0x0000068 _got.plt
ALLOC LOAD DATA HAS CONTENTS
```

在调用 `printf@plt` 函数后立即设置断点并运行程序：

```bash
(gdb) b *0x00483fa
Breakpoint 1 at 0x00483fa
(gdb) r
Hello there!
Breakpoint 1, 0x00483fa in main ()
```

让我们找出 `printf` 函数位于何处：

```bash
(gdb) p system
$3 = <text variable, no debug info> 0x7f7e82c80
```

因此 `GOT[3]` 必须有地址 `0x7f7e82c80`，这是 `printf` 的地址。为了确定这是真的，转储 `_got.plt` 表的前 4 个字节：

```bash
(gdb) x/4w 0x089495c
0x089495c <_GLOBAL_OFFSET_TABLE_>   0x0894958
0x7fff0598      0x7fff3598
```

因为这是 ELF 二进制文件中的可写地址，你可以在 `GOT[3]` 中放入任何你想要的地址。你可以通过进行指针算术来找出哪个地址等于 `GOT[3]`：

```bash
(gdb) x/4w 0x089495c+12
0x0894968 <printf@plt>          0x7f7e82c80
```

因此 `GOT[3]` 位于 `0x0894968`！让我们玩玩 GOT，你的目标将是执行 `system` 函数，而不是 "Hello world!" 消息。为此，首先找出 `system` 的地址在哪里：

```bash
(gdb) p system
$8 = <text variable, no debug info> 0x7f74c90
```

在调用 `printf@plt` 符号之前设置断点：

```bash
(gdb) b *0x00483f5
Breakpoint 2 at 0x00483f5
```

从头开始运行程序，直到它在 `0x80483f5` 处中断。然后，用 `system` 函数的地址覆盖偏移地址 `0x804968` 处的 GOT 条目（更正 OCR 错误 `0x8049698`）：

```bash
(gdb) set *0x804968 = system
(gdb) x/wx 0x804968
0x804968 <printf@plt+...>    0x7f74c90
```

在 `gdb` 中使用“`c`”命令继续执行：

```bash
(gdb) c
Continuing.
sh: Hello: command not found
```

你已成功将 GOT 条目中 `printf` 函数的地址覆盖为 `system`。但由于 `system` 期望从堆栈中获取要执行的命令，而堆栈中有字符串 "Hello world!\n"，`system` 试图执行 "Hello" 并失败！无论如何，你已修改了 GOT 表。为了防止这种情况，请使用完整 RELRO：

```bash
$ gcc -m32 -fno-builtin-printf -Wl,-z,relro,-z,now relro.c -o relro
```

现在，由于所有符号在链接器将控制权返回给可执行程序之前都已解析，因此不再需要将可写段加载到内存中。要检查这一点，使用 `readelf` 命令如下：

```bash
$ readelf -S ./relro | grep "got.plt"
```

## 审计未加强的二进制文件

在现代 GNU/Linux 发行版中，大多数二进制文件都预先编译启用了这些防护。要检查，你可以使用 `readelf` 工具或 `checksec` 脚本。

```bash
$ wget http://www.trapkit.de/tools/checksec.sh
```

使用 `checksec`，让我们测试之前编译代码在启用完整 RELRO 后的防护：

```bash
$ ./checksec.sh -file relro
Full RELRO    No canary found    NX enabled
No PIE
```

`checksec` 向你报告该二进制文件已使用完整 RELRO 和 NX 位进行强化。然而，其 `.text` 段未受 ASLR 保护，且没有堆栈破坏保护。

```bash
$ gcc -m32 -fstack-protector-all -fPIE -pie -fno-builtin-printf -Wl,-z,relro,-z,now relro.c -o relro
$ ./checksec.sh -file relro
Full RELRO    Canary found    NX enabled
PIE enabled
```

`checksec` 还允许你使用 `--proc-all` 标志检查系统中运行的每个进程并获取其防护。要获取可能容易受到堆栈破坏或 GOT 覆盖攻击影响的二进制文件列表，你可以运行以下内容：

```bash
# ./checksec.sh --proc-all | egrep 'No RELRO|No canary'
init          1 No RELRO    No canary found    NX enabled No PIE
rpc.statd 2426 No RELRO No canary found NX enabled No PIE
rpc.idmapd 2440 No RELRO No canary found NX enabled No PIE
...
```

然而，重要的是要注意，如果你在新的 GNU/Linux 发行版中编译遗留代码，很有可能它会在没有防护的情况下被构建。

> `checksec` 允许你检查系统中运行的每个进程并获取其防护

```bash
$ wget http://disbaux.es/wp-content/uploads/2012/10/xmgr-4.1.2.tar.bz2
```

解压缩文件并按常规启动构建过程：

```bash
$ tar xvjf xmgr-4.1.2.tar.bz2
$ cd xmgr-4.1.2/
$ ./configure && make
```

使用 `checksec` 脚本确保唯一启用的防护是 NX：

```bash
$ checksec.sh -file src/xmgr
No RELRO    No canary found    NX enabled    No PIE
```

通过修改其 `Makefile` 以设置适当的标志来强化它。现代 GNU/Linux 发行版包含一个自动开启这些标志的环境变量。编辑 `xmgr-4.1.2/Make.conf` 并将这些标志设置为 `CFLAGS0` 变量：

```makefile
CFLAGS0 = -fstack-protector-all -fPIE -pie -Wl,-z,relro,-z,now
```

也将 `-fPIC` 标志添加到 `cephos` 库中：

```makefile
# vi cephos/Makefile
...
CFLAGS= $(CFLAGS0) -fPIC -I$TOP -I.
```

现在重新编译二进制文件并再次检查其防护：

```bash
$ make clean
$ make
$ checksec.sh -file src/xmgr
Full RELRO    Canary found    NX enabled    PIE enabled.
```
