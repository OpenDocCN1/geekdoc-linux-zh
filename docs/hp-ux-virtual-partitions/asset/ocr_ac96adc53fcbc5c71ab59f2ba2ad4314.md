```
c2t2d0    simple    disk01    rootdg    online
#
```

The output of **vxdisk** shows two disks in our system. The first is the root disk, which is under LVM control, and the second is *disk01*, which is under VxVM control.

Next, let’s get some detailed information with **vxprint -ht**:

```
# vxprint -ht
Disk group: rootdg
  DM NAME    DEVICE  RLINK_CNT  MLOG  MINORS  GROUP-ID
  RV NAME     RVG     KSTATE    STATE   PRIMARY   DATAVOLS SRL
  V  NAME     RVG    KSTATE    STATE   REM HOST   REM DG   REM RLINK
  PL NAME     VOLUME  KSTATE    STATE   LENGTH   USRTYPE  PREFLEX RDOP
  SD NAME     PLEX    KSTATE    STATE   LENGTH   LAYOUT   NCOL/NRD MODE
  EV NAME     FLEX    DISK      DIEKSIZE LENGTH   [COL/]-OFF DEVICE MODE
  DG rootdg   FLEX    VOLUME    NVOLLLARS LENGTH   [COL/]OFF AM/BM   MODE
  dg rootdg   DEFAULT   DEFAULT   0      98930419   .1625.13
  dm disk01   c2t2d0   simple   1024     17782088
```

Notice that only the information related to *rootdg*, which is under the control of the Veritas Volume Manager, has been produced. The *dg* is information related to the *disk group* and *dm* is information related to the *disk mechanism*. In an upcoming **vxprint**, we’ll add the *-q* option to eliminate the extensive header information produced with this output.

Next let’s see what we have free on *rootdg* with the **vxdg** command:

```
# vxdg free
GROUP  DISK    DEVICE    TAG      OFFSET    LENGTH     FLAGS
rootdg  disk01  c2t2d0  c2t2d0  0         17782088  -
```

This output shows that we have nearly the full 18 GBytes of the disk free at this time.

We can now go back to the graphical interface and create a usable volume by selecting *rootdg* and entering information related to the new volume as shown in Figure 9-22: