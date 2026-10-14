
| Mnem. | Operations | Description |
|---|---|---|
| `load Rd` | `ACC ← Rd` | Load the accumulator with the contents of RAM address Rd. d is an address in the range [0..15]. |
| `load #d` | `ACC ← d` | Load the accumulator with the value d. d is a value in the range [0..15]. |
| `store Rd` | `Rd ← ACC` | Store the value in the accumulator into RAM location Rd. d is an address in the range [0..15]. |
| `add Rd` | `ACC ← ACC + Rd + C; C ← carry out` | Add the contents of RAM address Rd and the C flag to the accumulator. d is an address in the range [0..15]. |
| `add #d` | `ACC ← ACC + d + C; C ← carry out` | Add the value d and the flag C to the accumulator. d is a value in the range [0..15]. |
| `xor Rd` | `ACC ← ACC$Rd` | Exclusive-OR the contents of RAM address Rd with the accumulator. d is an address in the range [0..15]. |
| `test Rd` | `Z ← ACC&Rd` | Set the Z flag if the logical-AND of RAM address Rd and the accumulator is zero. Otherwise, clear the Z flag. d is an address in the range [0..15]. |
| `clear_c` | `C ← 0` | Clear the C flag to zero. |
| `set_c` | `C ← 1` | Set the C flag to one. |
| `skip_c` | `PC ← PC + 1 + C` | If C = 1, skip the next instruction by incrementing the program counter by two instead of one. If C = 0, execute the next instruction. |
| `skip_z` | `PC ← PC + 1 + Z` | If Z = 1, skip the next instruction by incrementing the program counter by two instead of one. If Z = 0, execute the next instruction. |
| `jump #a` | `PC ← a` | Jump to program address a and execute instructions from that point. a is an address in the range [0..127]. |

3. If the multiplier bit is one, we need to be able to shift the multiplicand left by the appropriate number of positions and then add it to the sum.

A flowchart for performing a binary multiplication is shown in Figure 9.4. It starts by clearing the product register, which will hold the result of the multiplication when the program is finished. The mask RAM location is set to 0001 and will be used to test each bit of the multiplier to see if it is zero or one.

![](img/5124daf79d2807d81e49f49c22f1f8c1_332_0.png)

## Figure 9.4 A flowchart for binary multiplication of 4-bit numbers.

Next, the mask and the multiplier are logically ANDed together. This will determine if the least-significant bit of the multiplier is zero. If it is not zero, then the multiplicand is added to the product. If it is zero, then the addition is skipped.

Next, the multiplicand has to be multiplied by 2 to prepare it for the next time it is needed. Then the mask is multiplied by 2 so it now contains the value

0010. This value is not equal to zero, so the program execution loops back toward the beginning of the program.

Now the value 0010 is ANDed with the multiplier, thus testing the second bit of the multiplier to see if it is one or zero. If the bit is one, the multiplicand is added to the product again. But the multiplicand has already been multiplied by 2, thus shifting it left by one bit position. So we can see that as the program proceeds, the multiplicand will be shifted left each time through the loop. This shifting ensures that the correct number of zeros will be added onto the right end of the multiplier each time it is added to the product, just as we saw was needed in the example of binary multiplication.

Of course, the looping has to stop sometime, but when? For this program, the multiplier only has 4 bits so the loop should terminate after four iterations. This is handled at the bottom of the program when a test is made to see if the mask is zero. How can the mask ever equal zero if it starts at 1 and gets doubled every time through the loop? Shouldn't it keep progressing in the sequence 1, 2, 4, 8, 16, 32,...? Since the GNOME handles 4-bit values, when the mask reaches eight (1000) and gets doubled, the leftmost one falls off the end and the result is 0000. This happens after four doublings, which is the same thing as four iterations through the program. So the check for the mask being zero terminates the program at the correct point.

How can the operations shown in Figure 9.4 be performed by the GNOME? Let's start by assigning the various quantities in the flowchart (or variables) to registers:

| Register | Variable |
|---|---|
| R0 | multiplier |
| R1 | LSN of multiplicand |
| R2 | MSN of multiplicand |
| R3 | LSN of product |
| R4 | MSN of product |
| R5 | mask |

Notice that the product requires two 4-bit registers because multiplying the 4-bit multiplier and the 4-bit multiplicand can give an 8-bit result. Since the multiplicand has to be added to the 8-bit product, the multiplicand is also assigned to two 4-bit registers. The program that operates on the registers and arrives at the product is shown in Listing 9.1.

The various initialization steps for the multiplication program are performed on lines 1–11 in Listing 9.1. The instructions on lines 1–4 load the values to be multiplied into the multiplier and multiplicand registers, respectively. Lines
