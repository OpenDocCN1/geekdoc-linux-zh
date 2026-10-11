
## 2.3.1.2 Anonymous Read-Write Document Server

We should view this configuration as a progression from the previous example. The difference is that shared access is now forced to the user identity of jackb and to the primary group jackb belongs to. One other refinement we can make is to add the user jackb to the smbpasswd file. To do this, execute:

```
root# smbpasswd -a jackb
New SMB password: m0r3pain
Retype new SMB password: m0r3pain
Added user jackb.
```

Addition of this user to the smbpasswd file allows all files to be displayed in the Explorer Properties boxes as belonging to jackb instead of to User Unknown.

The complete, modified smb.conf file is as shown in Example 2.3.2.

### Example 2.3.2 Modified Anonymous Read-Write smb.conf

```
# Global parameters
[global]
  workgroup = MIDEARTH
  netbios name = HOBBIT
  security = SHARE
[data]
  comment = Data
  path = /export
  force user = jackb
  force group = users
  read only = No
  guest ok = Yes
```

## 2.3.1.3 Anonymous Print Server

An anonymous print server serves two purposes:

- It allows printing to all printers from a single location.
- It reduces network traffic congestion due to many users trying to access a limited number of printers.

In the simplest of anonymous print servers, it is common to require the installation of the correct printer drivers on the Windows workstation. In this case the print server will be designed to just pass print jobs through to the spooler, and the spooler should be configured to do raw pass-through to the printer. In other words, the print spooler should not filter or process the data stream being passed to the printer.

In this configuration, it is undesirable to present the Add Printer Wizard, and we do not want to have automatic driver download, so we disable it in the following configuration. Example 2.3.3 is the resulting **smb.conf** file.

### **Example 2.3.3 Anonymous Print Server smb.conf**

```
# Global parameters
[global]
        workgroup = MIDEARTH
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

![](img/86d74c6cc862465e3a42e6dc3c90935a_69_0.png)

Make sure that the directory `/var/spool/samba` is capable of being used as intended. The following steps must be taken to achieve this:

- The directory must be owned by the superuser (root) user and group:

```
root# chown root.root /var/spool/samba
```

- Directory permissions should be set for public read-write with the sticky bit set as shown:

```
root# chmod a+twrx /var/spool/samba
```

The purpose of setting the sticky bit is to prevent users who do not own the temporary print file from being able to take control of it with the potential for devious misuse.

> **NOTE**
> On CUPS-enabled systems there is a facility to pass raw data directly to the printer without intermediate processing via CUPS print filters. Where use of this mode of operation is desired, it is necessary to configure a raw printing device. It is also necessary to enable the raw mime handler in the /etc/mime.conv and /etc/mime.types files. Refer to Section 21.3.4.

## 2.3.1.4 Secure Read-Write File and Print Server

We progress now from simple systems to a server that is slightly more complex.

Our new server will require a public data storage area in which only authenticated users (i.e., those with a local account) can store files, as well as a home directory. There will be one printer that should be available for everyone to use.

In this hypothetical environment (no eavesdropping was conducted to obtain this data), the site is demanding a simple environment that is secure enough but not too difficult to use.

Site users will be Jack Baumbach, Mary O'ville, and Amed Seltbab. Each will have a password (not shown in further examples). Mary will be the printer administrator and will own all files in the public share.

This configuration will be based on user-level security that is the default, and for which the default is to store Microsoft Windows-compatible encrypted passwords in a file called /etc/samba/smbpasswd. The default smb.conf entry that makes this happen is passdb backend = smbpasswd, guest. Since this is the default, it is not necessary to enter it into the configuration file. Note that the guest backend is added to the list of active passdb backends no matter whether it is specified directly in Samba configuration file or not.

### Example 2.3.4 Secure Office Server smb.conf

```
# Global parameters
[global]
  workgroup = MIDEARTH
  netbios name = OLORIN
  printcap name = cups
  disable spoolss = Yes
  show add printer wizard = No
  printing = cups
[homes]
  comment = Home Directories
  valid users = %S
  read only = No
  browseable = No
[public]
  comment = Data
  path = /export
  force user = maryo
  force group = users
  guest ok = Yes
  read only = No
[printers]
  comment = All Printers
  path = /var/spool/samba
  printer admin = root, maryo
  create mask = 0600
  guest ok = Yes
  printable = Yes
  use client driver = Yes
  browseable = No
```

1. Add all users to the operating system:

```
root# useradd -c "Jack Baumbach" -m -g users -P m0R3pain jackb
root# useradd -c "Mary Orville" -m -g users -p secret maryo
root# useradd -c "Amed Sehkah" -m -g users -p secret amed
```

2. Configure the Samba smb.conf file as shown in Example 2.3.4.

3. Initialize the Microsoft Windows password database with the new users:

```
root# smbpasswd -a root
New SMB password: bigsecret
Reenter smb password: bigsecret
Added user root.

root# smbpasswd -a jackb
New SMB password: m0r3p4in
Retype new SMB password: m0r3p4in
Added user jackb.

root# smbpasswd -a maryo
New SMB password: secret
Reenter smb password: secret
Added user maryo.

root# smbpasswd -a ameds
New SMB password: mysecret
Reenter smb password: mysecret
Added user ameds.
```

4. Install printer using the CUPS Web interface. Make certain that all printers that will be shared with Microsoft Windows clients are installed as raw printing devices.

5. Start Samba using the operating system administrative interface. Alternately, this can be done manually by executing:

```
root# nmbd; smbd;
```

Both applications automatically execute as daemons. Those who are paranoid about maintaining control can add the -D flag to coerce them to start up in daemon mode.

6. Configure the /export directory:

```
root# mkdir /export
root# chown maryo.users /export
root# chmod u=rwx,g=rwx,o=rwx /export
```

7. Check that Samba is running correctly:

```
root# smbclient -L localhost -U%
Domain=[MIDEARTH]  OS=[UNIX]  Server=[Samba-3.0.20]
```

| Sharename | Type | Comment |
| :---------- | :---- | :------ |
| public | Disk | Data |
| IPC$ | IPC | IPC Service (Samba-3.0.20) |
| ADMIN$ | IPC | IPC Service (Samba-3.0.20) |
| hplj4 | Printer | hplj4 |

Server | Comment
