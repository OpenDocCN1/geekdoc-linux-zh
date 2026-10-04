在汇编指令层面，Linux与Windows的编译结果却不大。它们的区别主要体现在字段（segment）名称和字段属性上：Linux生成的GCC的未初始化变量出现在bss段，对应的ELF文件描述了这个字段数据的属性。

+   - Segment type: Uninitialized
- Segment permissions: Read/Write

如果这个变量分配了初始值，比如10，那么这个变量就会出现在_data段，并且具有如下属性。

+   - Segment type: Pure data
- Segment permissions: Read/Write

# 7.2.4 MSVC: x64

指令清单7.6 MSVC 2012 x64

```
DATA SEGMENT
COMM x:DWORD
$SG2924 DB 'Enter X: ', 0AH, 00H
$SG2925 DB '%d', 00H
$SG2926 DB 'You entered %d.. ', 0AH, 00H
_DATA ENDS
```

```
TEXT SEGMENT
main PROC
$LN3:

sub rsp, 40

lea rcx, OFFSET FLAT:$SG2924 ; 'Enter X: '
call
printf
lea rcx, OFFSET FLAT:x
call
lea rcx, OFFSET FLAT:$SG2925 ; '%d'
call
scanf
mov edx, DWORD PTR x
lea rcx, OFFSET FLAT:$SG2926 ; 'You entered %d...'
call
printf

return 0
xor eax, eax

add rsp, 40
ret
ENDP
_TEXT
TEXT ENDS
```

这段64代码与x86的代码没有明显的区别。请注意变量x的传递过程：scanf()函数通过LEA指令获取变量的指针；而printf()函数是通过MOV指