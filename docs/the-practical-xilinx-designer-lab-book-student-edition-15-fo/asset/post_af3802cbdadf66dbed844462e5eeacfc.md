
## Table 10.1 DWARF instruction set. (Cont’d.)

| Mnem. | Operations | Descriptions |
|---|---|---|
| test Rd | Z ← ACC&Rd | AND the contents of register Rd with the accumulator, but do not store the result in the accumulator. Instead, set the Z flag if the result is 0; otherwise clear the Z flag. d is an address in the range [0..7]. |
| clear_c | C ← 0 | Clear the C flag to zero. |
| set_c | C ← 1 | Set the C flag to one. |
| jc #a | IF C = 1 → PC ← a ELSE PC ← PC + 2 | If C = 1, branch to address a. If C = 0, continue to the next instruction. a is in the range [0..255]. |
| jz #a | IF Z = 1 → PC ← a ELSE PC ← PC + 2 | If Z = 1, branch to address a. If Z = 0, continue to the next instruction. a is in the range [0..255]. |
| jump #a | PC ← a | Unconditionally branch to address a. a is in the range [0..255]. |
| jsr #a | RAM[SP] ← PC + 2<br>SP ← SP + 1<br>PC ← a | Save the address of the next instruction on the stack and increment the stack pointer. Then jump to address a. a is in the range [0..255]. |
| ret | SP ← SP − 1<br>PC ← RAM[SP] | Decrement the stack pointer and load the PC with the address found on the top of the stack. |
| reti | SP ← SP − 1<br>ACC ← RAM[SP]<br>SP ← SP − 1<br>PC ← RAM[SP] | Decrement the stack pointer and load the ACC with the value found on the top of the stack. Then decrement the SP and load the PC with the address at which to resume execution of the noninterrupt program. |

The encodings of these instructions are shown in Table 10.2. The last three bits of the opcode are used to store the address of the internal register that is used by the instruction. (Some instructions do not operate on the registers, so these bits are not used.) The remaining five bits are used to distinguish one instruction from another. Note that the use of 8-bit data and addresses makes it necessary to store some of the instructions in two bytes instead of one.

The basic architecture for the DWARF is shown in Figure 10.2. You are already familiar with most of these basic components from the GNOME design such as the instruction decoder, program counter (PC), instruction register (IR), arithmetic logic unit (ALU), accumulator (ACC), and carry and zero flags (C and Z). The new components are as follows:

**Stack pointer (SP):** The stack pointer contains the address of a location in data memory where the PC and the ACC can be stored during subroutine calls and interrupts.

## Table 10.2 DWARF instruction set encoding.

| Mnem. | # Bytes | Encoding |
|---|---|---|
| load Rd | 1 | 00100 d2 d1 d0 |
| load (Rd) | 1 | 00101 d2 d1 d0 |
| load #d | 2 | 0100000 d7 d6 d5 d4 d3 d2 d1 d0 |
| load d | 2 | 0110000 d7 d6 d5 d4 d3 d2 d1 d0 |
| load (d) | 2 | 00111000 d7 d6 d5 d4 d3 d2 d1 d0 |
| store Rd | 1 | 00000 d2 d1 d0 |
| store (Rd) | 1 | 00001 d2 d1 d0 |
| store d | 2 | 00010000 d7 d6 d5 d4 d3 d2 d1 d0 |
| store (d) | 2 | 00011000 d7 d6 d5 d4 d3 d2 d1 d0 |
| in Rd | 1 | 01100 d2 d1 d0 |
| out | 1 | 01101000 |
| xor Rd | 1 | 10000 d2 d1 d0 |
| add Rd | 1 | 10001 d2 d1 d0 |
| test Rd | 1 | 10010 d2 d1 d0 |
| clear_c | 1 | 10100000 |
| set_c | 1 | 10101000 |
| jc #a | 2 | 1100000 a7 a6 a5 a4 a3 a2 a1 a0 |
| jz #a | 2 | 11010000 a7 a6 a5 a4 a3 a2 a1 a0 |
| jump #a | 2 | 11010000 a7 a6 a5 a4 a3 a2 a1 a0 |
| jsr #a | 2 | 11011000 a7 a6 a5 a4 a3 a2 a1 a0 |
| ret | 1 | 11100000 |
| reti | 1 | 11101000 |

Register set (R0–R7): DWARF has 16 internal registers for holding data values. Eight of these are available for normal use, and the other eight are used during interrupts. The register set is built from a dual-port memory with two 8-bit outputs (A_OUT and B_OUT) and a single 8-bit input (A_IN). This lets the register set output two values and overwrite one of them in a single clock cycle.

I/O port (IOP): DWARF has eight output pins and eight input pins dedicated to general-purpose input/output.

Address selector: DWARF divides the external memory into three regions: PROGRAM (256 bytes), DATA (256 bytes), and STACK (256 bytes). The address selector enables one of these regions and sends it an
