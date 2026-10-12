
```
Aug 29 09:51:01 blizzard kernel: esi: 00000000 edi: bffffdb3 ebp: 00589f90
=>esp: 00589f8c
Aug 29 09:51:01 blizzard kernel: ds: 0018 es: 0018 fs: 002b gs: 002b
=>ss: 0018
Aug 29 09:51:01 blizzard kernel: Process oops_test (pid: 3374, process nr: 21,
=>stackpage=00589000)
Aug 29 09:51:01 blizzard kernel: Stack: 315e97cc 00589f98 0100b0b4 bffffed4
=>0012e3be 00240c64 003a6f00 00000001
Aug 29 09:51:01 blizzard kernel: 00000000 00237810 fffffff0 0010a7fa
=>00000003 00000001 00000000 bfffff00
Aug 29 09:51:01 blizzard kernel: bffffdb3 bffffe4d fffffffda 000002b
=>0007002b 000002b2 000002b 0000036
Aug 29 09:51:01 blizzard kernel: Call Trace: [oops:_oops_ioctl+48/80]
=>_sys_ioctl+254/272] [_system_call+82/128]
Aug 29 09:51:01 blizzard kernel: Code: c7 00 05 00 00 00 eb 08 90 90 90 90 90
=>90 90 90 89 ec 5d c3
```

This example is from the file oops-tracing.txt located in /usr/src/linux/Documentation. This file is required reading for any system administrator dealing with oops messages.

A kernel oops is essentially a protection fault, and oops messages were designed to help kernel maintainers and device-driver authors locate the source of the problem. When an oops condition occurs, the klogd daemon translates important memory addresses in the kernel log messages to their symbolic equivalents. This translated message is then forwarded from klogd to syslogd where, on Red Hat systems, it is logged by default to /var/log/messages.

The klogd daemon provides the name of the module that created the oops condition, and it provides as much symbolic information as possible. klogd performs two types of address resolution: static and dynamic. The static translation uses the System.map file, located at /boot/System.map on Red Hat systems.

Dynamic address translation is required for kernel loadable modules. Memory for these modules is allocated from the kernel's dynamic memory pools, so there are no fixed locations for the module or for its functions and symbols. For dynamic addresses, klogd draws upon system calls to determine which modules are loaded and where they are located in memory, building a symbol table that can be used to debug a protection fault in a loadable kernel module.

## Decoding Kernel Errors

For the most part, the only immediately useful information you can glean from an oops message, in its raw state, is identifying which program or driver is causing a problem. The Linux kernel maintainers have developed a system for decoding the results of oops messages and reporting them back to the maintainers. This includes running ksymoops to decode the oops message, saving the output to a report file, and filing a report, along with any system-specific information that might be useful.

## ksymoops

The program used to decode oops messages is ksymoops, which gets loaded on a Red Hat 6 system if you select “Kernel development” during a custom install. To use ksymoops, you need to compile it, then copy the oops message from /var/log/messages to a separate file and run it through ksymoops.

Before you can use ksymoops, you need to compile it for your system:

```
[root@wallace /root]# cd /usr/src/linux/scripts/ksymoops
[root@wallace ksymoops]# make
```

The documentation for ksymoops is /usr/src/linux/scripts/ksymoops/README. It does not create a man page, but the essential options are

```
Usage: ksymoops
[-v vmlinux] Where to read vmlinux
[-V] No vmlinux is available
[-o object_dir] Directory containing modules
[-O] No modules is available
[-k ksyms] Where to read ksyms
[-K] No ksyms is available
[-i lsmod] Where to read lsmod
[-L] No lsmod is available
[-m system.map] Where to read System.map
[-M] No System.map is available
[-s save.map] Save consolidated map
[-c code_bytes] How many bytes in each unit of code
[-f] One shot toggle (exit after first Oops)
[-d] Increase debug level by 1
[-h] Print help text
```

The purpose of ksymoops is to provide trace information for debugging an oops. In the previous oops message, for instance, use a text editor to extract and copy the raw oops message from the log file to the file /tmp/oops.txt. You would then run it through ksymoops as follows:

```
[root@wallace /root]# cd /usr/src/linux/ksymoops/ksymoops
[root@wallace ksymoops]# ./ksymoops < /tmp/oops.txt > /tmp/ksymoops.rpt
```

## A Sample ksymoops Report

Once a ksymoops report has been created, it can be examined for any immediately useful information. A typical ksymoops report will look similar to this example posted to the linux-kernel mailing list:

