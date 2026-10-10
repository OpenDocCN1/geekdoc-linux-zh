
Make sure that the server is running, and restart the client. If you see an error messages such as “Program not registered,” the needed NFS daemons aren’t running on the client system. If you see a message such as “Permission denied,” there’s a problem on the server side. You may have forgotten to run *exports* (see the section “Configuring `/etc/exports/,” earlier in this section).

## Configuring Samba Networking

Samba is a Linux implementation of the Server Message Block (SMB) protocol used in Windows networking. With Samba, you can easily create peer-to-peer networks (akin to the Network Neighborhood concept in Windows 95/98/NT) that provide seamless file exchange between Linux and Windows systems. In peer-to-peer networking, users can choose to share certain directories on the network. A directory that is made available for network access is called a *share*. In addition, users can specify the level of access that is available for a given share. In *share-level access*, the share is made available to any network user, although it is possible to protect the share with a pass-word. In *user-level access*, the share is made available only to a net-work user who has the same username as the local share’s owner. In both share- and user-level access, the share can be made available read only, or with full read and write privileges.

In Windows-only environments, Microsoft Windows NT Server is required to make user-level access available to Windows users. However, it is possible to use Samba to mimic the behavior of Windows NT Server so that user-level access (and other advanced networking capabilities) become available to network users, even though Windows NT Server is not running on the network. However, considerable more expertise—including familiarity with Windows NT Server—is required to configure Samba to emulate Windows NT. In accordance with this book’s focus on single-user Linux systems and small networks, this section focuses on configuring Samba for peer-to-peer networking for a small network of up to, say, a dozen computers.

To use Samba, you must configure your Linux system to start the Samba software automatically. The best way to do this is to choose the Samba option when you install your Linux distribution. If you did not enable Samba when you installed Linux, you may wish to do so by upgrading to a more recent version of your Linux distribution, which will ensure that you get the latest (and more secure) versions of the Samba software. Should you wish to keep using your current distribution, check your distribution’s manual to determine how to enable Samba services on your system.

## Configuring /etc/smb.conf

Samba distributions typically include a sample smb.conf file, which is installed in the /etc directory. By making a few simple changes to this file, you can quickly enable peer-to-peer networking. After you do so, Windows users will be able to access files made available on a Linux system.

The following tables discuss the smb.conf options that need to be enabled to establish peer-to-peer networking between Linux and Windows systems.

> **TIP** To enable user-level shares with Samba, you must establish user accounts on both systems—Windows and Linux—that share the same username. For example, suppose Suzanne uses a Windows 98 system with the username suzanne. To access her directories on a Linux system running Samba, the Linux system must recognize a user named suzanne. This is required because Windows systems automatically supply the current user’s name when requesting an SMB connection. It is not necessary for both of these accounts to have the same password.

After you enable these necessary options in smb.conf and restart your system, the Samba server will make a Windows user’s Linux directories available to a Windows user who has the same username. The Linux directories will show up in this Windows user’s Network Neighborhood (a networking feature of Windows 95/98/NT). These same options enable Linux users to access their shares on Windows systems, as long as these shares have been made available for network sharing. (See your Windows manual for information on enabling file sharing with Windows.)

The Samba configuration file (`/etc/smb.conf`) is divided into several sections, including Global, Home, and Printers. The following tables (Global Section Configuration, Home Section Configuration, and Printers Section Configuration) discuss only those options that are pertinent to peer-to-peer networking. In the sample `/etc/smb.conf`, you may see additional options that are commented out with a semicolon (`;`) or hash mark (`#`); leave these options unchanged.

## Configuring the Global Section Options

The Global section includes options that govern the general behavior of the Samba server. You can quickly enable peer-to-peer networking by making a few simple changes to this section, as noted in the Global Section Configuration table. You may see additional options in the sample `/etc/smb.conf` configuration file; leave them commented out.

### GLOBAL SECTION CONFIGURATION

| Use This Option | To Do This |
| :--- | :--- |
| `encrypt passwords=[ yes \| no ]` | Specify whether Samba should expect and send encrypted passwords. Note that encrypted passwords are enabled by default on Windows 98 and Windows NT 4.0 SP3 or later. If you are using Windows 95 or an earlier version of NT, choose **no**. To enable encrypted passwords with Samba, you must define the Samba users with the `smbpasswd` utility, discussed in this chapter. |
| `hosts allow=[IP address]` | Specify a comma, space, or tab-delimited list of the IP addresses of clients that have permission to access the Samba shares on this machine. |
| `load printers=[ yes \| no ]` | Choose whether to make local printers available to Samba users. |

| Use This Option | To Do This |
| :--- | :--- |
| `security= user \| share` | Specify whether the Samba server enables user-level or share-level access. With user-level access, a remote user can access only those files on the Linux system that are owned by the same username. With share-level access, remote users can access shared directories even if they do not have the same username as the user who owns the Linux files. Choose user-level access to make a specific user’s Linux directories available to that user, and that user only, via network connections. Choose share-level access to make the Linux directories available to all network users, provided they know the password required to access these directories. You should also choose share-level access if you want to enable guest accounts, which do not require a password. |
| `server string=string` | Use the specified string to describe the Samba server to network users. |
| `smb passwd file=filename` | Specify the location of the Samba password file, which is required if encrypted passwords are used. (See **encrypt passwords** in this table.) The default is `/etc/smbpasswd`. |
| `workgroup=WORKGROUP` | Specify the name of the Windows workgroup. By convention, this is typed in capital letters. This setting must correspond to the workgroup name specified in the Network Control Panel in Microsoft Windows. |

## Homes Section Configuration

In the Homes section, you specify how the Samba server makes remote users’ home directories available to them. By default, a remote user with a username corresponding to a valid username on the Linux system is granted access to that user’s home directory.

### HOMES SECTION CONFIGURATION

| Use This Option | To Do This |
| :--- | :--- |
| `available=[ yes \| no ]` | Make the service available (yes) or unavailable (no). |
| `browseable=[ yes \| no ]` | Display (yes) or hide (no) this share in share lists generated by users other than the share’s owner. |
| `comment=string` | Describe the share. This text is made available to users who are browsing available shares on the network. |
| `writable=[ yes \| no ]` | Make the share available as read and write (yes) or as read only (no). |

## Printers Section Configuration

The Printers section defines network access to local printers.

### PRINTERS SECTION CONFIGURATION

| Use This Option | To Do This |
| :--- | :--- |
| `browseable=[ yes \| no ]` | Specify whether to make local printers viewable when remote users browse available shares. |
| `comment=string` | Display the specified string in the comment column of network browsing utilities. |
| `guest ok=[ yes \| no ]` | Specify whether guest access is enabled. |
| `printable=[ yes \| no ]` | Enable (yes) or disable (no) printing. |
| `public=[ yes \| no ]` | Permit the guest users to print (yes) or prohibit printing by the guest user. |
