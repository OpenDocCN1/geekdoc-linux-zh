# An Uneasy Alliance

The DOS DEBUG utility provides a handy window into the CPU's hidden world of registers. How DEBUG does this is theblack of all black arts and I can't explain it in an introductory text. For now, consider DEBUG a magic box. One thing to keep in mind is that DEBUG is a real mode creature. It doesn't work in protected mode. You can only use it while debugging real mode programs, whether segmented or flat model. Protected mode debuggers exist, but DEBUG isn't one of them.

Looking at the registers from DEBUG doesn't even require that you load a program into DEBUG. Simply run DEBUG, and at the dash prompt type the single-command R. The display will look something very close to this:

```
- R
AX=0000 BX=0000 CX=0000 DX=0000 SP=FFEE BP=0000 SI=0000 DI=0000
DS=1980 ES=1980 SS=1980 CS=0100 NV UP EI PL NZ NA PO NC
1980:0100 389A5409 CMP [BP+SI0954],BL SS:0954-8A
```

I say "something very close" because details of the display will vary depending on what resident programs you have loaded in memory, which version of DOS you're using, and so on. What will be the values listed as present in the various registers, and the machine instruction shown in the third line of the display (here, CMP [BP+SI+0954],BL).

What will not vary is the fact that every CPU register has its place in the display, along with its current value shown to the right of an equals sign. The characters "NV UP EI PL NZ NA PO NC" are a summary of the current values of the flags in flags register.

The preceding display is that of the registers when no program has been loaded. All of the general-purpose registers except SP have been set to 0, and all of the segment registers have been set to the value 1980H. These are the default conditions set up by DEBUG in the CPU when no program has been loaded.(The1980H value will probably be different for you—it represents the first available segment in memory above DOS, and that segment falls depends on what else exists in memory both above and below DOS.)

Changing a register is done very simply, again using DEBUG's R command. To change the value of AX, type R and press Enter:

```
- R
AX:0000
:0A7B
```