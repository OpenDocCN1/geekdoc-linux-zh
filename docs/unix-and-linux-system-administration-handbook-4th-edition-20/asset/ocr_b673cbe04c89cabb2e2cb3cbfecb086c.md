# KVM

migrations. Table 24.2 describes the pertinent options; they are all commented
in a default Xen installation. After making changes, restart xend by running
/etc/init.d/xend restart.

# Table 24.2 Live migration options in the xend configuration file

| Option | Description |
| --- | --- |
| xend-relocation-server | Enables migration; set to yes |
| xend-relocation-port | Network port used for migration activities |
| xend-relocation-address | Interface to listen on migration connections. unspecified, xend listens on all interfaces in dom0. |
| xend-relocation-hosts-allow | Hosts from which to allow connections* |

+   a This should never be blank; otherwise, connections will be allowed from all hosts.

In the process of migrating a virtual machine between hosts, domU's memory
image traverses the network in an unencrypted format. Administrators should
keep security in mind if the guest has sensitive data in memory.

Before attempting a migration, the guest's configuration file must be in place
both the source and destination servers. If the location of the disk image diff-
bween hosts (e.g., if one server mounts the shared storage in /xend and the
other in /vm), this difference should be reflected in the disk = parameter of the
domain's configuration file.

The migration is this simple:

```
redhat$ sudo xm migrate --live chef server2.example.com
```

Assuming that our guest host is running, the command migrates to
another Xen host, server2.example.com. Omitting the -live flag pauses the-
main prior to migration. We find it interesting to run a ping against chef's IP
address during the migration to watch for dropped packets.

# KVM

KVM, the Kernel-based Virtual Machine, is a full virtualization tool that has
included in the mainline Linux kernel since version 2.6.20. It depends on the Intel
t AMD-V virtualization extensions found on current CPUs. It is the de-
fault virtualization technology in Ubuntu, and Red has also changed gears
from Xen to KVM after acquiring KVM's parent company, Qranet.

Since KVM virtualization is supported by the CPU hardware, many guest oper-
t systems are supported, including Windows. The software also depends on
modified version of the QEMU processor emulator.

+   4. Does your CPU have them? Try grep 'vmx|svm' /proc/cpuinfo to find out. If the command dis-
plays no output, the extensions are not present. On some systems, the extensions must be enabled in
t system BIOS before they become visible.

![](bbox=[0.95, 0.437, 0.99, 0.543])