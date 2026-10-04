```
000010A           one_case ; CODE XREF: f2+4
000010A               ADR R0, aOne ; jumpable 00000FA case
1
000010C 04 E0               B               loc_118
000010E\               loc_118
```

```
000010E           two_case ; CODE XREF: f2+4
000010E
000010E 8F A0   ADR R0, aTwo ; jumpable 00000FA case
2
0000110 02 E0               B               loc_118
```

```
0000112\           three_case ; CODE XREF: f2+4
0000112 90 A0   ADR R0, aThree ; jumpable 00000FA
case 3
0000114 00 E0               B               loc_118
```

```
0000116\           four_case ; CODE XREF: f2+4
0000116 91 A0   ADR R0, aFour ; jumpable 00000FA case
4
0000118\           loc_118 ; CODE XREF: f2+12
0000118                             ; f2+16
0000118 06 F0 6A 88   BL      _printf
000011C 10 BD               POP     [R4,PC]
```

```
000011E\           default_case ; CODE XREF: f2+4
000011E
000012E 82 A0   ADR R0, aSomethingUnkno ; jumpable
0000FA default case
0000120 FA E7               B               loc_118
```

```
000061D\           EXPORT _ARM_common_switch8_thumb
000061D
ARM_common_switch8_thumb ; CODE XREF:
example6_f2+4
000061D 78 47               BX      PC
00006D2 00 00               ALIGN 4
00006D2                             ; End of function _ARM_common_switch8_thumb
00006D2                             _32_ARM_common_switch8_thumb ; CODE
00006D4
XREF_ARM_common_switch8_thumb ;
00006D4 01 C0 5E 55   LDR     R12, [LR,-#1]
00006D6 00 53 23   CMP     R3, R12
00006DC 30 2E 27   LDRCB   R3, [LR,R12]
00006E0 03 30 27   LDRCC   R3, [LR,R3]
00006E4 43 80 8E E0   ADD     R12, LR,LSL#1
00006E8 1C FF 2F E1   BX      R12
00006E8\                             ; End of function
      _32_ARM_common_switch8_thumb
```