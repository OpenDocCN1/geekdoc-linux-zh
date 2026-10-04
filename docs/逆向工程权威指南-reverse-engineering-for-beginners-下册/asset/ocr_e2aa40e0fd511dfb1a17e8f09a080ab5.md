ret 0
_f ENDP GCC

如果关闭GCC 4.4.1的优化选项，会生成下列代码：

# 指令清单19.12 Non-optimizing GCC

```
public f
proc near
var_4 = dword ptr -4
arg_0 = dword ptr 8

push ebp
mov ebp, esp
sub esp, 10h
mov eax, [ebp+arg_0]
mov [ebp+var_4], eax
mov [ebp+var_4], 4000h
or [ebp+var_4], 0xFFFFFFDDh
mov eax, [ebp+var_4]
leave
retn
endp
```

虽然GCC的非优化编译结果存在冗余指令，但是这个程序仍然比MSVC的非优化编译程序较短。

接下来使用GCC的-O3选项进行优化编译。

# 指令清单19.13 Optimizing GCC

```
public f
proc near
arg_0 = dword ptr 8

push ebp
mov ebp, esp
mov eax, [ebp+arg_0]
pop ebp
or ah, 40h
and ah, 0FDh
retn
endp
```