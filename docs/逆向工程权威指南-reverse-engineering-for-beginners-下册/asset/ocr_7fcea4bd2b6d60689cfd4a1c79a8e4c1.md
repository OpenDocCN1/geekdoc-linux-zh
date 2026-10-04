```
call    time_
mov     unix_time_low, ax
mov     unix_time_high, dx
mov     ax, offset unix_time_low
call    localtime_
mov     bx, ax
mov     t, ax                      ; will not be used
in future...

push    word ptr [bx]      ; seconds
push    word ptr [bx+2]      ; minutes
push    word ptr [bx+4]      ; hour
push    word ptr [bx+6]      ; day
push    word ptr [bx+8]      ; month
mov     ax, [bx+0Ah]         ; year
add     ax, 1900
push    ax
mov     ax, offset a04d02d002d002  ; "%04d-
%02d-%02d %02d:%02d:%02d"
push    ax
mov     ax, offset strbuf
push    ax
call    sprintf_
add     sp, 10h
xor     ax, ax               ; NULL
push    ax
push    ds
mov     ax, offset strbuf
push    ax
push    ds
mov     ax, offset aCaption  ; "caption"
push    ax
xor     ax, ax               ; MB_OK
push    ax
call    MESSAGEBOX
xor     ax, ax               ; return 0
pop     bp
retn    0Ah
```

虽然编译器保留了汇编宏的默认值指令，但是这个值实际上并没有被后续代码调用。由于编译器无法判断其他模块（文件）是否会访问这个值，因此所有的保留了有关的默认值语句。