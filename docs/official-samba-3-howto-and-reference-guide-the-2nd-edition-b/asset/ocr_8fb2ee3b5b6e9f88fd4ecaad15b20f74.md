In this configuration, it is undesirable to present the Add Printer Wizard, and we do not want to have automatic driver download. so we disable it in the following configuration. Example 2.3.3 is the resulting **smb.conf** file.

# **Example 2.3.3 Anonymous Print Server smb.conf**

```
# Global parameters
[global]
        workgroup = MDEARTH
        netbios name = LUTHIEN
        security = share
        printcap name = cups
        disable spoolss = Yes
        show add printer wizard = No
        printing = cups
[printers]
        comment = All Printers
        path = /var/spool/samba
        guest ok = Yes
        printable = Yes
        use client driver = Yes
        browseable = No
```

The above configuration is not ideal. It uses no smart features, and it deliberately presents a less than clean solution. But it is basic, and it does print. Samba makes use of the direct printing application program interface that is provided by CUPS. When Samba has been compiled and linked with the CUPS libraries, the default printing system will be CUPS. By specifying that the printcap name is CUPS, Samba will use the CUPS library API to communicate directly with CUPS for all printer functions. It is possible to force the use of external printing commands by setting the value of the `printing` to either SYSV or BSD, and thus the value of the parameter *printcap name* must be set to something other than CUPS. In such case, it could be set to the name of any file that contains a list of printers that should be made available to Windows clients.

![](bbox=[0.07, 0.74, 0.94, 0.9])

Make sure that the directory `/var/spool/samba` is capable of being used as intended. The following steps must be taken to achieve this:

+   * The directory must be owned by the superuser (root) user and group: