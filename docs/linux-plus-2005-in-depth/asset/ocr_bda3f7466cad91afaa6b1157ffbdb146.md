| Option | Description |
| --- | --- |
| -s address | Specifies the source address of packets for a rule. |
| -d address | Specifies the destination address of packets for a rule. |
| -p protocol | Specifies the protocol type for a rule. |
| -j action | Specifies the action that is taken for a rule. |
| -L chain | Lists rules for a certain chain. If no chain is given, all chains are listed. |
| -P chain policy | Specifies the default policy for a certain chain type. |
| -D number | Deletes a rule for a chain specified by additional arguments. Rules start at number 1. |
| -R number | Replaces a rule for a chain specified by additional arguments. Rules start at number 1. |
| -F chain | Removes all rules for a certain chain. If no chain is specified, it removes all rules for all chains. |

# # Security

In the past decade, hundreds of new services have been made available to Linux systems and the number of Linux users has risen to millions. In addition, Linux systems today are typically made available across networks such as the Internet. As a result, Linux is more prone today to security loopholes and attacks both locally and from across networks. To protect your Linux computer, you should take steps to improve local and network security as well as understand how to detect intruders who manage to breach your Linux system.

# ## Securing the Local Computer

One of the most important security-related practices is to limit access to the physical Linux computer itself. If a malicious user has access to the Linux computer, that user could boot the computer using a floppy disk, USB flash memory drive, or CD-ROM that contains a small operating system and use it to access files on the partitions on the hard disk of the Linux computer without having to log in to the operating system installed on the hard disk. To prevent this, you should lock important computers, such as Linux servers, in a specific room to which only Linux administrators or trusted users have key access; this room is commonly called a **server closet**. Unfortunately, some Linux computers, such as Linux workstations, must be located in public areas. For these computers, you should remove the floppy and CD-ROM devices from the computer. In addition, you should ensure that the boot order listed in the com-