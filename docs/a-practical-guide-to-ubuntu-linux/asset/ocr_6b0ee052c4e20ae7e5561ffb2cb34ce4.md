# # LOADING A MODULE

After you install a module with module-assistant, you must load it to make it available to the running kernel. Table 15-1 lists some of the tools available to help you work with modules. Refer to the corresponding pages for options and more information.

**Table 15-1** Tools for working with modules

| Tool/utility | Function |
| --- | --- |
| depmod | Works with dependencies for modules. |
| insmod | Loads modules in a running kernel. |
| lsmod | Lists information about all loaded modules. |
| modinfo | Lists information about a module. |
| modprobe | Loads, unloads, and reports on modules. When it loads a module, it also loads dependencies. |
| rmmod | Unloads modules from a running kernel |

# # INSTALLING THE KERNEL, AND ASSOCIATED FILES

The next step is to copy the compiled kernel modules, and associated files to the appropriate directories—usually `/boot` and a subdirectory of `/lib/modules`. When you have a partition mounted at `/boot`, the files are kept in the root of this partition (`/boot`). Because you have created a `deb` package, installing these files is quite easy. The following command installs the new kernel in the partition directories:

```
$ cd ..
$ sudo dpkg -i linux-image-2.62.11+dm33.2171202298_2.62.11+dm33.2171202298-10.00.Custom_i386.deb
Selecting previously deselected package linux-image-2.62.11+dm33.2171202298
(Reading database... 13802 files and currently installed)
Unpacking linux-image-2.62.11+dm33.2171202298 (from linux-image-2.62.11+dm33.2171202298)
2.62.11+dm33.2171202298_2.62.11+dm33.2171202298-10.00.Custom_i386.deb
Setting up linux-image-2.62.11+dm33.2171202298 (2.62.11+dm33.2171202298 10.00.Custom)
Running depmod.
Examining /etc/kernel/postinst.d/
Running executing /etc/kernel/postinst.d/nvidia-comoot/vmlinuz-2.62.11+dm33.2171202298
Running executing /etc/kernel/postinst.d/pm-utils 2.62.11+dm33.2171202298
Running update-ramfs -u -k
Generating script /boot/initrd.img-2.62.11+dm33.2171202298
Generating grub.cfg
Found linux image: /boot/vmlinuz-2.62.11+dm33.2171202298
Found linux image: /boot/vmlinuz-2.62.19-generic
Found initrd image: /boot/initrd.img-2.62.19-generic
Found testboot86+: /boot/testboot86+.bin
done
```