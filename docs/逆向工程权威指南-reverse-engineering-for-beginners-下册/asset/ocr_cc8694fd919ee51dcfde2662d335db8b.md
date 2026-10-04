```
1 LC0:
2 .string "Enter X:"
3 LC1:
4 .string "%d"
5 LC2:
6 .string "You entered %d...\n"
7 LC3:
8 .string "What you entered? Huh?"
9 f6:
10 ; save FP and LR in stack frame;
11 stp x29, x30, [sp, -32]!
12 ; set stack frame (FP=SP)
13 add x29, sp, #0
14 ; load pointer to the "Enter X:" string:
15 adrp x0, x0
16 add x0, x0, :lol2::LC0
17 puts
18 ; load pointer to the "%d" string:
19 adrp x0, #LC1
20 add x0, x0, :lol2::LC1
21 ; calculate address of x in the local stack
22 add x1, x29, #28
23 bl isoc99_scanf
24 ; scanf returned result in W0.
25 cmp w0, #1
26\27 BNE Branch If Not Equal
28 ; if W0<0, jump to L2 will be occurred
29 bne L2
30 ; at moment value W0=1, meaning no error
31 ; load xdr w1, [x29,28]
32 ; load pointer to the "You entered %d...\n" string:
33 adrp x0, #LC2
34 add x0, x0, :lol2::LC2
35 printf
36 ; skip the code, which prints the "What you entered? Huh?" string:
37 b L3
38 L2:
39 ; load pointer to the "What you entered? Huh?" string:
40 adrp x0, #LC3
41 add x0, x0, :lol2::LC3
42 puts
43 L3:
44 ; return 0
45 mov w0, #0
46 ; restore FP and LR;
47 ldp x29, x30, [sp, 32]
48 ret
```

上述程序通过CMP/BNE指令控制分支语句。