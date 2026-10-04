
.text:00057F0 lea eax, (a_gen_tempname-1AF000h) [ebx]; "_gen_tempname" mov [esp+0ACH+var_A0], eax
.text:00057F96 mov eax, (a_SysdepsPosix-1AF000h) [ebx];
.text:00057FA9 lea eax, "../sysdeps/posix/temp.c"
.text:00057A00 mov [esp+0ACH+var_A8], eax
.text:00057A04 lea eax, (aInvalidKindIn-1AF000h) [ebx]; " \invalid \t> KIND in _gen_tempname"
.text:00057A0A mov [esp+0ACH+var_A4], 14Ah
.text:00057A12 mov [esp+0ACH+var_AC], eax
.text:00057A15 call assert_fail

```c
#include <stdio.h>

int global_variable=123;

int fi(int var)
{
    int rt=global_variable+var;
    printf("returning %d\n", rt);
    return rt;
}
```

我们在GCC 4.7.3下编译一下，然后使用IDA打开编译后的.so文件。

编译的命令行为：

```bash
gcc -fPIC -shared -O3 -o l.so l.c
```

# 指令清单67.2 GCC 4.7.3

```assembly
.text:0000040          public      x86_get_pc_thunk_bx
.text:0000040      x86_get_pc_thunk_bx proc near ; CODE XREF:
.init_proc+4
.text:0000040                               ;
.deregister_tm_clones+4    ...
.text:0000040              mov      ebx, [esp+0]
.text:00000443                      retn
.text:00000443      x86_get_pc_thunk_bx end
```

```assembly
.text:00000570          public      f1
.text:00000570      f1               proc near
.text:00000570
.text:00000570      var_1C      = dword ptr -1Ch
.text:00000570      var_18      = dword ptr -18h
.text:00000570      var_14      = dword ptr -14h
.text:00000570      var_8       = dword ptr -8
.text:00000570      var_4       = dword ptr -4
.text:00000570      arg_0       = dword ptr 4
```

```assembly
.text:00000573              sub      esp, 1Ch
.text:00000577              mov      [esp+1Ch+var_8], ebx
                              call     x86_get_pc_thunk_bx
.text:0000057C              add      ebx, 1A8h
.text:00000582                      [esp+1Ch+var_4], esi
.text:00000586              mov      eax, ds:(global_variable_ptr - 2000h) [ebx]
.text:0000058C              mov      esi, [eax]
.text:0000058E              lea      eax, (aReturningD - 2000h) [ebx]; "returning %d"
.text:00000594              mov      [esp+1Ch+arg_0]
.text:00000598              mov      [esp+1Ch+var_18], eax
.text:0000059C              mov      [esp+1Ch+var_1C], 1
.text:000005A3              mov      [esp+1Ch+var_14], esi
.text:000005A7              call     __printf
.text:000005AC              mov      esi, esi
.text:000005AE              mov      ebx, [esp+1Ch+var_8]
.text:000005B2              mov      esi, [esp+1Ch+var_4]
.text:000005B6              add      esp, 1Ch
.text:000005B9              ret
.text:000005B9      f1   end
```

上述代码的关键在于：每个函数在启动之前调整了字符串"returning %d"和global_variable的指针。x86_get_pc_thunk_bx 函数通过EBX返回指向自身的指针，而位于基偏移量0x570的指令再次对EBX进行了修正。这是一种获取PC指针（RIP）的通用方法。

常数0x1A84是函数的起始地址、全局偏移表（GOT）和过程链接表（PLT）。在可执行文件中，GOT、PLT都有各自的段（section）。global_variable的指针相对于全局偏移量。为了便于我们理解偏移量和表之间的关系，IDA对显示的偏移量进行了某种挑战。这部分的指令实际上是：

我们用旧版本的GCC将这段代码编译为64位目标文件。IDA在显示代码的时候隐藏了那些RIP的寻址细节。因此，我们通过objdump查看汇编代码：

```assembly
0000000000407220 <f1>:
48 8b 05 09 28 00 mov rax,QWORD PTR [rip+0x208b9] # 004072fe0
727: 53              push rbx
728: 89 fb             mov ebx,edi
72a: 48 8d 35 20 00 00 00 lea rsi,[rip+0x20] # 00407251
731: bf 01 00 00 00 mov edi,0x1
736: 03 18             add eax PTR [rax]
738: 31 c0             xor eax,eax
73a: 89 da             mov edx,ebx
73c: e8 df ff ff call 620 <_printf_chk<plt>
741: 89 d8             mov ebx,eax
743: 5b               pop rbx
744: c3               ret
```

我们来看看程序代码中的RIP之后的偏移量：

- 指令0x720。0x2008b9是该地址与全局变量global_variable之间的地址差
- 指令0x72A。0x20则是该地址与“returning %d”字符串之间的地址差

可能读者已经注意到，经常进行地址重复计算会降低程序的执行效率（虽然在64位系统下可能表现良好）。因此，注重性能的时候，最好采用静态链接的静态化。

# 67.1.1 Windows

