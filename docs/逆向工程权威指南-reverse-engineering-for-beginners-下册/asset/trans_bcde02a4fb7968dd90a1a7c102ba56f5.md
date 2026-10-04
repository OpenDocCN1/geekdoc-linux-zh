

```assembly
10	call    EBH_prolog4
11	mov     eax, 5B4Dh
12	cmp     ds:400000h, ax
13	jnz     short loc_40196
14	mov     eax, ds:40003Ch
15	cmp     dword ptr [eax+400000h], 4550h
16	jnz     short loc_40196
17	mov     ecx, 10Bh
18	cmp     [eax+400018h], cx
19	jnz     short loc_40196
20	cmp     dword ptr [eax+400074h], 0Eh
21	jbe     short loc_40196
22	xor     ecx, ecx
23	cmp     [eax+4000E8h], ecx
24	setnz  cl
25	mov     [ebp+var-1C], ecx
26	jmp     short loc_4019A

29	loc_40196: : CODE REQ;   tmainCRTStartup+18
30	;       tmainCRTStartup+29 ...
31	;and     [ebp+var-1C], 0

33	loc_4019A: : CODE REQ;   tmainCRTStartup+50
34	push    1
35	call    heap_init
36	pop     ecx
37	test    eax, eax
38	jnz     short loc_4010AE
39	push    1Ch
40	call    fast_error_exit
41	push    ecx

43	loc_4010AE: : CODE REQ;   tmainCRTStartup+60
44	call    _mtinit
45	test    eax, eax
46	jnz     short loc_4010BF
47	push    10h
48	call    fast_error_exit
49	push    ecx

51	loc_4010BF: : CODE REQ;   tmainCRTStartup+71
52	sub     esp, 40F2h
53	and     [ebp-ms_exc.disabled], 0
54	call    _loinit
55	test    eax, eax
56	jnge    short loc_4010D9
57	push    1Bh
58	call    _amsg_exit
59	push    ecx

61	loc_4010D9: : CODE REQ;   tmainCRTStartup+8B
62	call    dsGetCommandLineA
63	mov     dword_40D7F8h, eax
64	call    _crtGetEnvironmentStringsA
65	mov     dword_40AC60, eax
66	call    setargv
67	test    eax, eax
68	jnge     short loc_4010FF

69      push        8
70      call        __amsg_exit
71      pop         ecx

73  loc_0410FF: ; CODE XREF:  tmainCRTStartup+B1
74      call        setenvp
75      test        eax, eax
76      jge         short   loc_041110
77      push        9
78      call        __amsg_exit
79      pop         ecx

81  loc_041110: ; CODE XREF:  tmainCRTStartup+C2
82      push        1
83      call        cinit
84      pop         ecx
85      test        eax, eax
86      jz          short   loc_04123
87      push        eax
88      call        __amsg_exit
89      pop         ecx

91  loc_041123: ; CODE XREF:  tmainCRTStartup+D6
92      mov         envp, eax
93      mov         dword [0xAC80],eax ; envp
94      push        eax                 ; argv
95      push        argv               ; argv
96      push        argc                ; argc
97      mov         eax
98      call        _main
99      add         esp, 0              ; epch
100     mov         [ebp-var_20], eax
101     cmp         [ebp+var_1C], 0
102     jnz         short   LN28
103     push        eax                 ; uExitCode
104     call        LN32

106 LN28:      ; CODE XREF:  tmainCRTStartup+105
107     call        cexit
108     mov         short   loc_04186

110 LN27:      ; DATA XREF:  .rdata:stru_402D0
111     mov         eax, [ebp+ms_ec_ptr] ; Exception filter 0 for function
112 1044
113     mov         ecx, [eax]
114     mov         ecx, [eax]
115     mov         [ebp-var_24], ecx
116     push        eax
117     push        eax
118     call        XcpFilter
119     pop         ecx
120     pop         ecx

122 LN24:
123     retn

126 LN14:      ; DATA XREF:  .rdata:stru_402D0
127     mov         esp, [ebp+ms_ec_old] ; Exception handler 0 for function 41044
127    mov eax, [ebp+var_24]
128    mov [ebp+var_20], eax
129    cmp [ebp+var_1c], 0
130    jnz short $LN29
131    push          ; int
132    call
133    _exit

135 $LN29; ; CODE XREF:  tmainCRTStartup+135
136    call    c_exit
138 loc_04186; ; CODE XREF:  tmainCRTStartup+112
139    mov eax, [ebp-ms_disabled], 0xFFFFFFFE
140    mov eax, [ebp+var_20]
141    call        ; SEH_epilog
142    retn
```

在程序的第26行、第66行和74行我们分别看到的是GetCommandLineA、setenv这三个函数，从这三个函数的名称看出它们分别是`argc`、`argv`和`envp`三个变量。

