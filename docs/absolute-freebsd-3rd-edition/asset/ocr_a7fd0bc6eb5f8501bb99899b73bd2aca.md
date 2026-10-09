# **/etc/dma/**

The Dragonfly Mail Agent (DMA) stores its configuration in /etc/dma/. We discuss DMA in Chapter 20.

# **/etc/freebsd-update.conf**

This file is used by freebsd-update(8) when getting binary updates for your server. See Chapter 18 for details.

# **/etc/fstab**

See Chapter 10 for a discussion on the filesystem table, /etc/fstab.

# **/etc/ftp.\***

The FTP daemon ftpd(8) uses these files to determine who may access the system via FTP and what access they have upon a successful connection. Unless you’re running a large FTP site, you should be using sftp(1) instead.

# **/etc/group**

Assigning users to groups is covered in painful detail in Chapter 9.

# **/etc/hostid**

Certain software expects every host to have a universally unique ID, or UUID. If you’re running on real hardware, this UUID is burned into the mainboard and is accessible via kenv(8). Virtual hosts can generate a UUID from software. The /etc/hostid file contains that UUID.