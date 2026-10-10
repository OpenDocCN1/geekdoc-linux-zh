This is okay.

On the other hand the command may be coming from software that is using unsigned numbers. In this case the software sees the arithmetic that has just happened as

$$255 + 255 = 254.$$

This is not okay. The true answer, 510, has gone out of the one-byte unsigned range, 0-255. Hence the addition of FFH to FFH clears the overflow flag because the signed arithmetic answer is okay and sets the carry flag to notify software that there is an unsigned, out of range error.

As another example, suppose that one-byte registers receive a command to add 40H to 40H. The sum is 80H. If the above and below are used in place of the phrases greater than and less than. Hence the "jump if the arithmetic just done will appear as

$$64 + 64 = 128.$$

This is okay.

Suppose that the command has come from software working with signed numbers. Then the arithmetic looks like this:

$$64 + 64 = -128.$$

This is not okay. The true answer, +128, is outside the one-byte signed range, -128 to +127. The hardware sets the overflow flag because this is an out of range error in the signed number system, and clears the carry flag because there is no out of range error in the unsigned system. The hardware does not know which system the software is using, so it has to take care of both flags.

Both the carry and the overflow flags are out of range indicator flags. The carry flag is set if the arithmetic interpreted in the unsigned system has produced an out of range error. The overflow flag is set if the arithmetic interpreted in the signed system has produced an out of range error.

# ### 4.7.3 Still More Jump Commands

Given that we need a different command for "jump if less than" for use with unsigned numbers, we also need a different mnemonic. Moreover, considering all the other jump conditions, "greater than," "greater than or equal to," etc., we need a whole new set of commands and mnemonics. To systematize this new set, the words above and below are used in place of the phrases greater than and less than. Hence the "jump if less than" command which works for unsigned numbers uses the mnemonic $J_{B}$, for "jump if below." The full set of these commands is as follows:

```
JBE    below or equal         EAX = EBX
JA     above                  EAX > EBX
JAE    above or equal         EAX >= EBX
JNB    not below              EAX = EBX
JNBE   not below or equal     EAX ? EBX
JNA    not above              EAX ? EBX
JNAE   not above or equal     EAX ? EBX
```

# ## 4.8 Linux .s files

One of the intermediate steps that gcc uses in the translation of a C source program into an a.out file is an