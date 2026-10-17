
```
seg30:0125               loc_35A85; CODE XREF: sent_pro+DAJ
seg30:0125                             mov bl, [bp+var_3]
seg30:0125 8A 5E FD
seg30:0128               loc_35A88; CODE XREF: sent_pro+E2j
seg30:0128 F6 C1 80
test    cl, 08h
seg30:012B 74 03        jz      short_loc_35A90
seg30:012D 80 E3 7F      and     bl, 7Fh
seg30:0130               loc_35A90; CODE XREF: sent_pro+EAj
seg30:0130 8B 16 82 7E      mov     dx,_in_port_1_
seg30:0134 8A C3        mov     al, bl
seg30:0136 EE           out     dx, al
seg30:0137 8B C7        mov     ax, di
seg30:0139 5F           pop     di
seg30:013A 5E           pop     si
seg30:013B C9           leave
seg30:013C CB           retf
seg30:013C             sent_pro_end
```

可见，这个加密狗是 Sentinel Pro 出出的“哈希验证”型加密狗。通过程序过程中传递的字符串字符，我们能够访问这种加密字符串。而且它是 16 位的返回值，最终和固定值进行比较。

输出端口地址通常为`0x378`，USB 之后打印机所用的输出打印端口。在设计这个接口时，恐怕没有人会想到要从打印机接收数据，由于这个接口是单向通信接口[3]。程序通过`0x379`端口访问打印机的状态寄存器，获取“缺/`ack`”“忙”标记的状态信号。也就是说，打印机的状态寄存器是主机打印机工作状态的唯一途径。因此，加密狗肯定通过这个寄存器获取反馈信息，逐次遍历到位了。

源码中的`_in_port_1`和`in_port_1`标签，分别访问了状态寄存器（`0x379`）和控制寄存器（`0x37A`）。

看来，通过`seg30:009B`的指令，程序通过“忙”标记为获取返回信息：每个位都存储在`DI`寄存器中，由函数结尾的指令返回。

那么，发送输出端口的这些字节有什么含义呢？笔者没有进行深究，只知道发送加密的指令。而且这种任务来说，不必把每个控制指令清楚。

检测加密狗的指令如下：

```
00000000 struct_0      struct ; (sizeof=0x1B)
00000000 field_0       db 25 dup(?)      ; string (C)
00000001 _A             dw;
00000001 struct_0      ends
dseg:3CBC 61 63 73 72 75+_Q  struct_0 '<hello', 01122h>
dseg:3CBC 62 65 00 00 00+      ; DATA XREF: check_dongle+2Eo

  skipped

dseg:3E00 63 66 66 00+      struct_0 '<coffee', 7EB7h>
dseg:3E1B 64 6F 67 00+      struct_0 '<dog', 0FFADh
dseg:3E36 63 61 74 00+      struct_0 '<cat', 0FF5h
dseg:3E51 70 61 70 65+      struct_0 '<paper', 0FFDh
dseg:3E6C 63 6F 6B 65+      struct_0 '<coke', 05F68h
dseg:3E87 63 6C 6F 63+      struct_0 '<clock', 55EAh
dseg:3EA2 64 69 72 00+      struct_0 '<dir', 0FFAEh
dseg:3EBD 63 6F 70 79+      struct_0 '<copy', 05F57h
```

```
seg030145               check_dongle proc far ; CODE XREF:
sub_3771D+3EP
seg030145
var_6 = dword ptr -6
seg030145
var_2 = word ptr -2
seg030145
seg030145 C8 06 00 00+      enter      6, 0
seg030149 59               push       si
seg03014A 66 6A 00+      push       large 0
newtime
seg03014D 6A 00+         push       0               ; cmd
seg03014F 9A C1 18 00+      call       _biostime
seg030154 52               push       dx
seg030155 00+             push       ax
seg030156 66 58             pop        eax
seg030158 83 C4 06+      add        sp, 6
seg03015B 66 89 44 FA      mov        [bp+6], eax
seg03015F 66 3B 06 08+      cmp        expiration
seg030164 7E 44+          je       short_loc_35B0A
seg030166 6A 14+          push       14h
seg030168 90               nop
seg030169 0E               push       cs
seg03016A 88 52 00      call       near ptr get_rand
seg03016D 59               pop        cx
seg03016E 8B F0           mov        si, ax
```
