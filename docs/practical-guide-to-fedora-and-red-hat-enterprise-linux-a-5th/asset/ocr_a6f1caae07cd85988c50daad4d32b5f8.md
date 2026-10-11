When you configure the kernel to support loadable modules, you need to build and install the modules. Give the following command to compile the modules that you specified when you configured the kernel:

```
# make modules
```

Compiling the modules typically takes longer than compiling the kernel. The next command installs the modules in the `/lib/modules/kernel-versionEXTRAVERSION` directory. Run this command with **root** privileges even if you did not build any modules:

```
# make modules_install
```

Table 15-1 lists some of the tools available to help you work with modules. Refer to the corresponding **man** pages for options and more information.

Table 15-1 Tools for working with modules
| Tool/utility | Function |
|:-------------|:---------|
| depmod | Works with dependencies for modules. |
| insmod | Loads modules in a running kernel. |
| lsmod | Lists information about all loaded modules. |
| modinfo | Lists information about a module. |
| modprobe | Loads, unloads, and reports on modules. When it loads a module, it also loads dependencies. Looks in `/etc/modprobe.d/*.conf` for arguments. |
| rmmod | Unloads modules from a running kernel. |

# # INSTALLING THE KERNEL AND ASSOCIATED FILES

The next step is to copy the compiled kernel and associated files to the appropriate directory, usually `/boot`. When you have a **boot** partition, the files are kept in the root of this partition (`/boot`). Without a **boot** partition, the files are kept in a subdirectory of the root directory. Run the following command as **root** to install the new kernel files in the proper directory:

```
# make install
```

# # REBOOTING THE SYSTEM

Reboot the computer by selecting **Main menu: System->Shut Down** and then choosing **Restart**. If you are working at the console, press `CONTROL-ALT-DEL`. You can also give a **reboot** command from any character-based terminal or terminal emulator.