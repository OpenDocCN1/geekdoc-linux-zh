
## df
Filesystem      1k-blocks    Used Available Use% Mounted on
/dev/hda2       18714368  9642600  8121124 55% /
/dev/hda1        46636   13247    30981 30% /boot
none            120016       0   120016  0% /dev/shm
192.168.2.67:/music 36875376 20895920 14106280 60% /music

Make sure that the desired mount point exists before using the mount command. When finished using the directory (perhaps for copying backups), you can use the umount command to remove the remote file system. Note that if you specify the root directory (/) as a mount point, you cannot unmount the NFS directory until you reboot (because Linux complains that the file system is in use).

## Putting Samba to Work

Samba uses the Session Message Block (SMB) protocol to enable the Windows operating system (or any operating system) to access Linux files. Using Samba, you can make your Ubuntu machine look just like a Windows computer to other Windows computers on your network. You do not need to install Windows on your PC.

Samba is a complex program—so much so that the book Samba Unleashed (Sams Publishing, 2000, ISBN 0-672-31862-8) is more than 1,200 pages long. The Samba man page (when converted to text) for just the configuration file is 330KB and 7,013 lines long. Although Samba is complex, setting it up and using it does not have to be difficult. There are many options, which accounts for some of Samba's complexity. Depending on what you want, Samba's use can be as easy or as difficult as you would like it to be.

Fortunately, Ubuntu includes the Samba Web Administration Tool (SWAT), which you can use to configure Samba by using the Mozilla web browser. SWAT provides an easy way to start and stop the Samba server; set up printing services; define remote access permissions; and create Samba usernames, passwords, and shared directories. This section delves into the basics of configuring Samba, and you should first read how to manually configure Samba to get an understanding of how the software works. At the end of this section, you will see how to enable, start, and use SWAT to set up simple file sharing.

Like most of the software that comes with Ubuntu, Samba is licensed under the GPL and is free. Installation is straightforward and the software can be installed using either synaptic or apt-get.

Installing from source code can be more time-consuming. If you do not want to install using Ubuntu's default locations, however, installing from the source code is a more configurable method. Just download the source from http://www.samba.org/ and unpack the files. Change into the source directory and, as root, run the command ./configure along with any changes from the defaults. Then run make, make test (if you want), followed by make install to install Samba in the specified locations.

When you install Samba, it is a good idea to also install the samba-doc and samba-doc-pdf packages because they contain extensive documentation in text, PDF, and HTML format. After you install it, you can find this documentation in /usr/share/doc/samba*/doc. If

you install Samba using your Ubuntu disc, you can find a large amount of documentation in the directory tree starting at /usr/share/doc/samba-doc or /usr/share/doc/samba-doc.pdf in several formats, including PDF, HTML, and text, among others. Altogether, almost 3MB of documentation is included with the source code.

After installing Samba, you can either create the file /etc/smb.conf or use the smb.conf file supplied with Samba, which is located by default under the /etc/samba directory with Ubuntu. You can find nearly a dozen sample configuration files under the /usr/share/doc/samba/examples directory.

### NOTE

Depending on your needs, smb.conf can be a simple file of fewer than 20 lines or a huge file spanning many pages of text. If your needs are complex, I suggest picking up a copy of Samba Unleashed.

## Manually Configuring Samba with /etc/samba/smb.conf

The /etc/samba/smb.conf file is broken into sections. Each section is a description of the resource shared (share) and should be titled appropriately. The three special sections are as follows:

- [global]—Establishes the global configuration settings (defined in detail in the smb.conf man page and Samba documentation, found under the /usr/share/doc/samba/docs directory)
- [homes]—Shares users’ home directories and specifies directory paths and permissions
- [printers]—Handles printing by defining shared printers and printer access

Each section in your /etc/samba/smb.conf configuration file should be named for the resource being shared. For example, if the resource /usr/local/programs is being shared, you could call the section [programs]. When Windows sees the share, it is called by whatever you name the section (programs in this example). The easiest and fastest way to set up this share is with the following example from smb.conf:

```
[programs]
path = /usr/local/programs
writeable = true
```
