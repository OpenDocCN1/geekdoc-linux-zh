# 图23.4 tracer与IDA的联动/某些屏幕右侧边界之外

通过分析qs 函数使用的函数指针，IDA能够显示出相应的函数名称（PtFuncCompare）。

由于数据组存储的是32位数据，所以指针a和指针b指向数组组的相同地方，它们每次变换之间的地址是4字节。

我们还注意到0x401010和0x401012处的就没有被执行（所以被标记为白色）。这是因为传递给（comp）函数的值都不相同，函数返回值不会是0。

# 23.2 GCC

GCC的编译方法与MSVC的编译方式相似。

# 指令清单23.3 GCC

```
lea     eax, [esp+40h+var_28]
mov     [esp+40h+var_40], eax
mov     [esp+40h+var_28], 764h
mov     [esp+40h+var_24], 2Dh
mov     [esp+40h+var_20], 0C8h
mov     [esp+40h+var_1C], FFFFF9Eh
mov     [esp+40h+var_18], OFF7h
mov     [esp+40h+var_14], 5
mov     [esp+40h+var_10], FFFFFFC7h
mov     [esp+40h+var_Cj], 43h
mov     [esp+40h+var_8], 58h
mov     [esp+40h+var_4], OFFE7960h
mov     [esp+40h+var_34], offset comp
mov     [esp+40h+var_38], 4
mov     [esp+40h+var_3C], 0Ah
call   _qsort
```

comp()函数对应的代码如下所示。

```
public comp
proc near
arg_0      = dword ptr 8
arg_4      = dword ptr 0Ch

push     ebp
mov      ebp, esp
mov      eax, [ebp+arg_4]
mov      ecx, [ebp+arg_0]
mov      edx, [eax]
```