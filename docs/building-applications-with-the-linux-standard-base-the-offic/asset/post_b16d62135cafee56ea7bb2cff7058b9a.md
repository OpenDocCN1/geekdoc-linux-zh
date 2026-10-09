
system must be disabled so the connection actually reaches the daemon in the LSB-si chroot.

The base LSB-si does not have the **inetd** or **xinetd** servers, so by default these cannot be used to listen for service requests. The `lsb-si-archtest` package can be installed to provide **inetd**. Example 12.8 shows a normal run of `lsb-runtime-test` to validate the LSB-si. The `lsb-test` package is previously installed. One part of testing requires the `syslog` daemon, so the `syslogd` from the host system is shut down first. The test setup requires a true login, so **inetd** is started to watch over a `telnet` daemon.

### Example 12.8: Using the lsb-test Package to Run inetd

```
# sh /etc/init.d/syslog stop
# /usr/sbin/chroot /opt/lsbsi-ia32
# mount /proc
# /sbin/syslogd -m 0
# /usr/sbin/inetd
```

Now connect to the LSB-si chroot using telnet, and log in as a user defined inside the LSB-si (Example 12.9).

### Example 12.9: Connecting to chroot

```
$ telnet localhost
```

## 12.2.2 Sample Implementation Using UML

The UML LSB-si runs off a *root filesystem* that is encapsulated in a file. The LSB-si will not be able to "see" outside this filesystem except if running *hostfs*, in which case the filesystem tree of the host can be mounted and accessed. This is the easiest way to get files, such as packages, to be installed into the UML LSB-si.

It is also possible to copy files into the *root_fs* (root filesystem file) of the UML LSB-si. This is a little tricky, so proceed carefully (Example 12.10).

### Example 12.10: Copy Files into *root_fs*

```
# mkdir /mnt/lbsi
# losetup /dev/loop0 /opt/lsb-umlsi/lib/root_fs
# mount /dev/loop0 /mnt/lbsi
# cp lsb-lynx-2.8.4-1.1486.rpm /mnt/lbsi/tmp
# umount /mnt/lbsi
# losetup -d /dev/loop0
```

The UML LSB-si is started by running the User-Mode Linux kernel; a script is provided by the installable (RPM or Debian) packages to do this with appropriate arguments. If it has not been run previously, the *Configure* script will be run now to set up important parts of the hosted UML Sample Implementation (Example 12.11).

### Example 12.11: Running the *Configure* Script

```
# /opt/lsb-umlsi/bin/umlsi
```

An advantage of using the UML is that it allows the whole system, kernel and all, to be run in user space. This enables the testing and debugging of an LSB-supporting kernel without actually installing a new kernel on the host system. In addition, UML more stringently isolates the LSB-si from the hosting system.

## 12.2.3 Using a Bootable Sample Implementation

The base tarball plus the *lsbsi-arch-boot* tarball are nearly enough for a complete standalone bootable system. The two missing pieces are a Linux kernel and a bootloader setup, plus some final configuration needs to be done manually. Examples 12.12 to 12.15 show the steps to build a bootable LSB-si partition on an already-bootable system. You will need to augment further to put these on a “fresh” system with no existing Linux installation.

Locate an unused partition, such as */dev/sda9*, and make an appropriate filesystem on it (the -j option to *mk2fs* is used to create a journaling (ext3) filesystem). This partition will now contain most of a runnable system. There are a few more things that need to be done to it, such as building the correct filesystem mount table and setting up a kernel that works appropriately for this system.

### Example 12.12: Creating a Journaling Filesystem

```
# mke2fs -j /dev/sda9
# mkdir /mnt/lbs1
# mount empty-partition /mnt/lbs1
# cd /mnt
# tar -xvjf /tmp/lbs1-ia32-2.0.0.tar.bz2
# cd lbs1
# tar -xvjf /tmp/lbs1-test-ia32-2.0.0.tar.bz2
```

