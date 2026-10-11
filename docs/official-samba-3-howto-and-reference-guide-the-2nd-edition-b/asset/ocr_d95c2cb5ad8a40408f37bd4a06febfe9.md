# 21.19.9 Can't Use "cupsaddsmb" on Samba Server, Which Is a PDC

Do you use the "naked" root user name? Try to do it this way: `cupsaddsmb -U DO-\ MAINNAME\root -v printername>` (note the two backslashes: the first one is required to "escape" the second one).

# 21.19.10 Deleted Windows 200x Pxinter Driver Is Still Shown

Deleting a printer on the client will not delete the driver too (to verify, right-click on the white background of the **Printers** folder, select **Server Properties** and click on the **Drivers** tab). These same old drivers will be re-shown when you try to install a printer with the same name. If you want to update to a new driver, delete the old ones first. Deletion is only possible if no other printer uses the same driver.

# 21.19.11 Windows 200x/XP Local Security Policies

Local security policies may not allow the installation of unsigned drivers ("local security policies" may not allow the installation of printer drivers at all.

# 21.19.12 Administrator Cannot Install Printers for All Local Users

Windows XP handles SMB printers on a "per-user" basis. This means every user needs to install the printer himself or herself. To have a printer available for everybody, you might want to use the built-in IPP client capabilities of Win XP. Add a printer with the print path of `http://cupsserver:631/printers/printername`. We're still looking into this one. Maybe a logon script could automatically install printers for all users.

# 21.19.13 Print Change, Notify Functions on NT Clients

For print change, notify functions on NT++ clients. These need to run the **Server** service first (renamed to **File & Print Sharing for MS Networks** in XP).

# 21.19.14 Win XP-SP1

Win XP-SP1 introduced a Point and Print Restriction Policy (this restriction does not apply to "Administrator" or "Power User" groups of users). In Group Policy Object Editor, go to **User Configuration -> Administrative Templates -> Control Panel -> Printers**. The policy is automatically set to **Enabled** and the **Users** can only **Point and Print** to **machines** in **their Forest**. You probably need to change it to **Disabled** or **Users** can only **Point and Print** to these servers to make driver downloads from Samba possible.