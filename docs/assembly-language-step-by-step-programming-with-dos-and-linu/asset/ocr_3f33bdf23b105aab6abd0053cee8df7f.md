Given these AX = 01234H
initial register BX = 04BA7H
values: CX = 0FF17H
DX = 034E0H

After...

PUSH AX PUSH BX PUSH CX POP DX

| | | | |
|---|---|---|---||
| 12 | 12 | 12 | 12 |
| 34 | SP | 34 | 34 |
| | | 4B | 4B |
| | | A7 | SP | A7 | SP |
| | | | FF |
| | | | 17 | SP |

High Memory Low Memory

= free stack space DX now contains 0FF17H

Figure 8.2 How the stack works.

Its least significant byte is at SS:SP, and its most significant byte is at SS:SP+1. (Remember that both bytes are pushed onto the stack at once, as a unit!)

Each time one of the registers is pushed onto the stack, SP is decremented two bytes down toward SS. The first three columns show AX, BX, and CX being pushed onto the stack, respectively. But note what happens in the fourth column, when the instruction POP DX is