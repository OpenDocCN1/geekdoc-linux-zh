# ASSEMBLY LANGUAGE STEP-BY-STEP

```
cmp AL, 0AH ; see if board is a MCGA
jtl Try0 ; if less than OAH, it's not an MCGA
mov [FontSize], BYTE 16 ; MCGA supports *only* 16 pixel text font
jmp GetName ; jump ahead to look up adapter name string
```

```
Try: cmp [DispType], BYTE 01 ; Is the display adapter code, 1, for MDA?
jne TryCGA ; if not, go test for CGA code 2
mov [FontSize], BYTE 14 ; MDA uses *only 14-pixel text font
jmp GetName ; jump ahead to look up adapter name string
TryCGA: cmp [DispType], BYTE 02 ; Is the display adapter code 2, for CGA?
jne TryVGA ; if not, go for EGA/VGA size font
mov [FontSize], BYTE 08 ; CGA uses *only* 8-pixel text font
jmp GetName ; jump ahead to look up adapter name string
```

```
TryVGA: mov AH, 11H ; requires AH =11H and AL = 30H
mov AL, 30H ; 0 = Get info about current font
mov BH, 0
int 10H ; Call Video
mov [FontSize], CL ; Font size in pixels is returned in CL
```

; we get the name string for the board from the info table:

```
GetName:
mov AL, [DispType] ; Load adapter code into AL
xor AH, AH ; Zero so we don't copy info into DI
mov DI, AX ; Copy AX (with code AL) into DI
mov CL, 5 ; We must shift the code 5 bits to mult. by 32
shl DI, CL ; Multiply code by 32 to act as table index
mov BX, VidInfoTab ; Load address of origin table in BX
mov [BoardName], BX ; Save pointer to info table. in BoardName
add [BoardName], DI ; Add offset into table to right element
```

; we get the refresh buffer segment from the table:

```
mov AX, [BX+27] ; Index into table name string to segment
mov [VidSegment], AX ; Store segment from table to VidSegment variable
```

; we calculate the number of lines on-screen from font size:

```
xor AH, AH ; Make sure AH has no trash in it
mov AL, [FontSize] ; Load the font size in pixels into AL
cmp AL, 8 ; Is it the 8-pixel font?
jmp Try14 ; If not, the 14-pixel font
mov AL, 1 ; The 8-pixel font is table offset
jmp ReadLines ; Jump ahead to read screen lines from table
```

```
Try14: cmp AL, 14 ; Is it the 16-pixel font
mov AL, 2 ; The 14-pixel font is table offset 2
jmp ReadLines ; Jump ahead to read screen lines from table
mov AL, 3 ; The 16-pixel font is table offset 3
```

```
D16: add DI, AX ; Add font size to table element offset
mov AL, [BX+28] ; Load the screen lines value from the table
mov [VisibleY], AL ; and store it in the VisibleY
mov AH, [VisibleX] ; Load the screen columns value to AH
```