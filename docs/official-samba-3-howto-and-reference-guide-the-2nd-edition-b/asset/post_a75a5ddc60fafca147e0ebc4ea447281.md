
connection/authentication to the Windows host, and so on.

To install a printer with the smb backend on CUPS, use this command:

```
root# lpadmin -p winprinter -v smb://WINDOWSNETBIOSNAME/printer sharename \\
-P /path/to/PPD
```

The PPD must be able to direct CUPS to generate the print data for the target model. For PostScript printers, just use the PPD that would be used with the Windows NT PostScript driver. But what can you do if the printer is only accessible with a password? Or if the printer’s host is part of another workgroup? This is provided for: You can include the required parameters as part of the smb:// device-URI like this:

- `smb://WORKGROUP/WINDOWSNETBIOSNAME/printer sharename`
- `smb://username:password@WORKGROUP/WINDOWSNETBIOSNAME/printer sharename`
- `smb://username:password@WINDOWSNETBIOSNAME/printer sharename`

Note that the device URI will be visible in the process list of the Samba server (e.g., when someone uses the ps -aux command on Linux), even if the username and passwords are sanitized before they get written into the log files. This is an inherently insecure option; however, it is the only one. Don’t use it if you want to protect your passwords. Better share the printer in a way that does not require a password! Printing will only work if you have a working NetBIOS name resolution up and running. Note that this is a feature of CUPS and you do not necessarily need to have smbd running.

## 21.18 More CUPS Filtering Chains

The diagrams in Figure 21.17 and Figure 21.18 show how CUPS handles print jobs.

## 21.19 Common Errors

### 21.19.1 Windows 9x/Me Client Can’t Install Driver

For Windows 9x/Me, clients require the printer names to be eight characters (or “8 plus 3 chars suffix”) max; otherwise, the driver files will not get transferred when you want to download them from Samba.

### 21.19.2 “cupssaddssmb” Keeps Asking for Root Password in Never-ending Loop

Have you set security = user? Have you used smbpasswd to give root a Samba account? You can do two things: open another terminal and execute smbpasswd -a root to create the account and continue entering the password into the first terminal. Or, break out of the loop by pressing Enter twice (without trying to type a password).

**Figure 21.17** Filtering Chain 1.

CUPS in and of itself has this (general) filter chain (*italic* letters are *file-formats* or MIME types, other are filters (this is true for pre-1.1.15 of pre-4.3 versions of CUPS and ESP PrintPro):

![](img/86d74c6cc862465e3a42e6dc3c90935a_478_0.png)

ESP PrintPro has some enhanced “rastertosomething” filters as compared to CUPS, and also a somewhat improved “*pstoraster*” filter.

NOTE: Gimp-Print and some other 3rd-Party-Filters (like TurboPrint) to CUPS and ESP PrintPro plug-in where *rastertosomething* is noted.

If the error is “*Tree connect failed: NT_STATUS_BAD_NETWORK_NAME*”, you may have forgotten to create the */etc/samba/drivers* directory.

### 21.19.3 “cupsaddslmb” or “rpcclient addrivers” Emit Error

If cupsaddslmb, or rpcclient addrivers emit the error message WERR_BAD_PASSWORD, refer to Section 21.19.2.

### 21.19.4 “cupsaddslmb” Errors

The use of “cupsaddslmb” gives “No PPD file for printer...” message while PPD file is present. What might the problem be?

Have you enabled printer sharing on CUPS? This means, do you have a `<Location /printers>...</Location>` section in CUPS server's `cupsd.conf` that does not deny access to the host you run `cupsaddism` from? It could be an issue if you use cupsaddism remotely, or if you use it with a -h parameter: cupsaddm -H sambever -h cups-server -v printername.

Is your `TempDir` directive in `cupsd.conf` set to a valid value, and is it writable?

### 21.19.5 Client Can't Connect to Samba Printer

Use `smbstatus` to check which user you are from Samba's point of view. Do you have the privileges to write into the `[print$]` share?

### 21.19.6 New Account Reconnection from Windows 200x/XP Troubles

Once you are connected as the wrong user (for example, as `nobody`, which often occurs if you have `map to guest = bad user`), Windows Explorer will not accept an attempt to connect again as a different user. There will not be any bytes transferred on the wire to Samba, but still you'll see a stupid error message that makes you think Samba has denied access. Use `smbstatus` to check for active connections. Kill the PIDs. You still can't re-connect, and you get the dreaded `You can't connect with a second account from the same machine` message as soon as you try. And you do not see a single byte arriving at Samba (see logs; use `"ethereal"`) indicating a renewed connection attempt. Shut all Explorer Windows. This makes Windows forget what it has cached in its memory as established connections. Then reconnect as the right user. The best method is to use a DOS terminal window and `first do net use z: \\GANDALF\print$ /user:root.` Check with `smbstatus` that you are connected under a different account. Now open the `Printers` folder (on the Samba server in the `Network Neighorhood`), right-click on the printer in question, and select `Connect`......

### 21.19.7 Avoid Being Connected to the Samba Server as the Wrong User

You see per `smbstatus` that you are connected as user nobody, but you want to be root or printer admin. This is probably due to `map to guest = bad user`, which silently connected you under the guest account when you gave (maybe by accident) an incorrect username. Remove `map to guest` if you want to prevent this.

### 21.19.8 Upgrading to CUPS Drivers from Adobe Drivers

This information came from a mailing list posting regarding problems experienced when upgrading from Adobe drivers to CUPS drivers on Microsoft Windows NT/200x/XP clients. First delete all old Adobe-using printers. Then delete all old Adobe drivers. (On Windows 200x/XP, right-click in the background of `Printers` folder, select `Server Properties`..., select tab `Drivers`, and delete here).

### 21.19.9 Can't Use "cupsaddsmb" on Samba Server, Which Is a PDC

Do you use the "naked" root user name? Try to do it this way: `cupsaddsmb -U DO-\ MAINNAME\root -v printername>` (note the two backslashes: the first one is required to "escape" the second one).

### 21.19.10 Deleted Windows 200x Pxinter Driver Is Still Shown

Deleting a printer on the client will not delete the driver too (to verify, right-click on the white background of the **Printers** folder, select **Server Properties** and click on the **Drivers** tab). These same old drivers will be re-shown when you try to install a printer with the same name. If you want to update to a new driver, delete the old ones first. Deletion is only possible if no other printer uses the same driver.

### 21.19.11 Windows 200x/XP Local Security Policies

Local security policies may not allow the installation of unsigned drivers ("local security policies" may not allow the installation of printer drivers at all.

### 21.19.12 Administrator Cannot Install Printers for All Local Users

Windows XP handles SMB printers on a "per-user" basis. This means every user needs to install the printer himself or herself. To have a printer available for everybody, you might want to use the built-in IPP client capabilities of Win XP. Add a printer with the print path of `http://cupsserver:631/printers/printername`. We're still looking into this one. Maybe a logon script could automatically install printers for all users.

### 21.19.13 Print Change, Notify Functions on NT Clients

For print change, notify functions on NT++ clients. These need to run the **Server** service first (renamed to **File & Print Sharing for MS Networks** in XP).

### 21.19.14 Win XP-SP1

Win XP-SP1 introduced a Point and Print Restriction Policy (this restriction does not apply to "Administrator" or "Power User" groups of users). In Group Policy Object Editor, go to **User Configuration -> Administrative Templates -> Control Panel -> Printers**. The policy is automatically set to **Enabled** and the **Users** can only **Point and Print** to **machines** in **their Forest**. You probably need to change it to **Disabled** or **Users** can only **Point and Print** to these servers to make driver downloads from Samba possible.
