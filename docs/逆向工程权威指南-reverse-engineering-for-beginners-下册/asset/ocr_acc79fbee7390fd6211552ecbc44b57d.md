这里有132个值，是66×2的队列。字符的总量正好是66。那么，到底每一个字符串对应两个32位数据，还是说这32位数据完全就是两个互不相同计数组？我们继续分析。

以0x1000开头的值可能是某种地址。毕竟SYM文件是DLL文件的，而Win32的基地址是0x10000000，代码的起始地址通常是0x10001000。

使用IDA工具打开orwtc.dll文件，可以看到它的基址不是默认地址。尽管如此，我们可以看到它的第一个函数的对应代码为:

```
.text:60351000   sub_60351001
.text:60351000
.text:60351000 arg_0      = dword ptr  8
.text:60351000 arg_4      = dword ptr  0Ch
.text:60351000 arg_8      = dword ptr  10h
.text:60351000
.text:60351000               push
.text:60351001               mov      ebp, esp
.text:60351003               mov      eax, dword_60350314, eax
.text:60351008               cmp      eax, 0xFFFFFF
.text:6035100B               jnz      short  loc_6035104F
.text:6035100D               mov      ecx, hModule
.text:60351013               xor      eax, eax
.text:60351015               cmp      ecx, 0xFFFFFF
.text:60351018               mov      dword_60350314, eax
.text:6035101D               jnz      short  loc_60351031
.text:6035101F               call     sub_603510F0
.text:60351024               mov      ecx, eax
.text:60351026               mov      eax, dword_60350314
.text:6035102B               mov      hModule, ecx
.text:60351031
.text:60351031 loc_60351031:      ; CODE XREF:

sub_60351000+ID
.text:60351033               test     ecx, ecx
.text:60351033               jbe      short  loc_6035104F
.text:60351035               push     offset ProcName, "ax_reg"
.text:6035103A               push     ecx
.text:6035103B               call     ds:GetProcAddress
```

哦，我们见过类似字符串“ax_reg”！它不是在SYM文件的字符串里的第一个字符串串！可见，这个函数的名字就是“ax_reg”。

上述DLL文件的第二个函数是:

```
.text:60351080   sub_60351080
.text:60351080
.text:60351080 arg_0      = dword ptr  8
```