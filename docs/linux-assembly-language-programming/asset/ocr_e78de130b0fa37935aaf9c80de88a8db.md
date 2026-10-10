instruction. It means

let destination = destination + source + carry flag

whereas the ordinary ADD instruction means

let destination = destination + source

The addition can then be carried out in two stages, the first one using ADD and the next one using ADC.

![](bbox=[0.06, 0.2, 0.9, 0.32])

In order for the carrying to work, it is important that nothing disturb the carry flag between the low order addition and the high order addition. The following code does this arithmetic using the eight bytes starting at 100H as the destination and the eight bytes starting at 108H as the source. When this program finishes, the

# **Program 6.2**

```
; 8 byte Destination at 100H
; 8 byte Source at 108H
MOV EAX, [108H] ; Bottom 4 Source bytes
ADD [100H], EAX ; Add to bottom 4 Destination bytes
MOV EAX, [10CH] ; Top 4 Source bytes
ADC [104H], EAX ; Add to top 4 Destination bytes
```

eight-byte sum is located in the eight bytes starting at the address 100H. When the ADC instruction finishes, the overflow, carry, and sign flags will be correct for eight-byte arithmetic. The zero flag does not work so well for eight bytes. When set, it need not indicate that the eight-byte sum is 0.

# **Powers of 3**

Expanding on this idea, we can code a little 64-bit power of 3 calculator using the following algorithm:

Initialize y = 3

Then repeat:

x = y

y = y + x

y = y + x

Program 6.3 has no input or output. It can be observed by stepping through it in Edlinas. The [imm] format is useful in referring to a few fixed locations in memory. It is not useful in processing a long succession of bytes in memory.

# **Program 6.3**

```
; Edlinas program which finds 64-bit powers of 3.
; Store the 8 bytes of x starting at memory address 100H.
; Store the 4 least significant bytes of y in EAX.
; Store the 4 most significant bytes of y in EBX.
;
; y = 3
```