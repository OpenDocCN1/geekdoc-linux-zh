![](bbox=[0.19, 0.08, 0.44, 0.27])

# Figure 4.3  *The pseudo-System Folder on a Mac OS HFS boot volume contains everything you need to boot Linux.*

Another boot method you may want to explore is Ethan Benson's ybin. This utility, used in conjunction with Yaboot, offers some additional flexibility, and automatically configures an Apple Open Firmware boot script according to Yaboot's configuration file. For details, browse to http://www.alsaka.net/–erbenson/ybin/.

# ## Configuring LILO

SuSE PPC Linux includes a special version of the LILO (*Linux Loader*) for use with PPC Linux. This version obeys much of the syntax used in the version for Intel-based PCs, and works at the boot prompt nearly the same way. LILO was originally designed for Intel-based PC hardware. As a bootloader and boot utility, LILO is typically installed in the MBR (*Master Boot Record*) or in the root Linux partition on an IDE drive to support booting to Linux or other operating systems. A configuration file named *lilo.conf*, located under the /etc directory, contains directions and a roadmap for LILO's install and operation.

Under SuSE's PPC Linux, LILO is used to create files under the /boot directory that contain directions and a roadmap for booting either Mac OS or Linux. The /etc/lilo.conf contains a picture of your system, which is familiar to Intel Linux users. For example:

```
```
# partition of the HFS volume holding the pseudo System Folder
boot=/dev/hda10
# how long to wait before booting the default
timeout=100
```
```