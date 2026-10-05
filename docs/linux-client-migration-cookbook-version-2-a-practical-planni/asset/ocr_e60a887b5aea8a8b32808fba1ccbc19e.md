When planning for this, extra time should be included to test the pam-mount module on the Linux client chosen for the project. When it works, it is a very powerful method of mounting shares automatically.

**Planning tip:** Test and plan use of pam-mount extensively.

# Home directories and shares

During planning, it might be very tempting to push user home directories on Linux clients to Windows shares. This will enable a “inner” client.

Putting the user's home directory on a share would indeed enable logging on to any client and have the same home directory integrated. Using a graphical logon, this would mean getting the same desktop and environment on any client used.

However, care has to be taken. Some session managers (most notably KDE) need to create symbolic links or sockets in the user's home directory as part of normal operation. One of the shortcomings of the SMB file system is that symbolic links or sockets cannot be created in such a file system. This means that any KDE-based application would have problems when running on the desktop machine in a scenario where home directories are remotely mounted on shares.

**Planning tip:** A strategy using remote file shares for mounting of directories which will need to be carefully tested.

# 4.2.4 Printing services in the domain

Of course, it is possible to add printers directly to Linux clients. But this creates extra administrative overhead in a scenario where you are integrating Linux clients into an existing Windows domain that provides printing services already. Since almost all Linux distributions now include the Common UNIX Printing System (CUPS), it is possible to use CUPS in conjunction with Samba on the client to enable printing to the existing domain printers.

If you plan to use CUPS on the Linux clients to print to printers, some issues have to be taken into account:

+   - Is CUPS and Samba integration handled correctly?

+   - Do the printers need authentication? Domain passwords for shared printer access be exposed.

+   - What are the advantages of using print versus direct printing to the printers network interface?

+   - Are drivers available for CUPS for each printer model in use?