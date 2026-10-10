```
```bash
# grub-install /dev/sda
```
```

Note that you need to specify the *device* where GRUB Legacy will be installed, like `/dev/sda`, *not* the *partition* as in `/dev/sda1`.

By default GRUB will copy the needed files to the `/boot` directory on the specified device. If you wish to copy them to another directory, use the `--boot-directory=` parameter, followed by the full path to where the files should be copied to.

# ## Installing GRUB Legacy from a GRUB Shell

If you cannot boot the system for some reason and need to reinstall GRUB Legacy, you can do so from the GRUB shell on a GRUB Legacy boot disk.

From the GRUB shell (type `c` at the boot menu to get to the `grub>` prompt), the first step is to set the boot device, which contains the `/boot` directory. For example, if this directory is in the first partition of the first disk, the command would be:

```
```bash
grub> root (hd0,0)
```
```

If you do not know which device contains the `/boot` directory, you can ask GRUB to search for it with the `find` command, like below:

```
```bash
grub> find /boot/grub/stage1
 (hd0,0)
```
```

Then, set the boot partition as instructed above and use the `setup` command to install GRUB Legacy to the MBR and copy the needed files to the disk:

```
```bash
grub> setup (hd0)
```
```

When finished reboot the system and it should boot normally.

# ## Configuring GRUB Legacy Menu Entries and Settings

GRUB Legacy menu entries and settings are stored in the file `/boot/grub/menu.lst`. This is a simple text file with a list of commands and parameters, which can be edited directly with your favourite text editor.