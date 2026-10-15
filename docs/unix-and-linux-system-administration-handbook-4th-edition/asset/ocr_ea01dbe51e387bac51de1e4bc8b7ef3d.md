migrations. Table 24.2 describes the pertinent options; they are all commented out in a default Xen installation. After making changes, restart xend by running **/etc/init.d/xend restart**.

**Table 24.2  Live migration options in the xend configuration file**

| Option | Description |
|---|---|
| `xend-relocation-server` | Enables migration; set to yes |
| `xend-relocation-port` | Network port used for migration activities |
| `xend-relocation-address` | Interface to listen on for migration connections. If unspecified, Xen listens on all interfaces in dom0. |
| `xend-relocation-hosts-allow` | Hosts from which to allow connections⁽ᵃ⁾ |

ᵃ. This should never be blank; otherwise, connections will be allowed from all hosts.

In the process of migrating a virtual machine between hosts, the domU’s memory image traverses the network in an unencrypted format. Administrators should keep security in mind if the guest has sensitive data in memory.

Before attempting a migration, the guest’s configuration file must be in place on both the source and destination servers. If the location of the disk image files differs between hosts (e.g., if one server mounts the shared storage in `/xen` and the other in `/vm`), this difference should be reflected in the disk = parameter of the domain’s configuration file.

The migration itself is simple:

```
redhat$ sudo xm migrate --live chef server2.example.com
```

Assuming that our guest domain chef is running, the command migrates it to another Xen host, **server2.example.com**. Omitting the **--live** flag pauses the domain prior to migration. We find it entertaining to run a **ping** against chef’s IP address during the migration to watch for dropped packets.

# KVM

KVM, the Kernel-based Virtual Machine, is a full virtualization tool that has been included in the mainline Linux kernel since version 2.6.20. It depends on the Intel VT and AMD-V virtualization extensions found on current CPUs.⁴ It is the default virtualization technology in Ubuntu, and Red Hat has also changed gears from Xen to KVM after acquiring KVM’s parent company, Qumranet.

Since KVM virtualization is supported by the CPU hardware, many guest operating systems are supported, including Windows. The software also depends on a modified version of the QEMU processor emulator.

4. Does your CPU have them? Try **egrep '(vmx|svm)' /proc/cpuinfo** to find out. If the command displays no output, the extensions are not present. On some systems, the extensions must be enabled in the system BIOS before they become visible.