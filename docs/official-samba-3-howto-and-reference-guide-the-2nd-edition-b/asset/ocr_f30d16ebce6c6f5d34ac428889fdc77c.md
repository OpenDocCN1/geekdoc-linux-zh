However, currently only Windows NT, 2000, and XP are supported by the CUPS drivers. You will also need to get the respective part of the Adobe driver if you need to support Windows 95, 98, and Me clients.

# 21.10.2 Prepare Your smb.conf for cupsaddsmb

Prior to running **cupsaddsmb**, you need the settings in `smb.conf` as shown in Example 21.10.1.

# Example 21.10.1 smb.conf for cupsaddsmb Usage

```
```text
[global]
    load printers = yes
    printing = cups
    printcap name = cups
[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
    public = yes
# setting depends on your requirements
    guest ok = yes
    writable = no
    printable = yes
    printer admin = root
[print$]
    comment = Printer Drivers
    path = /etc/samba/drivers
    browseable = yes
    guest ok = no
    read only = yes
    write list = root
```
```

# 21.10.3 CUPS “PostScript Driver for Windows NT/200x/XP”

CUPS users may get the exact same package from `http://www.cups.org/software.html`. It is a separate package from the CUPS-based software files, tagged as CUPS 1.1.x Windows NT/200x/XP Printer Driver for Samba (tar.gz, 192k). The filename to download is `cups-samba-1.1.x.tar.gz`. Upon untar and unzipping, it will reveal these files:

```
```bash
root$ tar xvfz cups-samba-1.1.19.tar.gz
cups-samba.install
cups-samba.license
cups-samba.readme
cups-samba.remove
```
```