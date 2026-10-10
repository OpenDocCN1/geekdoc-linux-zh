Found valid GPT with protective MBR; using GPT.

Command (? for help):

The `gdisk` program identifies the type of formatting used on the drive. If the drive doesn't currently use the GPT method, `gdisk` offers you the option to convert it to a GPT drive.

Be careful with converting the drive method specified for your drive. The method you select must be compatible with the system firmware (BIOS or UEFI). If not, your drive will not be able to boot.

![](bbox=[0.16, 0.26, 0.23, 0.31])

The `gdisk` program also uses its own command prompt, allowing you to enter commands to manipulate the drive layout, as shown in Table 11.2.

**TABLE 11.2** Common `gdisk` commands

| Command | Description |
| :------ | :---------- |
| b | Back up GPT data to a file. |
| c | Change a partition's name. |
| d | Delete a partition. |
| i | Show detailed information on a partition. |
| l | List known partition types. |
| n | Add a new partition. |
| o | Create a new empty GUID partition table (GPT). |
| p | Print the partition table. |
| q | Quit without saving changes. |
| r | Recovery and transformation options (experts only). |
| s | Sort partitions. |
| t | Change a partition's type code. |
| v | Verify disk. |
| w | Write table to disk and exit. |
| x | Extra functionality (experts only). |
| ? | Print this menu. |