```
ksymoops -v /usr/src/linux-2.3.12/vmlinux -K -m
=>/usr/src/linux-2.3.12/System.map crash.txt
ksymoops 0.7c on i686 2.2.11. Options used
-v /usr/src/linux-2.3.12/vmlinux (specified)
-K (specified)
-l /proc/modules (default)
-o /lib/modules/2.2.11/ (default)
-m /usr/src/linux-2.3.12/System.map (specified)

No modules in ksyms, skipping objects
No ksyms, skipping lsmod
Oops: 0000
CPU: 0
EIP: 0010:<c01c72cb>
Using defaults from ksymoops -t elf32-i386 -a i386
EFLAGS: 00010202
eax: 04b02824 ebx: 00000000 edx: df24fe4c
esi: c0081f800 edi: 00a1af00 ebp: c0081c00 esp: df24fdd8
ds: 0018 es: 0018 ss: 0018
Process ifconfig (pid: 235, stackpage=df24f000)
Stack: 00000000 00000005 e0004000 00000000 0000250 0000014e e0004000 c025bfa0
c010b078 00000005 c025bf0c df24fe4c 00000050 c0b6290 00000005 df24fe44
c0110f1a 00000005 df24fe4c c06a920 df24fe4c 00000278 c0040a00 c010b1e3
Call Trace: [<c0040a00>] [<c0040a00>] [<c010b078>] [<c0110f1a>] [<c0040a00>]
[<c010b1e3>]
[<c010921b>]
[<c004010>] [<c0040a00>] [<c0004010>] [<c000001b>] [<c01c66da>]
=>[<c01c6f4f>]
[<c0040a00>] [<c016c3d0>]
[<c016fca8>] [<c016c16>] [<c016d51f>] [<c018538c>] [<c0168565>]
=>[<c0136c51>]
[<c010917c>]
Code: 8b 40 5c 01 86 bc 05 00 0b 8b 14 2b f0 ff 4a 70 df 94 c0 84
```

```
>>EIP; c01c72cb <speedo_interrupt+1e3/35c> <=====
Trace; c0004000 <END_OF_CODE=1fd4d0f0/????>
Trace; c0004000 <END_OF_CODE=1fd4d0f0/????>
Trace; c010b078 <handle_IRQ_event+50/80>
Trace; c0101fa <do_level_ioapic_IRQ+62/a8>
Trace; c0004000 <END_OF_CODE=1fd4d0f0/????>
Trace; c010b1e3 <do_IRQ+3b/5b>
Trace; c1090218 <ret_from_intr+0/20>
Trace; c0004010 <END_OF_CODE=1fd4e600/????>
Trace; c0004000 <END_OF_CODE=1fd4d0f0/????>
Trace; c0004010 <END_OF_CODE=1fd4e600/????>
Trace; c0004010 <END_OF_CODE=1fd4e600/????>
Trace; c0004018 <END_OF_CODE=1fd4e600/????>
Trace; c01c66da <mdio_read+3e/5c>
Trace; c01c68f4 <speedo_open+19c/1a8>
Trace; c0004000 <END_OF_CODE=1fd4d0f0/????>
Trace; c01c63d0 <dev_open+25/7c>
Trace; c01c6cf8 <dev_change_flags+54/110>
Trace; c01c6c10 <devinet_ioctl+22e/510>
Trace; c01c651f <dev_ioctl+17b/2cc>
Trace; c018838c <inet_ioctl+138/17c>
Trace; c0168565 <sock_ioctl+1d/24>
Trace; c0136c51 <sys_ioctl+1e1/240>
Trace; c010917c <system_call+34/38>
Code; c01c72cb <speedo_interrupt+1e3/35c>
00000000 <EIP>:
Code; c01c72cb <speedo_interrupt+1e3/35c> <=====
0: 8b 40 5c movl 0x5c(%eax),%eax <=====
Code; c01c72ce <speedo_interrupt+1e6/35c>
3: 01 c6 86 bc 05 00 00 addl %eax,0x5bc(%esi)
Code; c01c72d4 <speedo_interrupt+1ec/35c>
9: 8b 14 2b movl (%ebx,%ebp,1),%edx
Code; c01c72d7 <speedo_interrupt+1ef/35c>
c: f0 ff 4a 70 lock decl 0x70(%edx)
Code; c01c72db <speedo_interrupt+1f3/35c>
10: 0f 94 c0 sete %al
Code; c01c72de <speedo_interrupt+1f6/35c>
13: 84 00 testb %al,(%eax)
```

A kernel bug can be reported, along with this ksymoops report and other information about your setup, to linux-kernel@vger.rutgers.edu. Note however, that you should first check to see if yours is a known problem before firing off a report to the extremely busy linux-kernel mailing list. Check /usr/src/linux/REPORTING-BUGS for instructions on how to file a bug report.

## Using the System.map File

When you compile a kernel (or install a fresh system), the process creates a kernel System.map usually located in /boot/System.map. Experimental kernels will, by default, have their map located in /usr/src/linux/System.map. The System.map is a symbol table of the static addresses for a particular version of the kernel. The ksymoops program attempts to match up memory addresses with information from System.map in its report. For this reason, kernel oops messages have to be decoded on the machine that created the oops condition, to get the correct matchup.

A typical System.map contains the following type of information:

```
c01be29c t cdrom_ioctl
c01bef30 T cdrom_sysctl_info
c01bf328 t cdrom_procs_modcount
c01bf32c t cdrom_sysctl_register
c01bf364 T pci_find_slot
c01bf398 T pci_find_device
c01bf3d4 T pci_find_class
c01bf3f8 T pci_read_config_byte
c01bf424 T pci_read_config_word
c01bf450 T pci_read_config_dword
c01bf47c T pci_write_config_byte
c01bf4a8 T pci_write_config_word
c01bf4d0 T pci_write_config_dword
c01bf504 T pci_set_master
c01bf594 t proc_bus_pci_lseek
c01bf5f0 t proc_bus_pci_read
c01bf820 t proc_bus_pci_write
c01bfac0 T get_pci_dev_info
c01bfb38 T pci_proc_attach_device
c01bfbdc T pci_proc_detach_device
c01bfc18 t pci_lookup_dev
c01bfc74 t pci_strclass
c01c0130 t pci_strvendor
c01c0cec t pci_strdev
c01c0d10 t sprint_dev_config
```
