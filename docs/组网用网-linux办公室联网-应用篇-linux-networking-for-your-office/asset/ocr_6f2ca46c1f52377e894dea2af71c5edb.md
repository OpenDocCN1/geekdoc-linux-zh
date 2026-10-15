Using a Linux computer running Samba can be an excellent way to share printers on a network of DOS, Windows, or OS/2 computers. As described in Chapter 14, “Preparing to Share a Printer,” you can share a printer either “raw,” by using Windows drivers for the specific model you’re using, or by using Ghostscript to make the printer look like a PostScript printer to Windows. Of course, if the printer has PostScript built in, the two options produce very similar results in practice.

Printer sharing requires that you have Samba installed and running. Basic Samba configuration is covered in Chapter 11, “Samba: Sharing Files with DOS, Windows, and OS/2,” particularly in the section titled “Setting Samba Options.” This chapter helps you configure your Linux/Samba print server.

# Setting Samba Printer Options

Just as with Samba file sharing, you can configure Samba printer shares either using a GUI utility or by directly editing the /etc/smb.conf file. Unfortunately, the version of linuxconf included with Red Hat Linux 6.0 is rather fussy about the form of the printer share information in /etc/smb.conf, and the Samba printer configuration section of linuxconf doesn’t work with many configurations. You might therefore need to use the Samba Web Administration Tool (SWAT; see the sidebar on p. 262) for a GUI configuration tool for Samba. Figure 16.1 shows SWAT displaying a Samba printer share configuration.

![](bbox=[0.32, 0.78, 0.82, 0.95])