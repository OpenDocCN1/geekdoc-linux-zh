| Option | Meaning |
| :----- | :------ |
| i sector | Installs the kernel as the new boot sector. Can be read from the install configuration variable. |
| I name | Displays the path of the name kernel image file. If no matching name is found, an error is generated. The option “v” can be added after the name to verify the existence of the image file. This option uses the `BOOT_IMAGE` environment variable. |
| l | Generates linear sector addresses instead of the default `sector/head/cylinder` addresses. Can also be specified with the configuration variable `linear`. |
| m file | Uses `file` as the location of the map file. If no filename is given, `/etc/lilo/map` is used. |
| P fix | Allows LILO to adjust sector/head/cylinder addresses using the table file. Also specified with the `fix table` configuration variable. |
| P ignore | Overrides correction of sector/head/cylinder addresses. Also specified with the `ignore table` configuration variable. |
| q | Displays the currently mapped files. |
| r dir | Performs a `chroot` command on `dir` before continuing. This is necessary if the root file system is mounted in a different location from the map installer command. Because the current directory is changed with this command, use absolute pathnames for all files. |
| R words | Stores words in the map file for use by the boot loader. The words are parameters used by the boot process as part of the default command line. The first word must be the name of the boot image. |
| s file | Copies the original boot sector to `file` instead of `/etc/lilo/boot.hex_num`. |
| S file | Same as `s` but overwrites the old file if it exists. |
| t | Performs a test by executing the entire installation process except writing the map file and boot sector. Ideally used with the `v` option to verify accurate behavior of the map installer. |
| u dev | Restores the backup copy of the boot sector for `dev`. If no device is specified, the default value is used or, failing a valid value, the current root device. The backup copy is checked for a time stamp before the write is completed. |
| U dev | Same as `u` except no check for the time stamp. |
| v level | Uses the verbose output level specified to display messages. |
| V | Displays the version number of the map installer, then exits. |