Windows的DLL加载机制不是PIC机制。如果Windows加载要把加载到另一个进程，它就会内存中对DLL进行“修补”处理（重定向），从而可以正确地处理所有地址。这就意味着多个Windows进程无法在不同进程内存中的不同地址共享一份DLL，因为每个被加载在内存内的实例只能访问自己的空间。

# 67.2 在Linux下的LD_PRELOAD

Linux程序可以加载其他动态库之前、甚至在加载系统库（例如libc.so.6）之前加载自己的动态库。

借助这项功能，我们能够编写自定义的函数“替换”系统库中的同名函数。进一步说，劫持函数如read()、write()等系统函数并非易事。

接下来，我们以工具uptime来进行演示。我们都知道，应用可以显示计算机工作了多久。另一款strace可见，uptime通过/proc/uptime获取工作时长：

```bash
$ strace uptime
open("/proc/uptime", O_RDONLY) = 3
lseek(3, 0, SEEK_SET) = 0
read(3, "1666.86\n", 20) = 47
$ cat /proc/uptime
90
```

其实，proc/uptime并不是真正上的磁盘文件。它具有两个数值：

- 第一数值显示的是系统运行的总时长；
- 第二数值是计算机处于空闲状态的时间。

这两项数据都以秒为单位。我们编写一个open()、read()和close()函数的动态链接。首先处理的就是open()函数。它能判断程序打开的文件。如果两者相同，open()函数就记录文件描述，接下来处理的是read()函数。read()能判断程序打开的是我们要关注的文件。如果两者相同，我们就用某些符代替，否则调用libc.so里的原来的read。最后需要处理的是close()函数，它确保关闭已打开的外部文件。

本例通过dlopen()和dlsym函数获取同名函数在libc.so里的地址。简单的例子是要获取系统函数，另一方面如果我们支持strcmp()函数，这种劫持功能的源代码如下：

```c
#include <stdio.h>
#include <stdarg.h>
#include <stdlib.h>
#include <stdbool.h>
#include <unistd.h>
#include <dlfcn.h>
#include <string.h>

void *libc_handle = NULL;
int (*open_ptr)(const char *, int) = NULL;
int (*close_ptr)(int) = NULL;
ssize_t (*read_ptr)(int, void *, size_t) = NULL;

bool inited = false;

void die(const char * fmt, ...)
{
    va_list va;
    va_start(va, fmt);
    vprintf(fmt, va);
    exit(0);
}

static void find_original_functions()
{
    if (inited)
        return;
    libc_handle = dlopen("libc.so.6", RTL_LAZY);
    if (libc_handle==NULL)
        die("can't find libc.so.6\n");

    open_ptr = dlsym(libc_handle, "open");
    if (open_ptr==NULL)
        die("can't find open()\n");

    close_ptr = dlsym(libc_handle, "close");
    if (close_ptr==NULL)
        die("can't find close()\n");

    read_ptr = dlsym(libc_handle, "read");
    if (read_ptr==NULL)
        die("can't find read()\n");

    inited = true;
}

static int opened_fd=0;

int open(const char *pathname, int flags)
{
    find_original_functions();

    int fd=(open_ptr) (pathname, flags);
    if (strcmp(pathname, "/proc/uptime")==0)
        opened_fd=fd; // that's our file! record its descriptor
    else
        opened_fd=0;
    return fd;
}

int close(int fd)
{
    find_original_functions();

    if (fd==opened_fd)
        opened_fd=0; // the file is not opened anymore
    return (*close_ptr) (fd);
}

ssize_t read(int fd, void *buf, size_t count)
{
    find_original_functions();

    if (opened_fd!=0 && fd==opened_fd)
    {
        // that's our file!
        return snprintf(buf, count, "%d %d", 0x7fffffff, 0x7fffffff+1);
    }
    // not our file, go to real read() function
    return (*read_ptr)(fd, buf, count);
}
```

我们用通用的动态库来编译：

```bash
gcc -fpic -shared -Wall -o fool_utime.so fool_utime.c -ldl
```

最后，我们通过LD_PRELOAD指令优先加载自定义的函数库：

```bash
LD_PRELOAD='./fool_utime.so uptime
```

上述指令的输出结果为：

```
01:23:02 up 24855 days, 3:14, 3 users, load average: 0.00,
0.01, 0.05
```

我们在系统的环境变量中设定了LD_PRELOAD、让它指向我们自定义的动态链接库，那么所有的进程都会在启动之前加载自定义的动态链接库。

# 68章 Windows NT

# 68.1 CRT (Win32)

所有程序都是main函数开始执行的？事实并非如此。如果用IDA或者HIE打开可执行文件，我们可以看到OEP (Original Entry Point) 总是指向其他的段。这些代码会在启动之前进行一些维护和准备工作。这就是所说的启动代码/startup-codeCRT代码 (C Runtime)。

通常来说，不同的编译器会有不同的CRT代码：

以下的是MSVC 2008的CRT代码：

```assembly
1  tmainCRTstartup proc near
2      var_24 = dword ptr -24h
3      var_20 = dword ptr -20h
4      var_1C = dword ptr -1Ch
5      ms_exc = CPEH_RECORD ptr -18h
6
7
8
9      push          14h
      push          offset stru_04092D0
```
