| . | . |
| --- | --- |
| .text:0002B1F | push offset aDevRbs1 ; char * |
| .text:0002B24 | call _access |
| .text:0002B29 | add esp, 14h |
| .text:0002B2C | cmp eax, 0xFFFFFF |
| .text:0002B31 | jz short loc_22B48 |
| .text:0002B33 | lea eax, [ebx+7] |
| .text:0002B36 | push eax |
| .text:0002B37 | lea eax, [ebp+var_44] |
| .text:0002B3A | push offset aDevRbs1D ; "/dev/rbs1d" |
| .text:0002B3F | push eax |
| .text:0002B40 | call nl_sprintf |
| .text:0002B45 | add esp, 0Ch |
| .text:0002B48 | loc_22B48; CODE XREF: SSQC+79j |
| .text:0002B48 | mov edx, edi |
| .text:0002B4A | test edx, edx |
| .text:0002B4C | jle short loc_22b57 |
| .text:0002B4E | push eax ; int |
| .text:0002B4F | call _close |
| .text:0002B54 | add esp, 4 |
| .text:0002B57 | |
| .text:0002B57 | loc_22B57; CODE XREF: SSQC+94j ; int |
| .text:0002B59 | push 2 |
| .text:0002B59 | lea eax, [ebp+var_44] ; char * |
| .text:0002B5C | push eax |
| .text:0002B5D | call _open |
| .text:0002B62 | add esp, 8 |
| .text:0002B65 | test eax, eax |
| .text:0002B67 | mov [edx], eax |
| .text:0002B69 | jge short loc_22B78 |
| .text:0002B6B | loc_22B6B; CODE XREF: SSQC+47j |
| .text:0002B6B | mov edx, 0xFFFFFFFF |
| .text:0002B70 | pop eax |
| .text:0002B71 | pop esi |
| .text:0002B72 | pop edi |
| .text:0002B73 | mov esp,ebp |
| .text:0002B75 | pop ebp |
| .text:0002B76 | retn |
| .text:0002B78 | loc_22B78; CODE XREF: SSQC+B1j |
| .text:0002B78 | pop eax |
| .text:0002B79 | pop esi |
| .text:0002B7A | pop edi |
| .text:0002B7B | xor eax, eax |
| .text:0002B7D | mov esp, ebp |
| .text:0002B7F | pop ebp |
| .text:0002B80 | retn |