resolution problem). A tool such as wireshark can let you watch where the transaction fails.

Access changes to your shared printer are made in the `/etc/cups/cupsd.conf` file.

# ## Configuring a shared Samba printer

Your Linux printers can be configured as shared SMB printers. To share your printer as a Samba (SMB) printer, all you need to do is configure basic Samba server settings as described in Chapter 17. All your printers should be shared on your local network by default. The next section shows what the resulting settings look like and how you might want to change them.

# ## Understanding smb.conf for printing

When you configure Samba, as described in Chapter 17, the `/etc/samba/smb.conf` file is configured to allow all your configured printers to be shared. Here are a few lines you might find in the `[global]` and `[printers]` sections of the `smb.conf` file that relate to printer sharing:

```
```text
[global]
    workgroup = MYGROUP
    serverstring = Samba Server Version %v
    security = share
    printcap name = /etc/printcap
    load printers = yes
    printing = cups
    encrypt passwords = yes
    smb passwd file = /etc/samba/smbpasswd
    unix password sync = Yes

[printers]
    comment = All Printers
    path = /var/spool/samba
    guest ok = yes
    browseable = no
    writable = no
    printable = yes
```
```

The settings shown resulted from configuring Samba from the Samba Server Configuration (System → Administration → Samba) window. You need to install the system-config-samba package to use the Samba Server Configuration window. In this case, I selected to use encrypted passwords. The lines show that printers from `/etc/printcap` were loaded and that the CUPS service is being used. The `/etc/samba/smbpasswd` file stores the encrypted passwords. Because password sync is on, each user’s Samba password is synchronized with the local UNIX password for the user.