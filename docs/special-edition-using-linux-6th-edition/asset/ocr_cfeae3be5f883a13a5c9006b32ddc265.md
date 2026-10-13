The kernel version and timestamp that are reported in the preceding capture might be different, but the rest of the script will closely resemble what you see.

In Listing 19.3, the trusting version of the card utilities was selected, and 32-bit Cardbus support was selected. PnP BIOS resource checking was disabled. The package then gave a rundown of what it found in the kernel source tree. SCSI PCMCIA modules will not be built because SCSI support is disabled. If you want SCSI pcmcia modules, you'll need to rebuild the kernel with SCSI support. The same is true for any other options listed that show as disabled.

+   3. Compile the binaries and modules that make up the pcmcia-cs package:
+   
+      ```text
+      make all
+      ```

+   4. Install all the binaries and modules in their proper places:
+   
+      ```text
+      make install
+      ```

If an alternative directory was specified for installation during the make config step, the alternative directory becomes the equivalent of the root (/) directory during this installation step. Each subdirectory off the root directory that might have been affected (for example, /lib and some subdirectories off /etc) is duplicated off the alternative directory. (That is, if a file was supposed to go in /etc/rc.d, it goes in /alternate-directory/etc/rc.d instead.) This helps if the compiled binaries and modules are going to be packaged and moved to another system, or if there is no desire to overwrite an existing pcmcia-cs installation with a new version.

The configuration files for the pcmcia-cs package all reside in /etc/pcmcia (see Table 19.1).

Table 19.1 — Configuration Files for the pcmcia-cs Package

| Filename | Purpose |
|---|---|
| `cdrom` | Initialization script for PCMCIA CD-ROM device. |
| `cdrom.opts` | Contains configuration information for CD-ROM devices. |
| `cis/` | Directory containing CIS (Card Information Structure) information for various PCMCIA cards. |
| `config` | Main database of supported hardware and the modules associated with each device. Global, packagewide configuration information is stored here. |
| `config.opts` | Holds general configuration data for the pcmcia-cs package. Local configuration information is adjusted in this file, not the config file. |
| `ftl` | Initialization script for FTL flash memory cards (the only flash cards that are supported by pcmcia-cs). |
| `ftl.opts` | Contains configuration information for FTL flash memory cards. |
| `ide` | Initialization script for IDE adapters. |
| `ide.opts` | Holds general configuration data for IDE adapters. |
| `memory` | Initialization script for memory devices. |
| `memory.opts` | Contains configuration information for memory devices. |