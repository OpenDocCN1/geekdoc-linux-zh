You can see a list of all installed RPMs by using the following command:

```
rpm -qa
```

You see a long list of RPMs scroll by your screen. To view the list one screen at a time, type

```
rpm -qa | more
```

If you want to search for a specific package, feed the output of rpm -qa to the grep command. For example, to see all packages with kernel in their names, type

```
rpm -qa | grep kernel
```

The result depends on what parts of the kernel RPMs are installed on a system. For example, on my system this command shows the following:

```
kernel-pcmcia-cs-3.1.31-13
kernel-source-2.4.20-20.1.2013.nptl
kernel-2.4.20-20.1.2013.nptl
```

You can query much more than a package's version number with the rpm -q command. By adding single-letter options, you can find out other useful information. For example, try the following command to see the files in the kernel package:

```
rpm -ql kernel
```

Here are a few lines from the output of this command:

```
/boot/System.map-2.4.20-20.1.2013.nptl
/boot/config-2.4.20-20.1.2013.nptl
/boot/vmlinuz-2.4.20-20.1.2013.nptl
/boot/vmlinuz-2.4.20-20.1.2013.nptl
/dev/shm
/lib/modules
/lib/modules/2.4.20-20.1.2013.nptl/build
/lib/modules/2.4.20-20.1.2013.nptl/kernel
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/cpuid.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/edd.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/microcode.o
/lib/modules/2.4.20-20.1.2013.nptl/kernel/arch/i386/kernel/msr.o
(rest of the listing deleted)
```