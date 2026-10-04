```
.text:005410F3
.text:005410F3 loc_5410F3:      ; CODE
XREF: rotate2+25
.text:005410F3      push esi       ;
loop2
.text:005410F4      push edi       ;
loop1
.text:005410F5      push ebp       ;
arg_0
.text:005410F6      call get_bit
.text:005410FB      add esp, 0Ch
.text:005410FE      mov [ebx+esi], al ;
store to internal array
.text:00541101      inc esi       ;
increment loop1 counter
.text:00541102      cmp esi, 8
.text:00541105      jl short loc_5410F3
.text:00541107      inc edi       ;
increment loop2 counter
.text:00541108      add ebx, 8    ;
.text:0054110B      cmp edi, 8    ;
.text:0054110E      jl short loc_5410F1
.text:00541110      lea ebx, [esp+0x50-internal_array_64]
.text:00541114      mov edi, 7 ; loop1 counter
is is initial state 7
.text:00541119
.text:00541119 loc_541119:    ; CODE
XREF: rotate2+57
.text:00541119      xor esi, esi ; loop2
counter
.text:0054111B      mov al, [ebx+esi] ; get
.text:0054111B loc_54111B:    ; CODE
XREF: rotate2+4E
.text:0054111B      byte from internal array
.text:0054111E      push eax       ;
.text:0054111F      push edi       ; loop1
counter
.text:00541120      push esi       ; loop2
counter
.text:00541121      push ebp       ; arg_0
.text:00541122      call set_bit
.text:00541127      add esp, 10h
.text:0054112A      inc esi       ;
increment loop2 counter
.text:0054112B      cmp esi, 8
.text:0054112E      jl short loc_54111B
```