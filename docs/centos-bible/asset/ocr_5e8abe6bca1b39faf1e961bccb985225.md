# Part I Getting Started

you can see in the example, you can optionally indicate that there be no restrictions from host computers on a particular interface (--trust eth0). You can also allow an individual service (--ssI) or a particular port:protocol pair (--port 1234:udp).

```
firewall --enablel --trust=eth0 --ssh --port=1234:udp
```

The required authconfig command sets the type of authentication used to protect your user passwords. The --enabl shadow option enables the /etc/shadow file to store your passwords. The --passalgo=sha512 option enables SHA512-based encryption for the passwords. (You would typically use both.)

```
authconfig --enabl shadow --passalgo=sha512
```

The selinux command indicates whether or not Security Enhanced Linux is enabled. The following line shows it as enabled and enforcing:

```
selinux --enforcing
```

The timezone command sets the time zone for your Linux system. The default, shown here, is United States, New York (America/New_York). The --utc option indicates that the computer's hardware clock is set to UTC time. If you don't set a time zone, US/Eastern is used. Run the timezone command to see other valid time zones.

```
timezone --utc America/New_York
```

The bootloader command sets the location of the boot loader (GRUB, by default). For example, --location=mbr adds GRUB to the master boot record. (Use --location=none to not add GRUB.) The driverorder= option describes which hard disk to look on first for the master boot record. You can also add kernel options to be read at boot time using the append option (--append hdd=ide-scsi) or an optional password for GRUB (--password=GRUBpassword).

```
bootloader --location=mbr --driverorder=sda --append=\'rghb quiet\' password=GRUBpassword
```

Partitioning is required for a new install, optional for an upgrade. The code that follows is from the sample ksc file. The clearpart --linux value removes existing Linux partitions (or use --all to clear all partitions) on the first hard drive (--drives=sda). The part /boot, / and swap, sets the file system type (--fSTYPE) and partition name (--part) for each partition assignment. You can also set sizes of the partitions (--size) to however many megabytes you want. You can also create logical volume group (volGroup) and individual logical volume (logvol) entries for your partitioning.

```
# The following is the partition information you requested
# Note that any partitions you deleted are not expressed
# here so unless you clear all partitions first, this is
# not guaranteed to work
#clearpart --linux --drives=sda
```