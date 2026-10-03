> NOTE
On large file systems, the minfree is automatically determined so that disk space is not wasted. Use the mkfs -m command described next if you want to see the actual minfree value that newfs used.

page is misleading. With such large disk drives, you can afford to have minfree as low as 1 percent. This has been found to be a practical and affordable limit. In addition, performance does not become an issue because locating free blocks even within a 90MB area is efficient. A rule of thumb is to use the default 10 percent minfree value for file systems up to 1GB, and adjust the minfree value so that your minfree area is no larger than 100MB. As for the performance, applications do not complain about the lower minfree value. The one exception would be the root (/) file system, in which the system administrator can use his judgment to allow more free space just to be conservative, in case root (/) ever becomes 100 percent full.

Later, if you want to see what parameters were used when creating a file system, issue the mkfs command:

```
mkfs -m /dev/rdsk/c0t0d0s6
```

The system responds with this:

```
mkfs -F ufs -o nsect=117,ntrack=9,bsize=8192,fragsize=1024,cgsize=16,free=5,rps=90,nbpi=2062,opt=t,\
apc=0,gap=0,nrpos=8,maxcontig=15 /dev/rdsk/c0t0d0s6 205334
```

# The fstyp Command

Another good command to use to view file system parameters is the fstyp command. Use the -v option to obtain a full listing of a file system's parameters:

```
fstyp -v /dev/rdsk/c0t0d0s6
```

The system responds with this:

```
ufs
  magic 11954  format dynamic      time  Sat Oct      2 10:11:06 1999
  sblkno 16    cblkno 24    iblkno 32    dbl kno 528
  sbsize 3072  cgsize 2048  cgoffset     64      cgmask 0xffffffff0
  ncg 13       size 102667 blocks95994
  bsize 8192   shift 13     mask 0xffffe000
  fsize 1024   shift 10     mask 0xffffffc00
  frag 8       shift 3      fsbtodb      1
  minfree 5%   maxbpg 2048  optim time
  maxcontig 15 rot delay 0ms rps 90
  csaddr 528   cssize 1024  shift 9      mask 0xfffffe00
  ntrak 9      nsect 117    spc 1053     ncyl 195
  cpg 16       bpg 1053     fpg 8424      ipg 3968
  nindir 2048  inopb 64     nspf 2
  nbfree 11995 ndir 2       nifree 51577 nffree 1
  cgrotor 0    fmod 0        ron ly 0
  fs_reclaim is not set
```