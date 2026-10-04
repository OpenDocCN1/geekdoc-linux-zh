# # 第19章 操作

有很多程序员都把输入参数的某些位位当作标识标志位处理。在表面看来，使用布尔变量足以替代标志位寄存器，但是这种替代的做法并不理智。

# ## 19.1 特定位

# ### 19.1.1 x86

Win32的API 中有这么一段声明：

```
HANDLE fh;

h=CreateFile("file", GENERIC_WRITE | GENERIC_READ,
FILE_SHARE_READ, NULL, OPEN_ALWAYS, \
    FILE_ATTRIBUTE_NORMAL, NULL);
```

经过MSVC 2010编译，可以得到如下所示的指令。

指令清单19.1 MSVC 2010

```
push          0
push          128               ; 00000080
push          4
push          0
push          1
push         -1073174128      ; c0000000
push          OFFSET SSG78813
call          DWORD PTR  __imp_CreateFileA@28
mov           DWORD PTR  _fh$[ebp], eax
```

库文件WinNT.h对有关常量的相关区域进行了定义。

指令清单19.2 WinNT.h