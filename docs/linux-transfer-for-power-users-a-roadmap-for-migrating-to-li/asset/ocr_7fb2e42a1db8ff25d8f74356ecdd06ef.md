```
```text
[~root@fedcore-shell]# cdrecord -scanbus
cdrecord 1.10 (2008-96-linus-gnu) Copyright (C) 1995-2003 Jorg Schilling
Linux sg driver version: 3.1.24
Using libsg version 'whily-0.5'

  scsisbus0:
0,0,0 0) 'MATSHTA' 'UDA730 DVD/CURM' 1.04' Removable CD-ROM
0,1,0 1) *
0,2,0 2) *
0,3,0 3) *
0,4,0 4) *
0,5,0 5) *
0,6,0 6) *
0,7,0 7) *
```
```

**Figure 2.** Determining the CD-ROM's address via the cdrecord -scanbus command.

+   - 4. Next, issue the cdrecord command to do a test burn, using the three leading numbers from the results of the scanbus info dump, like so:
+   ```
+   cdrecord -dummy -v -eject speed=4 dev=0,0,0 /path/yarrow-1186-disc1.iso
+   ```
+   - 5. The speed should be set at whatever your CD writer supports. 4x, as used in this example, is pretty slow these days. The results are shown in **Figure 3**.
+   - 6. If that goes well, issue the following command to burn the real CD:
+   ```
+   cdrecord -dummy -v -eject speed=4 dev=0,0,0 /path/yarrow-1186-disc1.iso
+   ```
+   - 7. The results should look like **Figure 4**.
+   - 8. Once you've burned your CD, take a look at the contents using a tool like Nutilus. **Figure 5** shows what CD #1 should look like.
+   
+   For your convenience, I've also shown the contents of CD #2 in **Figure 6**, and the contents of CD #3 in **Figure 7**.