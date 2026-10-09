# **Boot Loader Configuration Problems**

The first action your Linux system performs after computer startup is to load the boot loader. Problems with boot loader configuration files can prevent the system from starting. In the best-case scenario you copied the configuration files and can either copy the backup to replace the files or can retype in information needed to correct the problem. Most installations of the Linux operating system use either GRUB or LILO as a boot loader. Configuration files for these boot loaders were discussed in Chapter 6.

**/boot/grub/grub.conf** This is the configuration file for the GRUB boot loader. Problems with this file can prevent the system from starting. Figure 13-3 shows a sample grub.conf file with a menu of two startup options. The first loads the smp (symmetric multiproccessing) kernel as the default.

![](bbox=[0.04, 0.27, 0.22, 0.3])

![](bbox=[0.28, 0.28, 0.84, 0.53])

**/etc/lilo.conf** This is the LILO configuration file. This configuration file is not read at every startup. Instead, it controls the operation of the lilo utility, which is used to install the LILO boot loader to be activated the next time the system boots. Figure 13-4 shows a sample lilo.conf file. The file uses the normal Linux configuration as the default, but a failsafe image is also available.

![](bbox=[0.04, 0.65, 0.22, 0.68])

![](bbox=[0.28, 0.66, 0.84, 0.96])