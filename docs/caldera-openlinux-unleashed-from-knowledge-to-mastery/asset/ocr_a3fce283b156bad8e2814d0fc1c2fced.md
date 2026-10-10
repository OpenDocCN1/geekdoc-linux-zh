UNIX has a strict and consistent notion of file ownership. Windows 95/98 SMB protocols have no concept whatsoever of file ownership. There is no way, therefore, for a UNIX SMB server to signal to a Windows 95/98 client that permission to access a file is denied because of lack of ownership.

Many SMB clients convert passwords to uppercase before transmitting them. Samba tries to compensate by trying various permutations of passwords. Other SMB clients encrypt passwords before transmitting them. Samba supports encrypted passwords.

SMB provides many types of locks to Windows clients. Samba can simulate most of these locks, but it cannot enforce locking against UNIX programs. That is, if a Windows client locks a file, it will be locked for other Windows clients, but a UNIX process can access the file without difficulty. This can lead to problems if both Windows and UNIX processes update a file at the same time.

Finally, SMB is poorly documented. Although the Samba team did receive some documentation and help from Microsoft, and SMB is an X/Open standard, much of the Samba functionality was implemented by reverse-engineering the protocol. It is a tribute to the Samba team’s tenacity that Samba works as well as it does.

# # Samba Configuration

Samba uses the file */etc/samba.d/smb.conf* to hold configuration options. Samba has a huge number of configuration options, all of which are described in the *smb.conf(5)* manual page. To aid in your understanding of Samba, let’s look at a simple configuration file that illustrates some of the common options and then build from there.

The configuration file (as is usual on UNIX) is a plain text file. Blank lines and lines beginning with *#* or *;* are ignored.

The configuration file is divided into a number of sections. The *global* section controls the overall behavior of Samba. Each *share* has its own section that controls parameters related to it. (A share is a shared resource such as a printer or disk directory that the server offers to clients.)

# ## Global Configuration Options

Global options apply to the Samba server as a whole. Here are some global settings. They are edited versions of the sample configuration options in */etc/samba.d/smb.conf.sample* supplied with Caldera OpenLinux.

```
# Sample SAMBA file
# The global settings begin with the tag [global]
```