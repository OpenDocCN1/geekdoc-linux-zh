指令之前分派了CDQ指令。IDIV指令就会进行MOVSX那样的符号位处理和数据扩展处理。

启用编译器的优化选项后，可得到如下程序：

# 指令清单41.2 采用MSVC 优化

```
a$           = 8             ; size = 4
_f PROC
mov         ecx, DWORD PTR  a$[esp-4]
mov         eax, 954437177   ; 38E38E39H
imul        ecx
sar         edx, 1
mov         eax, edx
shr        edx, 31        ; 0000001FH
add         eax, edx
ret
_f ENDP
```

编译器用乘法指令来转换为实际乘法运算。大家知道乘法会比除法运行很快。使用这里介绍[1]的方法可以有效提高程序效率、节省时间开销。

在编译优化中，我们常常常将其称为“强度减轻”的办法。

若使用GCC 4.4.1编译此程序，即使我们刻意启用优化选项，GCC的非优化编译结果和MSVC的优化编译结果相似。

# 指令清单41.3 不优化的GCC 4.4.1

```
public f
proc near
arg_0 = dword ptr 8

push        ebp
mov         ebp, esp
mov         ecx, [ebp+arg_0]
mov         edx, 954437177   ; 38E38E39H
mov         eax, ecx
imul        edx
sar         edx, 1
mov         eax, ecx
sar         eax, 1F
```