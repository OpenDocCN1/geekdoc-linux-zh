```
.text:6440501A      mov [ebp+var_10], ebx
.text:6440501D bypass:
.text:6440501D      mov eax, [esi+20h]
.text:64405020      test eax, eax
.text:64405022      jz short loc 6440503A
.text:64405024      cmp dword ptr [ebp+28h], 0
.text:64405028      jz short loc 6440503A
.text:6440502A      push offset aDataDataRecordMode ; "data
record mode switched on\n"
.text:6440502F      mov ecx, edi
.text:64405031      call ds:mfc90_945
.text:64405037      mov [ebp+var_10], ebx
.text:6440503A      loc_6440503A:
.text:6440503A      mov ecx, edi
.text:6440503E      mov eax, ebx
.text:6440503C      cmp [ebp+var_10], ebx
.text: 6440503F      jnz loc 64405142
.text:64405045      push offset AMaximumData ;
\nFor maximum data security \
\t delete/nthe$
```

; demangled name: ATL::CString::operator+=(char *


```
.text:6440504A      call ds:mfc90_945
.text:64405050      xor edi, edi
.text:64405052      push edi                ; FWinIn
.text:64405053      lea eax, [ebp+varParam]; ; PvParam
.text:64405056      push eax
.text:64405057      push edi                ; uiParam
.text:64405058      push eax
.text: 5055                30h                     ; uiAction
.text:6440505A      call ds:SystemParametersInfoA
.text:64405060      mov eax, [ebp+var34]
.text:64405063      mov eax, 1600
.text:64405068      jne short loc 64405072
.text:6440506A      cdq
.text:6440506B      sub eax, edx
.text:6440506D      sar eax, 1
.text:6440506F      mov [ebp+var_34], eax
.text:64405072  loc_64405072:     push edi                ; HWnd
.text:64405072      mov [ebp+cy], 0A0h
.text:6440507A      call ds:GetDC
.text:64405080      mov [ebp+var_10], eax
.text:64405083      mov ebx, 12Ch
.text:64405088      cmp eax, edx
.text:6440508A      jz loc 64405113        ; i
.text:64405090      push 11h
.text:64405092      call ds:GetStockObject
```