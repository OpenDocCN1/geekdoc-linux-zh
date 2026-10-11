```
```
62                rep
63                movsw   $go
64                ljmp    $INITSEG,

65 # bde - changed 0xff00 to 0x4000 to use debugger at 0x6400 up (bde). We
66 # wouldn't have to worry about this if we checked the top of memory. Also
67 # my BIOS can be configured to put the wfi drive tables in high memory
68 # instead of in the vector table. The old stack might have clobbered the
69 # drive table.

70 go:
        movw    $0x4000-12, %di        # 0x4000 is an arbitrary value >=
                                       # length of bootsect + length of
72                                       # setup + room for stack;
73                                       # 12 is disk parm size.
74                movw    %ax, %ds
75                movw    %ax, %ss
76                movw    %di, %sp      # put_stack at INITSEG:0x4000-12.
```
```

Lines 54–63 move the bootsector code from address 0x7C00 to 0x9000. This is achieved by:

+   1. set %ds:%si to $BOOTSEG:0 (0x7C0:0 = 0x7C00)
+   2. set %es:%di to $INITSEG:0 (0x9000:0 = 0x90000)
+   3. set the number of 16-bit words in %cx (256 words = 512 bytes = 1 sector)
+   4. clear DF (direction) flag in EFLAGS to auto-increment addresses (cld)
+   5. go ahead and copy 512 bytes (rep movsw)

The reason this code does not use `rep movsd` is intentional (hint – .code16).

Line 64 jumps to label `go:` in the newly made copy of the bootsector, i.e. in segment (0x9000). This and the following three instructions (lines 64–76) prepare the stack at $INITSEG:0x4000–0xC, i.e. %ss = $INITSEG (0x9000) and %sp = 0x3FF4 (0x4000–0xC). This is where the limit on setup size comes from that we mentioned earlier (see *Building the Linux Kernel Image*).

Lines 77–103 patch the disk parameter table for the first disk to allow multi-sector reads:

```
```
77 # Many BIOS's default disk parameter tables will not recognise
78 # multi-sector reads beyond the maximum sector number specified
79 # in the default diskette parameter tables - this may mean 7
80 # sectors in some cases.
81 #
82 # Since single sector reads are slow and out of the question,
83 # we must take care of this by creating new parameter tables
84 # (for the first disk) in RAM. We will set the maximum sector
85 # count to 36 - the most we will encounter on an ED 2.88.
86 #
87 # High doesn't hurt. Low does.
88 #
89 # Segments are as follows: ds = es = ss = cs - INITSEG, fs = 0,
90 # and gs is unused.

91                movw    %cx, %fs        # set fs to 0
92                movw    $0x78, %bx      # fs:bx is parameter table address
93                pushw   %ds
94                ldsq    fga:(%bx), %si # ds:si is source
95                movb    $6, %cl         # copy 12 bytes
```
```

# 1.3 Booting: BIOS POST