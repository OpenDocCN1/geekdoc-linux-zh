# Figure 17.8

The SWAT Password screen.

![](bbox=[0.25, 0.17, 0.9, 0.65])

# Caution

If you like to have your /etc/smb.conf file full of comments that explain the purpose of each entry or that maintain a change history, do not use the SWAT interface. SWAT does not maintain comments and writes a very packed configuration file.

# Analyzing the Samba Configuration File

Before we begin looking at Linux in specific roles in a Windows network, let's first take a look at the Samba configuration file. This file has numerous options available and complete coverage of them is beyond the scope of this book. However, we will cover the common options that someone new to Samba is likely to use and then provide some concrete examples of Linux as both a client and a server using Samba.

On Red Hat Linux systems, the default location of the Samba configuration file is in the /etc directory in a file named smb.conf. The smb.conf file that comes with Red Hat can serve as a starting point and with the exception of changing the workgroup name, it is what was used in the previous demonstration of smbclient.