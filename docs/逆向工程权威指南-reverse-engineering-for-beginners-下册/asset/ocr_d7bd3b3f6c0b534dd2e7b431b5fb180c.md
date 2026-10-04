```
cmp edi, 11
jg .L6
movsx rdi, edi
mov rax, QWORD PTR [0+rdi*8]
ret
```

```
.L6:
push rax
mov ecx, OFFSET FLAT:PRETTY_FUNCTION__2423
mov edx, 29
mov esi, OFFSET FLAT:.LC1
mov edi, OFFSET FLAT:.LC2
call __assert_fail
```

```
.PRETTY_FUNCTION__2423:
.string "get_monthl_checked"
```

从中可知，GC向异常处理函数传递了其调用函数的函数名称。

这种边界检查是否存在明显的开销问题。——在调用输入值的边界检查函数上使用了assert()宏，性能影响会非常
。以MSVC为例，Debug版的MSVC还有大量的assert()，而最终发行版的MSVC里就不再使用这个了。

微软Windows NT内核也有“checked”和“free”两个版本。前一个版本
还在输入值的边界检查，而后面的第二版本就不再使用assert()了。

# 18.6 多维数组

多维数组和线性数组在本质上是相同的。

计算机内存是连续的线性空间，它可以与一维数组直接对应。在被拆分
成多个一维数组后，多维数组与内线性空间相同存在直接直接的存储关
系。

例如，二维数组a[3][4]可转化为a[12]这样的12个元素一维数组
组，如表18.1所示。

表18.1 使用多维数组表示二维数组

| 存储地址 | 数组元素 |
| --- | --- |
| 0 | [0] [0] |