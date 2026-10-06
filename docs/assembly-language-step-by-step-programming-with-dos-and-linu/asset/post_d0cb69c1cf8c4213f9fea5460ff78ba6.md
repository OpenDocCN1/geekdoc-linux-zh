
tion. In the preceding example, Jump if Less or Equal to is logically identical to Jump if Not Greater. (Think about it!) If the importance of the preceding compare was to see if one value is less than equal to another, you'd use the JLE mnemonic. On the other hand, if you were testing to be sure one quantity was not greater than another, you'd use JNG. The choice is yours.

Another complication is that there is a separate set of instructions for signed and unsigned comparisons. I haven't spoken much about assembly language in this book, and thus haven't said much about the difference between signed and unsigned quantities. A signed quantity is one in which the high bit of the quantity is considered a built-in flag indicating whether the quantity is negative. If that bit is 1, the quantity is considered positive.

Signed arithmetic in assembly language is complex and subtle, and not as useful as you might immediately think. I won't be covering it in detail in this book, though most assembly language books treat it to some extent. All you need to know is a high-level understanding of signed arithmetic is that in signed arithmetic, negative quantities are legal. Unsigned arithmetic, on the other hand, does not recognize negative numbers.

## Greater Than versus Above

To tell the signed jumps apart from unsigned jumps, the mnemonics use two different expressions for the relationships between two values:

- Signed values are thought of as being greater than or less than. For example, to test whether one signed operand is greater than another, you would use the JG (Jump if Greater) mnemonic after a CMP instruction.

- Unsigned values are thought of as being above or below. For example, to tell whether one unsigned operand is greater than (above) another, you would use the JA (Jump if Above) mnemonic after a CMP instruction.

Table 10.6 summarizes the arithmetic jump mnemonics and their synonyms. Any mnemonics containing the words above or below are for unsigned values, while any mnemonics containing the words greater or less are for signed values. Compare the mnemonics with their synonyms and see how the two represent opposite viewpoints from which to look at identical instructions.

## Table 10.6 Arithmetic Jump Mnemonics and Their Synonyms

| MNEMONICS | SYNONYMS |
| --- | --- |
| JA Jump If Above | JNBE Jump If Not Below or Equal |
| JAE Jump If Above or Equal | JNB Jump If Not Below |
| JB Jump If Below | JNAE Jump If Not Above or Equal |
| JBE Jump If Below or Equal | JNA Jump If Not Above |
| JE Jump If Equal | JZ Jump If Result is Zero |
| JNE Jump If Not Equal | JNZ Jump If Result is Not Zero |
| JG Jump If Greater | JNLE Jump If Not Than or Equal |
| JGE Jump If Greater or Equal | JNL Jump If Not Less |
| JL Jump If Less | JNGE Jump If Not Greater or Equal |
| JLE Jump If Less or Equal | JNG Jump If Not Greater |

Table 10.6 simply serves to expand the mnemonics into a morehensible form and associate a mnemonic with its synonym. Table 10.7, on the other hand, sorts the mnemonics out by logical condition and according to their use used with signed and unsigned values. Also listed in Table 10.7 are the flags whose values are considered in each jump instruction. Notice

## Table 10.7 Arithmetic Tests Useful After a CMP Instruction

| CONDITION | PASCAL OPERATOR | UNSIGNED VALUES | JUMPS WHEN | SIGNED VALUES | JUMPS WHEN |
| --- | --- | --- | --- | --- | --- |
| Equal | = | JE | ZF=1 | JE | ZF=1 |
| Not Equal | <> | JNE | ZF=0 | JNE | ZF=0 |
| Greater than | | JA | CF=0 | JG | ZF=0 |
| Less than or equal to | | JNBE | ZF=0 | JNLE | SF=OF |
| Less than | | JB | CF=1 | JL | SF<>OF |
| Not Greater than equal to | | JNAE | | JNGE | |
| Greater than or equal to | >= | JAE | CF=0 | JGE | SF=OF |
| Not Less | | JNB | | JNL | |
| | <= | JBE | CF=1 or ZF=1 | JLE | ZF=1 and SF<>OF |
| Not Greater than | | JNA | | JNG |

