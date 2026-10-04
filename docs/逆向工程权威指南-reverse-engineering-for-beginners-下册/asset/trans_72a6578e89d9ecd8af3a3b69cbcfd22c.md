

At this point, all FPU condition code flags are zero. The value that was just POPed has already been transferred to the ST(7) register. This chapter has introduced FPU registers and the data stack in section 5.1, so they will not be repeated here.

Then, execute the `FNSTSW` instruction, as shown in Figure 17.8.

Figure 17.8 OllyDbg: Executing the `FNSTSW` instruction

