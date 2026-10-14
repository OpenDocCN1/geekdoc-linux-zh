# How to Connect to Windows Machines

Users frequently find themselves installing SuSE Linux in a network that contains Microsoft Windows-based PCs. Situations arise in which the user would want to exchange files and printing services with those PCs. The user always can use FTP to exchange files from a Linux machine to a Windows machine and back, but that isn't very convenient. Windows machines use a special networking protocol that enables them to share files and printers with each other. This protocol used to be called Server Message Block (SMB) but is now referred to as Common Internet File System (CIFS). If you have ever used a Windows machine in a network, you are familiar with the Network Neighborhood. The Network Neighborhood enables you to see all the Windows-based PCs that are on the network, connect to them, and exchange files and services.

Microsoft Windows PCs use the SMB protocol to communicate with each other. Andrew Tridgell started a project in 1991 that is currently known as Samba. Samba is the result of reverse engineering the SMB protocol by Andrew and others. Samba runs on UNIX machines to enable them to share files and printers with Microsoft Windows-based PCs on a network.

Samba is considered one of the most prominent projects produced by the open source community. It enabled the integration of Microsoft Windows PCs with the rest of the UNIX world and vice versa. Samba provided the missing link between the two worlds, and did a good job at it, too.

Even though SMB has been renamed CIFS, the rest of the UNIX world still refers to it as SMB. Therefore, to accommodate both worlds, we will refer to it as SMB/CIFS.

**TIP** If you are wondering how in the world Samba got its name, you might be surprised by the answer. Andrew Tridgell initially called it SMB server, but an existing product already had that name. So, he ran a command that searched the dictionary to find all the words that contained the letters S.M.B. A list of words came out, and he picked Samba.

# Installing Samba

Installing Samba should not be too difficult because it already comes pre-packaged with SuSE Linux. Chances are that it's already installed on your system. The package requirements for running Samba are as follows:

+   **Package requirements:**
+   **Series n:**
+   - Samba
+   **Kernel requirements:**
+   - Filesystems, Network filesystems, SMB filesystem support (only if you are planning to access Windows shares)