it is recommended to choose a **Processor type** of 386.  
If you wish to build a kernel with a configuration file (`/usr/src/linux/.config`)  
that you have already created with one of the above methods, you can omit  
the `make mrproper` and `make config` commands and use the command  
`make dep` followed by `make clean` to prepare the source tree for the build.

The next step consists of the actual compilation of the source code components into a working program that your machine can use to boot. The method described here is the easiest to recover from in the event of a mishap. If you are interested in other possibilities details can be found in the Kernel-HOWTO or in the `Makefile` in `/usr/src/linux` on your Linux system.

+   - Build the kernel with `make boot`.
+   - Build any modules you configured with `make modules`.
+   - Move the old set of modules out of the way with:
+     ```
+     rm -rf /lib/modules/2.0.29-old
+     mv /lib/modules/2.0.29 /lib/modules/2.0.29-old
+     ```
+     Of course, if you have upgraded your kernel, replace 2.0.29 with the version you are using.
+   - Install the new modules (even if you didn't build any) with `make modules.install`.

If you have a SCSI adapter and made your SCSI driver modular, build a new `initrd` image (see Section 5.1.2). Note that there are few practical reasons to make the SCSI driver modular in a custom kernel.

In order to provide a redundant boot source to protect from a possible error in a new kernel you should keep the original kernel available. Adding a kernel to the LILO menu is as simple as renaming the original kernel in `/boot`, copying the new kernel to `/boot`, adding a few lines in `/etc/lilo.conf` and running `/sbin/lilo`. Here is an example of the default `/etc/lilo.conf` file shipped with Red Hat Linux:
```bash
boot=/dev/hda
map=/boot/map
```