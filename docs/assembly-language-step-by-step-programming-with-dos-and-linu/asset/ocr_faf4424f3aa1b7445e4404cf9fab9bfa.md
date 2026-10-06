# ASSEMBLY LANGUAGE STEP-BY-STEP

handles all rigmarole for you. In assembly language, knowing where a variable is located is essential in order to do lots of important things.

# Making DOS Calls

What EAT.ASM really does, as I mentioned previously, is call DOS and instruct DOS to display a string at a particular place in memory. The string doesn't go anywhere; EAT.ASM tells DOS where the string is located, and then DOS reaches into your .data section and does what it must with the string data.

Calling DOS is done with something called a software interrupt. I explain these in detail later in this chapter. But if you look at the code you can get a sense of what's going on:

```
mov dx, eatmsg      ; Mem data ref without ; loads the ADDRESS!
mov ah,9           ; Function 9 displays text to standard output.
int 21H             ; INT 21H makes the call into DOS.
```

Here, the first line loads the address of the string into register DX. The second line loads the constant value 9 into register AH. The third line makes the interrupt call, to interrupt 21H.

The DOS call has certain requirements that be set up before the call is made. It must know which particular call you want to make, and each call has a 09H. This number must be placed in AH and, in this case, is call 09H (Display String). For this particular DOS call, DOS expects the address of the string to be displayed in register DX. If you satisfy those two conditions, you can make the DOS software inter-rupt INT 21H—and there's your string on the screen!

# Exiting the Program and Setting ERRORLEVEL

Finally, the job is done, Joe's been properly advertised, and it's time to let DOS have the machine back. Another DOS service, 4CH (Term-inate Process), handles the mechanics of courteously disentangling the machine from EAT.ASM's clutches. Term Process doesn't need the address of wishing, but it will take whatever value it finds in the AL register and place it in the ERRORLEVEL variable. DOS batch pro-grams can test the value of ERRORLEVEL and branch on it.

EAT.ASM doesn't do anything worth testing in a batch program, but if ERRORLEVEL will be set anyway, it's a good idea to provide some reli-