最后，第97行的主函数(main())获取这些参数。CRT的函数通常可以解释。例如第35行和54行的`heap_init()`和堆初始化是由CRT代码完成的。若没有CRT的情况下调用内存分配函数，就会引发异常并看到以下错误：runtime error R603 CRT not initialized。

在C++程序中，CRT代码在启动主函数()之前会初始化全局对象。主函数()返回的数值，或者是在LN32后传递给exit()。

我们可以通过下面的代码实现：

```cpp
#include <windows.h>

int main()
{
    MessageBox(NULL, "hello world", "caption", MB_OK);
}
```

选用以下命令进行编译：

```
cl main.c user32.lib /link entry:main
```

链接器显示：
> LINK : error LNK1014 ALIGN specified /DRIVER; image may not run

上述命令生成一个长度为720字节的可执行文件。它可以运行在x86架构上，但是不能在64位的Windows7上运行。

PE（Portable Executable）格式是微软Windows环境下执行文件（exe, dll, sys）的标准格式。与其他类型的PE文件的不同，exe和sys只有导入表而没有导出表。PE文件也有一个入口点（EP），就是Dll函数的地址。

为了方便专业人员分析和调试，PE文件包含：
- 头部（Header）
- 签名（Signature）
- 导入表（Import Table）
- 导出表（Export Table）
- 资源（Resource）
- 节（Section）
- 节数据（Section Data）

PE文件在读取时需要保存它的校验性。地址空间随机化（Address Space Randomization, ASLR）技术将其各个模块加载到随机的地址上。为了避免这个问题，地址空间的随机化ASLR技术应运生。在PE文件中通过设置一个标识来实现ASLR，这个标识的名称是IMAGE_CHARACTERISTICS_DYNAMIC_BASE。

在Windows Vista之前的系统中，系统的DLL（如kernel32.dll, user32.dll）基地址是已知的固定地址。

### 68.2 节

所有的执行文件分为若干节（sections）。段是代码、数据以及数据的组织形式。

- 带有IMAGE_SECTION_CNT_CODE或IMAGE_MEM_EXECUTE的段，封装的是可执行代码。
- 数据标识为IMAGE_SCN_CNT_INITIALIZED_DATA、IMAGE_SCN_MEM_READ或IMAGE_SCN_MEM_WRITE标记。
- 未初始化的空段为IMAGE_SCN_CNT_UNINITIALIZED_DATA、IMAGE_SCN_MEM_READ或IMAGE_SCN_MEM_WRITE。
- 常数段（其中的数据不可被重新赋值）的标识是IMAGE_SCN_CNT_INITIALIZED_DATA以及IMAGE_SCN_MEM_READ，但不包括IMAGE_SCN_MEM_WRITE。

### 68.2.1 模块

所有的执行文件分为若干节（sections）。段是代码、数据以及数据的组织形式。

- 带有IMAGE_SECTION_CNT_CODE或IMAGE_MEM_EXECUTE的段，封装的是可执行代码。
- 数据标识为IMAGE_SCN_CNT_INITIALIZED_DATA、IMAGE_SCN_MEM_READ或IMAGE_SCN_MEM_WRITE标记。
- 未初始化的空段为IMAGE_SCN_CNT_UNINITIALIZED_DATA、IMAGE_SCN_MEM_READ或IMAGE_SCN_MEM_WRITE。
- 常数段（其中的数据不可被重新赋值）的标识是IMAGE_SCN_CNT_INITIALIZED_DATA以及IMAGE_SCN_MEM_READ，但不包括IMAGE_SCN_MEM_WRITE。

### 68.2.2 系统

PE文件中指定了之一：

- NATIVE（驱动）
- console（控制台程序）
- GUI（图形界面程序）

### 68.2.3 版本

在Windows Vista之前的系统中，系统的DLL（如kernel32.dll, user32.dll）基地址是已知的固定地址。MSVC005编译的exe文件支持XP。MSVC008编译的应用程序兼容NT4。MSVC2012生成的exe文件，版本号默认6.00，指向Vista及后期。参阅：https://en.wikipedia.org/wiki/Windows_NT

### 68.2.4 段

PE执行文件的每个段都可以拥有一个段名。然而，名称是段的重要特征。通常来说，代码段的名称是text，数据的段名称是data，常数段的名称rdata（只读数据）。其他类型的段名还有：

- .idata: 导入段。IDA可能会给这个段分配一个伪名；详情请参阅参考书籍68.2.1节。
- .edata: 导出。这个段十分罕见。
- .pdata: 这个段存储的是用于异常处理的函数项，包含了信息。
- .reloc: 重定位段。
- .bss: 未初始的数据段（BSS）。
- .tls: 线程存储段（TLS）。
- .rsrc: 资源。
- .CRT: 在早期版本的MSVC编译的可执行文件中，可能出现这个段。

