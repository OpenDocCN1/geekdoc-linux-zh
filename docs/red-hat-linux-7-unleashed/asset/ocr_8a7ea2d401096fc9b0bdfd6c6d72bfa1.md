The most common and convenient command for creating a new kernel is

```
make dep clean zllilo modules_install
```

This one command line will do the following:

+   - Perform the dependency file generation.
+   - Clean the sources.
+   - Create a compressed kernel image.
+   - Move `$ (INSTALL_PATH)/vmlinuz` to `$ (INSTALL_PATH)/vmlinuz.old`, copy the new `zImage` kernel file to `$ (INSTALL_PATH)\vmli11uz`, and run `llilo` to install the new images.
+   - Build all modules and install these under `$ (INSTALL_MOD_PATH)/lib/modules/2.2.5`.

Putting all these commands on one line will ensure that if any stage of this build fails, subsequent stages will not be started. The whole process can also be scheduled to run in an xterm window or alt-console, can be run during off-peak hours as an at job, or can be used as an excuse to play some serious *NetHack* or *Xpilot*.

# Manually Installing a New Kernel

The new kernel file is always found in `/usr/src/linux/arch/$ (ARCH)/boot/zImage` and must be installed using the `lilo` boot loader or some other Linux loader before it can be used.

For example, to emulate the Red Hat `/boot` path scheme, you would need to copy the new `zImage` to `/boot/vmlinuz` (save the old one first!) and modify `/etc/lilo.conf` to include the backup version. Alternatively, to accommodate stubborn plug-and-play devices, you may need to copy this new kernel to your Windows 95 partition for use by the Linux `loadlin.exe` boot loader.

One frequent requirement is to create boot floppies. A boot floppy is nothing more than a kernel copied directly to a floppy disk and set to mount the **root** filesystem from the hard drive.

While it is far more mnemonic to create a boot floppy using the command

```
make zdisk
```

this is equivalent to using `dd` to copy the file directly to the raw sectors of the floppy disk device:

```
dd if=arch/i386/zImage of=/dev/fd0
```