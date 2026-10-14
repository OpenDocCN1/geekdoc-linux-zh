```
NET s1      LOC= P26;
NET s2      LOC= P24;
NET s3      LOC= P20;
NET s4      LOC= P23;
NET s5      LOC= P18;
NET s6      LOC= P19;
```

Once the design is compiled, you can download the GNOME1 microprocessor to the XS95 or XS40 Board. But what about a program for it to execute? That has to be loaded into the external RAM so GNOME can fetch instructions. Let's use the following addition program to test GNOME. The address and opcode for each instruction are listed in the two columns on the left.

```
0000 18   load #8     ; initialize the data registers
0001 30   store R0    ; with the numbers to be added
0002 14   load #4     ; we will do 0x29 + 0x48 = 0x71
0003 31   store R1
0004 19   load #9
0005 32   store R2
0006 12   load #2
0007 33   store R3
0008 00   clear_c     ; start carry flag with zero
0009 40   load R0     ; add the LSNs of each number and
000A 52   add  R2     ; also set carry for next addition
000B 34   store R4    ; store LSN of sum
000C 41   load R1
000D 53   add  R3     ; add MSNs of both numbers + carry
000E 35   store R5    ; store MSN of sum
loop:
000F 44   load R4     ; display LSN of sum
0010 45   load R5     ; display MSN of sum
0011 8F   jump #loop  ; display sum repetitively
```

The opcodes for the addition program can be stored in a file called ADD.HEX. The file contains a sequence of lines, each line beginning with a dash (-), the number of opcodes it contains, the beginning memory address at which to start placing the opcodes, and the list of opcodes. (All the numbers are in hexadecimal.) Here are the contents of the ADD.HEX file:

```
- 12 0000 18 30 14 31 19 32 12 33 00 40 52 34 41 53 35 44 45 8F
```

The first (and only) line of ADD.HEX says: "There are 18 opcodes in this line (0x12=18). Begin loading them into memory at address 0x0000=0. Here is the list of opcodes."

Now you can download the program and the GNOME microprocessor into the XS95 Board using the command: