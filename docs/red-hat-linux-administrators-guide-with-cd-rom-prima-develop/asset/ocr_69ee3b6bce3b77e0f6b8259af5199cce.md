During the initial installation, be sure that any other operating systems are already installed because lilo will overwrite any boot record on the Master Boot Record. Red Hat will also attempt to detect other systems and grant you the options to set one of them up as the default system.

The first entry in lilo.conf is also the default OS. Because the kernel labeled linux is the first entry, that kernel will begin booting after 20 seconds, without any interaction on my part. By placing an entry for the Windows partition in the first section, I ensure that Windows is my default boot OS. If something goes wrong with the new kernel, I also have the option to boot back into my older kernel. Be sure to save the System.map and the vmlinuz files in the /boot directory. Their names should correspond to their appropriate entries in lilo.conf.

![](bbox=[0.46, 0.38, 0.53, 0.4])

If you want to boot up other operating systems, Listing 14.2 shows an example of how you can set up Windows as the default OS. Though the Linux partition is not listed first, Linux provides a default option for specifying Windows as the default OS into which the system can boot.

# Listing 14.2 A Default lilo.conf File Generated During the Red Hat Install

```
boot=/dev/hda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
linear
default=windows

image=/boot/vmlinuz-2.2.14-5.0
label=linux
read-only
root=/dev/hda2

other=/dev/hda1
label=windows
```