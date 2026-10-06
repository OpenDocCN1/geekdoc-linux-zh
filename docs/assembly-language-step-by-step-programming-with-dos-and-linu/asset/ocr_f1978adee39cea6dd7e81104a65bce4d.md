# Bits, Flags, Branches, and Tables 365

ret ; and go home!

OldBords:

```
int 11H ; Call Equipment Configuration interrupt
and AL, 30H ; Mask out all but bits 4 & 5
cmp AL, 30H ; If bits 4 & 5 are both =1, it's an MDA
jne CGA ; otherwise it's a CGA
mov AL, 1 ; Store code 1 for MDA
ret ; and go home!
CGA:
mov AL, 2 ; Store code 2 for CGA
ret ; and go home!
```

[SECTION .data]

; DISPLAY INFORMATION VARIABLES
; The following block of variables all relate to the video
; system and are initialized by the VidCheck procedure:

DispType DB 0 ; Code for display adapter type
VidSegment DW 0B00H ; Segment of installed display buffer
VidOrigin DW 0 ; Offset for FAR pointer to refresh buffer
Visible DB 80 ; Number of columns on screen
Visible DB 25 ; Number of lines on screen
VidBufSize DW 4000 ; Default to 25 X 80 X 2 (char & attribute)
FontSize DB 8 ; Either 8, 14, or 16; default to 8
BoardName DW 0 ; NEAR pointer to name string of installed board
X,Y of 80 x 25 screen LR corner:
LRXY DW 14FH

; DISPLAY INFORMATION LOOKUP TABLE
; This is the lookup table containing information on all legal
; display adapters. The first field in each element is a 26-
; character string containing a brief description of the
; adapter. The next field is the segment of the video refresh
; buffer. The last three fields are the number of screen lines
; an adapter displays the 8-pixel, 14-pixel, and 16-pixel
; fonts are loaded, respectively. Note that not all adapters
; support all fonts, but a screen line count is given for all
; three fonts for all adapter types. Illegal combinations will
; not be accessed.

VidInfoTbl DW 'No adapter identified' ; Code 0
DW 0B00H
DB 25,25
DB 'Monochrome Display Adapter ' ; Code 1
DW 0B00H
DB 25,25