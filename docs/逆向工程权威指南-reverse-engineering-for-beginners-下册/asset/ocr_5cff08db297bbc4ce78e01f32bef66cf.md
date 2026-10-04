```
.text:0054108E mov [ebx+esi], al ; store to internal array
.text:00541091 inc esi ; increment loop 1 counter
.text:00541092 cmp esi, 8
.text:00541095 jl short first_loop2_begin
.text:00541097 inc edi ; increment loop 2 counter
```

```
; increment internal array pointer by 8 at each loop 1 iteration
.text:00541098 add ebx, 8
.text:0054109B cmp edi, 8
.text:0054109E jl short first_loop1_begin
```

这两个循环的控制变量，不仅取值范围都在0~7之间，而且它们分别充当了get_bit()函数的第一个、第二个参数。而get_bit()函数使用的第三个参数是rotate1()函数的唯一参数。之后，get_bit()函数的返回值存储在内部数组里。

函数再次复备了指向内存的结构:

```
.text:005410A0 lea ebx, [esp+50h+internal_array_64]
.text:005410A4 mov edi, 7 ; EDI is loop counter, initial state is 7
.text:005410A9 second_loop1_begin:
.text:005410A9 xor esi, esi ; ESI is loop 2 counter
.text:005410AB second_loop2_begin:
.text:005410AB mov al, [ebx+esi] ; value from internal array
.text:005410AE push eax
.text:005410AF push ebp ; arg_0
.text:005410B0 push edi ; loop 1 counter
.text:005410B1 push esi ; loop 2 counter
.text:005410B2 call set_bit
.text:005410B7 add esp, 10h
.text:005410BA inc esi ; increment loop2 counter
.text:005410BB cmp esi, 8
.text:005410BE jl short_loop2_begin
.text:005410C0 dec edi ; decrement loop2 counter
.text:005410C1 add ebx, 8 ; increment pointer
```