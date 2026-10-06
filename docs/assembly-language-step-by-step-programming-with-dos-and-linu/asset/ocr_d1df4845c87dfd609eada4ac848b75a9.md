However, assuming you did what I told you earlier and typed some text at line 9 of EAT2.ASM, the screen will split horizontally and a new window will be displayed beneath the text window containing EAT2.ASM. This window has the title "Error Information" and will look a lot like Figure 5.4.

If you recall, you made a change to EAT2.ASM a little earlier by typing the phrase "MVO ax,bx" mnemonic—on line 9. This phrase is something like assembly language—only something, and in the form I gave it to the assembler NASM will have no idea what to do with it. So, NASM dutifully complained in the form of an error message. You can see this error message in Figure 5.4. When NASM tells you "Parser: Instruction Expected" that means what it got in the line it paused at was not an instruction. You inserted an error into EAT2.ASM here because no instruction in the 86-family instruction set is named MVO. This may not prevent your fevered fingers from transforming MOV (which is a legal instruction) to MVO in the furious passion of creation—or under the influence of the caffeine shocks.

The error information window will remain on the screen until you close it, which you can do by clicking on the close control at the upper-left corner of the window. And until you fix the error you inserted into EAT2.ASM, that's as far as we can go here.

Fixing it, however, is easy. NASM-IDE is reasonably smart and has placed the cursor right where it thinks the error is in the edit window.

![](bbox=[0.176, 0.65335, 0.905, 0.9312999999999999])

**Figure 5.4** The error information window appears.