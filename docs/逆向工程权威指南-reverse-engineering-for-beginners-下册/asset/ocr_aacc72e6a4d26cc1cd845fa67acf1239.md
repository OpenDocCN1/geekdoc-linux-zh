```
.text:0811A2A5   loc_811A2A5: ; CODE XREF
kdiSerLengths+11C
.text:0811A2A5               ;
kdiSerLengths+1C1
.text:0811A2A5 8B 7D 08   mov edi, [ebp+arg_0]
.text:0811A2A8 8B 7F 10   mov edi, [edi+10h]
.text:0811A2A8 AF 06 57 14   movzx edx, byte ptr
[edi+14h]
.text:0811A2AF F6 C2 01   test dl, 1
.text:0811A2B2 75 3E       jnz short
loc_811A2F2
.text:0811A2B4 83 E0 01   and eax, 1
.text:0811A2B7 74 1F       jz short
loc_811A2D8
.text:0811A2B9 74 37       jz short
loc_811A2F2
.text:0811A2BB 6A 00       push 0
.text:0811A2BD FF 71 08   push dwordptr [ecx+8]
.text:0811A2C0 E8 5F FE FF FF call len2nbytes
```

这些问题属于编译器的bug。但是它们生成的程序将不会受到该bug的影响，所以可以被测试人员遗掉了。本书的19.2.4节、39.3节、47.7节、18.7节、12.4.1节、19.5.2节中都演示了这种问题。

本文演示了这些编译器问题，以证明编译器确实可能出现我们意想不到的奇怪行为。如果遇到了这种现象，读者就不必费尽力地去调试“编译器为什么会生成这种诡异代码”。