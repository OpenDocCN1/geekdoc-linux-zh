- The directory into which Samba will spool the file must have write access for the guest account. The following commands will ensure that this directory is available for use:

```
root# mkdir /var/spool/samba
root# chown nobody.nobody /var/spool/samba
root# chmod a+rw /var/spool/samba
```

The contents of the **smb.conf** file is shown in Example 7.3.2.

# **Example 7.3.2** smb.conf for Anonymous Printing

```
# Global parameters
[global]
workgroup = MIDEARTH
netbios name = GANDALF
security = SHARE
passdb backend = guest
printing = cups
printcap name = cups
[printers]
comment = All Printers
path = /var/spool/samba
printer admin = root
guest ok = Yes
printable = Yes
use client driver = Yes
browseable = No
```

> **NOTE**
> 
> On CUPS-enabled systems there is a facility to pass raw data directly to the printer without intermediate processing via CUPS print filters. Where use of this mode of operation is desired, it is necessary to configure a raw printing device. It is also necessary to enable the raw mime handler in the /etc/mime.conv and /etc/mime.types files. Refer to Chapter 21, “CUPS Printing Support”, Section 21.3.4.

The example in Example 7.3.2 uses CUPS for direct printing via the CUPS library API. This means that all printers will be exposed to Windows users without need to configure a printcap file. If there is necessity to expose only a sub-set of printers, or to define a special type of printer (for example, a PDF filter) the **printcap name = cups** can be replaced with the entry **printcap name = /etc/samba/mymprintcap**. In this case the file specified should contain a list of the printer names that should be exposed to Windows network users.