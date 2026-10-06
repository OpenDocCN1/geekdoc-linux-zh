
of the display adapters identified by DisPID. This is good, but not enough: Each adapter has a name, a display buffer address, and a screen size dictated by the size of the current character font. These items comprise a table of information about a display adapter, and if you wanted to put together a summary of all that information about legal display adapters, you'd have to create such a table of tables.

Below is such a two-level table:

| DISPLAY ADAPTER INFORMATION LOOKUP TABLE |
| :--- |
| This is the lookup table containing information on all legal display adapters: The first field in each element is a 26-character string containing a brief description of the adapter. The next field is the segment of the video refresh buffer; the last three fields are the number of screen lines an adapter displays when the 8-pixel, 14-pixel, and 16-pixel fonts are loaded, respectively. Note that not all adapters support all fonts, a screen line count is given for all three fonts for all adapter types. Illegal combinations will not be accessed. |
| VidInfoTbl | No adapter identified | Code 0 |
| DW | 0B00H |
| DB | 25,25 |
| DB | 'Monochrome Display Adapter ' | Code 1 |
| DW | 0B00H |
| DB | 25,25 |
| DB | 'Color Graphics Adapter ' | Code 2 |
| DW | 0B00H |
| DB | 25,25 |
| DB | 'Code 3: Undefined ' | Code 3 |
| DW | 0B00H |
| DB | 25,25 |
| DB | 'EGA with color monitor ' | Code 4 |
| DW | 0B00H |
| DB | 43,25 |
| DB | 'EGA with mono monitor ' | Code 5 |
| DW | 0B00H |
| DB | 43,25 |
| DB | 'Code 6: Undefined ' | Code 6 |
| DW | 0B00H |
| DB | 25,25 |
| DB | 'VGA with mono monitor ' | Code 7 |
| DW | 0B00H |
| DB | 50,27 |
| DB | 'VGA with color monitor ' | Code 8 |
| DW | 0B00H |
| DB | 50,27,25 |

# ASSEMBLY LANGUAGE STEP-BY-STEP

```
DB    'Code 9: Undefined      ; Code 9
DW    0B00H
DB    25,25,25
DB    'MCGA with digital color  ; Code 0AH
DW    0B80H
DB    25,25,25
DB    'MCGA with monochrome      ; Code 0BH
DW    0B00H
DB    25,25,25
DB    'MCGA with analog color     ; Code 0CH
DW    0B80H
DB    25,25,25
```

The table consists of 12 subtables, one for each possible code returned by DispID as well as a subtitle for undefined codes. We're going to follow the same general strategy of indexing into the table based on the value of the code. In other words, to get the information for code 4, we have to look at the fifth table which requires tables 0 through 4 already exist. Code 3 is undefined, yet something must hold its place in the table for our indexing scheme to work.

Each subtitle occupies three lines, for clarity's sake. Here's a typical subtable:

```
DB    'EGA with color monitor    ; Code 4
DW    0B800H
DB    43,25,25
```

The first line is a 27-character quoted string containing the name of the display adapter. The second line is a word-sized address, the segment address of the visible display buffer corresponding to that name. The third line contains three numeric values. These are screen sizes, in lines, relating to the font sizes currently in force. The first value is the number of lines on the screen with the 8-pixel font in force. The second value is the number of lines on the screen with the 14-pixel font in force. The third value is the number of lines on the screen with the 16-pixel font in force. The items stored in the subtables give you just about everything you'd really need to know about a given display adapter to useful work with it. The character string is set to precisely 27 characters in length so that with the addition of the display buffer segment address and the three screen size values, the length of the whole table entry comes out to exactly 32 bytes.

When your assembly language programs begin executing, they should inspect such a table and extract the values pertinent to the currently installed display adapter. These extracted values should be ordinary variables in the data segment, easily accessible without further table searching. These variables should be defined together, as a block, with comments explaining how they are related:

+ ; DISPLAY INFORMATION VARIABLES
; The following block of variables all relate to the video
; system and are initialized by the VidCheck procedure:

| DispType DW 0 ; Code for display adapter type |
| VidSegment DW 0B00H ; Segment of installed display buffer |
| Origin DW 0 ; Offset for FAR pointer to refresh buffer |
| Visible DW 80 ; Number of columns on screen |
| YVisible DW 25 ; Number of lines on screen |
| VidBufSize ; Default to 25 X 80 X 2 (char & attribute) |
| FontSize DW 8 ; Either 8, 14, or 16; default to 8 |
| BordName DW 0 ; NEAR pointer to name of installed board |
| 18H = 24D; 4FH = 79D; Combined-0-base X, Y of 80 by 25 screen LR corner |
| LRXY 184FH |

As the indicates, a single routine named VidCheck returns values from the two-level lookup table VidInfoTbl loads those values into the variables in the preceding listing.

VidCheck is an interesting creature and demonstrates the way of dealing with two-level tables. Read it over carefully—again, this is as complex piece of code as you're going to see in this book:

+ ; VidCheck -- Identifies display board & display parameters
; Last update 9/18/99
; 1 entry point:
; VidCheck:
; Caller need pass no parameters;
; VidCheck identifies the installed display board by
 calling DispId. It then calculates numerous display
; information values, which it stores in the block
; of display information variables in the data segment:

```
VidCheck:
; First task is to figure out which board is on the bus:
 call DispId ; Ask BIOS for adapter code; returns in AL
 mov [DispType],AL ; Store display adapter code in DispType

; Next we determine the font size currently in force:
```

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
mov [FontSize], BYTE 14 ; MDA uses *only* 14-pixel font
jmp GetName ; jump ahead to look up adapter string
TryCGA: cmp [DispType], BYTE 02 ; Is the display adapter code, 2, for CGA?
jne TryVGA ; if not, go for EGA/VGA
mov [FontSize], BYTE 08 ; CGA uses *only* 8-pixel font
jmp GetName ; jump ahead to look up adapter string
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
mov DI, AX ; Copy AX (with code) into DI
mov CL, 5 ; We must shift the code 5 bits
shl DI, CL ; Multiply code by 32 to act as table index
mov BX, VidInfoTab ; Load address of origin table
mov [BoardName], BX ; Save pointer to info. in BoardName
add [BoardName], DI ; Add offset into table to right element
```

; we get the refresh buffer segment from the table:

```
mov AX, [BX+27] ; Index into table string to segment
mov [VidSegment], AX ; Store segment from table to VidSegment
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
```