some of the jump instructions require one of two flag values in order to take the jump, while others require both of two flags. Some of the signed jumps compare two of the flags against another. JG, for example, will jump when either ZF is 0, or when the Sign flag (SF) is equal to the Overflow flag (OF). I won't want any further time explaining the nature of the Sign flag or Overflow flag. As long as you have the sense of each instruction under your belt, understanding how the flags can wait until you've gained some programming experience. Some people have trouble understanding how JE and JZ are synonyms, as are JNE and JNZ. Think again of the way comparison is done within the CPU: the second operand is subtracted from the first, and if the result is 0 (indicating the two operands were equal), the Zero flag is set to 1. That's why JE and JZ are synonyms: Both are simply testing the state of the Zero flag.

## Detecting the Installed Adapter

A useful example of CMP detecting the installed adapter. In the beginning of the 1980s, there were five different mainstream display adapters in reasonably use in PCs, from the first generation introduced with the original PC in 1981 to the VGA and MCGA introduced with the PS/2 series in 1987. Going into the twenty-first century, nearly all of those except for the VGA are mostly extinct. So the code I'm about to show you is mostly a technical exercise, but if you work with older machines (and one reason to work in assembly is that it may be useful for sorting out what any given machine can do from a text standpoint), it isn't enough to know which board is installed in a given machine. The way a certain board operates depends on whether a monochrome or color monitor is attached. The most obvious difference (and the one of most interest to the programmer) is that the memory address of the display buffer is one for the color monitor and a different address for the monochrome monitor. This quality of EGA, VGA, and MCGA is so pronounced that it makes sense to consider the EGA/color monitor combination entirely separate from the EGA/monochrome combination, and ditto from the VGA. In my method, I use a separate numeric code to represent each legal adapter/monitor combination. There are nine possibilities in all, summarized in Table 10.8. The codes are not consecutive; note that there is no code 3, 6, or 9. I didn't make these codes arbitrarily. They are, in fact, the display adapter/monitor combination codes returned by one of the BIOS services. The procedure DispID given in the following listing determines which display adapter is installed in the machine upon DisplayID returning one of the codes listed in Table 10.8. I recommend that your programs define a byte-sized variable in their data segments where this code can be stored throughout the duration. If you detect the adapter with DisplayID immediately on program startup, your program can inspect the code it needs to make a decision as to which video features to use.

## Table 10.8 Legal PC Display Adapter/Monitor Combinations

| CODE | ADAPTER/MONITOR | SEGMENT OF DISPLAY BUFFER |
| --- | --- | --- |
| 00 | None | None |
| 01H | MDA/monochrome | 0B00H |
| 02H | CGA/color | 0B00H |
| 04H | EGA/color | 0B00H |
| 05H | EGA/monochrome | 0B00H |
| 07H | VGA/monochrome | 0B00H |
| 08H | VGA/color | 0B00H |
| 0AH | MCGA/color (digital) | 0B00H |
| 0BH | MCGA/monochrome | 0B00H |
| 0CH | MCGA/color (analog) | 0B00H |

## Bits, Flags, Branches, and Tables

```assembly
; DispID - Identifies the installed display adapter
; Last update 9/18/89

; 1 entry point:

; DispID:
; Caller passes no parameters
; Routine returns a code value in AX.
; The codes are these:
; 0 : Adapter is unknown; recommend aborting
; 1 : MDA (Monochrome Display Adapter)
; 2 : CGA (Color Graphics Adapter)
```

```assembly
DispID:
mov AH,1H       ; Select PS/2 Identify Adapter Service
xor AX, AL      ; Select Get Combination Code Subservice (AL=0)
int 10H         ; Call Video
cmp AL,1AH      ; If AL comes back with 1AH, we have a PS/2
jne TryEGA       ; If not, jump down to test for the EGA
mov AL, BL      ; Put Combination Code into AL
ret             ; and go home!
TryEGA: mov AH,12H; Select EGA Alternate Function
mov BX,10H      ; Select Get Configuration Information service
int 10H         ; Call Video
cmp BX,10H      ; If BX comes back unchanged, EGA is 'not' there
je OldBorders   ; Go see whether it's an MDA or CGA
```

```assembly
OldBorders:
int 11H         ; Call Equipment Configuration interrupt
and AL,30H      ; Mask out all but bits 4 & 5
cmp AL,30H      ; If bits 4 & 5 are not =1, it's an MDA
jne CGA          ; otherwise it's a CGA
mov AL,1        ; Store code 1 for MDA
ret             ; and go home!
CGA:
mov AL,2        ; Store code 2 for CGA
ret             ; and go home!
```

DispID is the most complex piece of code shown so far in this book. The overall strategy is not obvious and warrants some attention.
