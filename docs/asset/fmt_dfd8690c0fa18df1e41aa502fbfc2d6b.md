
# Assembly Dump

```assembly
.text:00541040 set_bit

.text:00541040 endp
```

```assembly
.text:00541074      push ebp

.text:00541075      mov ebp, [esp+48h+arg_0]

.text:00541079      push esi

.text:0054107A      push edi

; EDI 是循环1计数器  xor edi, edi

.text:0054107D      lea ebx, [esp+50h+internal_array_64]

.text:00541081      first_loop1_begin:

; CODE XREF: rotate1+2E

.text:00541081      xor esi, esi

; E 是循环2计数器

.text:00541083      first_loop2_begin:

; CODE XREF: rotate1+25

.text:00541083      push ebp

; arg_0

.text:00541084      push esi

.text:00541085      push edi

.text:00541086      call get_bit

.text:0054108B      add esp, 0Ch

.text:0054108E      mov [ebx+esi], al ; 存储到内部数组  inc esi

.text:00541092      cmp esi, 8

.text:00541095      jl short first_loop2_begin

.text:00541097      inc edi

.text:00541098      add ebx, 8

.text:0054109B      cmp edi, 8

.text:0054109E      jl short first_loop1_begin

.text:005410A0      lea ebx, [esp+50h+internal_array_64]

.text:005410A4      mov edi, 7; EDI 是循环1计数器，初始状态为 7

.text:005410A9      second_loop1_begin: ; CODE XREF: rotate1+57

.text:005410A9      xor esi, esi ; ESI 是循环2计数器

.text:005410AB      second_loop2_begin: ; CODE XREF: rotate1+4E

.text:005410AB      mov al, [ebx+esi] ; 来自内部数组的值  push eax

.text:005410AE      push ebp      ; arg_0

.text:005410AF      push edi

.text:005410B1      push esi

.text:005410B2      call set_bit

.text:005410B7      add esp, 10h

.text:005410BA      inc       esi; 增循环2计数器

.text:005410BB      cmp esi, 8

.text:005410BE      jl short second_loop2_begin

.text:005410C0      dec       edi; 递循环2计数器

.text:005410C1      add ebx, 8

.text:005410C4      cmp edi, 0xFFFFFF

.text:005410C7      jg short second_loop1_begin

.text:005410C9      pop edi

.text:005410CA      pop esi

.text:005410CB      pop ebp

.text:005410CC      pop ebx

.text:005410CD      add esp, 40h

.text:005410D0      retn

.text:005410D0      rotate1 endp

.text:005410D1              align 10h

.text:005410E0      ; ========== SUBROUTINE ==========

.text:005410E0      rotate2 proc near      ; CODE XREF: rotate_all_with_password+7A

.text:005410E0      internal_array_64= byte ptr -40h

.text:005410E0      arg_0               dword ptr 4

.text:005410E0      sub esp, 40h

.text:005410E3      push esi

.text:005410E4      push ebx

.text:005410E5      push ebp

.text:005410E6      mov ebp, [esp+48h+arg_0]

.text:005410E9      push esi

.text:005410EA      push edi

.text:005410EB      xor esi, edi;循环1计数器

.text:005410ED      lea ebx, [esp+50h+internal_array_64]

.text:005410F1      loc_5410F1:      ; CODE XREF: rotate2+2E

.text:005410F1      xor esi, esi;循环2计数器

.text:005410F3      loc_5410F3:      ; CODE XREF: rotate2+25

.text:005410F3      push esi       ; loop2

.text:005410F4      push edi       ; loop1

.text:005410F5      push ebp       ; arg_0

.text:005410F6      call get_bit

.text:005410FB      add esp, 0Ch

.text:005410FE      mov [ebx+esi], al ; 存储到内部数组  inc esi;循环1计数器

.text:00541101      cmp esi, 8

.text:00541102      jl short_5410F3

.text:00541105      inc edi; 增循环2计数器

.text:00541107      add ebx, 8

.text:00541108      cmp edi, 8

.text:0054110B      jl short_5410F1

.text:0054110E      lea ebx, [esp+50h-internal_array_64]

.text:00541114      mov edi, 7 ; 循环1计数器初始状态为 7

.text:00541119      loc_541119:    ; CODE XREF: rotate2+57

.text:00541119      xor esi, esi ; 循环2计数器

.text:0054111B      mov al, [ebx+esi] ; 来自内部数组的值

.text:0054111B      loc_54111B:    ; CODE XREF: rotate2+4E

.text:0054111E      push eax       ; loop2

.text:0054111F      push edi       ; loop1

.text:00541120      push esi       ; loop2计数器

.text:00541122      call set_bit

.text:00541127      add esp, 10h

.text:0054112A      inc       esi; 增循环2计数器

.text:0054112B      cmp esi, 8

.text:0054112E      jl short_54111B

.text:00541130      dec       edi; 递循环2计数器

.text:00541131      add ebx, 8

.text:00541134      cmp edi, 0xFFFFFF

.text:00541137      jg short_541119

.text:00541139      pop edi
```