1. Handcraft an appropriate `/etc/fstab` that describes the root filesystem, swap (if any), and any additional mounts, including special filesystems such as `/proc`, `/dev/pts`, and so on.

### Example 12.13: Copying the modules Directory

```
# cp -r /lib/modules/2.4.18-24.8.0 /mnt/lbs1/lib/modules
# cp /boot/vmlinuz-2.4.18-24.8.0 /mnt/lbs1/boot
```

2. Copy over the modules directory matching a bootable kernel that already works on this system (Example 12.13).

### Example 12.14: Copying /etc/modules.conf

```
# cp /etc/modules.conf /mnt/lbs1/etc
```

3. Copy over a working `/etc/modules.conf` or similar, as appropriate for the system you will be running (Example 12.14).

4. Add instructions to boot the kernel of your choice using the appropriate partition to boot to. For example, to boot using **lilo**, you might add the contents of Example 12.15 to `/etc/lilo.conf`.

### Example 12.15: /etc/lilo.conf instructions to Boot to lilo

```
image=/boot/vmlinuz-2.4.18-24.8.0
    label=lsbs1-boot
    root=/dev/sda9
    initrd=/boot/initrd-2.4.18-24.8.0.img
    read-only
```

If you’re using a bootloader such as lilo that requires running a command to install the new configuration, don’t forget to do so!

## 12.2.4 Sample Implementation Using Knoppix

Knoppix² is a bootable CD that runs GNU/Linux in memory without disturbing the operating system installed on the hard disk. The LSB has a version of Knoppix with the LSB-si configured on it. This disk is useful for demonstrating the LSB-si or for a tutorial lab use. When used for a demo or in a tutorial lab, there should be no concerns about what kernel, compiler, or glibc libraries are installed. Almost everyone can simply insert the disk into their computer and reboot to run Knoppix LSB-si.

# 12.3 APPLICATION TESTING USING THE SAMPLE IMPLEMENTATION

The LSB-si is equipped with a copy of rpm, to meet the requirement that a conformant platform be able to install RPM packages of the specified format. Note that rpm itself is not required by the LSB Written Specification. The RPM database in the LSB-si is populated with a minimal set of provides. As required by the specification, it provides a versioned lsb package dependency that matches the LSB Written Specification version, that is, lsb=1.3 for LSB version 1.3, and lsb=2.0 for LSB version 2.0. The LSB Written Specification permits, but does not require, an implementation of a later version to also support an earlier version, but the LSB-si does not attempt multiple-version compatibility.

The LSB project has developed a package verification tool **lsbpkgchk** that should be run and whose output should be examined carefully. As of this writing, there were still some false negatives—warnings or errors that would not prevent a package from installing correctly (it appears that there is no version of **rpm** that 100% follows the rules in the LSB Written Specification). See the **lsbpkgchk** release notes for more information.

Packages need to be installed with normal dependency checking. Do not resort to installing with `rpm --nodeps`, as one of the purposes of testing in the LSB-si is to show that a given package can properly be installed by a strictly conforming implementation, and bending the rules by bypassing the dependency checking of **rpm** weakens this test.

Please report any issues back to the LSB team, preferably by filing a bug in the LSB Buggzilla¹ bugtracker.

### Example 12.16: Dependency Checking

```
# rpm -i /tmp/lsb-lynx-2.8.4-1.1486.rpm
```

# 12.4 BUILDING THE SAMPLE IMPLEMENTATION

It is not necessary to compile the LSB-si for testing; the official packages released by the LSB project should be used for this purpose. However, it may be instructive to see how the LSB-si is constructed to get to a clean implementation of the LSB Written Specification. The remainder of this section describes the process.

The LSB-si is built from clean upstream package sources. The build instructions are captured in a set of XML files that serve as input to a tool called **ALFS**; the concept is derived from the Linux From Scratch² project.

³ http://bugs.linuxbase.org

⁴ http://www.linuxfromscratch.org
