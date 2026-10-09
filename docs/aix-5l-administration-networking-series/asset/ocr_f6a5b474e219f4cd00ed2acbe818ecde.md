```
# lsvg rootvg
VOLUME GROUP:     rootvg            VG IDENTIFIER:   000b8a3bd3105eb23
VG STATE:              active          PP SIZE:       16 megarbyte(s)
VG PERMISSION:        read/write      TOTAL PPs:     1084 (17344 megarbytes)
MAX LVs:          256               FREE PPs:      710 (11360 megarbytes)
LVs:               9                 USED PPs:      374 (5984 megarbytes)
OPEN LVs:             8                 QUORUM:          1
TOTAL PVs:         2                 VG DESCRIPTORS:  1
STALE PVs:         0                 STALE PPs:         0
ACTIVE PVs:         2                 AUTO ON:         yes
MAX PPs per PV:  1016                MAX PVs:           32
LVG size:         128 kilobyte(s)    AUTO SYNC:       no
HOT SPARE:          no
```

# Cloning AIX Systems

When you clone AIX systems on *identical* hardware (exact same hardware!), you can just use a *mkssysb* bootable backup image. To clone a system to *different* hardware, you have to follow a special procedure and boot from the installation medium provided by IBM. The problem with booting from a *mkssysb* tape on different hardware is that you will not have all of the necessary drivers for any different hardware architecture on the backup tape. To get around this little problem, we boot from the installation CD-ROM, with the new *mkssysb* tape in the tape drive. When we get to the Options menu, we select **Start Maintenance Mode For System Recovery** and then select **Install From A System Backup** at the bottom of the list. Then the menu will prompt you to select the tape drive that holds the *mkssysb* tape. The system will install the system from the tape and use the CD-ROM to get the proper drivers and filesets for the particular machine. This is equivalent to running *smitty* *cfgmgr* with the Base Operating System CD-ROM in the CD drive to automatically add drivers to the system.

# INSTALLING AIX

If you are installing a brand new *pSeries* or *RISC System/6000*, parts of the base operating system (BOSt and product runtime environments may be preinstalled on the system. Note that the preinstalled system does not represent the full product or maintenance set. You must complete the installation of the remaining products and maintenance before configuring the system for use.

If you will be using a serial-attached TTY at the console, use the following settings on the TTY:

+   - 9600 bps
+   - 8,l,none
+   - 24 × 80 Display