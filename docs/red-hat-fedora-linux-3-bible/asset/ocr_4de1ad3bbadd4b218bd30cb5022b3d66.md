• /home — This is a similar concept to sharing mail, except that all users have access to their home directories from any of the NFS clients. Again, you would mount /home on the same mount point on each client computer. When the user logs in, that user has access to all the user’s start-up files and data files contained in the /home/user directory.

> TIP: If your users rely on a shared /home directory, you should make sure that the NFS server that exports the directory is fairly reliable. If /home isn’t available, the user may not have the start-up files to log in correctly, or any of the data files needed to get data done. One workaround is to have a minimal set of start-up files ( .bashrc, .Xdefaults, and so on) available in the user’s home directory when the NFS directory is not mounted. Doing so allows the user to log in properly at those times.

• /project — Although you don’t have to use this name, a common practice among users on a project is to share a directory structure containing files that people on the project need to share. This way everyone can work on original files and keep copies of the latest versions in one place. (Of course, a better way to manage a project is with CVS or some other version control-type software, but this is a simple work-around.)

• /var/log — An administrator can keep track of log files from several different computers by mounting the /var/log file on the administrator’s computer. (Each server may need to export the directory to allow root to be mapped between the computers for this to work.) If there are problems with a computer, the administrator can then easily view the shared log files live.

If you are working exclusively with Fedora, Red Hat Linux, and other UNIX systems, NFS is probably your best choice for sharing file systems. If your network consists primarily of Microsoft Windows computers or a combination of systems, you may want to look into using Samba for file sharing.

# Setting Up a Samba File Server

Samba is a software package that comes with Fedora and Red Hat Linux systems. Samba enables you to share file systems and printers on a network with computers that use the Server Message Block (SMB) protocol. SMB is the protocol that is delivered with Windows operating systems for sharing files and printers. Although you can’t always count on NFS being installed on Windows clients (unless you install it yourself), SMB is always available (with a bit of setup).

On Fedora, the Samba software package contains a variety of daemon processes, administrative tools, user tools, and configuration files. To do basic Samba configuration, you can start with the Samba Server Configuration window. This window provides a graphical interface for configuring the server and setting directories to share.

Most of the Samba configuration you do ends up in the/etc/samba/smb.conf file. If you need to access features that are not available through the Samba Server Configuration window,