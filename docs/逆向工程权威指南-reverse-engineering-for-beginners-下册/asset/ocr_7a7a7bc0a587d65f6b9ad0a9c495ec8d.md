```
add    ax, [bp+c]
pop     bp
retn   6
endp
```

func1

```
func2   proc near

arg_0   = word ptr 4
arg_2   = word ptr 6
arg_4   = word ptr 8
arg_6   = word ptr 0Ah
arg_8   = word ptr 0Ch
arg_A   = word ptr 0Eh

push    bp
mov     bp, sp
mov     ax, [bp+arg_8]
mov     dx, [bp+arg_A]
mov     bx, [bp+arg_4]
mov     cx, [bp+arg_6]
call    sub_B2 ; long 32-bit multiplication
add     ax, [bp+arg_0]
adc     dx, [bp+arg_2]
pop     bp
retn    12
endp
```

func2

```
func3   proc near

arg_0   = word ptr 4
arg_2   = word ptr 6
arg_4   = word ptr 8
arg_6   = word ptr 0Ah
arg_8   = word ptr 0Ch
arg_A   = word ptr 0Eh
arg_C   = word ptr 10h

push    bp
mov     bp, sp
mov     ax, [bp+arg_A]
mov     dx, [bp+arg_C]
mov     bx, [bp+arg_6]
mov     cx, [bp+arg_8]
call    sub_B2 ; long 32-bit multiplication
mov     cx, [bp+arg_2]
add     ax, cx
mov     bx, [bp+arg_4]
adc     bx, dx      ; BX=high part, CX=low
```