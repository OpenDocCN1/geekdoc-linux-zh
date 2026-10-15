![](bbox=[0.22, 0.11, 0.68, 0.48])

Figure 10.25 The bridged IP address, 192.168.20.4, starts with the same three number blocks as the eth0 adapter on the host.

# Sharing Files via FTP

Yes, it lacks a certain elegance. Yes, it's early 80s technology. But my friends, I tell you plainly, it is the easiest and most convenient way to swap files between your host PC and your virtual machines. NFS works well but requires additional configuration, and Samba, in a Linux-to-Linux setting, does not offer significantly greater advantages over FTP for most users. See Figure 10.26 for a Linux-to-VMware FTP session.

> Samba and NFS-based file sharing are covered in detail in Appendix B, "File Sharing with Samba and NFS in VMware."

Most Linux distributions run an FTP server by default. If you shut yours off for security purposes, turn it back on or just leave the server in your virtual machine enabled when you install its copy of Linux. For demonstration purposes, I assume the FTP server is running on the host, however.

There are literally dozens of FTP clients to choose from, ranging from plain-text terminal varieties such as ftp and ncftp (both standard in Linux distributions) as well as elaborate GUI implementations. There is copious documentation on FTP available anywhere you care to look, including the built-in man help pages in Linux.