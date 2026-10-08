You can then migrate the /boot, /, and /home files from your current hard disk to your RAID devices. Install your boot loader on the first RAID device, md0, and load the root file system from the second RAID device, md1.

Alternatively, you can first create the arrays with the mdadm command and then generate the ARRAY entries for an /etc/mdadm.conf file from the created RAID information to later manage your arrays, adding or removing components. The following commands would create the three RAID devices in the previous example:

```
mdadm --create /dev/md0 --raid-devices=2 /dev/hda1 /dev/hdc1 --level=1
mdadm -C /dev/md2 -n3 /dev/hda2 /dev/hdc2 -15
mdadm -C /dev/md2 -n3 /dev/hda3 /dev/hdc3 -15
```

You can then generate the ARRAY entries for the /etc/mdadm.conf file directly using the following command. You will still have to edit mdadm.conf and add the DEVICE entries as well as the monitoring entries, like MAILADDR.

```
mdadm --detail --scan > /etc/mdadm.conf
```