# 9.3 Installing Linux Printers on Windows

Much like the Windows system.ini, files are broken up into sections starting with a word in brackets; smb.conf file does the same. The [global], [printers], and [homes] are the only three reserved section headers. All others are assumed to be share names available for use. The [global] section options for the entire program. For example, the mangled map option says that all files that Samba end in .htm should instead be written to the Linux server as .html. This makes writing files in Windows and sending them to a Web server easier.

Other options of note include the following.

+   * log file—When smbd fires up, this is where it will write its log file. In the above case, the name of the log file is “log.” plus the name of the machine. This gives unique log files
* dead time—After <dead time> minutes are up no activity, the smb connection goes away. This is good not only to save resources on the Linux server but also allows Samba to recover when a Windows machine crashes. A good choice would be around 15 minutes or so.
* admin users—These users are as good as root. In fact, they have root privileges to all the shares. This should only be you or the person administering Samba here.
* workgroup—The workgroup to attach to. This should be the same name that you set earlier in Windows.

The sections will put in the browse network section of the Windows home directory for the user. The user can then click or mount that directory, and it’s their home directory on Linux.

Once Samba is installed on the network, you can test it by starting smbd and nmbd (which handle a function similar to DNS) and doing a network browse. You should see your Linux machine in the list of machines (see Figure 9–1).

# 9.3 Installing Linux Printers on Windows

Samba knows enough (via the printing = bsd and printcap name = /etc/printcap) to load in all the printers available in the /etc/printcap and make them available to SMB clients. The Linux side does not require any changes, but you may want to make sure that the /etc/printcap file is set successfully and you can print. Samba will also deal with any remote printers