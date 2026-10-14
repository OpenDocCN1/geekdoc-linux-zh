![](bbox=[0.06, 0.092, 0.784, 0.352])

*Figure 11.4: Entering Parameters for a Module to Load*

# The SuSE Rescue System

SuSE Linux contains several Linux rescue systems so that in emergencies, your Linux partitions on the hard disks are reachable “from the outside”: via a boot disk or the “Rescue” System, loaded from disk, CD, the network, or the SuSE FTP server. There is also a bootable SuSE Linux CD (the “LiveEval CD”) that can be used as a rescue system. The rescue system includes several help programs with which you can remedy large problems with inaccessible hard disks, misconfigured configuration files, or other similar problems.

Another aspect of the rescue system is Parted, which is used for modifying the partition size. This program can be launched from inside the rescue system itself, if you do not want to take advantage of the resizer integrated in YaST2. Information on Parted can be found at:

http://www.gnu.org/software/parted/

> **Tip**
> 
> Always have a boot and rescue disk at hand, because the slight effort for creating and maintaining the disk is negligible in comparison to the time wasted and work involved when, in the case of emergency, you cannot access your system or your CD-ROM drive.