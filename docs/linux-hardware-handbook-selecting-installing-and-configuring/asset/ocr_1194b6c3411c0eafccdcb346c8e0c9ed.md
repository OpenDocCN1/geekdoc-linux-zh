To further complicate matters, hard disk manufacturers often quote internal data transfer rates in megabits per second (Mbps), but external transfer rates in megabytes per second (MBps). The abbreviations for these terms vary only in the case of the letter *b*, but the difference is a factor-of-eight value. When the internal rate is reported as 240Mbps and the external rate is 66MBps, it’s easy to become confused and believe that the external rate is the bottleneck. It’s not—expressed in MBps, the internal rate is only 30MBps.

# ## Disk Data Density

Early hard disks used a fixed number of sectors per cylinder, no matter where on the disk that cylinder was located—an inner cylinder or outer one. This design resulted in a lower density of data on outer tracks than on inner ones. In the quest for increased disk storage capacity, engineers began squeezing more sectors onto outer cylinders than on inner ones, resulting in higher data capacity per platter (see Figure 5.5).

![](bbox=[0.2, 0.43, 0.82, 0.6])

Fixed Sectors/Cylinder
16 Sectors Total

Variable Sectors/Cylinder
24 Sectors Total

*Actual hard disks use far more sectors and cylinders than are depicted here, but the basic principle still holds.*

> **NOTE**
> 
> Floppy disks still used a fixed number of sectors per cylinder. Some exotic disk formats, such as the 400KB and 800KB formats used by early Macintoshes, varied the number of sectors per cylinder, but x86 floppies have never used such schemes.

In absolute terms, the number of bytes stored on each disk platter has increased substantially over the years. Hard drives sold in 2000 store tens of gigabytes in two or three 3.5-inch platters, as compared to a tenth the capacity on the same number of platters in the mid-1990s. This increase in data density translates into an increase in disk transfer speed, even when the