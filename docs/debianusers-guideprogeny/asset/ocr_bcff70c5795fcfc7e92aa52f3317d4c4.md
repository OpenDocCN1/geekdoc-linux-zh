1  Back up all important information.

While parted is generally safe to use, interruptions to your computer’s problems or other accidents could destroy information.

2  At a command line, type: **parted -OPTIONS DEVICE COMMAND.**

Note that:

+   - The -i ( “interactive” ) option prompts you for a decision if any are necessary. You can omit this option if you want.
+   - For information on how Linux names devices, see “Reading Linux Device Names,” page 40.

# The parted Command (Partitioning): Commands

| Command | Action |
| :--- | :--- |
| device | Defines the partition in blocks. |
| boot PARTITION | Sets the bootable partition. |
|  | Values are: |
|  | - 1-4: primary or extended partitions. |
|  | - 5 or higher: logical partitions. |
| cp SOURCE TARGET | Copies the file system on the source partition to the destination partition. |