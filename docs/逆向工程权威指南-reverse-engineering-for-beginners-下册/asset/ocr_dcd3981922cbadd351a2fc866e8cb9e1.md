slgcs

proc near

```
var_4          = dword ptr -4
arg_0          = dword ptr 8
```

```
push           ebp
mov             ebp, esp
push           esi
mov             [ebp+var_4], ebx
mov             eax, [ebp+arg_0]
call           $+5
pop            ebx
nop            ; PIC mode
mov             ebx, offset _GLOBAL_OFFSET_TABLE_
mov             dword ptr [eax], 0
call           sltrgatime64  ; PIC mode
push           0
mov             0Ah
push           edx
push           eax
call           __udivdi3      ; PIC mode
mov             ebx, [ebp+var_4]
add             esp, 10h
mov             esp, ebp
pop            ebp
retn
endp
```

slgcs

这个函数调用了sltrgatime64()，然后把返回值乘以10。[7]

在Win32版本的程序中，这个函数则是：

```
_slgcs         proc near      ; CODE XREF
_dbgefgHtElResetCount+15      
```

```
_dbgerRunActions+1528      
```

```
db             66h
nop            ebp
push           ebp
mov             ebp, esp
mov             eax, [ebp+8]
mov             dword ptr [eax], 0
call           ds:__imp__GetTickCount@0 ;
```

GetTickCount()

```
mov             edx, eax
```