```
```
sam_adduser  denise      1010    file
tdoIan       denise      1024    dir
trash        denise      4554    file
trash.out    denise      329     file
typescript   denise      2017    file

The files listed occupy 393605 bytes (0.3754 Mbytes)
Average file size is 13120 bytes
```

```


When we run lls um.orig, clearly the second group of informa- tion, which is the owner, starts at column 16 and not column 32:

```
```
$ lls um.orig
FILENAME          OWNER      SIZE     TYPE

README            denise     810      file
backup_files      denise     3408     file
biography         denise     427      file
csh test          denise     1024     dir
gkill             denise     1855     file
gkill.out         denise     191      file
hostck            denise     924      file
ifstat            denise     1422     file
ifstat.int        denise     2147     file
ifstat.out        denise     723      file
introdos          denise     54018    file
introux           denise     52476    file
letter            denise     23552    file
letter.auto       denise     69632    file
letter.auto.rec   denise     71680    file
letter.backup     denise     23552    file
letter.1ck        denise     57       file
letter.recover    denise     69632    file
llsum             denise     1267     file
llsum.orig        denise     1267     file
llsum.out         denise     1657     file
llsum.tomd.out    denise     1356     file
psg               denise     670      file
psg.int           denise     802      file
psg.out           denise     122      file
sam_adduser       denise     1010     file
tdoIan            denise     1024     dir
trash             denise     4554     file
trash.out         denise     329      file
typescript        denise     3894     file
```

```