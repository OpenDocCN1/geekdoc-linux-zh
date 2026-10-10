Shutting Down" at the end of this chapter for information on graphical logins. Carefully note the password! It does not have to be the same password used to log in, but if you password protect booting through your computer's BIOS and use a boot loader password here, you will subsequently need to enter three passwords (BIOS, boot loader, and login) to access Linux. Type in a password of at least eight characters twice (once on each line); then click OK or Cancel to exit the dialog.

# NOTE

If you are planning to dual boot your PC with Windows, it appears in the list of boot options as Other. You can click the Edit button to access options that enable you to rename it something a little more informative, or even set Windows as the default option for GRUB.

If you click the Configure Advanced Boot Loader Options button, you are asked for arguments to pass to the Linux kernel before booting. Kernel arguments are used to enable or disable various features of Linux at boot time. If you install the source to the Linux kernel, you can find documentation about the more than 200 different kernel arguments in the file `kernel1-parameters.txt` under the `/usr/src/linux/Documentation` directory. Click Next to set your boot loader configuration. You then proceed to the network interface configuration, as shown in Figure 1.18.

![](bbox=[0.09, 0.52, 0.84, 0.89])

FIGURE 1.18 Select or enter networking configuration information.