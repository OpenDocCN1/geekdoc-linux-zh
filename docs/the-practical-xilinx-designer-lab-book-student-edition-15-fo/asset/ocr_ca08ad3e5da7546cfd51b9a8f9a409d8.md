# Listing 6.13 XNF for an XC9500 CPLD built-in D flip-flop with asynchronous clear.

```
001- LCNAT, 5
002- SYM, Q, DFF, SCHNM=FDPC, LIBVER=2.0.0
003- PIN, D, I, D
004- PIN, C, I, C
005- PIN, PRE, I, PRE
006- PIN, CLR, I, CLR
007- PIN, Q, O, Q
008- END
009- EOF
```

![](bbox=[0.32, 0.35, 0.92, 0.64])

# Figure 6.12 Simulated waveforms for a built-in D flip-flop.

After compiling and downloading the BIDFF design to an XS40 or XS95 Board, the following sequence of commands should give you the indicated results:

| Command | ACLRB | D | C | LED SO (SQ) |
|---|---|---|---|---|
| XSPORT 101 | 1 | 0 | 1 | ??? |
| XSPORT 110 | 1 | 1 | 0 | Bright (1) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) |
| XSPORT 011 | 0 | 1 | 1 | Dark (0) |
| XSPORT 010 | 0 | 1 | 0 | Dark (0) |