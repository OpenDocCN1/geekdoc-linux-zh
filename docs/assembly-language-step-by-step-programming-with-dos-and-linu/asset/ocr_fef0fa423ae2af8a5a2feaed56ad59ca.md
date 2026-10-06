# Bits, Flags, Branches, and Tables

One minor caution: the instruction SHR DI,4 does not exist on the 8086 and 8088 CPUs. Prior to the 286, you could provide any immediate operand to the shift instructions except for 1. Now, any immediate value that may be expressed in 8 bits may be used as the shift count operand. You have to be able to run on any x86 CPU, replace SHR DI,4 with four SHR DI,1 instructions. It's a good idea to flag any use of instructions that do not exist on early CPUs in your source code. While it's true that there are damned old chips 8088s and 8086s left out there, there are a few, and the reaction of old chips to undefined instructions is always a crapshoot and may produce some crazy bugs.

Finally, there is the matter of storing the digit into the target string DS:SI. Notice that this time, there is no +1 in the MOV instruction:

```
MOV [SI],AH
```

Why not? The high nibble is the digit on the left, so it must be moved into the first byte of the target string. Earlier, we moved the low nibble into the byte on the right. String indexing begins at the left and works toward the right, so if the left digit is index 0 of the string, the right digit must be at index 0+1.

ByteStr does a fair amount of data fiddling in only a few lines. Read it over a few times while following the preceding discussion through its course until the whole thing makes sense to you.

# Converting Words to Their String Form

Having converted a byte-sized value to a string, it's a snap to convert 16-bit words to their string forms. In fact, it's not much more difficult than calling ByteStr... twice:

```
; WordStr -- Converts a word passed in AX to a string
; DS:SI
; Last update 9/18/99
; 1 entry point:
```

```
; WordStr:
; Caller must pass:
; AX : Word to be converted
; DS : Segment of destination string
; SI : Offset of destination string
```