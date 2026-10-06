# ASSEMBLY LANGUAGE STEP-BY-STEP

```
DB 'Color Graphics Adapter ; Code 2
DW 0800H
DB 25,25
DB 'Code 3: Undefined ; Code 3
DW 0800H
DB 25,25
DB 'EGA with color monitor ; Code 4
DW 0800H
DB 43,25
DB 'EGA with mono monitor ; Code 5
DW 0800H
DB 43,25
DB 'Code 6: Undefined ; Code 6
DW 0800H
DB 25,25
DB 'VGA with mono monitor ; Code 7
DW 0800H
DB 50,27
DB 'VGA with color monitor ; Code 8
DW 0800H
DB 50,27
DB 'Code 9: Undefined ; Code 9
DW 0800H
DB 25,25
DB 'MCGA with digital color ; Code 0AH
DW 0800H
DB 25,25
DB 'MCGA with monochrome ; Code 0BH
DW 0800H
DB 25,25
DB 'MCGA with analog color ; Code 0CH
DW 0800H
DB 25,25
```

```
Digits DB '0123456789ABCDEF' ; Lookup table for numeric/string conv.
```

; These two variables are screen-clear "atoms" useable by
; Clear macro. The high byte is the display attribute, while
; the low byte is the character with Clear fills the
; video refresh buffer to clear the screen.

```
HToneAtom DW 07B0H ; Clears screen to halftone pattern
ClearAtom DW 0720H ; Clears screen to blanks
```

; This is where all predefined string variables are stored.

```
CRLF DB ODH,0AH ; Newline string
IDString DB '>>>INFO V2.0'
LIDString EQU $-LIDString
```