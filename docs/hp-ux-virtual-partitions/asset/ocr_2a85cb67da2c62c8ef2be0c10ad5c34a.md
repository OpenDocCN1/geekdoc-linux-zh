# System Recovery with Iignite-UX

vg00 /dev/vg00/lvol3 /
vg00 /dev/vg00/lvol5 /home
vg00 /dev/vg00/lvol5 /opt
vg00 /dev/vg00/lvol1 /stand
vg00 /dev/vg00/lvol6 /tmp
vg00 /dev/vg00/lvol7 /usr
vg00 /dev/vg00/lvol8 /var

Create mount points
/appe
/work
/spill
/epil2
/rbdisk01
/rbdisk02
/rbdisk03
/rbdisk04
/rbdisk05
/rbdisk06
/rbdisk07
/rbdisk09
/rbdisk10
/rbdisk11
/rbdisk12
/rbdisk13
/rbdisk14
/rbdisk15
/rbdisk16
/rbdisk17
/rbdisk18
/ntfs

/opt is a mounted directory
It is in the Core Volume Group
Mounted at /dev/vg00/lvol5
/var is a mounted directory
It is in the Core Volume Group
Mounted at /dev/vg00/lvol8

Destination = /dev/rmt/0m
Boot LIF location = /var/tmp/uinstlf.recovery

*********************
Creating the configuration file.
Done
Modifying the configuration file.
Done
Backing up vg configurations
Volume Group vg00
Volume Group vg01
Volume Group vg03
Volume Group vg02
Done
Creating the /var/opt/Iignite/recovery/makrec.last file
Done
Going to create the tape.
Processing tape
Invoking instl_adm -T
Creating boot LIF
Done
Writing boot LIF to tape /dev/rmt/0mn