If you use ISA Plug&Play cards, you should cast a glance at the man texts of isapnp, pnpdump, and isapnp.conf.

+   - Mounting of the root partition in read/write mode.
- Mounting of the /proc directory.
- Starting module support for the kernel (only with older distributions with kernel; since kernel 2.2, this task is taken over by the kernel component knod).
- Activation of modules for sound cards, MIDI.
- Activation of RAID support; if /etc/mtstab exists, the virtual partitions listed there are created by means of maddd. See also page 157.
- Checking of partitions, according to /etc/fstab, are to be mounted into the file system.
- Mounting of partitions (no NFS partitions, because network services are not yet available).
- Setting of the character set for the text console (/sbin/setsysfont).
- Activation of quota for the entire file system.
- Setting of the system time (under consideration of /etc/sysconfig/clock).
- Linking of swap files (according to /etc/fstab).
- Initialization of the serial interfaces (by means of /etc/rc.d/rc.serial, which this file exists).
- If a SCSI stwier found, activation of the corresponding kernel module.
- Storing of kernel messages in /var/log/dmesg
- Initialization of the random number generator.

# rc files

init and initab bear responsibility for controlling the init process, the actual work is done by numerous rc scripts which are started from within /etc/rc.d/ rc is the new runlevel n. rc first processes the file /etc/rc.d/init.d/ functions, where macros such as daemon and killproc are executed. Then, all rc.d/S* scripts are executed on running processes. Finally, all S* start the new processes for the runlevel in which are executed.

```
rc1: (single user)
K09keytable K20rwhod K60atd K70syslog S00single
K15gpm K30sendmail K60cron K95nfs S01kernel
K20nfs K50init K60ipld K96pcmcia S20random
K20usersd K55rooted K65portmap K97network
```

```
rc3: (multi-user with network)
K20usersd S10network S40atd S50init S80sendmail
```

The following table shows which script files are executed for selected runlevels, when switching to single user mode, for example, various network services, cron and syslog are stopped.