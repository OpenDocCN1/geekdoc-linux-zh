```
setenv mtldid nand=neo1973-nand
setenv mtdparts mtdparts=neo1973-nand:0x00050000(u-boot),0x00004000(u-boot_env),\
0x00208000(kernel),0x00010000(splash),0x00394000(rootfs)\nand
write.e $kernel_addr u-boot $boot_size
```

In this case, we set U-Boot to boot from the kernel found at the address $kernel_addr$ (which was hardwired into the build of U-Boot for the GTA01) and to mount its root filesystem from flash memory. The remaining commands configure menu choices displayed to the user on the GTA01’s screen (not shown on the serial console), as well as a fancy splash image that will be used as a background graphical image on the screen shown to the user of the device during the bootloader process.

The setenv command adds the environment variables to the current session only. Hence, if you reset the system (either through software, or with the reset command), any environment variable you set only with setenv will be lost. For the environment variables to survive reboots in a persistent fashion, they must be saved to flash, which is done using the saveenv command:

```
=> saveenv
Saving Environment to NAND...
Erasing Nand...Writing to Nand... done
```

Be careful when using saveenv, because it will save all the environment variables currently defined, even those that you have intended to use temporarily. Before using saveenv, use printenv to take a look at the currently defined environment variables and delete any that you don’t need to save. Deleting a variable can be done simply by issuing setenv on the variable without providing any values. Here’s an example that defines and deletes an arbitrarily chosen variable name called RAMDisk_addr:

```
=> setenv RAMDisk_addr 40500000
=> printenv RAMDisk_addr
RAMDisk_addr=40500000
=> setenv RAMDisk_addr
=> printenv RAMDisk_addr
## Error: "RAMDisk_addr" not defined
```

Note that the setenv does not require an equals sign between the variable and its value. Thus, equals signs can be entered as part of the string making up the environment variable, as we saw earlier in this section. The following command, for example, has poor syntax (notice the extra = displayed by printenv compared to the same printenv shown in the previous capture):

```
=> setenv RAMDisk_addr = 40500000
=> printenv RAMDisk_addr
RAMDisk_addr = = 40500000
```

# ## Creating Boot Scripts

U-Boot environment variables can be used to create boot scripts. Such “scripts” are actually just U-Boot environment variables containing a set of U-Boot command sequences. Using a combination of the run command and the ; (semicolon) operator