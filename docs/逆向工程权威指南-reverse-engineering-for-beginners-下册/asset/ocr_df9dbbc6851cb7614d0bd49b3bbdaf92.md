in internal array cmp edi, 0FFFFFFFF

```
.text:005410C4
.text:005410C7 jg short_second_loop1_begin
.text:005410C9 pop edi
.text:005410CA pop esi
.text:005410CB pop ebp
.text:005410CC pop ebx
.text:005410CD add esp, 40h
.text:005410D0 retn
.text:005410D0 rotatel endp
```

虽然上述代码通过set_bit()函数将内部数组组的数据复制到了全局数组，但是数组的排列顺序完全不一样。第一层循环的控制变量从7逐渐变为，呈递减的变化趋势。

通过上面的分析，我们可以梳理出rotate1()的源代码如下：

```
void rotatel(int v)
{
    bool tmp[8];//internal array
    int i, j;

    for (i=0; i<8; i++)
        for (j=0; j<8; j++)
            tmp[i][j]=get_bit(i,j, v);

    for (i=0; i<8; i++)
        for (j=0; j<8; j++)
            set_bit(j, 7-i, v, tmp[x][y]);
}
```

既然已经搞清了rotate1()函数，那么我们继续研究rotate2()函数：

```
.text:005410E0 rotate2 proc near
.text:005410E0 internal_array_64 = byte ptr -40h
.text:005410E0 arg_0 = dword ptr 4
.text:005410E0
.text:005410E0 sub esp, 40h
.text:005410E3 push ebx
.text:005410E4 push ebp
.text:005410E5 mov ebp, [esp+48h+arg_0]
.text:005410E9 push esi
.text:005410EA push edi
```