that some of the jump instructions require one of two possible flag values in order to take the jump, while others require both of two flag values.

Several of the signed jumps compare two of the flags against one another. JG, for example, will jump when either ZF is 0, or when the Sign flag (SF) is equal to the Overflow flag (OF). I won't want any further time explaining the nature of the Sign flag or Overflow flag. As long as you have the sense of each instruction under your belt, understanding exactly how the instructions test the flags can wait until you've gained some programming experience.

Some people have trouble understanding how it is JE and JZ mnemonics are synonyms, as are JNE and JNZ. Think again of the way comparison is done within the CPU: The second operand is subtracted from the first, and if the result is 0 (indicating that the two operands were in fact), the Zero flag is set to 1. That's why JE and JZ are synonyms: Both are simply testing the state of the Zero flag.

# Detecting the Installed Display Adapter

A useful example of CMP detecting the installed display adapter. In the beginning of the 1990s, there were five different mainstream IBM display adapters in reasonably common use in PCs, from the first generation introduced with the original PC in 1981 to the VGA and MCGA introduced with the PS/2 series in 1987. Going into the twenty-first century, nearly all of those adapters except for the VGA are mostly extinct.

So, the code I'm about to show you is mostly a technical exercise, but if you work with older machines (and one reason to work in assembly is to create software that works quickly enough on older machines), it may be useful for sorting out what any given machine can do from a text video standpoint.

It isn't enough to know which board is installed in a given machine. The way a certain board operates can severely depending on whether a monochrome or color monitor is attached to the board. The most obvious difference (and the one of most interest to the programmer) is that memory address of the video display buffer is one address for the color monitor and a different address for the monochrome monitor. This schizophrenic quality of the EGA, VGA, and MCGA is so pronounced that it makes sense to consider the EGA/color monitor combination entirely