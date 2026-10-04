```
push    OFFSET __except_handler
mov     eax, DWORD PTR fs:0
push    eax ; prev
add     ebx, -24
push    ebx
push    edi
mov     eax, DWORD PTR $$security_cookie ; xored pointer to table
xor     [esp+6], eax
xor     eax, ebp                               ; ebp ^ security_cookie
push    eax
lea     DWORD PTR $$SEHRec[esp+8]      ; pointer to
VC_EXCEPTION_REGISTRATION_RECORD
mov     DWORD PTR fs:0, eax
mov     DWORD PTR $$SEHRec[esp], esp
mov     DWORD PTR _p$[esp], 0
mov     DWORD PTR $$SEHRec[esp+20], 0 ; entering outer try block,
previous try level1=
mov     DWORD PTR $$SEHRec[esp+20], 1 ; entering inner try block, setting
previous try level1=
push    OFFSET $SG85497 ; 'hello!'
call    printf
add     esp, 4
push    0
push    0
push    0
push    1122867 ; 00112233
call    DWORD PTR __impimp_RaiseException@16
push    OFFSET $SG85499 ; '0x112233 raised. now let's crash'
call    printf
add     esp, 4
mov     eax, DWORD PTR _p$[esp]
mov     DWORD PTR [eax], 13
mov     DWORD PTR $$SEHRec[esp+20], 0 ; exiting inner try block,
previous try level1 back to 0
jmp     SHORT LN2@main
; inner block filter:
$LN128main:
$LN18main:
mov     ecx, DWORD PTR $$SEHRec[esp+4]
mov     edx, DWORD PTR [ecx]
mov     eax, DWORD PTR [edx]
mov     DWORD PTR $7j[eb], eax
cmp     DWORD PTR $7j[eb], -107374189 ; 0c000005H
jne     SHORT LN5@main
mov     DWORD PTR tv72[eb], 1
jmp     SHORT LN6@main
$LN5main:
mov     DWORD PTR tv72[eb], 0
$LN6@main:
mov     eax, DWORD PTR tv72[eb]
$LN14main:
$LN16main:
ret
0
; inner block handler:
$LN13main:
mov     esp, DWORD PTR $$SEHRec[esp]
```