```
chat:
		ELF 32-bit LSB executable i386 (386 and up)
Version 1
pppd:
		ELF 32-bit LSB executable i386 (386 and up)
Version 1
```

# CONFIGURING PPP

Now, you're going to need to configure PPP. You'll need to run `/usr/sbin/`*`pppsetup`*. This section walks you through everything involved. When you enter the phone number, you'll need to enter your AT command before it so the modem recognizes it should dial. This is modem-specific (mine takes ATDT). Consult your modem manual for the specifics of your AT Commands.

For example, I would enter `ATDT8788888` to get it to dial. (See Figure 11-11.)

> The comma before the phone number means that the modem waits for another dial tone.

![](bbox=[0.05, 0.43, 0.84, 0.77])

If you disable call waiting, type the following:

```
ATDT*70,8788888
```

If you dial a nine before the number, type the following:

```
ATDT*9,8788888
```