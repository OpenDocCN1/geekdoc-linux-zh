of multiple code segments within a single program. (The linker has the power to rearrange multiple code segments for reasons that I can't explain in this book.) Better to have no doubt about it, and for that reason you programmer should pick a starting point and tell the assembler what it is.

You may notice that leaving out ..start: won’t keep NASM from assembling a program, and while the linker will complain about the lack of a starting point, the linker will default to starting execution at the beginning of the code segment—which in our case is the only code segment, so there’s no ambiguity there.

Nonetheless, it’s bad practice to leave out the starting point label.

# Assembling and Linking EATSEG.ASM

Although NASM can generate a .COM file (for a real mode flat model program) directly, it can’t generate a .EXE file for a real mode segmented model program in the same way. Once you move away from a single segment in real mode flat model, NASM needs the help of a linker to generate the final .EXE file.

I’ve obtained permission to distribute an excellent free linker with this book’s CD-ROM. The linker is ALINK, written by Anthony Williams. It’s on the CD-ROM, and if you copied the executable file ALINK.EXE to your hard drive along with everything else, you can invoke it simply by naming it.

NASM-IDE was intended for writing programs in real mode flat model, so it relies exclusively on NASM and does not have any machinery for invoking a linker. That means NASM-IDE won’t be able to do the assemble and link tasks for us. It’s time to face the fiendish command line.

If you’re working from DOS you can simply assemble and link from the DOS command line. If you’re working with NASM-IDE in a DOS box under Windows, it’s probably easier to “shell out” to the DOS command line from inside NASM-IDE. This is done by selecting the menu item | DOS Shell. You will see NASM-IDE vanish and be replaced by a blank screen with the DOS prompt. When you’re done with the DOS shell, type EXIT followed by Enter to return to NASM-IDE.

Assembling EATSEG.ASM is done with the following command line:

```
C:\NASM16 EATSEG.ASM -f obj -o EATSEG.OBJ
```