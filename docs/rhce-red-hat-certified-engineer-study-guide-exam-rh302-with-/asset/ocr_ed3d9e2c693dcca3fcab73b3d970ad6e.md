# Performing Multi-Boot Installations 181

# EXERCISE 8.2 (continued)

+   4. Run /sbin/lilo to update the boot map and install the boot sector.

+   5. Boot the system, and verify that your changes work as planned.

# LILO Error Messages

LILO actually loads in two stages. LILO's first stage resides in the MBR or boot sector of a partition, depending on whether LILO is installed as the primary or a secondary boot loader. LILO's second stage resides in the file /boot/boot/b. LILO displays its prompt by letter as it loads. So, an incomplete LILO prompt provides useful information about what went wrong. LILO sometimes displays a modified prompt that indicates an error condition. Table 8.3 describes the LILO error messages.

# TABLE 8.3 LILO Error Messages

| Prompt | Meaning |
| --- | --- |
| nothing | LILO did not load. |
| L | First stage loaded. |
| LI | Second stage loaded. |
| LIL | Second stage started. |
| LIL? | Second stage loaded at incorrect address. |
| LIL - | Descriptor table is corrupt. |
| LILO | LILO loaded correctly. |

# Windows 9x

Configuring a multi-boot system that boots Microsoft Windows 9x and Linux is straightforward. If possible, you should install Microsoft Windows before installing Linux. If you perform a Workstation or custom installation of Red Hat Linux, the installation program can automatically configure the system to boot both operating systems. Simply ensure that the installation program's LILO Configuration dialog box lists the partition containing Microsoft Windows.