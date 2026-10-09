
6 0000007f e8c4f8b 00000000 0040f96 0040f96

`App12_foo_thread+0x96` [`/home/ALCD2/x64/app12.main @ 72`]

```

```

05 0000ff7 ef481d0c0 00000413f3

06 0000ff7 ef481d0c0 0000045511f2

`2.28/nplt/thread_create.c:80`

07 0000ff7 ef481d0e88 fffffffffffff

08 0000ff7 ef48100e88 000000000000

```

```

`App12_thread_0x11` // `/home/coredump/ALCD2/x64/App12/main.cpp @ 72`

`App12!start_thread_0xf3` // `[build/glibc-vJB4T1/glibc`

`App12!clone_0x3f`

`0xffffffffffffffff`

```

`Unable to get thread for thread 3`

```

### Child-SP

`Id: 2.bda: Suspended: 0 at 0xb8`

`RetAddr`

09 0000ff7 e3a8c010 000004528f4

01 0000ff7 e3a8c0a0 00000401ffc

02 0000ff7 e3a8c0b0 00000401f9c

03 0000ff7 e3a8c0c0 00000401f8

04 0000ff7 e3a8c0d0 00000413f3

05 0000ff7 e3a8c0e0 0000045512f

`2.28/nplt/thread_create.c:80`

06 0000ff7 e3a8c0f0 ffffffffffff

07 0000ff7 e3a8c100 000000000000

```

```

`App12!unfreeze`

`App12!nanleep+0x40`

`App12!sleep+0xa6`

`App12!thread_0xe3` // `/home/coredump/ALCD2/x64/App12.cpp @ 73`

`App12!thread_0xe11` // `/home/coredump/ALCD2/x64/App12.cpp @ 73`

`App12!start_thread_0xf3` // `[build/glibc-vJB4T1/glibc]`

```

`Unable to get thread for thread 4`

```

### Child-SP

`RetAddr`

08 0000ff7 e3a7c110 0000045512f

`2.28/nplt/thread_mutex_lock+x54` `[build/glibc-vJB4T1/glibc`

`2.28/nplt/thread_mutex.c @ 80`

09 0000ff7 e3a7c120 ffffffffffff

01 0000ff7 e3a7c130 0000041d9

02 0000ff7 e3a7c140 0000041f3

03 0000ff7 e3a7c150 00000401d2

04 0000ff7 e3a7c160 ffffffffffff

05 0000ff7 e3a7c170 00000000000

```

```

`App12!unfreeze`

`App12!nanleep+0x40`

`App12!sleep+0xa6`

`App12!clone_0xe9` // `/home/coredump/ALCD2/x64/App12.cpp @ 75`

`App12!thread_0xe11` // `/home/coredump/ALCD2/x64/App12.cpp @ 75`

`App12!start_thread_0xf3` // `[build/glibc-vJB4T1/glibc`

`App12!clone_0x3f`

`App12!thread_xb3` // `[build/glibc-vJB4T1/glibc]`

```

`Unable to get thread for thread 5`

```

### Child-SP

`Id: 2.bda: Suspended: 0 at 0xb8`

`RetAddr`

00 0000ff7 ed7c6e70 000004528f4

01 0000ff7 ed7c6e80 0000040224

02 0000ff7 ed7c6e90 0000040204a

03 0000ff7 ed7c6ea0 00000402d4

04 0000ff7 ed7c6eb0 00000413f3

05 0000ff7 ed7c6ec0 0000045512f

`2.28/nplt/thread_create.c @ 48`

06 0000ff7 ed7c6ef0 ffffffffffff

07 0000ff7 ed7c6ff0 000000000000

```

```

`App12!unfreeze`

`App12!nanleep+0x40`

`App12!sleep+0xa6`

`App12!clone+0xe9` // `/home/coredump/ALCD2/x64/App12.cpp @ 75`

`App12!thread_0xe11` // `/home/coredump/ALCD2/x64/App12.cpp @ 75`

`App12!start_thread_0xf3` // `[build/glibc-vJB4T1/glibc]`

```

# 7. 如果我们想省略它们，请使用此命令：

```

0:000: `ki`

`RetAddr`

### Child-SP

00 0000ff7 e3a86600 000004528f4

