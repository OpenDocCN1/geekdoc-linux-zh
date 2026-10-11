2,4,20-4GB 500 4096 32 10.46 4.810% 22,227 20407.44 0.11800 
 0.00000 217

# Random Reads

| | CPU |
|---|---|
| Lat% | File Bk Num | Avg | Maximum | Lat% |
| Identifier | Size Size Thr | Rate (CPU%) | Latency | Latency | >2s |
| >10s | Eff | |
| --- - | |
| - - - | |
| 2,4,20-4GB | 500 | 4096 | 32 | 0.75 | 0.715% | 438.919 | 1926.01 | 0.00000 |
| 0.00000 | 104 | | | | | | |

# Sequential Writes

| | CPU |
|---|---|
| Lat% | File Bk Num | Avg | Maximum | Lat% |
| Identifier | Size Size Thr | Rate (CPU%) | Latency | Latency | >2s |
| >10s | Eff | |
| --- - | |
| - - - | |
| 2,4,20-4GB | 500 | 4096 | 32 | 2.94 | 3.460% | 1.798 | 9288.13 | 0.02279 | 0 |
| 0.00000 | 85 | | | | | | | |

# Random Writes

| | CPU |
|---|---|
| Lat% | File Bk Num | Avg | Maximum | Lat% |
| Identifier | Size Size Thr | Rate (CPU%) | Latency | Latency | >2s |
| >10s | Eff | |
| --- - | |
| - - - | |
| 2,4,20-4GB | 500 | 4096 | 32 | 0.50 | 1.081% | 0.198 | 206.05 | 0.00000 | 0 |
| 0.00000 | 46 | | | | | | | |

After tiobench is finished, run iostat again to look at the disk activity produced by this program. A sample of iostat output is shown here:

```
[View full width]

# iostat -x /dev/hda1

Linux 2.4.20-4GB
avg-cpu: %user %nice %sys %idle
1.73 0.00 0.62 97.65
Device: rrqm/s wrqm/s r/s w/s rsec/s wsec/s rkB/s wkB/s avgqrq-sz avgqu-sz await svctm %util
/dev/hda1 28.38 58.58 2.99 6.19 251.00 518.18 125.50 259.09 83.76 11.50
125.25 14.61 13.42

Linux 2.4.20-4GB (stevebo) 12/15/2003
Device: tps Blk_read/s Blk_wrtm/s Blk_read Blk_wrtm
dev3=0 0.00 0.00 0.00 0 0
dev3=1 0.15 0.10 2.61 459576 12354928
dev22=2 0.00 0.00 0.00 0 2852
Device: tps Blk_read/s Blk_wrtm/s Blk_read Blk_wrtm
dev3=0 0.00 0.00 0.00 0 0
dev3=1 0.10 1.20 0.00 24 0
dev22=2 0.00 0.00 0.00 0 0
Device: tps Blk_read/s Blk_wrtm/s Blk_read Blk_wrtm
dev3=0 0.00 0.00 0.00 0 0
```