# 1174

-c blockno Correct and repair the given block. This correct and repair option may not be applicable to all devices supported by rmformat, bad-block-management capability can be implemented in either the device or the driver. If the drive or driver supports management, a best effort is made to rectify the bad block. If the bad block cannot be rectified, a message is displayed to indicate the failure to repair. You can specify the block in decimal, octal, or hexadecimal format.

The normal diskette and PCMCIA memory and ata cards do not support bad-block management.

-D 720KB (3.5-inch) double-density diskette. This option is the default for double-density type drives. You need to use this if the drive is a high- or extended-density type.

-e Eject the medium on completion. This feature may not be available if the drive does not support motorized eject.

-F quick

Format the medium. The quick option starts a format without certification or format with limited certification of certain tracks on the medium.

The long option starts a complete format. For some devices this include the certification of the whole medium by the drive itself.

The force option starts a long format without user confirmation before the format is started. For drives that have a password protection mechanism, force clears the password while formatting. This feature is useful when a password is no longer available. On those medium that do not have such password protection, force starts a long format.

In legacy media such as diskette drives, all options start a long format depending on the mode (Extended-Density mode, High-Density, or Double-Density mode) with which the diskette operates by default. On PCMCIA memory cards, all options start a long format.

-H Format 1.44 MB (3.5-inch) high-density diskette. This option is the default for high-density type drives. Use this option if the drive is the Extended-Density type.

-p Print the protection status of the medium. This option prints information about whether the medium is write, read, or protected.

-R enable

Enable read/write protection with a password or disable the password read/write protection. This option always works in interactive mode default because the password is requested from the user in an interactive manner to maintain security.