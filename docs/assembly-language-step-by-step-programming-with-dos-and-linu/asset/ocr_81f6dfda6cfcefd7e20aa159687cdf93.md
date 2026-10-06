# Bit # Flags, Branches, and Tables

| Bit # | |
|---|---|
| 0 | = 1 if one or more diskette drives exist |
| 1 | = 1 if a math coprocessor is installed |
| Bit #2 = 1 if PS/2 mouse is installed! | 2 0 1 0 1 RAM on main
| | = 16K = 32K = 48K = 64K board for old
| | 3 0 0 1 1 PCs & PCjr |
| 4 | Boot-up video configuration; see details below |
| 5 | |
| 6 0 1 0 1 Number of
| 7 =1 =2 =3 =4 installed
| | 0 0 1 1 diskette drives |
| 8 | Undefined |
| 9 | |
| 10 | Number of RS232 serial ports installed
(expressed as a binary number) |
| 11 | |
| 12 | = 1 if joystick controller installed |
| Bit #13 = 1 if serial printer is on PCjr! | 13 | = 1 if internal modem installed (PC & XT) |
| 14 | |
| 15 | Number of printers installed
(expressed as a binary number) |

**Figure 10.5** Interrupt 11H configuration information.

you get 0. (Look it up in Table 10.2, the AND true table.) And if all bitwise AND operations come up 0, the result is 0, and the Zero flag is raised to 1, indicating that the result is 0.

Key to understanding **TEST** is thinking of **TEST** as a sort of Phantom of the Opcode, where the Opcode is **AND**. **TEST** pretends it is **AND**, but