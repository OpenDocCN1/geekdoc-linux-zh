```
MON> vparload -all
[MON] Booting uhnjlvp2...
[MON] Booting uhnjlvp1...
[MON] Console client set to uhnjlvp2

[MON] uhnjlvp2 loaded

[MON] uhnjlvp1 loaded
```

**lilfs**

Displays the files in the LIF area as shown below:

```
MON> lilfs
volume ISLI0 data size 7802 directory size 8
filename type start size implement created
================================================================================
ODB -12960 584 848
MAPFILE -12277 1432 128
SYSLIB -12280 1560 353
CONFIGDATA -12278 1920 218
SLMOD2 -12276 2144 140
SLDEV2 -12276 2288 134
SLDRV2 -12276 2424 168
SLSCSI2 -12276 2592 116
MAPPER2 -12279 2712 142
IOTEST2 -12279 2856 89
PERFVER2 -12279 2952 125
PVCD -12801 3080 64
SSINFO -12286 3144 2
ISL -12800 3152 306
AUTO -12289 3464 1
HPUX -12928 3472 848
LABEL -23951 4320 8
```

**getauto**

Displays the contents of the LIF area auto file as shown below:

```
MON> getauto
hpux
```