# Chapter 17: Setting Up Printers and Printing 751

At this point, you can configure other computers to use your printer. If you try to print from another computer and it doesn't work, here are a few things to try:

+   **Open your firewall** — If you have a restrictive firewall, it may not permit remote users to access your printers. You must allow access to port 513 (UDP and TCP) and possibly port 631 to allow access to printing on your computer. See Chapter 14 for information on configuring your firewall.
* **Enable LPD-style printing** — Certain applications may require an older LPD-style printing service in order to print on your shared printer. To allow LPD-style printing on your CUPS server, you must turn on the cups-lpd service. As root user, type `chkconfig cups-lpd service xinetd daemon restart`. Then restart install the package (yum install cups-lpd).
* **Check names and addresses** — Make sure that entered your computer's name and print queue properly when you configured it on the other computer. Using the IP address instead of the hostname (if that worked, it would indicate a DNS name, resolution problem). Running a tool such as wireshark can let you watch where the transaction fails.

Access changes to your shared printer are made in /etc/cups/cupsd.conf file.

# Configuring a shared Samba printer

Your Linux printers can be configured as shared Samba printers. To share your printer as a Samba (SMB) printer, all you need to do is configure basic Samba server settings as described in Chapter 18. All your printers should be shared on your local network by default. The next section shows what the resulting settings look like and how you might want to change them.

# Understanding smb.conf for printing

When you configure Samba, as described in Chapter 18, the /etc/samba/smb.conf file is configured to allow all your configured printers to be shared. Here are a few lines you might find in [global] and [printers] sections of the smb.conf file that relate to printer sharing:

```
[global]
workgroup = MYGROUP
serverstring = Samba Server
security = share
printcap name = /etc/printcap
load printers = yes
printing = cups
encrypt passwords = yes
smb passwd file = /etc/samba/smbpasswd
unix password sync = Yes
```

[printers]