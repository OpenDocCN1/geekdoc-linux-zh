**Table 14.1: (Continued)**

| | | | | | |
|---|---|---|---|---|---|
| cut | getty | lotsetup | ps | sulogin | watch |
| date | grep | lpd | pscan | sum | watchdog |
| dc | gunzip | lpq | pwd | sv | wc |
| dd | gzip | lpr | raidautorun | svlogd | wget |
| deallocvt | hd | ls | rdote | swapoff | which |
| delgroup | hdparm | lattr | rdev | swapon | who |
| deluser | head | lsmode | readlink | switch_root | whoami |
| depmod | hddump | lzmacat | readprofile | sync | xargs |
| devmem | hostid | lzop | reaptph | sysctl | yes |
| df | hostname | lzopcat | reformime | syslogd | zcat |
| dhcreplay | httpd | makernime | renice | | zip |
| diff | hush | man | reset | | |

BusyBox supports the `xconfig` and `menuconfig` make targets for configuration just like the kernel. Fig. 14.1 shows the `xconfig` menu, while Fig. 14.2 shows the top top-level `menuconfig` menu. Also, like the kernel, there is a `make help` target that lists the other make targets. Oddly, `xconfig` does not show in the list.

There are only a few `*_defconfig` targets for creating default configurations, and sadly none of them match the BeagleBone Black. I have not been able to find a default configuration for the BBB, so we are kind of left hanging. Let us see what happens if we just create a new one.

# **BusyBox Settings**

While the xconfig navigation panel shows a number of option categories, there are really only two: options to configure, build, and install BusyBox, and options to select the desired applets. Under `Build Options` you have the choice of building BusyBox either with statically linked libraries, or shared libraries. A statically linked BusyBox is a much bigger executable, but then you do not need the shared libraries. As an example, the BusyBox I built with shared libraries is 743 kb. The statically linked version is 1.5 MB. But the /lib directory, where the shared libraries are kept, adds up to 17 MB. So the question becomes, do you need those shared libraries for anything else?

Build Options is also where you can set the cross-compiler prefix. Set it to `arm-linux`...

Under `Installation Options`, you have a choice of how the symbolic links are created. They can be soft links, hard links, or script “wrappers.” The accompanying box describes the distinction between hard and soft links. Since hard links to the same data all share the same inode, that can be a useful option on systems with a limited number of inodes. Soft links are the default, and usually the best way to go.