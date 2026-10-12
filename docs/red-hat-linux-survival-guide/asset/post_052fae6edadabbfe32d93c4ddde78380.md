
## Configuring the kernel using make menuconfig

One major problem with the make config-based configuration script is that if you make a mistake, you can't fix it without starting over. Also, you can't review your choices unless you use a text editor to manually view the /usr/src/linux/.config file. To remedy these shortcomings (at least for beginning kernel hackers), use the make menuconfig utility. This runs a menu-driven configuration tool that is much more user-friendly than the make config script. The Main Menu screen is shown in Figure 11-1.

![](img/9eb7e89292d2f85707b4d49102c865b7_297_0.png)

Figure 11-1 The Main Menu for the make menuconfig script.

As you can see, the user interface is quite simple and easy to navigate. However, the configuration questions are exactly the same as in the make config-based configuration that I discuss in the last section (see that section for help on how to answer these questions). make menuconfig also allows you to save and load configuration files. In other words, you can create multiple configuration files with different settings and use these configuration files to experiment with various features of the new kernel.

![](img/9eb7e89292d2f85707b4d49102c865b7_297_1.png)

Although the make menuconfig is quite user-friendly, it imposes extra requirements on remote kernel configuration. For example, if you plan to configure and compile the kernel over a Telnet connection to a remote server, you have to make sure the Telnet client program on your side is capable of good terminal emulation, which is required for a full-screen menu application. Also, note that make menuconfig is not the fanciest way to configure a kernel. That title goes to the make xconfig script, which is described in the next section.

## Configuring the kernel using make xconfig

As you may have guessed from the script name, make xconfig requires the X Window System. On systems with X installed, this is the preferred method of kernel configuration. Figure 11-2 shows the Linux Kernel Configuration window, which appears when the make xconfig script is run from a GUI that's running X.

![](img/9eb7e89292d2f85707b4d49102c865b7_298_0.png)

Figure 11-2 The Linux Kernel Configuration window.

You can click any button to open a dialog box where you can configure a particular section of the entire configuration. For example, Figure 11-3 shows the Processor type and features dialog box.

As you can see, this is quite a user-friendly interface. Another advantage of this interface is that you can open multiple sections by clicking the appropriate buttons. For example, if you are configuring the Partitions Type section and want to confirm that you have enabled UFS file system support in the Filesystems section, you can click the buttons for these two sections and verify your selections.

![](img/9eb7e89292d2f85707b4d49102c865b7_299_0.png)

Figure 11-3 The Processor type and features dialog box.

## Compiling, installing, and booting the new kernel

Now you need to compile, install, and boot the newly configured kernel. Here is how:

- 1. Before you can compile the kernel, you need to run the following command to ensure all dependencies within the source are set up correctly:
  
      `make dep`
  
      This should return without error unless a problem exists with the kernel source code itself.
  
- 2. To compile and create a compressed Linux kernel, run the following command:
  
      `make bzImage`
  
- 3. If you have configured any part of the kernel as a module during configuration, you have to run the following command to compile the modules:
  
      `make modules`
  
- 4. After you have compiled the modules, install them in the /lib/modules/2.x.x directory by using the following command:
  
      `make modules_install`

- 5. Now you need to copy the new kernel to the /boot directory as follows:
  ```
  cp /usr/src/linux-2.x.x/arch/i386/boot/bzImage /boot/vmlinuz-2.x.x
  ```
- 6. Also copy and rename the new System.map file to the /boot directory as follows:
  ```
  cp /usr/src/linux-2.x.x/System.map /boot/System.map-2.x.x
  ```
- 7. Now remove the existing symbolic link for System.map as follows:
  ```
  rm -f /boot/System.map
  ```
- 8. Finally, create a new symbolic link called /boot/System.map as follows:
  ```
  ln -s /boot/System.map-2.x.x /boot/System.map
  ```
- 9. You also need to create a new initial ramdisk as follows:
  ```
  mkinitrd /boot/initrd-2.x.x.img 2.x.x
  ```
- 10. The final step before you boot the new kernel is to prepare LILO for the new kernel. See the “Configuring LILO” section earlier in this chapter for details on how you can create a new configuration segment in /etc/lilo.conf for the new kernel. After you have modified the /etc/lilo.conf file and have run /sbin/lilo, you can reboot the system and attempt to use the new kernel, as discussed in the “Booting with the new kernel” section earlier in this chapter.

If all things go well, you have a fresh, new, custom-configured kernel running all of your favorite Linux applications from now on.

![](img/9eb7e89292d2f85707b4d49102c865b7_300_0.png)

Do not forget to make a new boot floppy using the mkbootdisk --device /dev/fd0 2.x.x command.

## Patching a Kernel

You are likely to encounter situations when the entire kernel code does not change, only the small pieces. In such a case you need to know how to patch your kernel source and create a new kernel. It is not uncommon to have a situation when you need to patch an existing kernel to get something working the way you want. You can patch the kernel source from the /usr/src directory by using the following command:

```
gzip -cd patchXX.gz | patch -p0
```

![](img/9eb7e89292d2f85707b4d49102c865b7_301_0.png)

If multiple patches are available for a kernel, apply the patches in order. In other words, apply patch01.gz before you apply patch02.gz, and so on.

As an alternative, you can use the patch-kernel script to automate this process. Store the patch file(s) in the /usr/src directory, and from the /usr/src directory, run the following command:

```
./linux/scripts/patch-kernel
```

After patching the kernel, follow the instructions for compiling and installing the new kernel as discussed earlier in this chapter.

## Setting Up Kernel Parameters by Using kernelcfg

Because the modern Linux kernel supports modules you can load and unload automatically via the kerneld daemon, you might need to configure one or more parameters for these modules to work properly. You can use kernelcfg for just such a job. Figure 11-4 shows the main Kernel Configurator window.

![](img/9eb7e89292d2f85707b4d49102c865b7_301_1.png)

Figure 11-4 Using the Kernel Configurator to configure modules.

As you can see, you can add, delete, or modify module configuration information by using the Kernel Configurator. All module configuration information is stored in /etc/conf.modules. You can either modify this file manually or use the Kernel Configurator (kernelcfg) tool. To understand how to configure a module, take a look at the following sample /etc/conf.modules file, which is what the kernelcfg tool manages.

```
alias scsi_hostadapter ncr53c8xx
alias eth0 ne
options ne io=0x340 irq=5
```

To add a new module configuration, click the Add button, and select the module name from the drop-down menu, as in Figure 11-5.

![](img/9eb7e89292d2f85707b4d49102c865b7_302_0.png)

Figure 11-5 Adding a new module configuration for kerneld.

After you select the module name from the list of available modules, you can click OK to continue. If the module requires any arguments, you can add them in the next screen, as in Figure 11-6.

![](img/9eb7e89292d2f85707b4d49102c865b7_302_1.png)

Figure 11-6 Adding arguments for the new module configuration.

After you add the arguments and click the OK button in the argument entry window, the new module configuration appears in the main window. You can also edit or delete an existing module configuration by using the appropriate buttons on the interface.

After you are done making changes, you should restart the kerneld daemon by clicking the Restart kerneld button.
