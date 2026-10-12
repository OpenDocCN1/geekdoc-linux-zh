# # RAID

RAID is an acronym for Redundant Array of Inexpensive Disks. Using RAID it is possible to combine several disks in various ways and access them as one. In fact, under Linux it is possible to include just about any kind of block devices in a RAID set. There are several different levels of RAID; each level offers different ways of combining the underlying devices. The following RAID levels are the most used with Linux:

+   - Linear or appending—This will combine two or more disks, or devices, into one logical device that appears to be one single disk for all intents and purposes. As one device is filled with data, writing will commence on the next device in the set.
+   
+   - RAID 0 or striping—This works similarly to the linear mode. The difference is that accesses are done in parallel to the devices in the RAID set. Because accesses are done in parallel, performance is generally improved.
+   
+   - RAID 1 or mirroring—This mode will maintain exact copies of the data from the main device on all the other devices in the RAID set. This means that the devices must be of the same size; if there is a difference the RAID set will only use as much space as is available on the smallest device. If one of the disks breaks down, you will have a copy of the data available on the other devices.
+   
+   - RAID 4 or striping with parity—This RAID level is quite similar to RAID 1; however, instead of mirroring the entire disk only parity information is mirrored and only onto one other device. The other devices in the set will be used the same way as in RAID 0. If one of the disks in the set breaks down, the parity information can be used in the process of reconstructing the data. This RAID level is not used very often.
+   
+   - RAID 5 or striping with striped parity—This is the same as RAID 4, except that the parity information is also striped. This eliminates certain bottlenecks that exist in RAID 4. This RAID level is the most commonly used because it offers both high availability and increased performance. However, performance does not increase in all situations.

Linux supports both hardware and software RAID. To use hardware RAID you will need a RAID controller, which is a specialized hard drive interface. This controller creates an array of disks and presents these as a single drive to the operating system. Having these abilities in hardware reduces the load on the system. These kinds of controllers are generally rather expensive. Linux supports a number of RAID controllers. If you are about to purchase one or have access to one, be sure to check /usr/src/linux/Documentation to see whether it is supported by Linux. Because different RAID controllers have different user interfaces, we will not cover such controllers here.