**Caution**
Because `hdparm` enables you to change the behavior of your IDE/EIDE drive subsystem, it can sometimes cause the system to hang as a consequence of improper use or misconfiguration. I highly recommend that you back up your data before using `hdparm`. Also, it is a very good idea to experiment with `hdparm` in single-user mode so that no other user is using the hard drive when you are working on it. You can reboot your system and force it to go to single-user mode by entering `linux single` at the lilo prompt during boot up.

# Checking your hard drive settings with hdparm

After you have installed the `hdparm` tool, you are ready to investigate the state of your drive subsystem performance. Assuming that your IDE or EIDE hard drive is `/dev/hda`, run the following command to check the state of your hard drive configuration:

```
```bash
hdparm /dev/hda
```
```

You should see output similar to this:

```
```
/dev/hda:
 multcount    = 0 (off)
 I/O support  = 0 (default 16 bit)
 unmaskirq    = 0 (off)
 using_dma    = 0 (off)
 keepsettings = 0 (off)
 nowerr       = 0 (off)
 readonly     = 0 (off)
 readhead     = 8 (on)
 geometry     = 2494/255/63, sectors = 40079088, start = 0
```
```

As you can see, most everything in this default mode is turned off. Some of these defaults need to be changed to enhance your drive’s performance. Before proceeding further, more information is needed from the hard drive. Run the following command:

```
```bash
hdparm -i /dev/hda
```
```

The above command displays the drive identification info (if any) that was available during the last time you booted the system. You make use of some of the information displayed by this command later. Here, the command reports the model, configuration, drive geometry (cylinders, heads, sectors), track size, sector size, buffer size, supported DMA mode, PIO mode, and so on. Using the following command tests the drive subsystem:

```
```
/dev/hda:
 Model=WDC WD205AA, FwRev=05.05B05, SerialNo=WD-WMAA015136037
 Config| HardSector NotMFM HdSig>15/15Sec SpinMotCtl1 Fixed DTR>5MB FmtGapReq |
 RawCHS=16383/16/63, TrkSize=57600, SektSize=600, ECCbytes=40
 BuffType=DualPortCache, BuffSize=2048KB, MaxMultSect=16, MultSect=16
 CurCHS=16383/16/63, CurSects=16514064, LBA=yes, LBAsects=40079088
```
```