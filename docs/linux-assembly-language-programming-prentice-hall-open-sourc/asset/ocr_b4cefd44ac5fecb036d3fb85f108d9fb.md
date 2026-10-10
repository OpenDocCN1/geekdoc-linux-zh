```
IN AL, [61H]
OR AL, 3
OUT [61H], AL
```

To turn them off,

```
IN AL, [61H]
AND AL, 0FCH
OUT [61H], AL
```

will do.

It should be noted that in Linux, access to I/O ports by users is, by default at least, prohibited. I/O permissions can be given to a process, however, by the system calls ioperm() and iopl(), which are specially adapted to the x86 architecture.

# 10.3.2 Edge vs. Level Triggered IRQ Bits

The 8259 programmable interrupt controller discussed in chapter 9, section 9.2 has a register which determines whether the interrupts it receives will be processed as edge-triggered or level-triggered. There is one bit for each of the eight IRQ lines that it handles. The difference between the two triggering modes is important. If an I/O device uses level-triggered signaling and the 8259 treats its IRQ as edge-triggered, then interrupt signals from the I/O device could be ignored. By using bit manipulation commands, it is possible to single out one bit on this register and change it.

For example, suppose that we are installing a card which sends out edge-triggered interrupt requests on IRQ4. (IRQ4 is the request line conventionally associated with COM1.) On an EISA machine the register which controls this triggering is located at I/O port 4D0H. It is called an ELCR (Edge/Level Control Register). Each 0 bit makes the corresponding IRQ line edge-triggered; each 1 bit causes level triggering. The simplest way to make IRQ4 edge triggered would be to write a 0 to this port.

```
MOV AL, 0
MOV EDX, 4D0H ; ELCR's address is 4D0H.
OUT [DX], AL ; Store a zero in the ELCR.
```

But this would be a bad idea. It would make all eight bits in the ELCR 0. Any of the IRQs which happened to use level triggering would get fouled up. To set them all correctly, we must know what all the triggerings are for all eight inputs, or we can just leave them as they are except for the fourth bit. To make bit 4 zero, we can OR the contents of the ELCR with the binary number 1110 1111 = E FH. To do that we need to read from the ELCR, do the masking, and then write back to it.

Program 10.1

```
MOV EDX, 4D0H ; ELCR's address is 4D0H.
IN AL, [DX] ; Read the ELCR register.
AND AL, 0EFH ; Mask out bit 4.
OUT [DX], AL ; Write altered byte back out to the ELCR.
```

# 10.3.3 Disallowing Non—maskable Interrupts

On ISA machines, non—maskable interrupts can be stopped before they get to the processor. They run through a gate which is controlled by bit 7 of an I/O register located at port 70H. If this bit is 0, NMI s are allowed. Memory problems can cause a nonmaskable interrupt to occur. Suppose that we want to circumvent this safeguard by shutting off NMI s. To make bit 7 equal to 1 we can OR the contents of the I/O register with 1000 0000 = 80H.

Program 10.2

```
IN AL, [70H] ; Read the byte.
```