01 0000ff7 e3a86630 00000402121

02 0000ff7 e3a86670 00000041f11

03 0000ff7 e3a8b6c0 00000401d9a

04 0000ff7 e3a8b7c0 ffffffffffff

05 0000ff7 e3a8b7c8 00000000000

```

```

`Call Site`

`App12!nanleep+0x40`

`App12!sleep+0xa3`

`App12!main+0xd6`

`App12!libc_start+0x31`

`App12!start+0xa2`

`ffffffff`

```

# 8. 如果我们想在堆栈中包含参数，我们使用另一个变体：

```

0000>`k`

### Child-SP

`RetAddr`

`Call Site`

0 0000007f e8c2e00 00000000000028fa

`App12:nanleep+0x40`

1 0000007f e8c2e00 000000000000022

`App12:0+0x3a`

200000000ff8000000000000000071

`App12:main`

    `int arg = 0;`

    `char **arg = 0x000077ffe378a8d3`

3 0000007f e3c2c00 0000000000000d1a

`App12_libc_start_main+0xd3`

4 0000007f e3c2c7c0 00000000ffffffffffff

`12:start+0x2a`

`ffffffff`

```

# 9. 切换到帧 #2，列出参数和局部变量：

```

0000>`frame /2`

`0000077ffe378a670 00000417ff11` `App12!main+0xd6`

`[/home/coredump/ALCD2/x64/app12 main] @0`

`ffffffffffff rbx=0000000000040d00 rcx=0000000000452970`

`rdx=0000000000000000 rdi=0000077ffe378a630 rsi=0000077ffe378a630`

`rip=0000000000040211 rbp=0000077ffe378a630`

`rs=0000000000000000 r9=0000077fbced790 r10=0000077fbced790`

`r11=0000000000000000 r12=0000000000041850 r13=0000000000000000`

`r14=0000000000041018 r15=0000000000000000`

`l1p=0`

`    nv up ng az pc`

`cs=683 sss=0022 ds=0000 es=0000 fs=0000 gs=0000 efl=000000293`

`App12!main+0xd6:`

`    eax,0`

`000000000040121 mov`

```

# 10. 检查 args 行：

```

0000>`dpa 0x000077ffe378a7d8 L10`

`0000077ffe378a7d8 0000077fe378a7b4 "/App12"`

`0000077fe378a7e0 0000000000000000`

`0000077fe378a7e6 0000077fe378b756 "SHELL=/bin/bash"`

`0000077fe378a7f6 0000077fe378b737 "HISTCONTROL_NAME=ignoreboth"`

`0000077fe378a7b0 0000077fe378b730 "WSL_DIRECTORY=Debian"`

`0000077fe378a800 0000077fe378b794 "HOME_DESKTOP-ISV6l0"`

`0000077fe378a808 0000077fe378b7a9 "PATH=/home/coredump/ALCD2/x64/app12"`

`0000077fe378a810 0000077fe378b72c "LD_LIBRARY=coredump"`

`0000077fe378a818 0000077fe378b7d2 "MC_TMPDIR=/tmp/mc-coredump"`

`0000077fe378a820 0000077fe378b769 "MC_SIZE=14"`

`0000077fe378a828 0000077fe378b803 "HOME=/home/coredump"`

`0000077fe378a830 0000077fe378b817 "LANG=en_US.UTF-8"`

`0000077fe378a838 0000077fe378b828 "WSL_INTEROP=/run/wsl_8_interop"`

`0000077fe378a840 0000077fe378b847 "LS_COLORS=rs=0;di=01;31:34;ln=01;36;mh=00;pi=40;33;so=01;3"`

`0000077fe378a448 0000077fe378be29 "WAYLAND_DISPLAY=wayland-0"`

`0000077fe378a850 0000077fe378be43 "TERM=term-256-color"`

```

11. 我们也可以指定源代码的路径（通过 `.xcr` 命令重置上下文并使用参数设置帧后，将会源代码视图）：

```

0:000> `.srcpath C:\ALCD2\x64\App12`

`Source search path is: C:\ALCD2\x64\App12`

`************ Path validation summary **********`

`Response Time (ms) Location`

`OK C:\ALCD2\x64\App12`

0:000> `.xcr`

