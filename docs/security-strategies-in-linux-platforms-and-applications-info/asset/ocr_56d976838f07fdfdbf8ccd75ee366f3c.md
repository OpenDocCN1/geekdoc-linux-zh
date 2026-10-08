# PART 2 | Layered Security and Linux

| TABLE 4-7 Groups with special permissions for users |
| DESCRIPTION | GROUP NAME |
| Access external storage devices automatically | plugdev |
| Administer the system | admin |
| Configure printers | lpadmin |
| Connect to the Internet using a modem | dip |
| Connect to wireless and ethernet networks | netdev |
| Monitor system logs | adm |
| Mount user-space files (FUSE)* | fuse |
| Send and receive faxes | fax |
| Share files with the local network | sambashare |
| Use audio devices | audio |
| Use CD-ROM drives | cdrom |
| Use floppy drives | floppy |
| Use modems | dialout |
| Use tape drives | tape |
| Use video devices | video |

* FUSE is an acronym for Filesystems in Userspace.

The groups described in this section apply only to Ubuntu systems. It's certainly possible to configure other Linux distributions with such group privileges, however. To do so, you'll need to do the following:

+   - If the specified groups don't already exist on the target distribution, /etc/group and /etc/shadow configuration files, you may need to create them.
- On an Ubuntu system, identify the groups owned by the noted group. One method is with the find command. For example, the following command identifies those files owned by dip group. On Ubuntu systems, user members of that group are allowed to dial out through a telephone modem.
- # find -group dip
- Check the octal permissions associated with the noted files. For more information on octal permissions, see Chapter 5.
- If those same files exist on the target distribution, use commands like chmod to modify ownership and octal permissions accordingly. In some cases, you may need to create the target files.