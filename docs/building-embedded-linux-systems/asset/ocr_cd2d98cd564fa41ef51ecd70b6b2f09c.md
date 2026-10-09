allows you to make U-Boot run boot scripts. (The semicolons must be escaped because they have meaning to the shell and you want the shell to ignore them, so they are entered as part of the string in the environment variable.)

The environment variables we met in the previous section, for instance, are actually part of a boot script, `bootcmd`. It sets the special variable `bootargs` using other environment variables before calling the `bootm` command to “boot from memory” the kernel at the predefined flash memory address configured for the GTA01 hardware.

Rather than setting `bootcmd` directly (which limits you to one boot command at a time), you can set it to “run” another boot script. This is useful, for example, if you will need to switch between network booting and direct flash booting on your embedded device. Here is an example:

```
=> setenv bootcmd run other_boot_script
```

Or you can run boot scripts directly from the command line without changing the value of the `bootcmd` environment variable:

```
=> run other_boot_script
```

Scripts are a very useful feature of U-Boot, and you should use them whenever you need to automate a certain task. You can find much more information about their use and several examples on the U-Boot wiki pages, as well as on this book’s website.

# ## Preparing Binary Images

Since the raw flash within your embedded device (the partitions on your flash not already devoted to a filesystem such as JFFS2) is not structured like a filesystem and does not contain any sort of file headers, binary images downloaded to the target must carry headers for U-Boot to recognize their content and understand how to load them. The `mkimage` utility we installed earlier was packaged with U-Boot for this purpose. It adds the information U-Boot needs to recognize binary images while also attaching a checksum for verification purposes.

![](bbox=[0.16, 0.73, 0.26, 0.8])

Although the use of image headers is not a technical requirement for a bootloader, such headers are very convenient both during development and in the field. Hence U-Boot’s use of them.

To see the typical use of `mkimage`, type the command without any parameters:

```
$ mkimage
Usage: mkimage -l image
  -l = > list image header information
mkimage -A arch -O os -T type -C comp -a addr -e ep -n name -d data_file[:data_file... ] image
  -A = > set architecture to 'arch'
  -O = > set operating system to 'os'
  -T = > set image type to 'type'
```