# UFS On-Disk Format

The filestat shows that the first segment of the file occupies 192 (512-byte) blocks, followed by the next 16 Mbytes, which start in a different cylinder group. This particular file system was not empty when the file was created, which is why the next cylinder group chosen is a long way from the first.

We can observe the file system parameters of an existing file system with the fstat command. The fstat command simply dumps the superblock information for the file, revealing all of the cylinder group and allocation information. The following example shows the output for a 4-Gbyte file system with default parameters. We can see that the file system has 8,247,421 blocks and 167 cylinder groups spaced evenly at 6,272 (51-Mbyte) intervals. The maximum blocks to allocate for each group is set to the default of 2,048 8-Kbyte, 16 Mbytes.

```
# fstat -v /dev/vd/disk/homevol | more
ufs
magic 11954 format dynamic time Sat Mar 6 18:19:59 1999
sblkno 16 chblkno 24 iblkno 32 dblno 800
bsize 2048 size 8192 offset 32 cgmask 0xfffffffe0
cng 167 shift 13 mask 873836 blocks 8247421
bsize 8192 shift 10 mask 0xffffff00
fsize 1024 shift fbcdob 1
frag shift 3
minfree 18 maxpgb 2048 opt time
maxcontig 32 rotdelay 0ms rpo 120
scaadd 800 cssire shift 9 mask 0xfffffffe0
ntrak 32 nsect spc 2048 ncyl 8182
cpg 49 inobp 6272 tpg 50176 ipg 6144
nindir 2048 napf 2
nbfree 176719 ndir 10241 nfree 956753 nfree 21495
grotor 152 fmod 0 roly 0 logbn 0
```