0:000> `.frame 2`

```

![](img/3944f3cabeeec58663646c309af01b5f_509_0.png)

12. 将加载的 App12 模块的内容导出到二进制文件：

```

0:000> `1m`

`start module name`

`00000000 00400000 0000000004d4000`

`App12 T (service symbols: DWARF Private Symbols)`

`c:\alcd2\x64\symbols\App12`

`linux_vdso_so (deferred)`

0:000..`writem C:\ALDA2\x64\mem.raw 000000 0040000 000000 004d400`

`Writing d4001 bytes.`

`Unable to read memory at 00000000 00400800, file is incomplete`

```

## 13. 列出所有可用符号：

```

0:000* `X App12i!`

`0000000403d4a0` `App12mutexA` `=` `pthread_mutex_t`

`0000000403d4e0` `App12mutexB` `=` `pthread_mutex_t`

...

`000000000040202b` `App12main` `(int, char **)`

`0000000000402033` `App12thread_five` `(int, char **)`

`0000000000402027` `App12foo_five` `(int, char **)`

`0000000000402016` `App12lib_bar` `(int, char **)`

`00000000004021fe` `App12thread_four` `(int, char **)`

`00000000004021f2` `App12foo_int` `(int, char **)`

`00000000004021e6` `App12lib_bar_four` `(int, char **)`

`00000000004021fc` `App12thread_three` `(int, char **)`

`00000000004021c2` `App12foo_one` `(int, char **)`

`000000000040213` `App12lib_three` `(int, char **)`

`00000000004021f9` `App12thread_two` `(int, char **)`

`00000000004021f8` `App12foo_two` `(int, char **)`

`00000000004021f1` `App12thread_bar_two` `(int, char **)`

`0000000000402169` `App12free` `(int, char **)`

`00000000004021d5` `App12foo_one` `(int, char **)`

`000000000040214c` `App12bar_one` `(int, char **)`

`00000000004021f4` `App12bar_one` `(int, char **)`

`000000000040210b` `App12procB` `(int, char **)`

`00000000004021e5` `App12procA` `(int, char **)`

`00000000004021e8` `App12procC` `(int, char **)`

...

```

## 14. 列出所有类型和函数/变量：

```

0:000* `dt App12i!`

`App12!thread_mutex_t`

...

`000000000040204b` `App12main`

`0000000000402033` `App12thread_five`

`0000000000402027` `App12foo_five`

`0000000000402016` `App12lib_bar`

`00000000004021fe` `App12thread_four`

`00000000004021f2` `App12foo_four`

`00000000004021e6` `App12lib_bar`

`00000000004021fc` `App12thread_three`

`00000000004021c2` `App12foo_two`

`00000000004021fb` `App12bar_three`

`00000000004021f9` `App12thread_two`

`00000000004021f8` `App12foo_two`

`00000000004021f1` `App12lib_two`

`0000000000402169` `App12thread_one`

`00000000004021d5` `App12foo_one`

`000000000040214c` `App12bar_one`

`00000000004021f4` `App12bar_one`

`000000000040210b` `App12procB`

`00000000004021e5` `App12procA`

`00000000004021e8` `App12procC`

...

```

## 15. 我们注意到栈上的锁，由于锁有所有者（线程 ID），我们可以像之前的练习中那样检查其所有权状态来检测泄漏（可以使用 `dx` 或 `dt`）：

```

>`App12mutex`

`00000000 004d3a40` `App12mutexA` `=` `pthread_mutex_t`

`00000000 004d3a44` `App12mutexB` `=` `pthread_mutex_`

>`dx mutexA`

`mutexA`

`[Type: pthread_mutex_t]`

`[+0000] _data      [Type: pthread_mutex_s]`

`[+0000]   size      : ??? [Type: char [40]]`

`[+0000]   align     : 2 (Type: int)`

`0000: dx mutexA._data`

`mutexA._data  [Type: pthread_mutex_s]`

`[+0000] count       : 2 (Type: int)`

`[+0004] owner      : 0x0 (Type: unsigned)`

`[+0000] owner      : 700 (Type: int)`

`[+0000] nusers     : 0x1 (Type: unsigned)`

`[+0010] kind       : 0 (Type: int)`
