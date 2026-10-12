This will set the maximum size of shared memory to 2147483648 bytes, or 2GB. This is sufficient for the installation of Oracle 10g, but might not be enough to run with the size of SGA you require for normal operations. For a 32-bit system, you can create an SGA up to 2.7GB in size. For SGAs larger than 2.7GB, there are some special tricks you can do (described later in this book).

One way to have these commands executed on every boot is to put them in the /etc/rc.local file, just as you would any shell script:

```
```
# Configuration parameters for Oracle
echo "250 32000 100 128" > /proc/sys/kernel/sem
echo "2097152" > /proc/sys/kernel/shmall
echo "2147483648" > /proc/sys/kernel/shmmax
echo "4096" > /proc/sys/kernel/shmmni
echo "65536" > /proc/fs/file-max
echo "1024 65000" > /proc/net/ipv4/ip_local_port_range
```
```

The /etc/rc.local file is run every time the system boots, thus the parameters will be reset each time the system boots. However, the preferred method is to change /etc/sysctl.conf.

# Configuring Kernel Parameters Using the /etc/sysctl.conf File

The alternate method is to put the parameters into a file named /etc/sysctl.conf. This file sets the kernel parameters upon system boot. The /etc/sysctl.conf file contains the directory and value of the /proc file, as shown next:

```
```
kernel.shmall = 2097152
kernel.shmmax = 2147483648
kernel.shmmni = 4096
kernel.sem = 250 32000 100 128
fs.file-max = 65536
net.ipv4.ip_local_port_range = 1024 65000
```
```

Run the program /sbin/sysctl -p to load the values you put in this file, and verify that these parameters were set correctly. With Red Hat Linux, this file will be read on bootup by default. With SUSE Linux, use the following command to activate the sysctl.conf file:

```
```
/sbin/chkconfig boot.sysctl 1 on
```
```

# Adding Users and Groups

Before you can install Oracle on Linux, it is necessary to create an Oracle user account. This account must belong to the oinstall group and also be a member of the dba group. The groups are added with the groupadd command (usr/sbin/groupadd):

```
```
groupadd oinstall
groupadd dba
```
```