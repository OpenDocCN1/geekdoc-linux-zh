Anything between a `#` and the end of a line is regarded as a comment. Spaces and comments are ignored by LILO and can be used to improve readability.

The most important lines, step-by-step, are:

+   - **Global section** (Parameter part)
+     - `boot={bootdevice}`
+   
+       The device on whose first sector LILO should be installed. `{bootdevice}` may be a floppy disk drive (`/dev/fd0`), a partition (e.g. `/dev/hdb3`), or an entire disk (e.g. `/dev/hda`). The last means installing LILO in the MBR. Default: if this option is missing, LILO is installed on the current root partition.
+   
+     - `lba32`
+   
+       With this option, ignore the 1024-cylinder limit of LILO if your BIOS supports this.
+   
+     - `prompt`
+   
+       Forces the LILO prompt to be displayed. The default is no prompt (refer to Section *Other LILO Configuration Options* on the next page, option delay). This is recommended if LILO needs to manage more than one system. `timeout` should be set to guarantee an automatic reboot if nothing is entered at the prompt.
+   
+     - `timeout={tenth-seconds}`
+   
+       Sets a time-out for the prompted option, enabling an automatic reboot if no entry occurs in the given time. `{tenth-seconds}` is the remaining time in 0.1 second increments. Pressing `⇧ Shift` restarts the time-out. Default: infinite — no automatic reboot.

+   - **Linux section**
+     - `image={kernelimage}`
+   
+       Enter the name of the kernel image to boot, including its directory location. With your new system, this is most likely `/boot/vmlinuz`.
+   
+     - `label={name}`
+   
+       This name has to be unique in `/etc/lilo.conf`. Otherwise, freely choose a name for the system (e.g., Linux). Maximum length is 15 characters. Use only letters, numbers, and underscore in names — no blanks or special characters, for example. For more on the specific rules for which characters to use, see [Alm94], as described in Section *Boot Concepts* on page 92. The default is the file name of the kernel image (e.g., `/boot/vmlinuz`).